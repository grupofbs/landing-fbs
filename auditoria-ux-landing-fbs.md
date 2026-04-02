# Auditoria UX/UI — Landing Page FBS
**Auditora:** Sati — UX/UI Designer Grupo FBS  
**Data:** 2026-04-02  
**Urgência:** Alta — conversão necessária amanhã (R$12k)

---

## 1. HIERARQUIA VISUAL

### ✅ O que funciona
- Hero tem fluxo claro: badge → H1 → subtítulo → CTA
- `clamp()` no H1 é inteligente — escala bem entre mobile e desktop
- Gold/Navy criam contraste visual forte nas seções alternadas
- Pricing box com borda dourada chama atenção corretamente

### ❌ Problemas
| Problema | Severidade |
|----------|-----------|
| Hero não comunica o PRODUTO — "se eu pudesse te dar um presente" é teaser demais, sem âncora racional | 🔴 CRÍTICO |
| Formulário está visível no DOM desde o início (display: block), aparece antes do usuário entender o preço | 🔴 CRÍTICO |
| O botão "Quero escolher meu presente" no hero não deixa claro o que acontece depois | 🟡 ALTO |
| Seção reveal e pousada-details invisíveis por JS — hierarquia quebra antes da interação | 🟡 ALTO |
| Urgency bar sem timer real — "vagas limitadas" sem número não cria urgência | 🟡 ALTO |
| Sem social proof em lugar nenhum — zero logos, depoimentos ou números | 🟡 ALTO |

---

## 2. CONSISTÊNCIA DE CORES E TIPOGRAFIA

### ✅ O que funciona
- Navy #0A1628 e Gold #C9A84C aplicados de forma consistente
- Playfair Display nos headings, DM Sans no corpo — 100% alinhado ao brand
- Gold em Navy = **8.63:1 de contraste** ✅ (passa AAA)
- White em Navy = **18.66:1** ✅ Excelente

### ❌ Problemas
| Problema | Severidade |
|----------|-----------|
| `opacity: 0.5` no footer = branco transparente em fundo #060E1A ≈ **~4:1** — falha AA para body text | 🔴 CRÍTICO |
| `opacity: 0.7` em `.price-guarantee` e `.price-compare` — texto de preço importante com legibilidade comprometida | 🟡 ALTO |
| `--gold-light: #E8D5A0` no hover do CTA: contraste com Navy ≈ 10.2:1 ✅ (passa), mas o botão fica lavado visualmente | 🟢 BAIXO |
| `color: #666` nas descrições dos cards — contraste **5.74:1** ✅ passa AA, mas borderline em telas com glare | 🟡 MÉDIO |
| `opacity: 0.85` no hero `<p>` — funcional mas poderia ser cor sólida para consistência | 🟢 BAIXO |

---

## 3. ESPAÇAMENTO E ALINHAMENTO

### ✅ O que funciona
- Padding de seções consistente (80px 20px)
- `max-width` nos containers controla bem a legibilidade em telas largas
- Gap entre cards bem proporcionado (30px)

### ❌ Problemas
| Problema | Severidade |
|----------|-----------|
| `.math-box` com `justify-content: space-between` pode truncar textos longos em 375px (295px úteis após padding) | 🟡 MÉDIO |
| `.choice-card` com `min-width: 280px` — em 375px no modo coluna funciona, mas sem padding lateral extra pode costar | 🟢 BAIXO |
| `.hero-badge` com `letter-spacing: 2px` em font-size 0.85rem em 375px — pode ficar espremido se texto crescer | 🟢 BAIXO |

---

## 4. ESTADOS INTERATIVOS

### ✅ O que funciona
- Hover nos choice-cards: border gold + translateY(-5px) + shadow — ótimo feedback
- Hover nos CTAs: background change + translateY(-2px) + shadow — adequado
- Focus nos inputs: border-color gold — satisfatório

### ❌ Problemas
| Problema | Severidade |
|----------|-----------|
| Botão de submit sem estado `disabled` + loading durante abertura do WA — usuário pode clicar múltiplas vezes | 🔴 CRÍTICO |
| Choice-cards sem `tabindex="0"` e sem handler de teclado — inacessíveis por Tab/Enter | 🟡 ALTO |
| Sem `:focus-visible` nos botões — remove outline nativo sem substituir | 🟡 ALTO |
| Sem estado `active` (pressed) nos CTAs — falta de feedback tátil | 🟢 BAIXO |
| Sem feedback visual de sucesso após submit do formulário | 🟡 ALTO |

---

## 5. ACESSIBILIDADE

