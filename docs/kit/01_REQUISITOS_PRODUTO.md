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
