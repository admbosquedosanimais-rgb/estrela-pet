# Prompt Lovable — Auditoria e refatoração completa (follow-up)

> Cole esta mensagem como **resposta** no mesmo chat do Lovable onde você rodou o prompt anterior. É uma instrução de auditoria forçada — o agente vai listar o que falta e completar.

─────

# AUDITORIA OBRIGATÓRIA — refatoração incompleta

Você fez algumas mudanças no design system seguindo o prompt anterior, mas **não terminou o trabalho em todas as páginas**. O briefing era explícito: o sistema visual novo (cremes + verde-floresta `#2C4A2E` + dourado `#B89148` + Cormorant Garamond + Geist + Geist Mono) deve estar **aplicado de forma consistente em TODAS as páginas e TODOS os componentes do projeto**, não só na homepage.

Antes de qualquer nova alteração, execute essa auditoria e me devolva o relatório:

---

## Passo 1 — Inventário forçado

Liste, em formato de tabela markdown:

| Rota | Arquivo principal | Header novo? | Footer novo? | Tipografia (Cormorant + Geist) aplicada? | Cores antigas remanescentes? | Componentes novos usados? | Status |
|---|---|---|---|---|---|---|---|
| /   | app/page.tsx       | ✅ / ❌ | ✅ / ❌ | ✅ / ❌ | sim/não | sim/não | ✅ refatorada / ⚠️ parcial / ❌ não tocada |
| /planos | ... | ... | ... | ... | ... | ... | ... |
| ... (TODAS as rotas que existem no projeto) | ... | ... | ... | ... | ... | ... | ... |

Inclua **todas** as rotas: marketing, autenticação (login, signup, reset), checkout, dashboard logado, perfil, configurações, memorial, FAQ, políticas, termos, LGPD, 404, error pages, qualquer página administrativa. Se há rotas dinâmicas (`/pet/[id]`, `/memorial/[slug]`), liste o template.

---

## Passo 2 — Inventário de violações de design system

Faça um `grep` ou busca no projeto inteiro e me reporte:

### Cores hard-coded fora dos tokens
Liste todos os arquivos que ainda contêm cores fora do novo sistema (qualquer `#xxxxxx`, `rgb(...)`, `hsl(...)`, `bg-blue-*`, `text-gray-*`, `border-red-*` etc. que NÃO sejam um dos tokens definidos: `--bg`, `--bg-soft`, `--bg-paper`, `--ink`, `--ink-mid`, `--ink-soft`, `--forest`, `--forest-deep`, `--gold`, `--gold-warm`, `--gold-soft`, `--line`, `--danger`).

### Fontes hard-coded fora do sistema
Liste todos os arquivos que referenciam `Inter`, `Roboto`, `Arial`, `system-ui`, `Helvetica`, `Manrope`, `Poppins` ou qualquer outra fonte que **não seja** Cormorant Garamond, Geist ou Geist Mono.

### Componentes legados não substituídos
Liste todos os botões, cards, headers, footers, inputs e modais que ainda usam markup antigo (não chamam os novos componentes globais `<Header/>`, `<Footer/>`, `<FounderBar/>`, `<PrimaryButton/>`, `<Eyebrow/>`, `<Reveal/>`, etc).

---

## Passo 3 — Plano de execução

Com base na auditoria, monte um plano de execução numerado:

1. Pra cada página em status ⚠️ ou ❌, o que precisa ser feito (em 1 linha).
2. Pra cada violação de cor/fonte/componente, qual a correção.
3. Ordem sugerida (priorize páginas comerciais primeiro: home, planos, plataforma, como-funciona, bosque-dos-animais, cadastro, depois login, depois dashboard, depois legais, depois 404).

---

## Passo 4 — Execução

**Não pare na primeira página.** Refatore TODAS as páginas do plano, na ordem. Aplicando integralmente:

- Header global novo em todas as páginas marketing/auth (esconda só em dashboard se houver layout próprio)
- Footer global novo em TODAS as páginas
- Barra de fundadores nas páginas comerciais (home, planos, plataforma, bosque)
- Tipografia: H1/H2 sempre em `font-serif` (Cormorant Garamond) com 1–2 palavras-chave em italic dourada (`text-gold italic`); body em Geist; labels em Geist Mono uppercase tracking 0.08em
- Cards: `bg-paper` + border 1px `--line` + radius 14–18px + sombra `0 30px 60px -30px rgba(0,0,0,0.18)`
- Botões primários verde-floresta com seta dourada
- Eyebrows mono com estrela em todas as seções marketing
- Reveal-on-scroll nos blocos principais
- Layout **narrow column** centralizado (max-width 460–500px) em desktop nas páginas marketing — laterais com `--forest-deep`
- Cores: 100% via CSS vars / tokens Tailwind — zero hard-coded
- Preserve TODA a lógica de negócio, autenticação, ASAAS, schema do banco, env vars, webhooks

---

## Passo 5 — Validação final

Quando terminar, rode novamente a tabela do Passo 1 e me devolva. Critério de "✅ refatorada" pra uma página:
- Header e Footer novos presentes
- Nenhuma cor fora dos tokens
- Nenhuma fonte fora das 3 escolhidas
- Componentes globais novos sendo usados (não copy-paste de HTML antigo)
- Layout responsivo conforme política descrita

Se uma página NÃO puder ser refatorada por algum motivo técnico (ex: integração 3rd-party com markup próprio), me explique exatamente o motivo — não pule silenciosamente.

---

## Regras inegociáveis

1. **Não invente novas seções nem features** além das descritas no prompt anterior. Apenas aplique o sistema visual ao conteúdo existente de cada página.
2. **Não toque em lógica de negócio, banco, auth, pagamentos**.
3. **Não pule páginas**. Se a auditoria listou 12 rotas, todas as 12 precisam virar ✅ ou ter justificativa explícita.
4. **Não pare no meio**. Execute o plano inteiro num passe só.
5. **Mostre o resultado** ao final: screenshots da homepage + 2–3 outras páginas refatoradas + a tabela do Passo 5.

Comece pelo Passo 1 agora.
