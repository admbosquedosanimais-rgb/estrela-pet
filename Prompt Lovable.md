# Prompt para Lovable.dev — Clube Estrela Pet

> Cole o conteúdo abaixo da linha `─────` no Lovable. Está em PT-BR, otimizado pra resposta direta do agente.

─────

# Construa: Clube Estrela Pet — landing page + fluxo de cadastro

Construa uma **landing page mobile-first** + **fluxo de cadastro multi-step** para o **Clube Estrela Pet**, um clube de assinatura do ecossistema **Bosque dos Animais (BH)** que organiza a vida inteira do pet (saúde, finanças, lembretes, memórias) e oferece amparo até a despedida.

Stack: **Next.js (App Router) + TypeScript + Tailwind CSS + shadcn/ui + Framer Motion**. Use React Hook Form + Zod para validação. Lucide para ícones.

---

## 1. Sistema de design (defina como tokens no Tailwind)

**Cores (estética: cream + verde-floresta + dourado editorial)**
- `--bg`: `#F1ECE2` (creme principal)
- `--bg-soft`: `#E8E1D2`
- `--bg-paper`: `#FBF8F2` (cards)
- `--ink`: `#1F2A1E` (texto forte)
- `--ink-mid`: `#3D4A3A` (texto corpo)
- `--ink-soft`: `#6B6856` (texto suave / labels)
- `--forest`: `#2C4A2E` (verde primário · botões / header)
- `--forest-deep`: `#1A2E1C`
- `--gold`: `#B89148` (acento / italics)
- `--gold-warm`: `#D4A857`
- `--line`: `rgba(31,42,30,0.12)` (divisores)

**Tipografia (Google Fonts)**
- **Serif display:** Cormorant Garamond (italics são MUITO usadas como acento dourado — sempre que houver uma palavra-chave romântica/afetiva)
- **Sans UI:** Geist (300–700)
- **Mono labels:** Geist Mono — uppercase, tracking 0.06–0.14em, fontSize 9–11px (usada para "eyebrows", labels de campos, ribbons)

**Padrões visuais:**
- Headlines display sempre com 1–2 palavras-chave em `Cormorant Garamond italic` + cor dourada (`--gold`). Ex: *"Num só lugar"*, *"Vida inteira"*, *"Pra vida toda"*.
- "Eyebrows" sempre em `mono uppercase` + ícone de estrela ⭐ pequeno + texto curto. Ex: `★ CLUBE DE BENEFÍCIOS · BOSQUE DOS ANIMAIS`.
- Cards: `border: 1px solid var(--line)`, `border-radius: 14–18px`, `background: var(--bg-paper)`, sombra suave `0 30px 60px -30px rgba(0,0,0,0.18)`.
- Botões primários: `--forest` background, `--bg` texto, `border-radius: 14px`, padding generoso (18px 22px), ícone de seta dourada à direita.
- Tom geral: **editorial, calmo, premium**. Muito respiro vertical. Tipografia faz o peso. NUNCA use gradientes chamativos, neon, emoji decorativo, AI-slop.

**Logo:** estrela 5 pontas (SVG simples) + wordmark `"Clube Estrela Pet"` (com "Estrela" em italic dourado). Sub-tagline `"CUIDADO EM TODAS AS FASES · BH"` em mono pequena.

---

## 2. Estrutura da landing (uma página, scroll vertical)

Sticky header (verde-floresta) + barra de fundadores (verde-escuro com bullet dourado pulsando) → todas as 15 seções abaixo, separadas por bandas de cor alternadas (`bg`, `bg-soft`, `forest`, `forest-deep`).

### 2.1 Header (sticky)
- Logo + sub-tagline à esquerda
- À direita: botão "Entrar" outline + ícone hamburger (abre menu modal)
- Menu modal (slide-down, backdrop blur): links *Início · Como funciona · Plataforma · Planos · Bosque dos Animais* + CTA "Quero fazer parte" dourado

### 2.2 Barra de fundadores
- Background verde-escuro, texto dourado
- "VAGAS DE FUNDADOR · 37 DE 100 RESTANTES" em mono
- Bullet dourado com glow pulsante

### 2.3 Hero
- Eyebrow: `★ CLUBE DE BENEFÍCIOS · DO BOSQUE DOS ANIMAIS`
- Headline (4 linhas):
  ```
  Todo o cuidado
  com seu pet.
  Num só lugar.        ← italic dourada
  Pra vida toda.
  ```
