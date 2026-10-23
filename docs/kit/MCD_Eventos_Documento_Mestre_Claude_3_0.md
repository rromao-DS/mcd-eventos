# MCD Eventos — Documento mestre para Claude

**Versão 3.0 — 23/10/2026**

Este é o documento completo reunido para um único upload ao Claude. A versão em arquivos separados, dentro do ZIP, é preferível quando for possível anexar vários documentos. O protótipo desta fase não deve conter backend nem uso de dados reais.

> **REGRA CRÍTICA:** ao abrir cada evento, manter os módulos **INTERMITENTES** e **FUNCIONÁRIOS DO EVENTO** separados. O fluxo de folha do segundo grupo não deve ser agregado aos intermitentes.



---

# ARQUIVO: 00_COMECE_AQUI.md

# MCD Eventos — Kit de implantação do projeto no Claude

**Pacote:** versão 3.0 • **Data:** 23/10/2026 • **Etapa:** definição de produto + UX/UI + protótipo no Claude (sem backend de produção).

## O que é

Plataforma MCD Eventos para gerenciar eventos de grande porte e digitalizar **convocação → aceite → confirmação cadastral → alocação → assinatura de 3 documentos por trabalhador → conferência → fechamento documental e exportação para contabilidade**. Cenário inicial: Maracanã. O processo físico/manual atualmente retarda o fechamento da folha do evento; a meta de negócio é permitir operação próxima de D+1 quando todos os requisitos forem atendidos.

## REGRA MAIS IMPORTANTE: dois grupos que NÃO SE MISTURAM

Ao entrar em um **evento** pelo calendário, o sistema apresenta **dois módulos independentes**:

1. **INTERMITENTES** — lista, convocações, formulários, equipes e documentação específica deste grupo; seu fluxo deve permanecer isolado.
2. **FUNCIONÁRIOS DO EVENTO** — lista, áreas/alocação, lideranças, funcionários, pacotes de documentos, conferência e **fechamento de folha do evento**; todas as modificações relevantes da área de assinatura deverão possuir **trilha de auditoria/backlog** na futura implementação.

**Não combinar listas, filtros, totais, permissões, status, modelos de documentos, lotes de exportação ou fechamento de folha entre os grupos.** A mesma pessoa pode existir em um cadastro mestre, mas a participação em cada evento precisa ter um `grupo_participacao` explícito e isolado. Não transferir automaticamente pessoas de um módulo ao outro.

O desenho dos 3 documentos é requerido para o fluxo de assinatura. Os tipos exatos de documento podem variar conforme o grupo e dependem de validação jurídico/DP. O foco inicial do protótipo é o módulo **Funcionários do Evento**, sem deixar de representar o acesso separado a **Intermitentes**.

## Como configurar o Claude

**Nome do projeto:** `MCD Eventos | Produto, UX/UI e Protótipo`

**Meta:** `Desenhar e prototipar no Claude a plataforma MCD Eventos, seguindo a identidade visual da MCD, para gerir eventos, convocações, áreas, lideranças, assinaturas de três documentos e fechamento de folha. Manter Intermitentes e Funcionários do Evento em módulos inteiramente separados. Projetar operação para 3.000 pessoas por evento e 9.000 documentos, com rastreabilidade, exportação e arquivamento operacional em 30 dias.`

**Contexto curto (colar no campo Contexto):**

> Você é Product Manager, UX Lead e arquiteto conceitual do projeto MCD Eventos. Leia todos os arquivos deste projeto antes de criar telas. Use o site https://www.mcdcontabil.com.br/ e a captura de login MCD enviada como referência visual (sem reaproveitar credenciais). O protótipo é em português brasileiro, responsivo para desktop e tablet, realizado no Claude Artifacts com dados fictícios. Início: Login → Calendário + Destaques → Cartões de eventos no dia → Evento → escolha independente entre Intermitentes e Funcionários do Evento. Para Funcionários do Evento: Áreas → Lideranças → Funcionários → 3 PDFs → assinatura e bloqueio → fechamento e envio ao Drive/contabilidade. Convocação e aceite vêm antes da alocação definitiva. A lista de Convocados contém também recusados e sem resposta; não confunda aceite, formulário, presença e assinatura. Intermitentes têm área e registros próprios que não devem ser misturados com Funcionários do Evento. O sistema operacional mostra apenas 30 dias de eventos; documentos e trilhas históricos permanecem arquivados pelo prazo legal/contratual a definir. Alterações críticas deverão ter auditoria, mas o backend de auditoria é etapa futura. Nesta fase não integrar banco real, envio de mensagens, Google Drive nem assinatura válida juridicamente. Consulte `01_REQUISITOS_PRODUTO.md`, `02_JORNADAS_E_TELAS.md`, `03_DESIGN_SYSTEM.md`, `04_MODELO_DE_DADOS_E_ARQUIVAMENTO.md`, `05_CRITERIOS_DE_ACEITE.md` e `06_PROMPT_INICIAL_CLAUDE.md`. Não invente políticas trabalhistas nem declare as cores/fontes da captura como oficiais sem verificar.

## Arquivos do kit — ordem de leitura

1. `00_COMECE_AQUI.md` — este documento e configuração do projeto.
2. `01_REQUISITOS_PRODUTO.md` — requisitos, decisões firmes, regras e escopo.
3. `02_JORNADAS_E_TELAS.md` — mapa de navegação, telas e fluxos.
4. `03_DESIGN_SYSTEM.md` — referência visual, cores aproximadas e componentes.
5. `04_MODELO_DE_DADOS_E_ARQUIVAMENTO.md` — modelo lógico, escala, segurança, Drive, 30 dias e auditoria futura.
6. `05_CRITERIOS_DE_ACEITE.md` — cenários de teste do protótipo.
7. `06_PROMPT_INICIAL_CLAUDE.md` — comando inicial para colar na conversa do Claude.
8. `07_DECISOES_ABERTAS.md` — pontos pendentes a validar, sem bloquear o primeiro design.
9. `08_DADOS_DE_EXEMPLO.json` — dataset fictício para a navegação do protótipo.
10. `09_CONTRATOS_DE_TELA.md` — campos, operações e estados por interface.

## Sobre a imagem de referência

A captura fornecida da tela de login contém **usuário e senha visíveis**. **Não envie o arquivo original ao Claude ou a outras pessoas sem ocultar completamente os dois campos.** Em vez disso, o Claude pode seguir as orientações de `03_DESIGN_SYSTEM.md`, ou receber uma versão da captura com credenciais cobertas por tarjas opacas. Caso a senha seja real, altere-a.

## Entrega de primeira fase

1. Mapa visual da arquitetura de informação (incluindo a separação dos módulos).
2. Tokens do Design System e componentes.
3. Protótipo clicável no Claude Artifacts: Login, Calendário, Eventos do dia, Tela do Evento com dois módulos, Funcionários do Evento → Áreas → Lideranças → Funcionários → 3 documentos → bloqueio; Convocados com aceite e formulário; fila de fechamento/Drive simulada.
4. Estados de erro, vazio, sem conexão, pendente, concluído e bloqueado.
5. Ações simuladas com dados fictícios, **sem backend**.

## Como usar imediatamente

Faça upload de todos os arquivos deste diretório ao projeto Claude. Na primeira conversa, copie o conteúdo do arquivo `06_PROMPT_INICIAL_CLAUDE.md`. Se o Claude exceder o espaço de uma entrega, divida em entregas sequenciais sem alterar os requisitos nem misturar os dois grupos.


---

# ARQUIVO: 01_REQUISITOS_PRODUTO.md

# MCD Eventos — Especificação de produto (PRD)

**Versão:** 3.0 — consolidação do briefing fornecido pelo idealizador.  
**Status:** requisitos de design; regras técnicas e jurídicas a validar antes da implementação real.

## 1. Visão, problema e resultado

Hoje a operação convoca trabalhadores por e-mail, recebe aceite e coleta documentos e assinaturas. No dia do evento existem **três documentos a assinar por trabalhador**. Papéis são encaminhados fisicamente no dia seguinte e digitalizados/conferidos manualmente pela contabilidade, atrasando o fechamento da folha, por vezes uma semana ou mais.