| Problema | Severidade | Norma |
|----------|-----------|-------|
| `<label>` sem atributo `for` correspondente ao `id` do input — não associados | 🔴 CRÍTICO | WCAG 1.3.1 |
| `onclick` inline nos choice-cards sem `role="button"` — screen readers não anunciam como interativo | 🔴 CRÍTICO | WCAG 4.1.2 |
| Emojis (🏖️, 📊, ✓) sem `aria-label` ou `aria-hidden` — leitores leem nomes completos | 🟡 ALTO | WCAG 1.1.1 |
| Sem `aria-live` region para anunciar quando reveal aparece | 🟡 ALTO | WCAG 4.1.3 |
| Animação `shimmer` infinita sem `prefers-reduced-motion` | 🟡 MÉDIO | WCAG 2.3.3 |
| Footer opacity 0.5 falha contraste AA | 🔴 CRÍTICO | WCAG 1.4.3 |
| Links "→" sem texto descritivo acessível | 🟡 MÉDIO | WCAG 2.4.6 |
| Sem `lang` nos elementos de idioma misto | 🟢 BAIXO | WCAG 3.1.2 |

---

## 6. MOBILE-FIRST (375px)

### ✅ O que funciona
- `@media (max-width: 600px)` empilha os cards corretamente
- `clamp()` no H1 e H2 são excelentes
- Padding 15px no hero mobile — adequado
- Máscara de WhatsApp funciona por input event

### ❌ Problemas
| Problema | Severidade |
|----------|-----------|
| `.math-box` sem `overflow-x: auto` — pode gerar scroll horizontal em valores longos | 🟡 MÉDIO |
| Delay de 2000ms no reveal (escolha "gestão") sem loading indicator — 2s de tela sem feedback causa abandono | 🔴 CRÍTICO |
| `.pousada-details` aparece ANTES do reveal (gestão path) — usuário rola para baixo e vê contexto fora de ordem | 🟡 ALTO |
| Formulário sem `inputmode="numeric"` e sem `autocomplete` nos campos | 🟡 MÉDIO |

---

## TOP 5 MELHORIAS PRIORITÁRIAS (para converter amanhã)

### 🥇 #1 — Countdown Timer Real na Urgency Bar
**Impacto:** Conversão +15-30%  
**Implementar:** Timer regressivo até meia-noite ("encerra em 04:32:17")  
**Risco:** Zero — só adiciona CSS/JS

### 🥈 #2 — Formulário Simplificado (Nome + WhatsApp apenas)
**Impacto:** Fricção -50%, submits +30%  
**Remover:** Campo "Você tem empresa?" e "O que te interessou mais?"  
**Por quê:** O vendedor qualifica no WhatsApp. Cada campo extra = abandono.

### 🥉 #3 — Corrigir Labels e Acessibilidade do Formulário
**Impacto:** Funcionalidade básica — sem isso, usuários mobile (preenchimento automático) têm mais fricção  
**Implementar:** `for`/`id` corretos, `autocomplete`, `inputmode`

### 4️⃣ #4 — Loading State + Reduzir Delay para 500ms
**Impacto:** Reduz abandono no mid-funnel significativamente  
**Implementar:** Spinner ou pulse nos 500ms + scroll suave imediato para reveal

### 5️⃣ #5 — Corrigir Contraste do Footer e Opacidades Críticas
**Impacto:** Acessibilidade legal (LGPD/WCAG) + legibilidade do CNPJ  
**Implementar:** Remover `opacity: 0.5` do footer, subir para cor sólida #8899AA

---

## DESIGN TOKENS DOCUMENTADOS

