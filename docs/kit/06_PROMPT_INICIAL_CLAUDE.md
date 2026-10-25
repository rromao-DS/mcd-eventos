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