A plataforma **MCD Eventos** substituirá trabalho manual por gestão de convocação, distribuição operacional, coleta documental em tablet, bloqueio e auditoria de versões, consolidação e disponibilização dos documentos à contabilidade. **Meta desejada:** reduzir significativamente o tempo de fechamento; D+1 é meta condicionada à conclusão de assinaturas, apuração de jornada, validação dos documentos e rotinas de folha.

## 2. Escala-alvo

- **3.000 pessoas em um evento** como cenário de referência de capacidade. Não interpretar como número de pessoas simultaneamente assinando.
- **3 documentos por participante** nos fluxos que exigirem o pacote: **até 9.000 instâncias de documentos por evento**, excluindo revisões, formulários, convites e anexos.
- Um mesmo dia pode conter **dois ou mais eventos**, separados entre si.
- Um evento pode ter **múltiplas áreas** e **várias lideranças por área**.
- Painéis devem ter busca por código/nome, filtros, paginação ou listas virtualizadas e operação em lote. Não renderizar 3.000 registros de uma vez no navegador.

## 3. Separação obrigatória de população

O detalhe de um evento abre uma página com **duas entradas grandes, independentes**:

### 3.1 Intermitentes

- Cadastro/participação no evento, convocação por e-mail/app/portal, resposta, formulário e documentação específica.
- Lista de convocados, participação, status e exportações **próprios**, sem aparecer misturados nos relatórios de Funcionários do Evento.
- Termos, apuração e rotinas contábeis próprias devem ser definidos pelo DP; **não herdar automaticamente a regra de fechamento de folha do outro módulo**.

### 3.2 Funcionários do Evento

- Cadastro/participação, convocações, áreas, lideranças e escalas.
- Coleta de 3 documentos e controle individual de bloqueio.
- **Fechamento da folha do evento** e sua documentação de suporte.
- Deve existir planejamento de **trilha de auditoria/backlog para toda alteração relevante e digitação confirmada nesse ambiente**, incluindo autoria, horário, justificativa quando exigida, contexto e versões. A implementação integral do motor de auditoria é futura; **o design já deve reservar histórico, status e ações**.

### 3.3 Regras de isolamento

- Separar por **evento + grupo** (`INTERMITENTE` | `FUNCIONARIO_EVENTO`), mesmo havendo um cadastro mestre de pessoas.
- Nunca somar/intercalar listas nos dashboards de operação por grupo, nem gerar um ZIP misto por padrão.
- Cada um possui convocações, status, alocações, documentos, revisões, controles de acesso, pendências e exportações identificadas por grupo.
- Se uma pessoa for cadastrada nos dois grupos do mesmo evento, exibir **alerta de possível conflito** para decisão administrativa; nenhuma migração automática.
- Valores ilustrativos em telas sempre incluem nome do grupo selecionado para evitar operação no módulo errado.

## 4. Calendário e primeiro acesso

1. Login/recuperação de acesso com identidade visual MCD.
2. Home pós-login: **calendário** em primeiro plano; abaixo seção **Destaques** para alertas, avisos e notificações futuras.
3. Clicar numa data revela cartões/quadrados dos eventos com **banner ou logotipo do evento**, nome, local, horário e estado.
4. Um dia pode conter múltiplos eventos; a pessoa escolhe um cartão.
5. Cabeçalho do evento exibe **logo MCD, logo/banner do evento, nome, local, data e horários**.
6. No detalhe, mostrar os cartões/módulos **Intermitentes** e **Funcionários do Evento**; primeiro selecionar o tipo de público, sem misturá-los.

## 5. Navegação operacional por hierarquia

No módulo **Funcionários do Evento**:

`Data → Evento → Funcionários do Evento → Área/Alocação → Liderança → Lista de Funcionários → Ficha → 3 documentos`

Áreas iniciais configuráveis (exibir nesta ordem no protótipo):

1. BAR
2. AMBULANTE
3. SERVIÇOS GERAIS
4. FINANCEIRO
5. ESCRITÓRIO
6. COZINHA
7. PRODUÇÃO
8. ESTOQUISTA
9. STAFF

Regras:

- Ao abrir uma área, listar **uma ou mais lideranças**, cada qual com **código, nome completo e quantidade de pessoas**.
- Ao abrir liderança, mostrar apenas os trabalhadores **alocados àquele líder, naquele evento e naquela data**.
- Colunas mínimas da tabela de funcionários: código, nome completo, status de convocação, status do formulário, presença (se aplicável), progresso dos três documentos, status do pacote, ação de abrir.
- Um trabalhador só deve constar da lista operacional ativa conforme regras de aptidão (aceite + formulário + critérios definidos). Recusados/sem resposta ficam visíveis em **Convocados**, não entram silenciosamente na equipe de assinatura.
- Clicar na linha abre ficha com foto autorizada, código, nome, telefone, e-mail, endereço (com restrição de perfil), função, área, líder, turno, andamento e histórico.

## 6. Convocação antes do dia do evento

- Admin/coordenador escolhe pessoas previamente cadastradas, define **evento, grupo, área, liderança, função e turno**, e envia o convite individual ou em lote.
- Canais desejados: **e-mail** (atual) e **aplicativo/site/portal** (novo). Envio de verdade não faz parte do protótipo.
- O trabalhador pode **Confirmar** ou **Não confirmar/Recusar**. Quem ainda não respondeu fica **Não respondeu**.
- Quando confirma, recebe um **formulário** para completar/validar cadastro e informações necessárias; terminar esse formulário é condição de aptidão, conforme configuração.
- A área **Convocados** do grupo selecionado mostra sempre **todos os convidados**, incluindo aceitos, recusados e sem resposta. A pessoa confirmada **não sai** de Convocados: apenas pode também entrar na lista operacional quando estiver apta.
- A confirmação do convite **não comprova** presença nem assinatura documental.

Estados independentes recomendados:

| Domínio | Estados básicos | Observações |
|---|---|---|
| Convite | Rascunho; Enviado; Não respondeu; Confirmado; Não confirmado; Cancelado | Manter histórico de tentativas/resposta. |
| Formulário | Pendente; Em preenchimento; Concluído; Requer correção | Não inferir do aceite. |
| Alocação | Prevista; Apta; Suspensa; Cancelada | Sempre vinculada a evento + grupo + área + liderança. |
| Presença/jornada | Não registrada; Presente; Ausente; Em apuração; Concluída | Definir origem e regras futuramente. |
| Documento | Pendente; Pronto para assinar; Assinado/bloqueado; Em correção; Substituído | Três registros independentes. |
| Pacote individual | Pendente 0/3; Parcial 1/3 ou 2/3; Completo 3/3; Conferido; Bloqueado | Pode estar em exceção aprovada. |
| Fechamento de evento/grupo | Em coleta; Com pendências; Pronto para fechamento; Fechado/bloqueado; Exportado; Arquivado | Fechamento por **grupo**, nunca um misto. |

## 7. Assinatura dos documentos

- Cada participante ativo do fluxo documental possui **pacote individual de 3 documentos**; os tipos finais deverão ser configuráveis por evento e grupo.
- No tablet, abrir o documento/PDF, permitir rolagem/zoom, visualizar termos e capturar assinatura com dedo/caneta; depois **Confirmar assinatura**.
- Ao confirmar, documento fica **bloqueado para edição** e mostra status, versão, nome/código do trabalhador, data/hora, operador e confirmação.
- Quando os 3 documentos exigidos estão corretamente concluídos, o pacote individual pode ser **conferido e bloqueado**.
- Reabertura: apenas usuário autorizado, com motivo, data/hora e log; a versão anterior é **preservada**, mas marcada como substituída/invalidada conforme a regra. **Não apagar a assinatura anterior do histórico**.
- O funcionário assina novamente em uma **nova versão**. Qualquer reabertura de documento pode devolver pacote/evento para pendências e exigir reexportação versionada.
- **Importante:** assinatura desenhada em tela por si só não garante validade jurídica. A implementação real exigirá identificação, integridade, evidências e validação de DP/jurídico. Não pressupor que ponto ou contracheque possa ser assinado antes de sua apuração/geração. Até validação, usar `Documento 1`, `Documento 2`, `Documento 3` no protótipo.

## 8. Fechamento, bloqueio e entrega

