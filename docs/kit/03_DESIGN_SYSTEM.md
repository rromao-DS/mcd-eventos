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