- Subline: "Saúde, finanças, lembretes, memórias e uma *despedida digna* — reunidos numa só plataforma, com a estrutura do **Bosque dos Animais em BH**."
- CTA primário verde: "Quero fazer parte" + seta dourada
- Micro-copy mono: `A PARTIR DE R$ 19,90/MÊS · CANCELE QUANDO QUISER · ACESSO IMEDIATO`
- Imagem do hero (placeholder para foto real de tutor + pet) com:
  - Estrela dourada decorativa no canto superior direito
  - Card flutuante na base mostrando 5★ + contador animado "+370 avaliações 5★ no Google"
- Watermark: estrela gigante de baixa opacidade (5%) no fundo

### 2.4 Marquee/ticker
- Frases italic douradas correndo: "saúde organizada · finanças sob controle · memórias guardadas · lembretes pontuais · amparo até o fim · do primeiro ao último dia"
- Velocidade lenta (~38s loop)

### 2.5 Identificação da dor (background `bg-soft`)
- Eyebrow: `★ A ROTINA DE QUEM AMA UM PET`
- H2: "Cheia de *pontas soltas.*"
- Lista numerada (01–05) com divisores horizontais:
  1. A carteira de vacina some bem na hora que você precisa.
  2. Você nunca sabe ao certo quanto gasta com ele por mês.
  3. A próxima vacina? "Acho que é mês que vem…"
  4. As fotos e lembranças estão espalhadas em mil pastas do celular.
  5. E aquele pensamento que você empurra com a barriga: "um dia eu vou precisar tomar uma decisão difícil — e não faço ideia de como."
- Card de fechamento: *"Cuidar de verdade é mais do que amar."* / **"É estar preparado."**

### 2.6 Solução + 6 funcionalidades (background `bg`)
- Eyebrow: `★ A SOLUÇÃO · CLUBE ESTRELA PET`
- H2: "A primeira plataforma que organiza a *vida inteira* do seu pet — e te ampara até o momento mais delicado."
- Body: "Não é app de lembrete. Não é plano de saúde. Não é clube de descontos solto. É *tudo isso reunido*, com inteligência *(de verdade, IA)*, numa experiência só."
- Lista vertical de **6 funcionalidades**, cada uma com: número mono dourado, label em serif, descrição, e um **mockup interativo** abaixo:

  1. **Carteira Digital** — mostra pet (avatar, nome, idade, peso, ID) + lista de vacinas com status (em dia / atenção). *"Vacinas, exames e dados do pet sempre à mão — mesmo na emergência."*

  2. **Jornada da Saúde** — timeline com 4 eventos próximos (mês/dia + tag: vacina/consulta/rotina), próximo evento em destaque dourado. *"A plataforma te avisa do que está por vir. Você nunca é pego de surpresa."*

  3. **Jornada Financeira** — donut chart com 4 categorias (Ração, Saúde, Higiene, Outros) + valores + comparativo "−12% vs abril" + média de 6 meses. *"Pare de gastar no escuro. Veja pra onde vai cada real e planeje com tranquilidade."*

  4. **Lembretes Inteligentes** — lista de 3 notificações (vermífugo, reagendar consulta, renovar ração) com horário e ícone. *"A IA aprende a rotina e te avisa no momento certo — nada passa em branco."*

  5. **Histórico & Memórias** — grid 3x2 de placeholders de fotos com data + label (1º banho, parque, aniversário, etc), última célula é verde com "+138" italic. *"Cada fase guardada e protegida. Não perdida em mil pastas do celular."*

  6. **Estrela IA · 24h** — chat: bolha do tutor "A Luna está coçando muito a orelha. É normal?" → bolha da IA "Coceira frequente pode ser otite. Olhei o histórico — ela teve algo parecido em fev/25." com chips de ação ("📅 Agendar consulta", "Saber mais") + indicador "digitando…" animado + input bar. *"Apoio inteligente que entende seu pet. Tira dúvida, sugere consulta, prevê o que vai precisar."*

### 2.7 Benefícios (background `--forest`, cor `--bg`)
- Eyebrow: `★ A TRANSFORMAÇÃO`
- H2: "O que muda no dia a dia com seu pet."
- 8 itens, cada um com círculo outline dourado + check dourado + headline em serif + descrição:
  1. Nunca mais perca um dado importante.
  2. Saiba o que vem pela frente.
  3. Tenha controle real do quanto custa.
  4. Guarde cada momento pra sempre.
  5. Economize de verdade no Bosque. *(até 20% de desconto)*
  6. Tenha a decisão difícil já resolvida. *(cremação inclusa)*
  7. Eternize a homenagem. *(memorial Premium)*
  8. Sinta-se amparado, não vendido.