- Todos os pacotes individuais aplicáveis devem estar **completos/bloqueados** ou ter **exceções formalmente aprovadas**, e os pré-requisitos de jornada/folha conferidos.
- O gestor realiza/autoriza **fechamento documental do grupo no evento** e o lote ganha identificador, data/hora, versão e manifesto.
- O lote **fechado e bloqueado** é preparado para salvar dados/metadados no banco e documentos no armazenamento de arquivos; disponibilizar/exportar para **Google Drive** e para a **contabilidade**, sob permissões.
- O envio/arquivamento precisa exibir estados **Aguardando → Processando → Entregue → Erro/Retentativa**. Não afirmar sucesso antes de haver confirmação do destino.
- Armazenar metadados à medida que o processo acontece; **não esperar o fim do evento para registrar tudo no banco**. No fechamento, consolidar e registrar o lote final.
- Para fechamento de folha de Funcionários do Evento, prever dados e relatórios de jornada, presença, alocação, pendências e documentação; a folha propriamente dita dependerá de cálculo, integrações e revisão contábil a especificar.
- Se um documento de lote exportado for reaberto, manter lote original imutável e criar **nova versão de retificação/reexportação**, registrada na auditoria.

## 9. Retenção de 1 mês na interface operacional

A intenção informada é **manter só um mês de eventos no sistema operacional**. Recomenda-se interpretar para o protótipo como:

- Listas e painéis **operacionais mostram os eventos dos últimos 30 dias**, e eventos mais antigos saem da rotina.
- Após esse prazo, mover o evento para **Arquivo** (ou ocultá-lo do ambiente operacional), mantendo os dados/documentos/versões/logs acessíveis apenas a papéis autorizados, no banco/armazenamento e no Drive conforme política.
- **Não excluir definitivamente documentos de RH, folha, assinatura ou auditoria após 30 dias.** Prazos legais/contratuais, privacidade e regras de exclusão devem ser definidos com jurídico/DP e responsáveis por dados.
- O corte exato (30 dias corridos da data do evento, do fechamento ou mês calendário) é decisão pendente. No protótipo, use 30 dias corridos da data do evento e mostre isso como hipótese configurável.

## 10. Papéis e permissões (iniciais)

| Papel | Escopo esperado |
|---|---|
| Administrador MCD | Gerencia usuários, eventos, modelos, ambos os módulos, exceções, exportações e auditoria. |
| Coordenador do evento | Convoca, aloca, acompanha e fecha dentro do evento/grupo autorizado. |
| Responsável de área | Enxerga sua área e lideranças; aprova/conduz pendências sob permissão. |
| Líder | Enxerga somente equipe própria; coleta assinaturas quando autorizado. |
| Contabilidade/DP | Confere folha, documentos, lotes e relatórios permitidos; sem editar assinatura confirmada. |
| Trabalhador | Aceita/recusa convite, completa cadastro, consulta seus dados/documentos autorizados. |

Exibir PII de forma restrita: telefones, e-mails, endereços e foto apenas para quem necessita. Registro de auditoria deve evitar capturar senhas ou texto sensível de forma indevida.

## 11. Requisitos não funcionais

- Interface responsiva: desktop administrativo e tablet no evento (touch confortável, busca rápida, tela cheia para assinar).
- Confiável sob 3.000 participantes/9.000 documentos por evento; listas paginadas, atualizações incrementais e prevenção de duplicidades.
- Transações idempotentes para aceite, confirmação de assinatura, conclusão e envio de lote.
- Política definida de conectividade no estádio, com erro, reenvio e sincronização visualmente explícitos. Assinatura offline real só após estudo de segurança.
- Segurança por autenticação, segregação de papéis, segregação por evento/grupo, proteção de PDFs e trilha de versões.
- Relatórios: convidado/aceite, formulário, alocação, documentos pendentes, pendências por área/líder, fechamento, exportações e histórico.

## 12. O que NÃO é para implementar já

Nesta etapa no Claude, **não** criar banco real, APIs de produção, login funcional com credenciais reais, envio real de e-mail, upload real ao Drive, assinatura com garantia jurídica, cálculo trabalhista ou exclusão automática definitiva. É um **protótipo navegável e documentado**, com dados fictícios e ações simuladas.


---

# ARQUIVO: 02_JORNADAS_E_TELAS.md

# MCD Eventos — Arquitetura de informação, telas e jornadas

## 1. Estrutura de navegação obrigatória

```text
LOGIN MCD EVENTOS
  └── HOME
      ├── CALENDÁRIO
      └── DESTAQUES (avisos, eventos, notificações e pendências futuras)
          ↓ [clicar em uma data]
      EVENTOS DA DATA — cards com banner/logo, nome, local e horário
          ↓ [clicar em um evento específico]
      DETALHE DO EVENTO — cabeçalho MCD + evento + local + data
          ├── MÓDULO 1: INTERMITENTES (isolado)
          │   ├── Convocados (todos: confirmou / não respondeu / não confirmou)
          │   ├── Convite → Aceite → Formulário
          │   ├── Operação e documentos específicos, conforme regras do grupo
          │   └── Pendências / exportações do grupo (sem misturar com outro)
          │
          └── MÓDULO 2: FUNCIONÁRIOS DO EVENTO (isolado)
              ├── RESUMO
              ├── CONVOCADOS (todos os convidados do grupo)
              │    └── Convidar → confirmar/recusar → formulário → aptidão
              ├── ÁREAS / ALOCAÇÃO
              │    ├── BAR
              │    ├── AMBULANTE
              │    ├── SERVIÇOS GERAIS
              │    ├── FINANCEIRO
              │    ├── ESCRITÓRIO
              │    ├── COZINHA
              │    ├── PRODUÇÃO
              │    ├── ESTOQUISTA
              │    └── STAFF
              │         ↓ [selecionar área]
              │     LISTA DE LIDERANÇAS (código + nome completo)
              │         ↓ [selecionar líder]
              │     LISTA DE FUNCIONÁRIOS DESTE LÍDER NESTE EVENTO/DATA
              │         ↓ [selecionar funcionário]
              │     FICHA (foto, código, nome, contato, endereço restrito)
              │         ↓
              │     PACOTE INDIVIDUAL DE 3 DOCUMENTOS
              │         ├── Doc 1 → ler → assinar → confirmar → BLOQUEADO
              │         ├── Doc 2 → ler → assinar → confirmar → BLOQUEADO
              │         └── Doc 3 → ler → assinar → confirmar → BLOQUEADO
              │               ↓ [3/3, conferência concluída]
              │           PACOTE INDIVIDUAL BLOQUEADO
              ├── PENDÊNCIAS / DOCUMENTOS
              ├── FECHAMENTO DE FOLHA (grupo Funcionários do Evento)
              │     ↓ [regras de fechamento satisfeitas]
              │   LOTE DO GRUPO NO EVENTO BLOQUEADO
              │     ↓
              │   EXPORTAR / REGISTRAR → banco + armazenamento + Google Drive
              └── AUDITORIA / BACKLOG (interface planejada para fase futura)
```

**Regra de navegação:** não apresentar uma tabela única misturando os dois módulos. Sempre indicar no topo a trilha `Evento > Grupo > Área > Líder`, quando aplicável.

## 2. Inventário de telas

