# MCD Eventos — Modelo conceitual de dados, escala e arquivo

> Este documento descreve **a futura arquitetura**, não exige implementação de banco de dados no Claude Artifacts. Serve para que os designers não criem telas incompatíveis com o fluxo real.

## 1. Separação de camadas

1. **Banco transacional**: cadastros, eventos, vínculo do participante, convites, alocação, status, metadados de documentos, versões, permissões, logs e lotes.
2. **Armazenamento protegido de arquivos**: modelos e instâncias PDFs, assinaturas e anexos com metadados/versionamento.
3. **Google Drive / contabilidade**: distribuição controlada de lotes finais, manifests e relatórios; não substitui automaticamente o repositório de guarda legal.
4. **Camada de interface operacional**: mostra eventos recentes e em andamento; arquiva/oculta os antigos de acordo com política de 30 dias.

**Importante:** alterações e documentos devem ser registrados durante a operação, não apenas no envio final. Fechamento consolida e bloqueia a versão do lote.

## 2. Modelo lógico mínimo

| Entidade | Chave e campos essenciais | Regras |
|---|---|---|
| `pessoas` | `pessoa_id`, `codigo_funcionario`, `nome_completo`, `foto_url?`, `email?`, `telefone?`, `endereco?` | Cadastro mestre, dados protegidos. Código único na organização/cliente — escopo a definir. |
| `eventos` | `evento_id`, `nome`, `data`, `inicio`, `fim`, `local`, `banner_url?`, `status`, `arquivado_em?` | Dois eventos podem compartilhar data; IDs diferentes. |
| `grupos_evento` | `evento_id`, `grupo` (`INTERMITENTE` ou `FUNCIONARIO_EVENTO`), `status` | Grupo é **escopo obrigatório**; fechado/exportado separadamente. |
| `areas` | `area_id`, `nome`, `ativo` | Áreas configuráveis (BAR, COZINHA etc.). |
| `liderancas` | `lider_id`, `codigo_lider`, `pessoa_id?`, `nome_completo` | Código e nome completos obrigatórios na tela. |
| `equipes_evento` | `equipe_id`, `evento_id`, `grupo`, `area_id`, `lider_id` | Uma área pode ter N líderes; grupos isolados. |
| `participacoes` | `participacao_id`, `pessoa_id`, `evento_id`, `grupo`, `equipe_id?`, `funcao`, `turno`, `apto`, `status_presenca` | Identidade de participação por evento/grupo; **não inferir o grupo pela pessoa**. |
| `convocacoes` | `convocacao_id`, `participacao_id`, `enviada_em?`, `canal`, `status`, `respondida_em?` | Todos os convocados permanecem no histórico do grupo. |
| `formularios` | `formulario_id`, `participacao_id`, `versao`, `status`, `concluido_em?` | Separado do status do convite. |
| `modelos_documento` | `modelo_id`, `grupo`, `tipo`, `versao`, `ativo`, `exige_assinatura`, `etapa_permitida` | 3 modelos obrigatórios no fluxo configurado, sem assumir nomes jurídicos. |
| `pacotes_individuais` | `pacote_id`, `participacao_id`, `status`, `total_obrigatorios=3`, `quantos_bloqueados`, `conferido_em?` | Pacote de uma pessoa de um grupo/evento. |
| `documentos` | `documento_id`, `pacote_id`, `modelo_id`, `status`, `versao_ativa`, `arquivo_referencia` | Um registro por documento obrigatório. |
| `versoes_documento` | `versao_id`, `documento_id`, `numero`, `pdf_url_protegida`, `hash_sha256`, `assinada_em?`, `substituida_em?` | Versão anterior imutável; nunca sobreescrever ao corrigir. |
| `assinaturas` | `assinatura_id`, `versao_id`, `pessoa_id`, `coletada_por_usuario_id`, `confirmada_em`, `evidencia_ref` | Exigir identificação e evidências conforme validação legal. |
| `solicitacoes_correcao` | `solicitacao_id`, `documento_id`, `requisitante`, `aprovador?`, `motivo`, `status`, `criada_em` | Reabertura restrita, motivo explícito. |
| `fechamentos_grupo` | `fechamento_id`, `evento_id`, `grupo`, `versao`, `status`, `fechado_por`, `fechado_em?` | Nunca juntar intermitentes e funcionários do evento em um único fechamento. |
| `lotes_exportacao` | `lote_id`, `fechamento_id`, `versao`, `status`, `drive_folder_id?`, `manifesto_ref`, `tentativas`, `concluido_em?` | Entrega rastreada, idempotente e versionada. |
| `registros_auditoria` | `auditoria_id`, `evento_id`, `grupo`, `usuario_id`, `acao`, `entidade`, `entidade_id`, `antes_resumido`, `depois_resumido`, `motivo?`, `ocorrido_em` | **Implementação futura**; contrato desenhado desde já. |
| `usuarios_permissoes` | `usuario_id`, `papel`, `escopo_eventos`, `escopo_grupos`, `escopo_areas`, `escopo_equipes` | Princípio do menor privilégio. |

