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