| ID | Tela | O que precisa aparecer | Ação principal |
|---|---|---|---|
| 01 | Login | Painel institucional azul, cartão branco, marca MCD, campos de acesso | Entrar (simulação) |
| 02 | Home | Calendário mensal/semanal e seção Destaques abaixo | Selecionar dia |
| 03 | Eventos na data | Cards com banner/logo, local, horário, mais de um evento | Abrir evento |
| 04 | Detalhe do evento | Logo MCD, banner/evento, data, local; 2 cartões INDEPENDENTES | Entrar em Intermitentes ou Funcionários do Evento |
| 05 | Painel Intermitentes | Totais e acessos exclusivos ao módulo Intermitentes | Abrir seus convocados/fluxos |
| 06 | Painel Funcionários do Evento | Cards áreas, convocados, documentos, fechamento | Abrir Áreas/Alocação |
| 07 | Convocados do grupo | KPIs confirmado/não respondeu/não confirmado; tabela por código/nome | Abrir pessoa / convidar |
| 08 | Nova convocação | Seleção individual/lote, evento, grupo, área, liderança, turno | Simular envio |
| 09 | Portal de convite | Evento, local, função, horários, aceite/recusa | Confirmar ou recusar |
| 10 | Formulário após aceite | Informações cadastrais necessárias, estado pendente/concluído | Finalizar formulário |
| 11 | Áreas de alocação | 9 áreas em cards com indicadores | Escolher BAR, COZINHA etc. |
| 12 | Lideranças da área | Código, nome completo, total de alocados e progresso | Escolher liderança |
| 13 | Funcionários do líder | Código, nome, convocação, formulário, docs 0/3 a 3/3 | Abrir funcionário |
| 14 | Ficha do funcionário | Foto, dados restritos, evento, grupo, área/líder, 3 documentos | Abrir documento |
| 15 | Visualizador de PDF | PDF ilustrativo, zoom, rolagem, identificação do documento | Assinar |
| 16 | Assinatura e confirmação | Área de desenho simulada, resumo, confirmador | Confirmar e bloquear |
| 17 | Pacote 3/3 | 3 linhas bloqueadas, conferência, versão e carimbo temporal fictícios | Bloquear pacote |
| 18 | Solicitar correção | Motivo obrigatório, autorização, histórico de versões | Simular reabertura autorizada |
| 19 | Pendências | Filtros por área/líder, indicadores em falta, ausências/exceções | Resolver/conferir |
| 20 | Fechamento do evento/grupo | Checklist de regras, progresso, bloqueio e versão | Simular fechamento |
| 21 | Entrega/Drive | Lote, manifesto, estados de envio, destino e versão | Simular exportação |
| 22 | Relatórios | Convocados, documentos, alocação, fechamento de folha, download simulado | Filtrar/exportar |
| 23 | Auditoria (futuro) | Lista demonstrativa de alterações, motivo, autor, antes/depois, timestamp | Consultar histórico simulado |
| 24 | Arquivo (30 dias) | Eventos fora do período operacional, somente acesso autorizado | Consultar arquivo simulado |

## 3. Comportamento da página de evento (importante)

Após clicar no cartão do evento, **não entrar diretamente em uma lista única de funcionários**. O usuário primeiro vê:

```text
[MCD]  EVENTO: Maracanã — Evento demonstrativo
       Local: Estádio do Maracanã | Data: 25/10/2026

  [INTERMITENTES]              [FUNCIONÁRIOS DO EVENTO]
  Grupo independente           Grupo independente
  Convocados: 900              Convocados: 2.100
  Confirmados: ...             Confirmados: ...
  Abrir módulo →               Abrir módulo →

  Observação: valores fictícios e apenas demonstrativos.
```

Depois de clicar **Funcionários do Evento** é que aparecem suas **Áreas/Alocação**, lideranças, funcionários e fechamento. Se clicar **Intermitentes**, todas as telas permanecem no escopo deste grupo e nunca puxam documentos/folha do outro.

## 4. Página Convocados — tabela e filtros

Cabeçalho: MCD + evento + data/local + etiqueta visível `FUNCIONÁRIOS DO EVENTO` ou `INTERMITENTES`.

Indicadores: Total de convidados, Confirmados, Não responderam, Não confirmados, Formulários pendentes, Aptos.

| Código | Nome completo | Área prevista | Liderança | Resposta | Formulário | Operação |
|---|---|---|---|---|---|---|
| 001245 | Ana Carolina Souza | BAR | 0801 — Carlos Pereira | Confirmado | Concluído | Apta |
| 001246 | Pedro Martins Lima | COZINHA | 0802 — Paula Ribeiro | Não respondeu | — | Fora da lista operacional |
| 001247 | Maria de Fátima Costa | SERVIÇOS GERAIS | 0803 — Bruno Almeida | Não confirmado | — | Fora da lista operacional |

Exibir busca por código e nome, filtros de resposta, área, liderança, formulário; campos sensíveis apenas na ficha autorizada.

## 5. Página Áreas → Lideranças → Funcionários

### Áreas
Cards ex.: `BAR — 420 pessoas / 4 lideranças / 380 pacotes 3/3`. O total e a quantidade de líderes vêm só do evento/grupo selecionado.

### Lideranças
Lista ou cards com `Código`, `Nome completo`, `Área`, `Total da equipe`, `Pacotes completos`, `Pendências`. Várias lideranças por área são regra, não exceção.

### Funcionários do líder
Tabela com `Código`, `Nome`, `Área`, `Líder`, `Confirmação`, `Formulário`, `3 documentos`, `Pacote` e ação. O filtro é fixo a **evento/data/grupo/área/líder**; não colocar pessoas de outro líder em resultados.

### Ficha do funcionário
Exibir foto de rosto fictícia (ou avatar, caso não haja consentimento/base adequada), código, nome, dados cadastrais autorizados, telefone, e-mail e endereço em detalhes protegidos, cargo/função, hora/turno, líder, progresso `0/3`, `1/3`, `2/3` ou `3/3`, documentos e versão ativa. Acesso ao histórico de assinatura permitido apenas para perfis adequados.

## 6. Fluxos passo a passo

### A. Convocação
Admin escolhe grupo → busca cadastrado → atribui evento, área, liderança e turno → envia convite (simulado) → estado `Não respondeu` → trabalhador confirma → vai a formulário → formulário concluído → entra em escala operacional apta do **mesmo grupo** → permanece em Convocados com etiqueta de confirmado.

### B. Coleta de 3 assinaturas
Operador abre evento do dia → Funcionários do Evento → BAR → liderança 0801 → funcionário 001245 → ficha → Documento 1 → assina e confirma → bloqueia documento → repete Docs 2 e 3 → operador confere → pacote individual fica `3/3 BLOQUEADO` → mostra data/hora/versão simuladas.

### C. Retificação
Operador detecta falha → solicita correção com justificativa → perfil autorizado aprova → documento muda para `em correção`, com versão anterior preservada → nova assinatura e confirmação → pacote volta a concluído após reconferência → lote do evento, se já fechado, exige retificação formal e nova exportação, nunca alteração silenciosa do lote antigo.

### D. Fechamento
Conferir pacote de cada pessoa elegível e exceções → verificar pré-requisitos de jornada/folha → fechar **Funcionários do Evento** para aquele evento → bloquear versão do lote → gerar manifesto e exportação (simulados) → status `Entregue ao Drive` e `Disponível à contabilidade` somente após sucesso confirmado na futura solução real → registrar histórico de entrega.

### E. Arquivamento operacional
Após 30 dias (hipótese configurável), evento deixa a listagem operacional comum → aparece no Arquivo autorizado → lotes, PDFs e auditoria preservados segundo política legal. No protótipo mostrar etiqueta `Arquivado` e acesso restrito, sem excluir dados.

## 7. Estados UX necessários

- **Não respondeu:** nunca pintar como recusado; ícone neutro/cinza ou âmbar.
- **Recusado/Não confirmado:** estado distinto do sem resposta.
- **Assinado e bloqueado:** sinal visual inequívoco, com ação de editar desabilitada.
- **Aguardando autorização:** reabertura ainda não executada.
- **Upload pendente:** Drive não recebeu; não exibir `Concluído`.
- **Erro e tentativa:** preservar estado local e indicar recuperação.
- **Sem rede:** indicador evidente; evitar confirmar assinatura offline como finalizada sem segurança validada.
- **Acesso negado:** não revelar dados de outro grupo/área/liderança.
- **Evento arquivado:** somente leitura conforme perfil.

## 8. Ordem de prototipação recomendada

**Sprint de design 1:** 01 Login, 02 Home, 03 Eventos, 04 Evento/2 módulos, 06 Funcionários do Evento, 11 Áreas, 12 Lideranças, 13 Funcionários, 14 Ficha, 15/16 Docs/Assinatura, 17 Pacote bloqueado.

**Sprint de design 2:** 07 Convocados, 08 Convocar, 09 Convite, 10 Formulário, 19 Pendências, 20 Fechamento, 21 Drive.

**Sprint de design 3:** módulo Intermitentes separado, Relatórios, Auditoria simulada, Arquivo, estados especiais e navegação de validação.

