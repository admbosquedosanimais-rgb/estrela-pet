# Prompt para Lovable.dev — Aplicar o design produzido em TODAS as páginas existentes do clubeestrelapet.com

> Cole o conteúdo abaixo da linha `─────` no Lovable, **dentro do projeto existente** do clubeestrelapet.com (não em um projeto novo). É uma instrução de **refatoração visual global**, mantendo todas as rotas, dados, autenticação e integrações já implementadas.

─────

# Refatoração de design — Clube Estrela Pet (todo o site)

## Contexto

Este projeto já está rodando em `clubeestrelapet.com` com várias páginas, autenticação, dados e integrações (provavelmente ASAAS para pagamentos, possivelmente Supabase pra dados). **Não toque na lógica de negócio, na autenticação, no schema do banco, nas chamadas de API ou nos webhooks.** A intervenção é **100% de UI / design system / copy de superfície**, aplicada de forma consistente em **todas as páginas existentes do projeto**.

Antes de começar:
1. Liste todas as rotas/páginas existentes do projeto (homepage, planos, plataforma, dashboard, login, cadastro, checkout, FAQ, políticas, memorial, etc.).
2. Identifique os componentes globais (Header, Footer, Layouts, Sidebar) que se repetem.
3. Identifique todos os tokens de cor/fonte que estão sendo usados hoje.

Em seguida, aplique a refatoração descrita abaixo **em todas as páginas e componentes**.

---

## 1. Novo sistema de design (substitua o atual integralmente)

### Cores — defina como CSS vars no `globals.css` e como tokens no Tailwind. Substitua todas as cores hard-coded existentes pelos tokens equivalentes em todos os arquivos.

```css
--bg: #F1ECE2;         /* fundo cream principal */
--bg-soft: #E8E1D2;    /* alternância de seções */
--bg-paper: #FBF8F2;   /* cards / superfícies elevadas */
--ink: #1F2A1E;        /* texto forte / display */
--ink-mid: #3D4A3A;    /* corpo de texto */
--ink-soft: #6B6856;   /* labels / hints / mono */
--forest: #2C4A2E;     /* primário · header · botões verdes · cremação */
--forest-deep: #1A2E1C;/* footer · variantes escuras */
--gold: #B89148;       /* italics / acentos / dourado fosco */
--gold-warm: #D4A857;  /* botões dourados / glows */
--gold-soft: rgba(184,145,72,0.14);
--line: rgba(31,42,30,0.12);  /* divisores */
--danger: #9E3A2E;     /* erros de formulário */
```

**Regra:** o site INTEIRO usa essa paleta. Cremes nos fundos. Verde-floresta como cor de marca. Dourado como acento emocional (italics, badges, prova social). Sem azul, sem cinza neutro, sem cores acidentais.

### Tipografia — substitua todas as fonts existentes

- **Display serif:** `Cormorant Garamond` (300, 400, 500, 600, 700 + italic) — Google Fonts
- **UI sans:** `Geist` (300–700) — Google Fonts
- **Mono labels:** `Geist Mono` (400, 500) — Google Fonts

Defina três classes utilitárias globais:
```css
.serif { font-family: 'Cormorant Garamond', Georgia, serif; font-weight: 500; letter-spacing: -0.015em; }
.serif-it { font-family: 'Cormorant Garamond', Georgia, serif; font-style: italic; font-weight: 500; }
.mono { font-family: 'Geist Mono', monospace; text-transform: uppercase; letter-spacing: 0.08em; font-size: 10px; font-weight: 500; }
```

**Regra de hierarquia:** todo H1/H2 usa `serif`, com 1–2 palavras-chave em `serif-it` + `color: var(--gold)`. Todo "eyebrow" / label / disclaimer usa `mono` + `color: var(--ink-soft)` ou `var(--gold)`. Body em `Geist` regular, `--ink-mid`, line-height 1.55.

---

## 2. Componentes globais — substitua os existentes

### Header (em TODAS as páginas, exceto checkout / dashboard logado se houver layout próprio)
- Background `--forest`, texto cream
- Logo: estrela 5 pontas em SVG num quadrado cream + "Clube *Estrela* Pet" (Estrela em italic dourado) + sub-tagline mono "CUIDADO EM TODAS AS FASES · BH"
- Direita: botão "Entrar" outline + hamburger menu (modal slide-down com backdrop blur)
- Menu: links pra TODAS as rotas existentes (descubra e plote) — Início, Como Funciona, Plataforma, Planos, Bosque dos Animais, FAQ, etc. — em serif grande, com sub-label mono cinza dourado, separadores horizontais
- Sticky com `position: sticky; top: 0; z-index: 40`