- Estrela gigante decorativa de fundo (10% opacidade)

### 2.8 Prova social (background `bg`)
- Eyebrow + H2: "Confiança que vem de *quem já cuida* com a gente."
- Grid 2x2 de stats em serif grande verde:
  - **+370** avaliações 5★ no Google *(contador animado quando entra na viewport)*
  - **#1** mais bem avaliada do segmento
  - **1** única plataforma que reúne tudo
  - **24h** amparo do primeiro dia ao último
- 3 cards de depoimentos (placeholders): cada um com 5★, "linhas" de texto simulando depoimento, avatar circular striped + label "[capturar com tutor real]" — tags: organização / amparo / desconto

### 2.9 Planos (background `bg-soft`)
- Eyebrow + H2: "Dois planos. *Zero pegadinha.*"

**Card Essencial** (claro, outline):
- Mono "PLANO" + serif "Essencial"
- R$ **19,90**/mês em verde
- Lista de 4 itens com check verde:
  - Todas as funcionalidades da plataforma
  - Carteira digital, jornadas, lembretes e histórico
  - Cremação coletiva inclusa
  - 10% de desconto no Bosque
- Botão outline "Assinar Essencial"

**Card Premium** (background `--forest`, texto creme):
- Badge dourado "MAIS ESCOLHIDO" no canto superior
- Estrela decorativa no fundo (10%)
- R$ **38,90**/mês em dourado, com italic abaixo: *"menos de R$ 1,30 por dia."*
- Lista de 4 itens com check dourado:
  - Tudo do Essencial
  - Cremação individual com devolução das cinzas
  - 20% de desconto no Bosque
  - Página memorial de homenagem póstuma
- Botão dourado "Assinar Premium"

- Disclaimer mono: `SEM FIDELIDADE · CANCELE QUANDO QUISER · LGPD`

### 2.10 Quebra de objeções (background `bg`)
- Eyebrow + H2: "E se você ainda *tiver dúvida…*"
- 3 blocos com aspas em serif italic verde + resposta em texto corpo:
  1. **"Não quero pensar em morte agora."** → A gente entende — e nem é sobre isso. O Clube é sobre viver melhor cada fase. A tranquilidade do fim é só uma consequência…
  2. **"Meu pet é novo e saudável."** → Que ótimo — esse é exatamente o melhor momento. Pet saudável = mais memórias registradas, mais economia acumulada…
  3. **"Já tenho plano de saúde pro meu pet."** → Perfeito. O Clube não substitui — complementa. Plano cuida da consulta. O Clube cuida da organização, finanças, memórias, benefícios e amparo.

### 2.11 Garantia + Fundadores (background `--forest-deep`, cor `--bg`)
- Card outline dourado: "Entra hoje e, se sentir que não é pra você, *cancela quando quiser* — sem multa, sem burocracia."
- Subseção Fundadores com:
  - Eyebrow `★ ASSOCIADOS FUNDADORES`
  - H2: "Quem entra agora entra como *fundador.*"
  - Descrição curta
  - **Contador animado de vagas** (desce de 100 → 37 quando entra na viewport, com barra de progresso preenchendo até 63%, cor dourada)

### 2.12 FAQ (background `bg`)
- Eyebrow + H2: "Pode *perguntar.*"
- 7 perguntas em accordion (uma aberta por vez, animação smooth max-height + opacity):
  1. O Clube substitui plano de saúde pet?
  2. Preciso usar a plataforma todo dia?
  3. E se meu pet for muito novo?
  4. Como funciona a cremação inclusa?
  5. Tem fidelidade?
  6. Quais as formas de pagamento?
  7. Meus dados e do meu pet estão seguros?
- Cada item: número mono à esquerda + pergunta em serif + botão "+" rotacionando 45° quando aberto

### 2.13 CTA final (background `bg-soft`)
- Estrela dourada centralizada no topo (12% opacidade, 64px)
- *"Seu pet cuida de você todos os dias."* (serif italic verde, centralizado)
- H2: "Agora é a *sua vez* de cuidar dele do jeito certo."
- CTA verde grande: "Quero fazer parte do Clube"
- Micro-copy mono
- *"Leva menos de 2 minutos."* (serif italic)

### 2.14 P.S. (background `bg`)
- "P.S." gigante em serif italic dourada (38px) + parágrafo reforçando empresa mais bem avaliada + escassez das 100 vagas