No Claude Artifacts, pode gerar tudo em um único protótipo React com estados e fixtures, **sem integrações reais**.


---

# ARQUIVO: 03_DESIGN_SYSTEM.md

# MCD Eventos — Design System para Claude

## 1. Fonte da identidade visual

**Referência prioritária:** imagem da tela de login do **Portal MCD Normas** fornecida pelo cliente na conversa. **Referência institucional complementar:** https://www.mcdcontabil.com.br/.

A captura mostra: logo com símbolo amarelo + lettering azul; painel institucional azul-petróleo à esquerda; cartão de login branco com cantos bastante arredondados à direita sobre fundo cinza claro; título institucional branco de alto contraste; pequenos rótulos em amarelo; botões azuis; textos escuros; ornamentos semicirculares discretos.

**Não afirmar que os valores abaixo são oficiais.** São aproximações da captura; confirmar identidade oficial posteriormente. Não reproduzir usuário/senha presentes na captura.

## 2. Tokens visuais propostos

| Token | Cor HEX aproximada | Uso |
|---|---|---|
| `--mcd-primary` | `#1C7D9D` | Azul principal, CTA, sidebar, links |
| `--mcd-primary-dark` | `#146C88` | Hover, cabeçalho, fundo de elementos fortes |
| `--mcd-accent` | `#F4C225` | Marca, destaques, notificações selecionadas |
| `--mcd-bg` | `#F2F2F2` | Fundo de páginas |
| `--mcd-surface` | `#FFFFFF` | Cards, tabelas e formulários |
| `--mcd-text` | `#404950` | Texto principal |
| `--mcd-muted` | `#647681` | Legendas, subtítulos |
| `--mcd-border` | `#D7E0E5` | Bordas delicadas |
| `--mcd-success` | `#2F8C67` | Confirmação, pacote completo |
| `--mcd-warning` | `#B88417` | Aguardando, pendente |
| `--mcd-danger` | `#BB4C49` | Recusa, erro e bloqueio de operação |

Cores de status são **propostas de interface**, não necessariamente integrantes da paleta da marca. Verificar contraste acessível, especialmente amarelo sobre branco; preferir amarelo para ícones e acentos, não para textos longos.

## 3. Tipografia

A família de fonte exata **não pôde ser confirmada a partir da captura**. Para prototipagem, usar `Inter, Arial, sans-serif` (ou `system-ui`), identificando-a como **fonte provisória**. Ajustar após receber manual de marca ou inspecionar fonte do site e do portal.

Hierarquia sugerida: título da página 28–32 px/semibold, cabeçalho 22–26, corpo 14–16, labels 12–14, botões 14–16. Em tablet, jamais usar corpo muito pequeno em lista densa.

## 4. Espaçamento, raio, borda e interação

- Grid de **8 px**, espaçamentos comuns 8 / 12 / 16 / 24 / 32.
- Cards `border-radius: 16–24px`; cartão de login até `28–32px`.
- Botões altura 44–52 px; alvos touch mínimos confortáveis próximos de 44px.
- Inputs altura 44–50 px; borda clara e foco azul perceptível.
- Cards sobre fundo quase branco com sombra sutil (não intensa).
- Filtros em linha, chips de status discretos; contagens e ações em posição previsível.
- Navegação por breadcrumb com evento/grupo/área/líder; etiqueta do grupo sempre muito visível.
- Estados de foco, loading, disabled, hover e erros com contraste suficiente; não depender apenas de cor.

## 5. Login (seguir composição da imagem)

**Desktop:** layout em duas áreas: aproximadamente 57% à esquerda azul-petróleo com logo/símbolo, tagline, frase institucional e pequenos benefícios; 43% à direita cinza-claro com cartão branco central contendo logo MCD, `ACESSO RESTRITO`, título `Portal MCD Eventos`, usuário/e-mail, senha, lembrar acesso, recuperar senha e botão `Entrar no portal`.

**Tablet:** preservar o painel de marca em proporção menor ou simplificado; cartão branco central e campos grandes. **Celular:** empilhar marca e formulário, sem cortar logo.

Exemplo de texto original para o produto (não precisa copiar texto de outro sistema):

- Sobrelinha: `PLATAFORMA DE GESTÃO DE EVENTOS`
- Título: `Operações organizadas. Eventos com mais agilidade.`
- Descrição: `Convocação, equipes, assinaturas e fechamento documental em um só lugar.`
- Formulário: `Portal MCD Eventos` / `Acesso restrito`.

## 6. Página inicial

- Header fixo claro ou azul MCD com logo, título `MCD Eventos`, notificações e perfil.
- Corpo com título `Calendário de eventos`, alternância de mês e grade. Um dia com vários eventos pode ter um badge numérico.
- Ao escolher dia, exibir seção `Eventos de [data]` com cards/banner, nome, local, horário e status. Não pressupor um evento por dia.
- **Abaixo do calendário, seção/aba `Destaques`**, com cards de avisos e notificações futuras (ex.: eventos em aproximação, convites sem resposta, assinaturas pendentes, entregas em atraso). O sistema deve suportar estado vazio.

## 7. Detalhe do evento: escolha entre 2 módulos

A tela precisa tornar a separação **visualmente inequívoca**:

- Cabeçalho com logo MCD, imagem do evento, título, local e data.
- Dois cards de mesmo nível, cada um com título, ícone, descrição, métricas **do próprio grupo**, botão de acesso:
  - `Intermitentes` — `Gerenciar intermitentes`.
  - `Funcionários do Evento` — `Áreas, lideranças, documentos e folha`.
- Não usar tab única `Todos os funcionários` nem somar números sem identificar grupos.

## 8. Área / liderança / lista

**Áreas**: card grid 3x3 em desktop ou 2 colunas em tablet; área com nome legível e número de lideranças/funcionários e progresso.

**Lideranças**: tabela ou cards em colunas `Código`, `Nome completo`, `Funcionários`, `Documentos completos`, `Pendências`; vários líderes por área.

**Funcionários**: tabela densa porém tocável, header fixo, busca global pelo código/nome, filtros de status, barra com progresso `X/3` e botão `Abrir ficha`; em tablet, cards individuais responsivos quando necessário.

## 9. Ficha e assinatura no tablet

- Cabeçalho: mini foto/placeholder, código, nome completo, evento + grupo, área + liderança.
- Informações complementares (tel./email/endereço) em seção colapsável com controle de permissão.
- Três cartões `Documento 1`, `Documento 2`, `Documento 3` com status, versão, última ação.
- Visualização ampla em PDF; ação `Assinar` destacada, caixa de assinatura com suporte a toque/caneta em **simulação**.
- Fluxo `Revisar → Confirmar assinatura → Documento bloqueado`; confirmação em modal para evitar toques acidentais.
- Bloqueado = cadeado visível, metadados e ação comum indisponível. Correção exige `Solicitar reabertura` para perfil autorizado.

## 10. Auditoria/backlog (UI planejada)

Mostrar seção `Histórico de alterações (planejado)` com protótipo visual de registro: data/hora, autor, ação, entidade afetada, versão, motivo. NÃO fingir que eventos estão sendo realmente gravados no protótipo. Não armazenar cada tecla digitada, mas ações e alterações confirmadas na futura implementação.

## 11. CSS de referência para o Claude Artifacts

```css
:root {
  --mcd-primary: #1C7D9D;
  --mcd-primary-dark: #146C88;
  --mcd-accent: #F4C225;
  --mcd-bg: #F2F2F2;
  --mcd-surface: #FFFFFF;
  --mcd-text: #404950;
  --mcd-muted: #647681;
  --mcd-border: #D7E0E5;
  --mcd-success: #2F8C67;
  --mcd-warning: #B88417;
  --mcd-danger: #BB4C49;
  --mcd-radius-card: 20px;
  --mcd-radius-input: 14px;
  --mcd-shadow: 0 10px 30px rgb(16 50 66 / 7%);
  font-family: Inter, system-ui, Arial, sans-serif;
}
```

**Observação:** se o site atual e a captura divergirem, utilizar **a captura do Portal MCD Normas como referência visual principal**, que foi a preferência expressa pelo cliente. Confirmar com marca institucional antes de desenvolvimento final.


---

# ARQUIVO: 04_MODELO_DE_DADOS_E_ARQUIVAMENTO.md

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


