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