```css
:root {
  /* ── CORES ── */

  /* Primária — Navy */
  --color-primary:          #0A1628;  /* Fundo principal, texto em bg claro */
  --color-primary-dark:     #060E1A;  /* Footer, mais profundo */
  --color-primary-light:    #152238;  /* Hover states, gradients */

  /* Secundária — Gold */
  --color-secondary:        #C9A84C;  /* Accent, CTAs, bordas premium */
  --color-secondary-light:  #E2C97A;  /* Hover do secondary (melhor que #E8D5A0 atual) */
  --color-secondary-muted:  rgba(201, 168, 76, 0.12);  /* Backgrounds suaves */
  --color-secondary-border: rgba(201, 168, 76, 0.30);  /* Bordas sutis */

  /* Backgrounds */
  --color-bg-base:          #FFFFFF;  /* Seções claras */
  --color-bg-alt:           #F7F6F3;  /* Alternativo claro (levemente quente) */
  --color-bg-surface:       rgba(255, 255, 255, 0.05);  /* Cards sobre navy */
  --color-bg-surface-hover: rgba(255, 255, 255, 0.08);  /* Cards hover */

  /* Texto */
  --color-text-primary:     #0A1628;  /* Heading em bg claro */
  --color-text-body:        #3A3A3A;  /* Body em bg claro — 12.6:1 contraste */
  --color-text-secondary:   #595959;  /* Secundário — 7.0:1 contraste ✅ */
  --color-text-muted:       #757575;  /* Muted — 4.6:1 contraste ✅ mínimo AA */
  --color-text-inverse:     #FFFFFF;  /* Texto sobre navy */
  --color-text-inverse-muted: rgba(255, 255, 255, 0.75);  /* Muted sobre navy */

  /* Feedback */
  --color-success:          #2D7A4F;
  --color-error:            #C0392B;
  --color-warning:          #E67E22;

  /* ── TIPOGRAFIA ── */

  --font-heading: 'Playfair Display', Georgia, 'Times New Roman', serif;
  --font-body:    'DM Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;

  /* Escala modular (ratio 1.25) */
  --text-xs:    0.75rem;   /* 12px */
  --text-sm:    0.875rem;  /* 14px */
  --text-base:  1rem;      /* 16px */
  --text-lg:    1.125rem;  /* 18px */
  --text-xl:    1.25rem;   /* 20px */
  --text-2xl:   1.5rem;    /* 24px */
  --text-3xl:   1.875rem;  /* 30px */
  --text-4xl:   2.25rem;   /* 36px */
  --text-5xl:   3rem;      /* 48px */
  --text-6xl:   3.75rem;   /* 60px */

  /* Line-heights */
  --leading-none:     1;
  --leading-tight:    1.2;
  --leading-snug:     1.35;
  --leading-normal:   1.5;
  --leading-relaxed:  1.625;
  --leading-loose:    1.8;

  /* Font weights */
  --weight-regular:   400;
  --weight-medium:    500;
  --weight-semibold:  600;
  --weight-bold:      700;

  /* Letter spacing */
  --tracking-tight:   -0.02em;
  --tracking-normal:  0;
  --tracking-wide:    0.05em;
  --tracking-widest:  0.15em;  /* Badges/labels uppercase */

  /* ── ESPAÇAMENTO (base 4px) ── */

  --space-1:   4px;
  --space-2:   8px;
  --space-3:   12px;
  --space-4:   16px;
  --space-5:   20px;
  --space-6:   24px;
  --space-7:   28px;
  --space-8:   32px;
  --space-10:  40px;
  --space-12:  48px;
  --space-14:  56px;
  --space-16:  64px;
  --space-20:  80px;
  --space-24:  96px;
  --space-32: 128px;

  /* Seções */
  --section-padding-y:      80px;
  --section-padding-y-sm:   48px;  /* Mobile */
  --container-max:          900px;
  --container-form-max:     500px;

  /* ── BORDER RADIUS ── */

  --radius-none:    0;
  --radius-sm:      6px;
  --radius-md:      10px;
  --radius-lg:      14px;
  --radius-xl:      20px;
  --radius-2xl:     28px;
  --radius-full:    9999px;

  /* ── SOMBRAS ── */

  --shadow-xs:      0 1px 3px rgba(0,0,0,0.08);
  --shadow-sm:      0 4px 12px rgba(0,0,0,0.08);
  --shadow-md:      0 8px 24px rgba(0,0,0,0.10);
  --shadow-lg:      0 16px 48px rgba(0,0,0,0.12);
  --shadow-gold-sm: 0 4px 16px rgba(201,168,76,0.20);
  --shadow-gold-md: 0 10px 30px rgba(201,168,76,0.25);
  --shadow-gold-lg: 0 20px 60px rgba(201,168,76,0.30);

  /* ── TRANSIÇÕES ── */

  --transition-fast:   150ms ease;
  --transition-base:   250ms ease;
  --transition-slow:   350ms ease;
  --transition-reveal: 500ms cubic-bezier(0.16, 1, 0.3, 1);
}
```

---

## UX DO FORMULÁRIO — RECOMENDAÇÕES

### Diagnóstico atual
```
Campos: Nome | WhatsApp | Empresa (required) | Interesse (não-required)
Ação: Abre WhatsApp com texto pré-preenchido
Feedback: Nenhum (zero confirmação visual)
```