---

# ARQUIVO: 05_CRITERIOS_DE_ACEITE.md

# MCD Eventos — Critérios de aceite do protótipo

## Como validar

Os cenários abaixo usam **pessoas/eventos fictícios** e **simulação local**, não envios/assinaturas reais. O protótipo deve navegar sem telas mortas nas tarefas centrais.

| ID | Cenário | Resultado esperado |
|---|---|---|
| C01 | Acessar login | Visual segue referência MCD: painel azul, cartão branco, detalhes amarelos; sem credenciais reais. |
| C02 | Entrar | Abre **Calendário**, com **Destaques abaixo**. |
| C03 | Selecionar 25/10/2026 | Mostra **dois eventos diferentes no mesmo dia** em cards com banner/logo e local. |
| C04 | Abrir um evento | Cabeçalho com MCD, evento, local e data; **dois módulos separados**: Intermitentes e Funcionários do Evento. |
| C05 | Abrir Intermitentes | Nenhuma lista, lote, total ou folha do módulo Funcionários do Evento aparece por engano. |
| C06 | Abrir Funcionários do Evento | Mostra navegação própria: Resumo, Convocados, Áreas/Alocação, Documentos, Fechamento de Folha. |
| C07 | Entrar em Áreas | Aparecem BAR, AMBULANTE, SERVIÇOS GERAIS, FINANCEIRO, ESCRITÓRIO, COZINHA, PRODUÇÃO, ESTOQUISTA e STAFF. |
| C08 | Abrir BAR | Mostra **múltiplas lideranças** com código e nome completo. |
| C09 | Abrir uma liderança | Lista somente pessoas atribuídas àquela liderança naquele evento/grupo/data. |
| C10 | Pesquisar por código | Filtra rapidamente sem carregar visualmente todas as 3.000 pessoas. |
| C11 | Abrir pessoa | Mostra foto/placeholder, código, nome completo e contato/endereço de forma autorizada. |
| C12 | Abrir Convocados | Totais e estados **Confirmado, Não respondeu e Não confirmado**; todos os convidados permanecem na lista. |
| C13 | Aceitar convite | Status vira Confirmado, mas formulário fica pendente e não há assinatura automática. |
| C14 | Completar formulário | Pessoa elegível passa a integrar a lista operacional, mas continua em Convocados. |
| C15 | Recusar convite | Pessoa não entra na lista operacional apta; segue visível em Convocados como Não confirmado. |
| C16 | Abrir pacote | Mostra 3 documentos separados e contagem `0/3`. |
| C17 | Confirmar Doc 1 | Doc 1 bloqueado; contagem `1/3`; Docs 2 e 3 ainda pendentes. |
| C18 | Confirmar Docs 2 e 3 | Contagem `3/3`; pacote pode ser conferido e bloqueado. |
| C19 | Tentar editar documento bloqueado | Edição não é possível; há procedimento especial de reabertura autorizada. |
| C20 | Simular reabertura | Pede motivo, guarda versão anterior (simulada), cria nova versão/novo estado; não apaga histórico. |
| C21 | Fechar com pendências | Bloqueia fechamento ou exige exceção expressamente aprovada; não declara exportação completa. |
| C22 | Fechar com todos requisitos | Gera lote bloqueado **do grupo correto**, manifesto e envio simulado. |
| C23 | Simular falha no envio Drive | Exibe `Erro/Tentar novamente`, sem status falso de Entregue. |
| C24 | Entregar ao Drive | Mostra status `Entregue` apenas após sucesso simulado, com data/hora e versão. |
| C25 | Corrigir após lote exportado | Exige **nova versão de exportação**, mantendo lote antigo intocado. |
| C26 | Ver status de folha | Apenas módulo **Funcionários do Evento** tem fluxo de fechamento de folha que foi pedido. |
| C27 | Ver auditoria/backlog | Exibe previsão/visualização de histórico fictício e identifica que o backend real será posterior. |
| C28 | Filtrar eventos antigos | Após regra fictícia de 30 dias, evento aparece em Arquivo; documentos não desaparecem. |
| C29 | Usar tablet | Botões tocáveis, filtros fáceis, visualizador de documentos legível, navegação responsiva. |
| C30 | Tentar abrir outro grupo sem autorização | UI nega acesso ou orienta; nenhuma informação privada de outro módulo é exibida. |

## Matriz mínima de permissão (protótipo)

| Ação | Admin | Coordenador | Líder | Contabilidade |
|---|---|---|---|---|
| Criar evento/cadastros | Sim | Conforme permissão | Não | Não |
| Convocar pessoas | Sim | Sim | Não, por padrão | Não |
| Ver outra liderança | Sim | Sim, no evento | Não | Conforme necessidade |
| Coletar assinatura | Conforme permissão | Conforme permissão | Sim, para sua equipe | Não |
| Reabrir documento | Sim ou aprovador designado | Solicitar/aprovar conforme política | Solicitar | Não |
| Fechar grupo/folha | Sim | Conforme permissão | Não | Conferir/aprovar conforme política |
| Exportar/consultar lote | Sim | Conforme permissão | Não | Sim, em seu escopo |
| Ver auditoria sensível | Sim | Restrito | Restrito | Restrito |

## Casos obrigatórios de não mistura

1. `INTERMITENTE` e `FUNCIONARIO_EVENTO` são seleções mutuamente explícitas na navegação.
2. Mesmo código de pessoa em dois eventos distintos gera **participações separadas**.
3. Uma lista de liderança não traz pessoa da mesma área, mas de outra liderança.
4. Convite confirmado não é `documento assinado` nem `presença confirmada`.
5. Um lote de Funcionários do Evento não contém PDFs ou lançamentos de Intermitentes.
6. Encerramento de um grupo não fecha automaticamente o outro.

## Definição de pronto para a fase de design

- O fluxo completo é clicável com dados fictícios e design consistente.
- Há explicação de decisões de UX, componentes, breakpoints e regras de tela.
- Os dois módulos ficam separados em todas as áreas críticas.
- Protótipo reconhece pendências, bloqueios, retificações, Drive e arquivo em 30 dias como **simulações**.
- Claude apresenta limitações e perguntas abertas, sem presumir definições jurídicas e trabalhistas.


---

# ARQUIVO: 06_PROMPT_INICIAL_CLAUDE.md

# PRIMEIRA MENSAGEM PARA ENVIAR AO CLAUDE

Você será meu **Product Designer sênior, UX Architect e responsável pela prototipação no Claude Artifacts** para o projeto **MCD Eventos**.

**Leia integralmente os documentos anexados**, na ordem indicada em `00_COMECE_AQUI.md`, e use o `08_DADOS_DE_EXEMPLO.json` como base para os dados fictícios. Não comece a programar backend.

## Contexto e problema

Hoje os trabalhadores são convocados por e-mail, aceitam, preenchem/assinam documentos e, no dia do evento, precisam assinar um pacote de três documentos. Os papéis são enviados à contabilidade no dia seguinte e digitalizados manualmente, causando atraso no fechamento da folha. Quero uma plataforma visualmente alinhada à MCD para operar eventos grandes, como no Maracanã, com referência de 3.000 pessoas e 9.000 documentos por evento.

## Minha prioridade principal: NÃO MISTURAR OS GRUPOS

**Depois de clicar em um evento, preciso enxergar e escolher entre 2 módulos INDEPENDENTES:**

- **INTERMITENTES**
- **FUNCIONÁRIOS DO EVENTO**

Navegação, convocados, funcionários, documentação, status, relatórios e exportação não podem ser misturados. No módulo **Funcionários do Evento**, preciso do **fechamento da folha do evento** e de uma futura **trilha de auditoria/backlog** das alterações confirmadas no ambiente de assinatura (o backend do log ficará para outra fase). Não invente que o fluxo de folha dos Intermitentes seja idêntico.

## Fluxo de interface que quero visualizar