### 2.15 Footer (background `--forest-deep`, cor creme)
- Logo + nome
- Descrição curta CLUBE ESTRELA PET LTDA
- Links: Política de Privacidade, LGPD, Termos, Contato, Instagram, Bosque dos Animais
- Copyright + CNPJ mono pequeno

---

## 3. Fluxo de cadastro (modal slide-up mobile-first)

Ao clicar em qualquer CTA "Quero fazer parte" / "Entrar" / "Assinar Essencial" / "Assinar Premium", abre um **modal fullscreen mobile** (slide-up animation, backdrop blur) com 5 passos:

**Header de cada passo:** botão "Voltar" + label `PASSO X / 4` mono + barra de progresso (4 segmentos, preenchidos em verde) + H2 grande + sub.

### Passo 1 — Escolher plano
- Título: "Como você quer cuidar?"
- 2 cards selecionáveis (radio): Essencial e Premium (com badge "MAIS ESCOLHIDO" e ancoragem "R$ 1,30/dia"). Premium pre-selecionado se veio do CTA Premium.
- Card destaque dourado: "VAGA DE FUNDADOR — Você entra entre os primeiros 100 associados. **37 restantes.**"
- Botão "Continuar com Premium/Essencial"

### Passo 2 — Dados do tutor
- Título: "Sobre você"
- Campos (com máscara e validação Zod):
  - Nome completo (min 3 chars)
  - E-mail (regex válido)
  - Celular (máscara brasileira, min 10 dígitos)
  - CPF (máscara + validação de dígito verificador)
- Checkbox LGPD obrigatório: "Ao me associar, concordo com a Política de Privacidade e com o tratamento dos meus dados conforme a LGPD."
- Estados de erro em vermelho terra (`#9E3A2E`)

### Passo 3 — Dados do pet
- Título: "Sobre seu pet"
- Segmented control: Cão / Gato / Outro
- Nome do pet (texto)
- Grid 2col: Nascimento (MM/AAAA) + Peso (kg)
- Raça (opcional, com hint "Se não souber, pode deixar como SRD")
- Upload de foto (placeholder dashed border, opcional, mostra inicial do nome do pet quando vazio)

### Passo 4 — Pagamento
- Resumo do plano selecionado com link "alterar" dourado
- Tabs Cartão / Pix
- **Modo cartão:** mockup de cartão verde-floresta com gradient, logo estrelado dourado, número/titular/validade preenchidos em tempo real conforme o usuário digita
- Campos: Número, Nome no cartão, Validade (MM/AA), CVV
- **Modo Pix:** placeholder de QR code (xadrez preto e branco)
- Selo `🔒 PAGAMENTO SEGURO · ASAAS · LGPD`
- Botão "Confirmar e fazer parte"

### Passo 5 — Boas-vindas (background `--forest`)
- Estrela dourada gigante de fundo (10%)
- Ícone quadrado dourado com estrela
- Mono dourada: "ASSOCIADO FUNDADOR · Nº 064"
- H1 enorme em serif: "Bem-vindo ao Clube, *{primeiro nome do tutor}.*"
- Parágrafo: "A partir de agora, você e *{nome do pet}* têm acesso completo à plataforma…"
- Card recap (plano, próxima cobrança "28 jun · R$ XX,XX", pet) em background semi-transparente
- 3 bullets de próximos passos com check dourado
- Botão dourado "Abrir minha plataforma"
- Mensagem: "Um e-mail de boas-vindas foi enviado para **{email}**"

---

## 4. Interações e animações

- **Scroll reveal:** todos os elementos importantes fazem `translateY(16px) → 0` + `opacity 0 → 1` ao entrar na viewport (IntersectionObserver, threshold 0.1), duration 0.7s cubic-bezier(.2,.7,.2,1), com delay escalonado em listas (60–80ms entre itens).
- **Contadores numéricos:** quando a stat entra na viewport, anima de 0 → valor final em 1.4s (easing easeOutCubic). `+370` e o contador `37/100 fundadores` (que desce de 100 → 37 acompanhado da barra de progresso preenchendo).
- **Marquee:** animação CSS linear infinita, 38s.
- **FAQ accordion:** smooth max-height 0 → 400px + opacity, 0.4s cubic-bezier(.2,.7,.2,1).
- **Bullet pulsante** na barra de fundadores: opacity 1 → 0.4 → 1 em 2s loop.
- **Chat IA "digitando…":** 3 bolinhas com opacity 0.3 → 1 → 0.3 com stagger de 0.2s.
- **Modal de cadastro:** fade backdrop + slide-up do painel (translateY 20px → 0, 0.35s).
- **Hover de botões primários:** sombra mais densa + leve `translateY(-1px)`.