### Problemas
| Problema | Impacto |
|----------|---------|
| `<label>` sem `for` associado ao `id` do input | Preenchimento automático falha, acessibilidade quebrada |
| Campo "Você tem empresa?" — barreira desnecessária | Leads sem CNPJ formal (MEI informal) abandonam |
| Campo "O que te interessou mais?" — redundante | Já sabemos pelo comportamento na página |
| `required` inconsistente (empresa sim, interesse não) | Confusão do usuário |
| Sem `autocomplete` nos inputs | Mobile não sugere dados salvos |
| Sem feedback de loading no submit | Multi-clique abre múltiplos chats |
| Sem mensagem de sucesso | Usuário não sabe se funcionou |

### Formulário Recomendado

```html
<!-- VERSÃO MÍNIMA FRICTION (recomendada para conversão amanhã) -->
<form id="lead-form" onsubmit="submitForm(event)" novalidate>

  <div class="form-group">
    <label for="nome">Nome</label>
    <input 
      type="text" 
      id="nome" 
      name="nome"
      autocomplete="given-name"
      required 
      placeholder="Como posso te chamar?"
      aria-required="true"
    >
    <span class="field-error" id="nome-error" role="alert" aria-live="polite"></span>
  </div>

  <div class="form-group">
    <label for="whatsapp">WhatsApp</label>
    <input 
      type="tel" 
      id="whatsapp" 
      name="whatsapp"
      autocomplete="tel-national"
      inputmode="numeric"
      required 
      placeholder="(00) 00000-0000"
      aria-required="true"
      aria-describedby="whatsapp-hint"
    >
    <span id="whatsapp-hint" class="field-hint">Vamos entrar em contato por aqui</span>
    <span class="field-error" id="whatsapp-error" role="alert" aria-live="polite"></span>
  </div>

  <button type="submit" class="cta-btn" id="submit-btn">
    <span class="btn-text">Falar com a equipe no WhatsApp →</span>
    <span class="btn-loading" aria-hidden="true" style="display:none">Abrindo WhatsApp...</span>
  </button>

</form>
```

### Campos removidos e por quê
- **"Você tem empresa?"** → Vendedor qualifica em 30s no WA. Cada campo extra = 5-15% de abandono.
- **"O que te interessou mais?"** → Dado já capturado pelo comportamento na página (qual card clicou). Se precisar: capture por parâmetro de URL na abertura do WA.

### Qualificação sem fricção
Passar o interesse escolhido invisível na mensagem do WA:
```js
// Captura quando o usuário clica no card
let selectedChoice = '';
function selectChoice(type) {
  selectedChoice = type; // 'pousada' ou 'gestao'
  // ... resto do código
}

// Inclui na mensagem sem pedir ao usuário
const msg = `Olá! Me chamo ${nome}.\nInteresse: ${selectedChoice === 'gestao' ? 'Gestão empresarial' : 'Cota da pousada'}\nWhatsApp: ${whatsapp}`;
```

### Validação visual recomendada
```css
/* Estado de erro */
.form-group input.has-error { border-color: var(--color-error); }
.field-error { color: var(--color-error); font-size: 0.8rem; margin-top: 4px; display: none; }
.field-error.visible { display: block; }

/* Estado de sucesso */
.form-group input.is-valid { border-color: var(--color-success); }

/* Hint text */
.field-hint { color: var(--color-text-muted); font-size: 0.8rem; margin-top: 4px; display: block; }

/* Loading state no botão */
.cta-btn[disabled] { opacity: 0.7; cursor: not-allowed; transform: none; }
```

---

## RESUMO EXECUTIVO

| Categoria | Status | Prioridade |
|-----------|--------|-----------|
| Hierarquia visual | ⚠️ Média | Melhorar hero e social proof |
| Consistência brand | ✅ Boa | Manter |
| Acessibilidade | ❌ Crítica | Corrigir labels e contraste urgente |
| Mobile 375px | ⚠️ Média | Math-box e delay |
| Estados interativos | ⚠️ Média | Loading e focus |
| Formulário UX | ❌ Crítica | Simplificar imediatamente |
| Urgência/Conversão | ❌ Crítica | Countdown + social proof |

**Estimativa de impacto das melhorias top 5:**
- Simplificar formulário (Nome+WA) → +25-35% de submits
- Countdown timer real → +15-20% de conversão
- Loading state → -10-15% de abandonos mid-funnel
- Corrigir labels → +5-8% em mobile (preenchimento automático)
- Contraste footer → conformidade LGPD/WCAG

**Bottom line:** A landing está 70% boa. Os 30% que faltam são exatamente os que afetam conversão.

---
*Auditoria Sati — Grupo FBS UX/UI | 2026-04-02*