1. **Login** seguindo o estilo do screenshot do Portal MCD Normas: painel azul-petróleo à esquerda, logo amarelo/azul, cartão branco à direita, acentos amarelos, botões azuis e layout limpo. Site complementar: https://www.mcdcontabil.com.br/. Nunca copie usuário/senha do screenshot.
2. **Home** após o login com **calendário** e uma seção **Destaques logo abaixo** para avisos e notificações futuras.
3. Ao clicar na data, exibir **cards com logo/banner dos eventos**, permitindo **múltiplos eventos no mesmo dia**.
4. Ao clicar num evento, exibir cabeçalho `logo MCD + nome + local + data + banner` e dois grandes cards para escolher **Intermitentes** ou **Funcionários do Evento**.
5. Entrando em **Funcionários do Evento**, mostrar `Convocados`, `Áreas/Alocação`, `Documentos`, `Fechamento de Folha` e `Relatórios`.
6. `Convocados` tem **TODOS** os convidados com código, nome completo, área, liderança, status `Confirmado / Não respondeu / Não confirmado`, situação do formulário e filtros. Ao confirmar convite por aplicativo/portal ou e-mail, a pessoa fica confirmada; depois precisa concluir formulário para estar apta na operação. Ela **continua na lista Convocados**, e só aparece na lista operacional se apta.
7. Em `Áreas/Alocação`, exibir **BAR, AMBULANTE, SERVIÇOS GERAIS, FINANCEIRO, ESCRITÓRIO, COZINHA, PRODUÇÃO, ESTOQUISTA, STAFF**.
8. Ao clicar numa área, exibir **múltiplas lideranças**, cada uma com **código e nome completo**.
9. Ao clicar numa liderança, exibir a **lista de funcionários daquela liderança, naquele evento/data**, por código e nome, com status e progresso `0/3 → 3/3`.
10. Ao clicar no funcionário, abrir ficha com **foto fictícia, código, nome completo, telefone, e-mail, endereço (restrito), grupo, área e líder**, e **três documentos**.
11. Simular abrir PDF, assinar com dedo/caneta, confirmar, **bloquear documento**; ao completar 3/3, **conferir e bloquear o pacote individual**.
12. Mostrar painel de pendências, checklist de fechamento e, quando tudo exigido estiver correto (ou exceções aprovadas), **fechar e bloquear o lote documental do módulo/evento**, preparando entrega ao **banco/armazenamento e Google Drive/contabilidade**, com estados de envio. Não misturar lotes dos dois grupos.
13. Mostrar a área `Auditoria / Backlog — planejado` com registros fictícios de quem alterou o quê, quando e por qual motivo. Deixar explícito que o mecanismo real será implementado depois; nunca apagar versões antigas em reaberturas.
14. Prever política operacional de **30 dias**: eventos antigos saem da operação e vão para `Arquivo`, mas não há exclusão automática definitiva de PDFs e documentos trabalhistas sem política de retenção validada.

## Entrega que quero AGORA

**Primeiro**, resuma em até 15 linhas o entendimento das regras de negócio e apresente o sitemap, destacando visualmente a separação de Intermitentes e Funcionários do Evento.

**Segundo**, defina os tokens do Design System usando as cores aproximadas da referência visual: azul `#1C7D9D`, amarelo `#F4C225`, branco `#FFFFFF`, cinza `#F2F2F2` e texto `#404950`. Trate-os como provisórios; a fonte também é provisória até verificação da identidade oficial. Dê especial atenção à versão desktop e tablet.

**Terceiro**, **crie um protótipo navegável de verdade no Claude Artifacts**, com navegação funcional e estados locais simulados, com estas telas prioritárias:

- Login
- Calendário + Destaques
- Cards de múltiplos eventos no mesmo dia
- Evento com **2 módulos separados**
- Funcionários do Evento > Áreas > Lideranças > Funcionários
- Convocados, convite, aceite e formulário
- Ficha individual + 3 documentos + assinatura simulada + bloqueio
- Pendências, fechamento de folha e simulação de envio ao Drive
- Visão breve do módulo Intermitentes, **isolada**, para provar que não há mistura

Utilize os dados fictícios anexados e gere registros adicionais localmente se necessário. Todos os botões principais do fluxo devem realizar uma ação de protótipo ou navegar para a etapa correspondente, nunca simular envio de e-mail, Drive ou assinatura real sem informar claramente.

**Quarto**, apresente a lista de componentes reutilizáveis, critérios de aceite atendidos e pontos abertos para a futura implementação no Lovable ou Flutter.

## Regras finais

- UI inteira em português do Brasil.
- Use breadcrumbs para manter explícitos evento > grupo > área > liderança.
- Separe aceite do convite, formulário, presença, assinatura e fechamento.
- Não incluir pessoas recusadas em alocação operacional ativa.
- Reabertura exige permissão e motivo; versões anteriores permanecem no histórico.
- Fechamento final não deve acontecer automaticamente apenas porque 3/3 aparecem; exige checagem de pendências, exceções e requisitos de folha.
- Banco de dados, Google Drive, notificações reais, assinatura válida juridicamente e automação de auditoria não serão implementados nesta etapa.
- Se faltar alguma decisão, use a hipótese explicitamente marcada em `07_DECISOES_ABERTAS.md`, sem bloquear a primeira apresentação.
- Não simplifique a hierarquia `Evento → Grupo → Área → Liderança → Funcionários → Pacote de 3 documentos`.

**Comece agora pela arquitetura das telas e entregue o protótipo com o design MCD.**


---

# ARQUIVO: 07_DECISOES_ABERTAS.md

# MCD Eventos — Decisões para confirmar com operação, DP e contabilidade

Este é um **registro de dúvidas e hipóteses**, não impedimentos ao início do protótipo. O Claude deve adotar as hipóteses abaixo com rótulo `A VALIDAR` onde necessário.

| Tema | Hipótese para protótipo | Pergunta de validação antes da implementação |
|---|---|---|
| Quantidade de pessoas | ~3.000 por evento, somando participantes, com escala de 9.000 PDFs nos fluxos com 3 docs | O pico por evento é 3.000 no total ou só em Funcionários do Evento? |
| Dois grupos | Dois módulos independentes por evento | Há alguma pessoa que possa participar nos dois grupos do mesmo evento? Como resolver esse conflito? |
| Intermitentes | Convocação, aceite, formulário e documentos separados | O pacote dos 3 documentos também é obrigatório a todos os intermitentes? Quais são os modelos? |
| Funcionários do Evento | Possuem operação de documentos e fechamento de folha por evento | Quais campos/apurações compõem o fechamento de folha deste grupo? |
| Documento 1/2/3 | Três documentos configuráveis em cada fluxo | Quais os nomes exatos, regras, ordem e momento legal de cada assinatura? |
| Formulário pós-aceite | Concluir formulário antes de entrar na lista operacional | Quais campos são obrigatórios e há aprovação humana? |
| Líder | Uma pessoa alocada sob uma liderança por turno/evento | Há troca de líder/área durante o evento? Mantemos histórico por período? |
| Jornada/presença | Estado separado da assinatura | Como presença, ponto e horas trabalhadas serão apurados? |
| Coleta por tablet | Operador autenticado coleta assinatura diante do trabalhador | Há necessidade de modo offline? Como identificar/validar assinante? |
| Bloqueio de evento | Fechamento apenas com todos elegíveis completos ou exceções aprovadas | Quais tipos de exceção permitem fechar (falta, substituição, documento dispensado)? |
| Envio para contabilidade | Exportação organizada por grupo com Drive + banco/armazenamento | A contabilidade quer PDFs individuais, ZIPs por líder ou lotes de evento? |
| Drive | Pasta por ano/evento/grupo/versão | Qual conta Google Workspace, unidade compartilhada e perfil de acesso? |
| Um mês de eventos | 30 dias corridos contados da data do evento | É mês calendário, 30 dias da data ou 30 dias do fechamento? |
| Guarda legal | Arquivar sem exclusão definitiva em 30 dias | Qual política de retenção e descarte aprovada pelo jurídico/DP/LGPD? |
| Auditoria/backlog | Registro de alterações confirmadas, motivos e versões; implementação futura | Quais ações exigem aprovação, alertas e revisão? Quem pode ver os logs? |
| Marca | Paleta aproximada da captura, tipografia provisória | Possuem logo em SVG/PNG transparente, manual de marca e fonte oficial? |
| Volume de eventos | Múltiplos no mesmo dia | Quantos eventos simultâneos e operadores/tablets no pico? |