### Barra de fundadores (logo abaixo do header em páginas comerciais — home, planos, plataforma)
- Background `--forest-deep`, texto `--gold-warm`
- Texto mono "VAGAS DE FUNDADOR · 37 DE 100 RESTANTES" centralizado
- Bullet dourado com `box-shadow: 0 0 14px var(--gold-warm)` e `animation: pulse 2s infinite`
- Não exibir em páginas internas/logado

### Footer (em TODAS as páginas)
- Background `--forest-deep`, texto creme 60% opacity
- Logo + nome
- Parágrafo curto: "CLUBE ESTRELA PET LTDA. Plataforma do ecossistema Bosque dos Animais — referência em cuidado pet em Belo Horizonte."
- Links: Política de Privacidade, LGPD, Termos, Contato, Instagram, Bosque dos Animais
- Copyright + CNPJ em mono pequena cinza dourado

### Cards (padrão global)
- `background: var(--bg-paper)`
- `border: 1px solid var(--line)`
- `border-radius: 14–18px`
- `box-shadow: 0 1px 0 var(--line), 0 30px 60px -30px rgba(0,0,0,0.18)`

### Botões primários (padrão global)
- `background: var(--forest)`, texto `--bg`
- `border-radius: 14px`, padding `18px 22px`
- Ícone de seta dourada à direita
- `box-shadow: 0 10px 30px -10px rgba(44,74,46,0.55)`
- Hover: leve lift + sombra mais densa

### Botões secundários
- Outline 1px `var(--forest)`, texto verde, fundo transparente, mesmas dimensões

### Botões "premium" / destaque
- `background: var(--gold-warm)`, texto `var(--forest-deep)`, mesmo radius/padding

### Eyebrows (padrão global, repetido em todas as seções "marketing")
```jsx
<div className="mono flex items-center gap-2 mb-5">
  <EstrelaMark size={9} color="var(--gold)"/>
  <span style={{ color: 'var(--ink-soft)' }}>TEXTO DA SEÇÃO</span>
</div>
```

### Inputs de formulário (padrão global em login, cadastro, checkout, perfil)
- Label mono uppercase 9.5px acima
- Container: `bg-paper`, border 1px `line`, radius 11px, padding 12x14
- Foco: border passa pra `--forest`
- Erro: border `--danger`, label `--danger`, hint vermelho abaixo

### Eyebrow + H2 + body — fórmula para abrir QUALQUER seção
1. Eyebrow mono com estrela (3–6 palavras uppercase)
2. H2 serif 32–38px, line-height 1.0, letter-spacing -0.025em, font-weight 500, com 1–2 palavras-chave em serif-it dourado
3. Body 14–15px, line-height 1.55–1.6, `--ink-mid`

---

## 3. Aplicação página por página

### 3.1 Homepage (`/`)
Refaça a homepage com **TODAS as 15 seções** abaixo, na ordem (substituindo o conteúdo atual da homepage):

1. **Header sticky** + **Barra de Fundadores**
2. **Hero:**
   - Eyebrow: `★ CLUBE DE BENEFÍCIOS · DO BOSQUE DOS ANIMAIS`
   - Headline (4 linhas): "Todo o cuidado / com seu pet. / *Num só lugar.* / Pra vida toda." — "Num só lugar" em serif-it dourada
   - Subline: "Saúde, finanças, lembretes, memórias e uma *despedida digna* — reunidos numa só plataforma, com a estrutura do **Bosque dos Animais em BH**."
   - CTA "Quero fazer parte" verde
   - Micro-copy mono: "A PARTIR DE R$ 19,90/MÊS · CANCELE QUANDO QUISER · ACESSO IMEDIATO"
   - Imagem hero (mantenha a foto atual da tutora com o cão, ou peça uma nova) com card flutuante dourado mostrando "+370 avaliações 5★ no Google" (contador animado)
