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
