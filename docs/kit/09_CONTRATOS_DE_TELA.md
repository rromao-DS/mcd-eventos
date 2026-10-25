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