## Decisões que **já foram expressamente dadas** e não devem voltar a ser tratadas como dúvida

- **Calendário na home** e seção **Destaques logo abaixo**.
- A mesma data pode ter **vários eventos**.
- Cabeçalho do evento com **MCD + nome + local + data**.
- **Intermitentes ≠ Funcionários do Evento**, sem mistura de listas ou fechamento.
- Áreas iniciais são BAR, AMBULANTE, SERVIÇOS GERAIS, FINANCEIRO, ESCRITÓRIO, COZINHA, PRODUÇÃO, ESTOQUISTA e STAFF.
- Cada área pode ter **vários líderes**, identificados por **código e nome completo**.
- Abaixo do líder estão somente seus funcionários no evento/dia.
- O fluxo documental descrito possui **3 documentos por trabalhador**, com bloqueio após confirmação.
- O responsável precisa conseguir iniciar uma correção auditável, sem apagar histórico anterior.
- A meta é eliminar digitalização e repasse manual dos documentos.
- **Funcionários do Evento têm fechamento de folha do evento**.
- Auditoria/backlog de alterações no ambiente de assinatura será detalhado **mais à frente**, mas deve ser prevista no design.
- Somente **um mês de eventos deve permanecer no ambiente operacional**; a guarda documental é questão distinta.


---

# ARQUIVO: 09_CONTRATOS_DE_TELA.md

# MCD Eventos — Contratos de tela e ações de protótipo

A finalidade deste documento é deixar explícitos **dados de entrada, itens visíveis, filtros, ações e estados**. Todos os campos e operações são simulados no Claude Artifacts nesta fase.

## T01 — Login

**Visível:** marca, título, usuário/e-mail, senha em branco, recuperar senha, botão entrar, texto de proteção de acesso.

**Ação:** Entrar → T02. Não pré-preencher credenciais da imagem. Se houver senha no protótipo, usar apenas validação fictícia local e legenda `Demonstração`.

## T02 — Home/Calendário

**Visível:** data atual simulada/configurável, calendário mensal, indicadores de datas com eventos, `Destaques` abaixo com `Avisos`, `Convites pendentes`, `Documentos pendentes` e `Novidades` (sem integração real).

**Ação:** clicar dia → T03. Alterar mês não deve quebrar navegação.

## T03 — Eventos do dia

**Visível:** cards por `evento_id`, banner/logo, nome, local, horário, status de operação.

**Ação:** clicar card → T04 para `evento_id` exato. Ter ao menos dois eventos na mesma data nos dados fictícios.

## T04 — Detalhe do evento

**Visível:** logo MCD, banner, nome, data, local, dois módulos com **totais separados por grupo**.

**Ação:** `Abrir Intermitentes` → T05 e `Abrir Funcionários do Evento` → T06. Mostrar breadcrumb.

## T05 — Intermitentes

**Visível:** cabeçalho marcado `INTERMITENTES`, convocados deste grupo, alertas, acesso aos seus documentos, histórico e exportações, sem dados do outro grupo.

**Ação:** Convocados → T07 filtrado pelo grupo Intermitentes. Não oferecer botão de folha do grupo Funcionários do Evento neste módulo.

## T06 — Funcionários do Evento

**Visível:** cabeçalho `FUNCIONÁRIOS DO EVENTO`, KPIs próprios, menu `Convocados`, `Áreas/Alocação`, `Documentos`, `Fechamento de folha`, `Relatórios` e `Auditoria — planejada`.

**Ação:** Áreas → T11; Convocados → T07 com `grupo=FUNCIONARIO_EVENTO`.

## T07 — Convocados

**Visível:** métricas independentes; colunas `código, nome completo, área prevista, liderança, resposta, formulário, aptidão`; filtro por área, líder, convite, formulário; busca por nome/código.

**Ações:** pessoa → T14; `Convidar` → T08. Confirmado ainda permanece na tabela Convocados. Recusa nunca vira aceite automaticamente.

## T08 — Convocar

**Visível:** seletor de pessoa(s), código, evento fixo, grupo fixo e visível, área/líder, cargo/função, turno, canal (`e-mail` ou `portal/app`).

**Ação:** `Simular envio` → estado Enviado/Não respondeu, criado somente na simulação local.

## T09 — Responder convite

**Visível:** evento, data/local/turno, grupo, função, líder quando apropriado, `Confirmar`, `Não confirmar`.

**Ações:** Confirmar → altera resposta e segue T10; Não confirmar → status Não confirmado; permanece em Convocados.

## T10 — Formulário

**Visível:** dados cadastrais necessários, campos de teste não sensíveis, consentimentos/informações juridicamente pertinentes a validar, botão Concluir.

**Ação:** Concluir → habilita aptidão quando demais regras atendidas. Não gera assinatura nem presença automaticamente.

## T11 — Áreas/Alocação

**Visível:** nove áreas obrigatórias com contagem de líderes e trabalhadores **apenas do grupo selecionado**.

**Ação:** selecionar área → T12. Guardar `area_id` no estado de navegação.

## T12 — Lideranças

**Visível:** códigos, nomes completos, total de alocados aptos, pendências/3 documentos por liderança.

**Ação:** selecionar líder → T13 com `evento_id + grupo + area_id + lider_id`.

## T13 — Funcionários do líder

**Visível:** código, nome completo, convite, formulário, situação de presença (se aplicável), progresso docs e status de pacote.

**Ação:** clicar linha → T14. Não listar recusados/sem resposta como aptos, nem de outro líder/grupo.

## T14 — Ficha

**Visível:** foto/avatar, código, nome completo, contatos e endereço com visualização restrita, evento, grupo, área, liderança, turno, três documentos, mini-histórico.

**Ação:** abrir doc → T15; solicitar correção → T18 (sujeito a permissão).

## T15/T16 — PDF e assinatura

**Visível:** título, índice de documento, resumo de condições, PDF fictício, rolagem/zoom, área de assinatura simulada, aviso de que a assinatura é **demonstração**.

**Ação:** `Confirmar` → altera status local da versão para `Bloqueado` e incrementa `x/3` sem duplicação; se já confirmado, bloquear novo clique e exibir estado correto.

## T17 — Pacote completo

**Visível:** três documentos individualmente bloqueados e versionados, progresso 3/3, resultado de conferência, status final do pacote.

**Ação:** `Conferir e bloquear pacote` (simulado, após requisitos cumpridos).

## T18 — Correção e histórico

**Visível:** solicitação, motivo obrigatório, papel autorizador, versões atuais e anteriores.

**Ação:** solicitar → aprovar como administrador fictício → gerar `v2` deixando `v1` disponível no histórico e não mais ativa. Mostrar necessidade de reconferência e retificação se lote já entregue.

## T19 — Pendências

**Visível:** progressos do evento/grupo, filtros por áreas/lideranças/participante, exceções, pendências de documentação e jornada.

**Ação:** abrir funcionário ou retornar à liderança para concluir tarefas.

## T20 — Fechamento de folha/documental

**Visível:** checklist `pacotes concluídos`, `ausências justificadas`, `jornada apurada`, `conferência`, `aprovação`; data/versão do lote.

**Ação:** `Fechar e bloquear` somente no módulo autorizado, com requisitos simulados completos. No módulo Intermitentes, não oferecer o fechamento da folha do outro módulo.

## T21 — Exportação Drive

**Visível:** lote do **grupo selecionado**, manifesto, versão, status `Aguardando`, `Processando`, `Entregue`, `Falhou`; destino lógico do Drive e permissões.

**Ação:** `Simular envio` com opção de sucesso e falha. Não usar Drive real nesta fase.

## T22/T23/T24 — Relatórios, auditoria e arquivo

**Relatórios:** filtros por evento/grupo/área/liderança e dados agregados, sem exportação misturada. **Auditoria:** timeline fictícia com autor, ação e momento; rótulo `Implementação futura`. **Arquivo:** eventos fora da janela operacional de 30 dias, acesso somente leitura conforme perfil e **sem apagar documentos**.


---

## DADOS FICTÍCIOS

O dataset demonstrativo detalhado está no arquivo `08_DADOS_DE_EXEMPLO.json` da pasta/ZIP. Upload separado recomendado para usar os exemplos diretamente no protótipo.