## 3. Chaves de isolamento de dados (regra crítica)

Cada consulta sobre participantes/documentos/fechamento deve estabelecer ao menos `evento_id` e `grupo`, e `area_id/lider_id` quando aplicável. Exemplo conceitual:

```text
WHERE evento_id = :evento_escolhido
  AND grupo = 'FUNCIONARIO_EVENTO'
  AND area_id = :area_escolhida
  AND lider_id = :lider_escolhido
```

O cadastro mestre de pessoa pode ser compartilhado, mas a participação, o status, o pacote, o histórico e o fechamento são específicos. Não permitir que um pacote de Intermitentes apareça na folha de Funcionários do Evento.

## 4. Cardinalidades e volume

```text
Evento 1:N GruposEvento (tipicamente 2)
Evento + Grupo 1:N Participações
Evento + Grupo 1:N Equipes
Área 1:N Lideranças por evento/grupo
Liderança/Equipe 1:N Participações
Participação 1:N Convocações (tentativas/retificações)
Participação 1:1 Pacote (por configuração de fluxo)
Pacote 1:3 Documentos obrigatórios (padrão atual; configurável)
Documento 1:N Versões (correção cria nova versão)
Fechamento 1:N Lotes/Versões de entrega
```

Carga de referência: **3.000 participações x 3 documentos = 9.000 PDFs** por evento quando todos exigem o pacote. Isso **não é 3.000.000**: a expressão coloquial “3000 mil” foi interpretada como a escala descrita repetidamente de ~3.000 pessoas.

Cálculo **ilustrativo**, a depender do PDF: 9.000 arquivos x 250 KiB ≈ 2,15 GiB por evento; 9.000 x 1 MiB ≈ 8,79 GiB. Esse volume cresce com versões, anexos, PDFs com fotos, cópias e redundância. Dimensionamento final exige medições reais.

### Desempenho

- Pesquisar por código e nome; paginar tabelas e virtualizar listas grandes.
- Índices/consultas por `(evento_id, grupo, status_convocacao)`, `(evento_id, grupo, area_id, lider_id)`, `(pacote_id, status)`, `(fechamento_id, status_exportacao)`.
- Importação de milhares de pessoas em lote com deduplicação e relatório de erros.
- Geração/consolidação/exportação dos PDFs por fila assíncrona com progresso e retentativas no backend futuro.
- Evitar enviar 9.000 arquivos na mesma requisição e não exigir baixar todos os PDFs para renderizar uma tabela.

## 5. Regra de transição e travamento de assinatura

```text
DOCUMENTO: PENDENTE → DISPONÍVEL → ASSINATURA CONFIRMADA → BLOQUEADO
                                    ↘ correção aprovada → NOVA VERSÃO

PACOTE: 0/3 → 1/3 → 2/3 → 3/3 → CONFERIDO → BLOQUEADO

FECHAMENTO EVENTO+GRUPO: EM COLETA → PRONTO → FECHADO/BLOQUEADO
                                               ↓
                                        EXPORTAÇÃO EM FILA
                                               ↓
                                         ENTREGUE AO DRIVE
```

- Não permitir a transição para pacote bloqueado enquanto faltar documento obrigatório sem exceção formal.
- Não liberar fechamento de grupo sem verificar as regras de presença/jornada/folha aplicáveis ou exceções formalmente validadas.
- Reabertura autorizada gera solicitação/log, nova versão e possível invalidação do estado `Pronto` / necessidade de retificação.
- Depois que um lote for fechado, **nunca sobrescrever o anterior**; corrigir por lote versão 2, 3, etc.

## 6. Banco + Google Drive

Fluxo recomendado para a futura implementação:

1. No aceite e formulário, banco registra mudanças e status.
2. Ao confirmar cada assinatura, registrar versão do documento, referências do PDF protegido, integridade e metadados.
3. Ao bloquear pacote 3/3, atualizar status agregado e anexar referência às versões válidas.
4. Ao fechar o evento/grupo, gerar um `fechamento_id` com **manifesto de integridade** contendo evento, grupo, trabalhador, códigos, versões, status, hashes e timestamps.
5. Criar um **lote de exportação** por grupo; preparar arquivos e resumo para contabilidade.
6. Enviar ao Google Drive com credencial de serviço/permissões adequadas (nunca público), esperar confirmação e guardar `drive_folder_id`, IDs de arquivo, data/hora e estado.
7. Se falhar, deixar lote `Erro / Tentar novamente`. Evitar uploads duplicados pela mesma chave de lote/versão.
8. Disponibilizar para contabilidade visão de consulta/download por permissão, sem compartilhar conteúdo por e-mail aberto por padrão.

Estrutura lógica sugerida:

```text
MCD_EVENTOS/
  2026/
    2026-10-25__EVT-001__Evento-Maracana/
      FUNCIONARIOS_EVENTO/
        LOTE-V01/
          manifesto.csv
          resumo-fechamento.pdf
          documentos-lote-001.zip
          documentos-lote-002.zip
      INTERMITENTES/
        LOTE-V01/
          manifesto.csv
          documentos-lote-001.zip
```

O número de ZIPs e agrupamento (por área/líder ou lotes) é decisão técnica; **nunca misturar grupos dentro do mesmo lote**. Se o escritório precisar de PDFs individuais no Drive, oferecer organização por grupo/área/liderança/código com IDs estáveis e manifesto. Planejar limites/cotas e políticas de acesso do Drive.

## 7. Somente um mês no sistema operacional

O requisito do cliente: **“só manteremos no sistema um mês de evento”**. Não assumir exclusão permanente de documentos trabalhistas em 30 dias.

**Comportamento de produto proposto:**

- Até 30 dias corridos após a data do evento: evento nas listas operacionais, com filtros ativos.
- Depois: etiqueta `Arquivado`, remoção da home operacional, acesso restrito ao módulo Arquivo para consulta/contabilidade.
- Dados e arquivos permanecem conservados segundo política aprovada de RH, contabilidade, jurídico e privacidade (a definir), com acesso e trilha de auditoria.
- Caso seja exigido remover de um banco ativo, migrar para um banco/arquivo histórico seguro com verificação de integridade **antes de excluir cópias temporárias**.
- Drive é destino de exportação; precisa de definição expressa se é repositório oficial, cópia operacional ou backup.
- Nunca mover/arquivar um evento com falha de envio sem visibilidade para administradores; arquivamento e entrega são estados distintos.

## 8. Trilha de auditoria / backlog (planejada para próxima fase)

O pedido do cliente é que **tudo que for alterado ou digitado e confirmado no ambiente de assinatura e fechamento tenha registro**. Proposta responsável:

- Registrar ações de criação/edição, alterações de dados, mudança de área/liderança, convites e respostas, assinatura, confirmação, bloqueio, correção, autorização, fechamento e exportação.
- Registrar: `quem`, `quando`, `o quê`, `onde` (`evento+grupo+área+liderança+pessoa`), valor anterior/novo **quando apropriado**, justificativa e referências de versão.
- Logs com comportamento **append-only**, controle de acesso e proteção de integridade; não disponibilizar edição de eventos históricos.
- **Não gravar senhas, conteúdo de campos sensíveis indiscriminadamente, movimentos da caneta ou cada tecla pressionada**; auditar ações e valores confirmados, conforme necessidade e LGPD.
- No protótipo, mostrar UI de `Histórico (planejado)` e registros fictícios, sem alegar persistência.

## 9. Segurança, disponibilidade e conformidade

- Permissão por papel/evento/grupo/área/equipe e necessidade operacional.
- Criptografia em trânsito e repouso; não expor links públicos de documentos com dados de trabalhador.
- Validação jurídica do mecanismo de assinatura e das evidências (autoria, integridade, consentimento quando aplicável e não repúdio em nível compatível).
- Regras documentais de ponto/recibo definidas por DP/contabilidade; os 3 modelos permanecem abstratos até aprovação.
- Consentimento e base legal para foto e dados cadastrais; regras de acesso, retenção, descarte e exportação alinhadas à LGPD.
- Eventos e operações críticas suportando rede ruim, concorrência, reversão segura, retentativas e reconciliação.
