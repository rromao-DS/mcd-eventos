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
