# GM91 — Colour Psychology & Brand Voice Research

**Issue:** [#3](https://github.com/bala91px/gm91/issues/3) · **Research lead:** Kevin · **Date:** 2026-06-22
Grounds design decisions for the CRO landing page (`audit.html`) and the future checkout/payments page.

> Contrast ratios below were computed against the page's **actual hexes**, so the recommendations are drop-in safe on both the ink and cream surfaces.

---

## TL;DR — DECISIONS (implementation-ready)

**Colour — landing page (`audit.html`):**
- **Keep** the warm system: ink `#1A1510`, cream `#F7F2EA`, gold `#BD9648`/`#9C7A33`.
- **Introduce ONE action colour for the primary CTA only: terracotta `#C0492B`, white text** — 4.97:1, passes WCAG AA; isolates against ink, cream *and* gold. Hotter-urgency alt: burnt orange `#C25A28`.
- **Demote gold** from primary-button fill to brand/secondary/outline use. Gold filled with white text is **2.76:1 → fails AA**, and gold-on-cream barely separates (~2.5:1) — that's the current conversion leak.
- **Make WhatsApp green `#25D366` clearly secondary** to the terracotta primary (lighter/outline/smaller) so two buttons stop competing for the same attention.
- **Colour budget: 3 accents max** (terracotta action · gold brand · WhatsApp green platform) + 2 functional states (success `#1F7A4D`, error `#C0392B`). No fifth attention colour.

**Colour — future checkout page:**
- **Keep the warm brand frame** for continuity; add a **cool-neutral encapsulated card-field container** (`#EFE9DD` or light grey, 1px border) with **1–2 recognisable gateway/security badges inside it** (Razorpay/UPI/Stripe) + **lock icon + "Secure payment" text** beside the pay button.
- **Pay button = the reserved action colour** (terracotta `#C0492B`, or success-green `#1F7A4D` if you prefer the safe/"go" convention) — pick one, reserve it.
- **Functional states:** error red `#C0392B`, success green `#1F7A4D` (both AA on cream).
- **Layout must be pixel-perfect** — one visual glitch destroys perceived security.

**Voice:**
- Plain English, Grade 6–8, **"you" = customer / "we" = GM91**, zero SEO/CRO jargon.
- Ad LP: urgency + benefit + curiosity, ~60/40 warmth/authority.
- Checkout: drop urgency → reassurance + clarity, ~50/50, competent and steady. State price, cadence, cancel-anytime, "secure" explicitly.

---

## 1. Colour psychology — the CRO ad landing page

### The red-vs-green myth: it was never about the colour
The famous "red beat green by 21%" result (HubSpot, 2011) is the most-misread test in CRO. Red won **because the page was already green** — the red button was the only contrasting element. There is **no universal best colour**; these tests measure **visual contrast**, not pigment. The mechanism is the **Von Restorff (isolation) effect**: the most visually distinct element gets the most attention. One synthesis found **contrast was ~3.2× more predictive of CTA success than hue**. ([CXL](https://cxl.com/blog/which-color-converts-the-best/), [Atticus Li](https://atticusli.com/blog/posts/cta-button-psychology-size-color-copy-research/), [OptinMonster](https://optinmonster.com/which-color-button-converts-best/))

**Implication:** the question isn't "is gold right" — it's "is the primary CTA the single most isolated element on the page." Right now it isn't: gold-on-cream is low-contrast and the green WhatsApp button competes with it.

### Does gold give enough contrast to convert? Partly — and that's the problem
WCAG maths on the actual hexes — gold as a **filled button** is the weak link:

| Surface | Gold `#BD9648` filled | Verdict |
|---|---|---|
| White text on gold | **2.76:1** | ❌ fails AA (4.5:1) |
| Ink text on gold | 6.58:1 | ✅ passes, but gold barely separates from cream |
| Gold fill vs cream bg | ~2.5:1 | ❌ button blends into cream — weak isolation |

**Recommendation: keep gold as the brand colour, introduce ONE dedicated high-contrast action colour reserved exclusively for the primary CTA.**

| Option | Hex | White-on-fill | vs ink | vs cream | Read |
|---|---|---|---|---|---|
| **Terracotta (recommended)** | `#C0492B` | **4.97:1 ✅** | 3.65:1 | 4.46:1 | Warm, confident, unmistakably the action |
| Burnt orange (alt) | `#C25A28` | 4.39:1 ✅ | 4.13:1 | 3.94:1 | Hotter / more urgent |

Terracotta is an earthy, premium-warm red that belongs in a cream/ink/gold world (clay, not fire-engine red) — Von Restorff contrast without breaking the editorial feel. Keep gold for the logo, eyebrows, underlines, secondary/outline buttons, ladder accents.

### Colour budget & the WhatsApp competition
Three-colour hierarchies converted **~22% better** than four+ primary colours; NN/g's rule is to use colour *sparingly and intentionally*. ([60-30-10](https://www.freecodecamp.org/news/the-60-30-10-rule-in-design/), [Inkbot](https://inkbotdesign.com/60-30-10-rule/), [NN/g](https://www.nngroup.com/articles/color-enhance-design/))
- **Terracotta** → primary CTA only (the scarce, high-value colour).
- **WhatsApp green** → only the WhatsApp affordance (a platform cue). **Fix:** make it clearly secondary so it stops competing with the primary.
- **Gold** → brand/trust accents.
- **Functional only:** success green / error red — status, not hierarchy.

### Emotional read: warm gold/cream for an Indian local-SMB audience
- **Gold** reads as wealth, prestige, quality — and carries strong positive cultural associations in India (auspicious, valuable). Must stay a controlled accent on dark/cream (large fills drift to "dirty yellow") — exactly how GM91 already uses it. ([gold psychology](https://www.empower-yourself-with-color-psychology.com/gold-in-business.html), [IJIP study PDF](https://ijip.in/wp-content/uploads/2025/05/18.01.141.20251302.pdf))
- **Blue ≠ automatic trust.** Warm tones read friendly and human for *approachable local* businesses, where SaaS blue feels corporate-cold. ([ITBee](https://itbeesolution.com/the-psychology-of-color-in-saas-branding-why-blue-isnt-always-the-answer-for-trust/), [Concept Studio](https://conceptstudio.com/blog/color-psychology-in-branding-consumer-behavior/))

**Net:** keep the warm identity; the only fix is the under-powered CTA contrast → terracotta action colour.

---

## 2. Colour psychology — the payments / checkout page

### What reduces payment anxiety (perceived security is *visual*)
Baymard's research — anxiety peaks at card entry, and trust is built visually:
- **Encapsulate the card fields** in a distinct container (solid light-grey bg / border). Users trust fields that *look* set apart.
- **Lock icon + "Secure checkout" text together** beats either alone.
- **1–2 recognisable trust seals inside the encapsulated area** (recognisability > technical merit).
- Trust signals can cut abandonment ~18%; ~18% abandon specifically over security concerns.
- **One layout glitch erodes all trust** — checkout must look flawless.
([Baymard](https://baymard.com/blog/perceived-security-of-payment-form), [BTNG](https://www.btng.studio/articles/trust-signals-checkout-abandonment/), [TrustSignals](https://www.trustsignals.com/blog/trust-badges-work-and-we-have-the-receipts-to-prove-it), [Mobiloud](https://www.mobiloud.com/blog/trust-signals-cart-abandonment))

The blue/green "trust convention" is a *convention*, not a requirement — Stripe uses a purple action colour and feels maximally secure because execution is flawless and validation is inline. **Trust = craft + clear security cues, not hue.** ([Stripe teardown](https://www.illustration.app/blog/stripe-payment-ux-gold-standard))

### Keep warm or shift cooler? — recommendation
**Keep GM91's warm brand on checkout, but more restrained + explicit security scaffolding.**
- **For:** brand continuity ad→audit→payment avoids the "is this the same company?" jolt. For recurring ₹500–₹5,000/mo plans sold after a WhatsApp conversation, trust = relationship + flawless execution.
- **Tradeoff:** warm palettes don't get the "free" cool-colour trust association — you must **earn** it: encapsulated fields, lock + "Secure payment" text, recognisable gateway/seal badges, pixel-perfect layout. Warm + proper cues > cool + sloppy.
- **Decision:** warm frame, cool-neutral card container, explicit lock/seal/secure cues, one reserved action colour for the pay button.

---

## 3. Brand voice — the landing page

**Plainspoken, warm, confident, benefit-first.** Governing rule (Mailchimp): *"it's always more important to be clear than entertaining."* ([Mailchimp Voice & Tone](https://styleguide.mailchimp.com/voice-and-tone/))
- **Reading level:** ~Grade 6–8. Short sentences, one idea per line.
- **Person:** "you" = customer, "we" = GM91.
- **Jargon:** ban SEO/CRO/GBP/SERP/funnel. Say "showing up on Google," "your Google listing," "more calls."
- **Balance:** ~60% warmth / 40% authority on the ad LP — expert neighbour, not agency flexing.
- **English/Hinglish:** clean simple English for page body (pan-India, translatable); reserve light Hinglish for ad creatives / WhatsApp.

### 6 voice principles — do/don't + rewrite of real page lines
1. **Lead with the customer's outcome, not the service.** "First, see exactly where your business shows up on Google. Free."
2. **Ask a question they're already asking.** *"Is your salon getting found on Google?"* → "When someone Googles a salon near you — do they find you, or the one down the road?"
3. **Plain words over industry words.** "see where you show up on Google, what's quietly losing you customers, and the fastest way to fix it."
4. **Short, concrete, low-commitment promises.** Keep: *"Drop your number — that's it. We do the rest on WhatsApp."*
5. **Confident, never hypey.** Keep: *"A real audit. Not a sales call in disguise."*
6. **Reassure at every friction point.** Keep: *"Free · one tap · no card, no commitment."*

### Voice shift: ad LP vs payments page
- **Ad LP (cold):** urgency + benefit + curiosity. Verbs, outcomes, competitor FOMO. Goal = one micro-yes (a number).
- **Payments (warm, deciding to pay):** drop urgency (pressure at pay = scam signal). Plain, calm, specific — price, what they get, when, how to cancel, that it's secure. "₹500/month. Cancel anytime. Secure payment." ~50/50, competent and steady.

---

## Implementation notes for Blake
1. **WhatsApp number is still `91XXXXXXXXXX`** in `audit.html` — must be swapped before any paid traffic or every CTA dead-ends.
2. Terracotta `#C0492B` is drop-in safe on both ink and cream (contrast verified).
3. This doc is research/recommendations only — **no code changed**. Applying the terracotta CTA + WhatsApp-demotion would be a follow-up issue once Bala approves the direction.

### Sources
[CXL](https://cxl.com/blog/which-color-converts-the-best/) · [Atticus Li](https://atticusli.com/blog/posts/cta-button-psychology-size-color-copy-research/) · [OptinMonster](https://optinmonster.com/which-color-button-converts-best/) · [NN/g](https://www.nngroup.com/articles/color-enhance-design/) · [60-30-10](https://www.freecodecamp.org/news/the-60-30-10-rule-in-design/) · [Inkbot](https://inkbotdesign.com/60-30-10-rule/) · [Baymard](https://baymard.com/blog/perceived-security-of-payment-form) · [Stripe teardown](https://www.illustration.app/blog/stripe-payment-ux-gold-standard) · [TrustSignals](https://www.trustsignals.com/blog/trust-badges-work-and-we-have-the-receipts-to-prove-it) · [Mobiloud](https://www.mobiloud.com/blog/trust-signals-cart-abandonment) · [ITBee](https://itbeesolution.com/the-psychology-of-color-in-saas-branding-why-blue-isnt-always-the-answer-for-trust/) · [IJIP PDF](https://ijip.in/wp-content/uploads/2025/05/18.01.141.20251302.pdf) · [Mailchimp](https://styleguide.mailchimp.com/voice-and-tone/)