---

## 5. Responsividade

- **Mobile-first** (390px de design width). Tudo deve funcionar bem de 320px a 480px sem ajustes.
- **Tablet (768px+):** centralize o conteúdo numa coluna de no máx. 460px, com bordas laterais respirando.
- **Desktop (1024px+):** SEM rebuilding da landing — mantenha o mesmo layout mobile centralizado em uma coluna estreita de 460px, com background `--forest-deep` cobrindo as laterais. **A página é deliberadamente "narrow column" no desktop** (estilo editorial premium tipo Stripe Press / Linear), com a coluna central ganhando sombra lateral pra parecer um artefato impresso. Não tente forçar grid horizontal.

---

## 6. Conteúdo legal e técnico

- **LGPD:** checkbox obrigatório no cadastro. Política de Privacidade e Termos em rotas próprias.
- **CNPJ:** placeholder `XX.XXX.XXX/0001-XX` no footer — campo a preencher posteriormente com CLUBE ESTRELA PET LTDA.
- **Tracking sugerido:** insira `<Script>` placeholder para Meta Pixel e GA4 no `app/layout.tsx` (apenas estrutura, deixe IDs vazias com TODO comment).
- **Eventos:** dispare `track('Lead')` ao abrir o modal de cadastro, `track('InitiateCheckout')` ao chegar no passo 4, `track('Subscribe')` no submit do passo 4.

---

## 7. Estrutura de pastas sugerida

```
app/
  layout.tsx          (fonts Cormorant + Geist + Geist Mono, metadata SEO)
  page.tsx            (landing — orquestra as 15 seções)
  privacy/page.tsx
  terms/page.tsx
components/
  brand/
    EstrelaMark.tsx   (SVG estrela 5 pontas reutilizável)
    Logo.tsx
  layout/
    Header.tsx
    Footer.tsx
    FounderBar.tsx
    MobileMenu.tsx
  sections/
    Hero.tsx
    Marquee.tsx
    Pain.tsx
    Solution.tsx
    Benefits.tsx
    SocialProof.tsx
    Plans.tsx
    Objections.tsx
    Guarantee.tsx
    FounderCounter.tsx
    FAQ.tsx
    FinalCTA.tsx
    PostScript.tsx
  mockups/
    MockCarteira.tsx
    MockJornada.tsx
    MockFinanceira.tsx
    MockLembrete.tsx
    MockMemorias.tsx
    MockIA.tsx
  signup/
    SignupModal.tsx        (orquestrador)
    StepPlan.tsx
    StepTutor.tsx
    StepPet.tsx
    StepPayment.tsx
    StepWelcome.tsx
    schema.ts              (Zod schemas)
  ui/
    Reveal.tsx             (scroll reveal wrapper)
    AnimatedNumber.tsx
    Eyebrow.tsx
    Accordion.tsx
    Placeholder.tsx        (striped image placeholder com label mono)
lib/
  cn.ts
  format.ts                (máscaras CPF, telefone, cartão)
```

---

## 8. Estilo geral / "não faça"

- ❌ Não use emojis decorativos (apenas o lock 🔒 e o 📅 no chip do mockup IA — o resto é ícone Lucide ou SVG)
- ❌ Não use gradientes psicodélicos
- ❌ Não use Inter, Roboto, Fraunces (já temos Cormorant Garamond + Geist)
- ❌ Não invente ilustrações de pets em SVG — use placeholders striped com label mono "foto · tutor + pet"
- ❌ Não use cards arredondados com left-border accent (tropo de AI-design)
- ✅ Use muito espaço em branco / vertical rhythm
- ✅ Italic dourada como "voz emocional" do design — escolha 1 palavra por seção
- ✅ Mono uppercase pequena como contraponto técnico ao serif italic
- ✅ Cards com borda fina + sombra muito difusa (não dura)
- ✅ Headlines em serif com `letter-spacing: -0.02em` e `font-weight: 500`
- ✅ Componha hierarquia com tamanho + cor + estilo, não com peso forte

---

## 9. Dados iniciais para a demo

Quando o cadastro chegar ao passo 5, use estes valores se não houver input real ainda:
- Tutor: Maria Fernanda Silva · maria@email.com.br
- Pet: Luna · cão · 3 anos · 12,4 kg · SRD
- Plano: Premium · Próxima cobrança 28 jun · R$ 38,90
- Nº de fundador: 064

---

Construa tudo num primeiro passe completo — não fragmente. Priorize qualidade visual sobre features extras. Quando terminar, mostre a homepage rodando.