3. **Marquee** ticker italic dourado: "saúde organizada · finanças sob controle · memórias guardadas · lembretes pontuais · amparo até o fim · do primeiro ao último dia"
4. **Identificação da dor:**
   - Eyebrow `★ A ROTINA DE QUEM AMA UM PET`
   - H2 "Cheia de *pontas soltas.*"
   - Lista numerada 01–05 com as 5 dores do briefing (carteira de vacina, gastos, próxima vacina, fotos espalhadas, decisão difícil)
   - Card de fechamento: *"Cuidar de verdade é mais do que amar."* / "É estar preparado."
5. **Solução + 6 funcionalidades** (com mockups originais):
   1. **Carteira Digital** — perfil do pet + status de vacinas
   2. **Jornada da Saúde** — timeline de eventos
   3. **Jornada Financeira** — donut chart + categorias + comparativo
   4. **Lembretes Inteligentes** — notificações com IA aprendendo a rotina
   5. **Histórico & Memórias** — grid de fotos com timeline
   6. **Estrela IA · 24h** — chat assistente com bubble do tutor + resposta da IA cruzando histórico + chips de ação ("📅 Agendar consulta") + indicador "digitando…"
6. **Benefícios** (background verde-floresta, texto creme): 8 transformações do briefing, cada uma com círculo outline dourado + check + headline serif + descrição
7. **Prova social:** grid 2x2 de stats (+370 / #1 / 1 / 24h) com contadores animados + 3 cards de depoimentos com placeholders e tags (organização / amparo / desconto)
8. **Planos:** Essencial R$19,90 (card claro) + Premium R$38,90 (card verde-floresta com badge dourado "MAIS ESCOLHIDO" e ancoragem *"menos de R$1,30/dia"*)
9. **Quebra de objeções:** 3 aspas em serif italic verde + respostas (não quero pensar em morte / pet novo e saudável / já tenho plano de saúde)
10. **Garantia + Fundadores** (background verde-escuro): card outline dourado de garantia + contador animado de fundadores (desce de 100 → 37 com barra de progresso preenchendo até 63%)
11. **FAQ:** 7 perguntas em accordion com smooth animation
12. **CTA final:** estrela dourada centralizada + "*Seu pet cuida de você todos os dias.*" / "Agora é a *sua vez*…" + CTA verde grande
13. **P.S.** em serif italic dourada gigante + parágrafo de fechamento
14. **Footer**

### 3.2 Página /planos (ou equivalente)
- Mantenha a integração ASAAS / backend
- Header global + Barra Fundadores
- Hero curto: eyebrow `★ PLANOS · CLUBE ESTRELA PET` + H1 "Dois planos. *Zero pegadinha.*" + subline curto
- **Seção comparativa** lado a lado dos planos Essencial e Premium (mesmo design dos cards da home, mas grande e detalhado)
- **Tabela de comparação detalhada** (background `bg-soft`):
  - Linhas com features: Carteira digital, Jornadas, Lembretes IA, Histórico, Cremação, Desconto no Bosque, Memorial
  - Colunas: Essencial / Premium
  - Marcadores verdes (check) ou cinza (—)
- **Bloco de garantia** outline dourado
- **FAQ** focado em planos (3–5 perguntas: cancelamento, troca de plano, formas de pagamento, fidelidade, comprovante)
- CTA final + Footer

### 3.3 Página /como-funciona (se existir, ou crie)
- Hero com H1 "Como o Clube cuida do seu pet, todos os dias."
- Linha do tempo vertical com 4 passos:
  1. **Você se associa** — escolhe o plano, cadastra você e seu pet (2 min)
  2. **Recebe acesso à plataforma** — Carteira digital ativada na hora
  3. **A plataforma trabalha por você** — Estrela IA aprende a rotina, lembretes começam, jornadas ativas
  4. **Você é amparado em cada fase** — saúde, finanças, memórias, benefícios no Bosque e, se for o caso, amparo no momento da despedida
- Cada passo: número grande em serif dourada + label + descrição + ilustração de tela do app (use os mockups da homepage)
- CTA final + Footer

### 3.4 Página /plataforma (se existir, ou crie)
- Hero "Conheça a plataforma. *Pra vida toda do seu pet.*"
- Apresentação detalhada das 6 funcionalidades (use os mesmos mockups da homepage, mas com mais espaço cada e descrições expandidas — 2–3 parágrafos por funcionalidade)
- Bloco IA com destaque maior: como a Estrela IA aprende padrões, sugere ações, cruza histórico
- Bloco "Segurança e LGPD" com selos
- CTA final + Footer

### 3.5 Página /bosque-dos-animais (se existir, ou crie)
- Hero "O ecossistema que sustenta o Clube."
- Apresentação do Bosque dos Animais como referência em cuidado pet em BH
- Stats reais: +370 avaliações 5★, anos de operação, # de famílias atendidas
- Diferenciação: o Clube é a ponta digital de um ecossistema físico (consultório, cremação, sepultamento, produtos)
- CTA para conhecer o Bosque físico + CTA para se associar ao Clube
- Footer

### 3.6 Página /cadastro ou /checkout
- **Não recriar a lógica** — preserve o fluxo ASAAS/auth atual
- **Substitua a UI** por um fluxo de 5 passos em modal-like ou página fullscreen:
  1. **Escolher plano** (cards Essencial + Premium com badge "MAIS ESCOLHIDO" + card destaque "VAGA DE FUNDADOR")
  2. **Dados do tutor** (Nome, E-mail, Celular com máscara, CPF com validação de DV, checkbox LGPD obrigatório)
  3. **Dados do pet** (espécie segmented control, nome, nasc, peso, raça opcional, upload de foto)
  4. **Pagamento** (resumo + tabs Cartão/Pix; cartão com mockup visual verde-floresta com gradient que preenche em tempo real; selo "🔒 PAGAMENTO SEGURO · ASAAS · LGPD")
  5. **Boas-vindas** (background verde-floresta; estrela dourada; "ASSOCIADO FUNDADOR · Nº 064"; H1 "Bem-vindo ao Clube, *{primeiro nome}.*"; recap card; bullets; botão "Abrir minha plataforma")
- Validação com React Hook Form + Zod
- Header de cada passo com barra de progresso (4 segmentos)

### 3.7 Página /login
- Layout centralizado, background `--bg`
- Card central `bg-paper` com border + sombra suave
- Logo estrelado no topo
- H1 serif: "Entrar no Clube"
- Campos: e-mail + senha + "esqueci minha senha"
- Botão primário verde
- Link: "Ainda não é associado? *Quero fazer parte.*"
- Sem sidebar / sem distrações

### 3.8 Dashboard logado (se existir)
- **Mantenha a estrutura de dados real** (perfil do pet, lembretes, histórico, etc)
- Aplique o sistema visual: sidebar `--forest-deep` colapsível com ícones Lucide + labels mono, conteúdo principal sobre `--bg`
- Topbar com logo estrelado + avatar do tutor + nome do pet ativo
- Widgets/dashboards usando os mesmos mockups (Carteira Digital como card principal, Jornada da Saúde, Jornada Financeira, Lembretes feed, Memórias grid, Estrela IA chat persistente em side drawer)
- Botões e tipografia seguem o sistema global

### 3.9 Páginas legais (`/politica-privacidade`, `/termos`, `/lgpd`)
- Header + Footer globais
- Container centralizado max-width 720px
- Tipografia: H1 serif 40px, H2 serif 24px, body Geist 15px line-height 1.7
- Aplicar o nome **CLUBE ESTRELA PET LTDA** (e não "Bosque dos Animais") nos documentos
- Adicionar última atualização em mono pequena no topo
- Sem ornamentação visual além do typography rhythm

### 3.10 Página de memorial (se existir, plano Premium)
- Layout cinematográfico, mais sensível
- Background `--bg-paper` com micro textura sutil
- Foto grande do pet + nome em serif italic dourada gigante
- Linhas da vida (data nascimento → data partida) em mono
- Galeria de memórias em grid de 6–9 fotos
- Bloco "Em homenagem a {nome}, por {tutor}" em serif italic
- Tom: discreto, respeitoso, NENHUMA estrela decorativa cheia — só linhas, só tipografia

### 3.11 Página 404 / Erro
- Centralizada, mínima
- Estrela dourada gigante no fundo (10% opacity)
- H1 serif "Não achamos essa página."
- Subline italic "Mas a gente ainda está cuidando dos pets."
- Botão "Voltar pra home"

---

## 4. Interações globais a aplicar em todas as páginas

- **Scroll reveal** (`IntersectionObserver`) em todos os blocos de conteúdo principal: `translateY 16px → 0` + `opacity 0 → 1`, 0.7s `cubic-bezier(.2,.7,.2,1)`, com delay escalonado em listas (60–80ms)
- **Contadores animados** em todas as stats numéricas (+370, 37/100, etc), 1.4s easeOutCubic
- **FAQ accordion** com smooth max-height + opacity
- **Marquee CSS** linear infinite 38s
- **Pulse animado** em bullets de fundadores
- **Modal slide-up** com backdrop blur em qualquer modal (cadastro, login, confirmação)
- **Transições de página** suaves (fade 200ms)

---

## 5. Responsividade — política global

Esta marca é **deliberadamente mobile-first com layout "narrow column"** mesmo em desktop:
- 0–480px: layout mobile cheio
- 480–1024px: centralize em coluna max-width 460px
- 1024px+: mantenha a coluna 460–500px centralizada, com background `--forest-deep` cobrindo as laterais, dando sensação de "artefato impresso" (estilo Stripe Press / Linear / Cron)
- **Não tente layouts horizontais multi-coluna em desktop** — vai contra o tom editorial premium da marca

Exceção: dashboard logado pode usar layout horizontal com sidebar (típico de app SaaS).

---

## 6. Preserve

- Toda a autenticação atual (login, signup, reset)
- Toda a integração com ASAAS para pagamentos
- Toda a estrutura de dados (Supabase / Prisma / etc.) — NÃO mexa em schema
- Webhooks, edge functions, env vars
- SEO existente (meta tags) — apenas atualize valores para refletir o novo posicionamento se necessário (cor do theme deve ser `#2C4A2E`)
- Rotas existentes (mesmas URLs)

## 7. Remova ou substitua

- Toda a paleta antiga (cores hard-coded fora do novo sistema)
- Fontes antigas (substitua por Cormorant + Geist + Geist Mono)
- Qualquer componente que não siga o novo design system — refaça com a linguagem nova
- Emojis decorativos espalhados (mantenha só 🔒 em selo de segurança e 📅 em chip do mockup IA — nada mais)
- Gradientes psicodélicos / cores acidentais
- Cards com left-border accent colorida (tropo a evitar)

---

## 8. Conteúdo de marca — vocabulário a usar consistentemente

- "Clube Estrela Pet" (sempre completo no primeiro uso de cada página; "o Clube" depois)
- "Bosque dos Animais" — sempre que mencionar, associar a "em BH" ou "ecossistema"
- "Estrela IA" — nome da assistente
- "Associados Fundadores" — para os primeiros 100
- "Cuidado em todas as fases" — tagline auxiliar
- Tom: equilibrado — **afetivo na abertura, racional no meio, sensível no fim**

Evite em copy / ads:
- "única plataforma" como afirmação absoluta (use "a plataforma que reúne tudo num só lugar")
- "mais bem avaliada do segmento" (use "uma das mais bem avaliadas" se não houver comparativo formal)

---

## 9. Ordem de execução sugerida

1. Atualize `globals.css` / Tailwind config com os novos tokens
2. Importe as 3 fontes do Google Fonts no layout raiz
3. Crie os componentes globais: `EstrelaMark`, `Header`, `Footer`, `FounderBar`, `MobileMenu`, `Eyebrow`, `Reveal`, `AnimatedNumber`, `Accordion`, `Placeholder`, `PrimaryButton`, `SecondaryButton`, `FormField`
4. Crie os componentes de mockup: `MockCarteira`, `MockJornada`, `MockFinanceira`, `MockLembrete`, `MockMemorias`, `MockIA`
5. Refatore a homepage com todas as 15 seções
6. Refatore cada página listada (/planos, /como-funciona, /plataforma, /bosque-dos-animais, /cadastro, /login, /404, /politica-privacidade, /termos, /memorial, dashboard se houver)
7. Verifique consistência: NENHUMA cor hard-coded fora dos tokens, NENHUMA font fora das 3 escolhidas, todos os botões e cards seguem o padrão

---

## 10. Quando terminar

- Liste todas as páginas refatoradas
- Mostre um screenshot da homepage rodando
- Liste qualquer página que você NÃO conseguiu refatorar (com motivo)
- Liste qualquer integração que você TOCOU acidentalmente (idealmente: nenhuma)

Execute tudo num passe completo. Priorize fidelidade visual ao sistema descrito sobre features extras. Não invente novas seções nem novas funcionalidades que não estejam aqui.
