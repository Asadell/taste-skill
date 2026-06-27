---
name: taste-skill-lovable
description: Use when asked to build or redesign any landing page, portfolio, marketing site, or frontend UI. Applies anti-slop design rules: reads the brief, infers the right design direction, enforces strict layout discipline, bans AI-tell patterns, and ships premium interfaces that do not look templated.
---

# Taste Skill — Anti-Slop Frontend for Lovable

> For landing pages, portfolios, and redesigns. Not dashboards, not data tables.
> Every rule is **contextual** — read the brief first, then apply only what fits.

---

## 0. BRIEF INFERENCE (Read the Room First)

Before touching any code, infer what the user actually wants.

### 0.A Signals to read
1. **Page kind** — landing (SaaS / consumer / agency), portfolio, redesign, editorial
2. **Vibe words** — "minimalist", "Linear-style", "Awwwards", "brutalist", "premium consumer", "Apple-y", "playful", "dark tech"
3. **Reference signals** — URLs, screenshots, named products, competitor brands
4. **Audience** — B2B procurement vs. design-conscious consumer vs. recruiter
5. **Quiet constraints** — accessibility-first, public-sector, trust-first, regulated industries (these OVERRIDE aesthetic preference)

### 0.B Output a one-line "Design Read" before generating
> "Reading this as: `<page kind>` for `<audience>`, with a `<vibe>` language, leaning toward `<design system or aesthetic family>`."

### 0.C If ambiguous, ask ONE question only
Never a multi-question dump. Example: *"Should this feel closer to Linear-clean or Awwwards-experimental?"*
If you can confidently infer from context, do not ask. Just declare the design read and proceed.

### 0.D Anti-Default Discipline
Do NOT default to: AI-purple gradients, centered hero over dark mesh, three equal feature cards, generic glassmorphism everywhere, Inter + slate-900. These are LLM defaults. Reach past them deliberately.

---

## 1. THE THREE DIALS

After the design read, set three dials. Every layout, motion, and density decision is gated by these.

- **`DESIGN_VARIANCE: 8`** — 1 = Perfect Symmetry, 10 = Artsy Chaos
- **`MOTION_INTENSITY: 6`** — 1 = Static, 10 = Cinematic / Physics
- **`VISUAL_DENSITY: 4`** — 1 = Art Gallery / Airy, 10 = Cockpit / Packed Data

**Baseline:** `8 / 6 / 4`. Override conversationally based on brief. Do not ask the user to edit this file.

### Dial inference table
| Signal | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| "minimalist / clean / calm / Linear-style" | 5-6 | 3-4 | 2-3 |
| "premium consumer / Apple-y / luxury" | 7-8 | 5-7 | 3-4 |
| "playful / Awwwards / agency / experimental" | 9-10 | 8-10 | 3-4 |
| "landing page / portfolio / marketing (default)" | 7-9 | 6-8 | 3-5 |
| "trust-first / public-sector / a11y-critical" | 3-4 | 2-3 | 4-5 |
| "redesign - preserve" | match existing | +1 | match existing |
| "redesign - overhaul" | +2 | +2 | match existing |

---

## 2. STACK & ARCHITECTURE DEFAULTS

Unless a real design system is chosen:

- **Framework:** React or Next.js. Default to Server Components (RSC).
- **Styling:** Tailwind v4. For v4 use `@tailwindcss/postcss` or Vite plugin — NOT the old `tailwindcss` postcss plugin.
- **Animation:** `motion/react` (formerly Framer Motion). Import: `import { motion } from "motion/react"`. Use GSAP + ScrollTrigger for full-page scroll-hijack patterns only.
- **Fonts:** Always `next/font` or self-host with `@font-face + font-display: swap`. Never `<link>` to Google Fonts in production.
- **State:** `useState` for isolated UI only. For continuous values driven by mouse/scroll — use `useMotionValue` / `useTransform` / `useScroll`. Never `useState` for these (re-renders on every frame, collapses on mobile).
- **Icons:** Priority order: `@phosphor-icons/react` > `hugeicons-react` > `@radix-ui/react-icons` > `@tabler/icons-react`. Lucide only on explicit user request. One icon family per project. Never hand-roll SVG paths.
- **RSC Safety:** Any component using Motion, scroll listeners, or pointer physics MUST have `'use client'` at the top.

---

## 3. DESIGN SYSTEM MAP

### When to use an official system
| Brief reads as | Use |
|---|---|
| Microsoft / enterprise SaaS | `@fluentui/react-components` |
| Google-ish / Material product | `@material/web` + Material 3 tokens |
| IBM-style B2B / enterprise | `@carbon/react` + `@carbon/styles` |
| Shopify app | Polaris web components |
| GitHub devtool / community | `@primer/css` or `@primer/react-brand` |
| Public-sector UK | `govuk-frontend` |
| US public-sector | `uswds` |
| Modern accessible React | `@radix-ui/themes` |
| Modern SaaS (owned components) | shadcn/ui — never in default state, always customized |
| Indie / small team | Tailwind v4 + `dark:` variant |

**One system per project.** Do not mix Fluent + Carbon, or shadcn/ui into a Material 3 app.

### Aesthetic directions (no official package)
| Aesthetic | Implementation |
|---|---|
| Glassmorphism | `backdrop-filter`, layered borders, highlight overlays. Solid fallback for `prefers-reduced-transparency`. |
| Bento grids | CSS Grid with mixed cell sizes. No single library owns this. |
| Brutalism | Native CSS, monospace, raw borders. No library. |
| Kinetic typography | Native CSS animations, scroll-driven, GSAP for scroll hijacks. |
| Apple Liquid Glass | Web approximation only — label it as such. `backdrop-filter + layered borders + highlights`. Not an official web API. |

---

## 4. TYPOGRAPHY

- **Display / Headlines:** Default `text-4xl md:text-6xl tracking-tighter leading-none`
- **Body / Paragraphs:** Default `text-base text-gray-600 leading-relaxed max-w-[65ch]`
- **Sans font — discouraged as default:** Inter. Pick `Geist`, `Outfit`, `Cabinet Grotesk`, or `Satoshi` first.
- **Good pairings:** `Geist + Geist Mono`, `Satoshi + JetBrains Mono`, `Cabinet Grotesk + Inter Tight`

### Serif discipline
Serif is **very discouraged as the default**. Only use serif when:
- The brand brief literally names a serif font, OR
- The aesthetic is genuinely editorial / luxury / publication AND you can articulate why

**Banned as defaults:** `Fraunces` and `Instrument_Serif` (the two most common LLM-favorite serifs).

For creative/studio/premium briefs, default to **sans display** (Geist Display, Cabinet Grotesk Display, PP Neue Montreal, Inter Display).

### Italic descender clearance (mandatory)
When italic is used in display type with descender letters (`y g j p q`), use `leading-[1.1]` minimum and add `pb-1` reserve. Never `leading-none` or `leading-[1]` with italic descenders.

---

## 5. COLOR RULES

- Max **1 accent color** per project. Saturation < 80%.
- **No AI Purple as default.** Use neutral bases (Zinc / Slate / Stone) with a single high-contrast accent.
- **One palette per project.** Do not mix warm and cool grays in the same project.
- **COLOR CONSISTENCY LOCK:** Once an accent is chosen, it is used across the WHOLE page. A warm-grey site does not suddenly get a blue CTA in section 7.

### Premium-consumer palette ban (mandatory)
For premium-consumer briefs (cookware, wellness, artisan, luxury, DTC), the LLM default is:
- Backgrounds: warm beige/cream (`#f5f1ea`, `#fbf8f1`)
- Accents: brass/clay/oxblood (`#b08947`, `#b6553a`)
- Text: espresso near-black (`#1a1714`)

**This palette is banned as the default.** Alternatives to rotate through:
- Cold Luxury: silver-grey + chrome + smoke
- Forest: deep green + bone + amber
- Black and Tan: true off-black + warm tan, sharp contrast
- Cobalt + Cream: saturated blue + single neutral
- Pure monochrome + one saturated pop accent

---

## 6. LAYOUT DISCIPLINE (Hard Rules)

- **ANTI-CENTER BIAS:** Centered hero is avoided when `DESIGN_VARIANCE > 4`. Use Split Screen (50/50), left-aligned content / right-aligned asset, or asymmetric whitespace.
- **`min-h-[100dvh]`** — Never `h-screen` for full-height sections (iOS Safari viewport bug).
- **CSS Grid over flex-math.** Never `w-[calc(33%-1rem)]` for columns. Use `grid grid-cols-3 gap-6`.
- **Hero must fit the initial viewport:** headline max 2 lines, subtext max 20 words, CTAs visible without scroll.
- **Hero top padding cap:** max `pt-24` at desktop.
- **Hero stack discipline — max 4 text elements:**
  1. Eyebrow OR brand strip (pick zero or one)
  2. Headline (max 2 lines)
  3. Subtext (max 20 words)
  4. CTAs (1 primary + max 1 secondary)
  - Banned in hero: tagline below CTAs, trust micro-strip, pricing teaser, feature bullet list
- **Navigation must render on ONE line at desktop.** Height max 80px, default 64-72px.
- **Bento cells:** exactly as many cells as you have content for. No empty cells.
- **Section-Layout-Repetition Ban:** each layout family can appear at most ONCE per page.
- **Zigzag Alternation Cap:** max 2 consecutive sections with left-image/right-text pattern.
- **EYEBROW RESTRAINT:** Max 1 eyebrow per 3 sections. If section A has an eyebrow, the next 2 sections cannot.
- **SPLIT-HEADER BAN:** "left big headline + right small floating paragraph" is banned. Stack them vertically instead.
- **Mobile collapse must be explicit per section:** every multi-column layout must declare the `< 768px` fallback.
- **Shape Consistency Lock:** Pick ONE corner-radius scale and stick to it across the whole page.

---

## 7. INTERACTIVE STATES

Always implement full state cycles — not just "static successful state":

- **Loading:** Skeletal loaders matching final layout shape. No generic circular spinners.
- **Empty States:** Beautifully composed, with guidance on how to populate.
- **Error States:** Clear, inline for forms, toast only for transient.
- **Tactile Feedback:** On `:active`, use `-translate-y-[1px]` or `scale-[0.98]`.
- **BUTTON CONTRAST (mandatory a11y):** Every CTA must pass WCAG AA (4.5:1 body, 3:1 large text). White-on-white = banned.
- **CTA WRAP BAN:** Button text MUST fit on one line at desktop. Wrapped CTA = Pre-Flight Fail.
- **NO DUPLICATE CTA INTENT:** "Get in touch" + "Let's talk" = same intent = pick ONE label.
- **FORM CONTRAST (mandatory a11y):** Inputs, placeholders, focus rings, labels — all pass WCAG AA contrast.

---

## 8. VISUAL ASSET STRATEGY

Landing pages are **visual products**. Text-only pages with placeholder divs = slop.

**Priority order:**
1. **Image-generation tool first** — generate section-specific assets (hero photography, product shots, mood images).
2. **Real web images second** — use `https://picsum.photos/seed/{descriptive-seed}/{w}/{h}` for placeholders.
3. **Last resort: explicit placeholder slots** — `<!-- TODO: hero product photo, 1600x1200 -->` and inform the user.

**Real company logos for social proof:**
- Use Simple Icons: `https://cdn.simpleicons.org/{slug}/ffffff`
- Or `simple-icons` npm package for any known brand
- For invented brand names: generate a simple monogram SVG mark
- **LOGO-ONLY rule:** logo wall = logos only. No industry labels below each logo.

**Div-based fake screenshots are banned.** A "hand-built product preview" made of `<div>` rectangles is the #1 AI Tell.

---

## 9. MOTION RULES

- **`MOTION_INTENSITY > 4` = page must actually move.** Entry transitions on hero, scroll-reveal on key sections, hover physics on CTAs.
- **MOTION MUST BE MOTIVATED:** Before adding any animation, ask: "what does this communicate?" Valid: hierarchy, storytelling, feedback, state transition. Invalid: "it looks cool."
- **MARQUEE MAX ONE PER PAGE:** Horizontal scrolling marquees at most once per page.
- **Reduced motion (mandatory):** Any `MOTION_INTENSITY > 3` MUST honor `prefers-reduced-motion`. Wrap with `useReducedMotion()` from `motion/react`.
- **FORBIDDEN animation patterns:**
  - `window.addEventListener("scroll", ...)` — hard ban. Use `useScroll()`, `ScrollTrigger`, `IntersectionObserver`, or CSS `animation-timeline`.
  - `requestAnimationFrame` loops that touch React state — use `useMotionValue` + `useTransform`.
  - Animating `top`, `left`, `width`, `height` — animate only `transform` and `opacity`.

### GSAP Sticky-Stack (canonical pattern)
```tsx
"use client";
import { useRef, useEffect } from "react";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { useReducedMotion } from "motion/react";

gsap.registerPlugin(ScrollTrigger);

export function StickyStack({ cards }: { cards: React.ReactNode[] }) {
  const ref = useRef<HTMLDivElement>(null);
  const reduce = useReducedMotion();

  useEffect(() => {
    if (reduce || !ref.current) return;
    const ctx = gsap.context(() => {
      const cardEls = gsap.utils.toArray<HTMLElement>(".stack-card");
      cardEls.forEach((card, i) => {
        if (i === cardEls.length - 1) return;
        ScrollTrigger.create({
          trigger: card,
          start: "top top",
          endTrigger: cardEls[cardEls.length - 1],
          end: "top top",
          pin: true,
          pinSpacing: false,
        });
        gsap.to(card, {
          scale: 0.92,
          opacity: 0.55,
          ease: "none",
          scrollTrigger: {
            trigger: cardEls[i + 1],
            start: "top bottom",
            end: "top top",
            scrub: true,
          },
        });
      });
    }, ref);
    return () => ctx.revert();
  }, [reduce]);

  return (
    <div ref={ref} className="relative">
      {cards.map((card, i) => (
        <div key={i} className="stack-card sticky top-0 min-h-[100dvh] flex items-center justify-center">
          {card}
        </div>
      ))}
    </div>
  );
}
```
Critical: `start: "top top"`, `pin: true`, cleanup via `ctx.revert()`.

---

## 10. DARK MODE

- **Dual-mode by default.** Never assume light-only unless the brief is print-emulating editorial.
- **Page Theme Lock:** One theme for the whole page. Sections do not invert modes mid-page.
- **No `#000000` or `#ffffff`** — use off-black (zinc-950) and off-white.
- **Token strategy (pick one, stick to it):**
  - Tailwind `dark:` variant for utility-first projects
  - CSS variables (`--surface`, `--text-primary`, `--accent`) for design-system projects
- Test in both modes before declaring done.

---

## 11. PERFORMANCE & ACCESSIBILITY

- **LCP < 2.5s** — hero image must be `next/image priority` or preloaded.
- **INP < 200ms** — heavy work off main thread.
- **CLS < 0.1** — reserve space for images, fonts, embeds.
- **`will-change: transform`** — sparingly, only on elements that will actually animate.
- **Grain/noise overlays** — only on `position: fixed; pointer-events: none` pseudo-elements. Never on scrolling containers.
- **z-index discipline** — no arbitrary `z-50` or `z-[9999]`. Define a systemic z-index scale.

---

## 12. AI TELLS — BANNED PATTERNS

Avoid these signatures unless the brief explicitly asks for them.

### Visual
- No neon / outer glows. Use inner borders or tinted shadows.
- No pure `#000000`. Use off-black.
- No oversaturated accents.
- No excessive gradient text on large headers.
- No custom mouse cursors.

### Typography
- Never Inter as default (see Section 4).
- No "three equal H2 cards" generic feature row.
- Serif only for editorial/luxury (see Section 4).

### Content
- No "John Doe" / "Jane Smith" — use realistic diverse names.
- No "99.99%" / "50%" — use organic, messy data (`47.2%`, `+1 (312) 847-1928`).
- No "Acme", "Nexus", "SmartFlow" — invent contextual, premium-sounding names.
- No "Elevate", "Seamless", "Unleash", "Next-Gen", "Revolutionize" — use concrete verbs.

### Layout patterns (banned as defaults)
- Version labels in hero (V0.6, BETA, EARLY ACCESS)
- Section-number eyebrows (`001 · Capabilities`, `06 · how it works`)
- `01 / 4`-style pagination on bento tiles
- Middle-dot overuse — max 1 per line in metadata strips
- Decorative status dots on every list item
- Locale / city / time / weather strips (`LIS 14:23 · 18°C`) unless brief is place-focused
- Scroll cues (`Scroll`, `↓ scroll`, animated mouse wheel)
- `border-t` + `border-b` on every row of a long list
- "Quietly trusted by" / "From the field" / "Field notes" social-proof headers
- Progress bars with filled background tracks as comparison visuals
- Photo-credit captions as decoration (`Field study no. 12 · Ines Caetano`)
- Version footers on marketing pages (`v1.4.2`, `Build 0048`)
- Decoration text strip at hero bottom (`BRAND. MOTION. SPATIAL.`)
- Floating top-right sub-text in section headings

### EM-DASH BAN (non-negotiable)
**Em-dash (`—`) is COMPLETELY banned.** Zero tolerance, zero exceptions.

- Banned in headlines, eyebrows, pills, body copy, quotes, attribution, captions, buttons, alt text.
- In body: restructure the sentence with a period, comma, colon, or parentheses.
- In quotes: use a regular hyphen with spaces (` - `) or a line break.
- En-dash as separator is also banned. Use a regular hyphen for date ranges (`2018-2026`).

If output contains a single `—` or `–` used as separator, it fails Pre-Flight.

---

## 13. REDESIGN PROTOCOL

When redesigning an existing project:

1. **Detect mode first:**
   - Preserve: modernize without breaking the brand
   - Overhaul: new visual language, preserve content + IA
   - If ambiguous, ask once: *"Should this preserve the existing brand, or start visually from scratch?"*

2. **Audit before touching:** document current brand tokens, IA, content blocks, patterns to keep vs. retire.

3. **Modernization levers (apply in order, stop when brief is satisfied):**
   1. Typography refresh (biggest visual lift, lowest risk)
   2. Spacing and rhythm
   3. Color recalibration
   4. Motion layer
   5. Hero and key-section recomposition
   6. Full block replacement (only when existing block is unsalvageable)

4. **Never modify without explicit approval:**
   - URL structure / route slugs
   - Primary nav labels
   - Form field names (breaks analytics + autofill)
   - Brand logo or wordmark
   - Legal / consent / cookie copy

---

## 14. FULL OUTPUT ENFORCEMENT

When generating code:

- **Never truncate.** Never use `// ...`, `// rest of code`, `// implement here`, `// TODO`, `/* ... */`, or `// similar to above`.
- **Never use prose shortcuts:** "Let me know if you want me to continue", "for brevity", "the rest follows the same pattern".
- If approaching token limit, stop at a clean breakpoint and write: `[PAUSED — X of Y complete. Send "continue" to resume from: next section name]`.
- On "continue": pick up exactly where stopped. No recap.

---

## 15. FINAL PRE-FLIGHT CHECK

Run every box before outputting. If any fails, the output is not done.

- [ ] Brief inference one-liner declared?
- [ ] Dial values explicit and reasoned from the brief?
- [ ] ZERO em-dashes anywhere (headlines, body, quotes, buttons, alt text)?
- [ ] Page Theme Lock: one theme for the whole page, no mid-page section flips?
- [ ] Color Consistency Lock: one accent across all sections?
- [ ] Shape Consistency Lock: one corner-radius system throughout?
- [ ] Button Contrast: every CTA text readable against background (WCAG AA 4.5:1)?
- [ ] CTA Button Wrap: no label wraps to 2+ lines at desktop?
- [ ] Form Contrast: inputs, placeholders, labels all pass WCAG AA?
- [ ] Hero fits viewport: headline ≤ 2 lines, subtext ≤ 20 words, CTAs visible?
- [ ] Hero top padding: max `pt-24` at desktop?
- [ ] Hero stack discipline: max 4 text elements?
- [ ] Eyebrow count: ≤ ceil(sectionCount / 3)?
- [ ] Split-Header Ban: no "left headline + right floating paragraph"?
- [ ] Zigzag Alternation Cap: no 3+ consecutive image+text-split sections?
- [ ] No Duplicate CTA Intent (same intent, two different labels)?
- [ ] Logo wall = logos only, no industry labels?
- [ ] Bento: min 2-3 cells with real visual variation (image, gradient, pattern)?
- [ ] Real images used (gen-tool, Picsum-seed, or explicit placeholder slots)?
- [ ] No div-based fake screenshots?
- [ ] Copy Self-Audit: every visible string re-read, no AI-hallucinated phrases?
- [ ] No banned AI Tells from Section 12?
- [ ] Motion motivated: every animation justified in one sentence?
- [ ] Marquee max one per page?
- [ ] Navigation on ONE line at desktop, height ≤ 80px?
- [ ] Section-Layout-Repetition: no two sections share the same layout family?
- [ ] Bento has exact cell count (N items = N cells, no empty cells)?
- [ ] Reduced motion respected for everything `MOTION_INTENSITY > 3`?
- [ ] Dark mode tokens defined and tested in both modes?
- [ ] Mobile collapse explicit for all high-variance layouts?
- [ ] `min-h-[100dvh]` used, never `h-screen`?
- [ ] `useEffect` animations have strict cleanup functions?
- [ ] Icons from allowed library only (Phosphor / HugeIcons / Radix / Tabler)?
- [ ] No `window.addEventListener('scroll')` — using Motion/ScrollTrigger/IO/CSS-timeline only?
- [ ] Core Web Vitals plausibly hit (LCP < 2.5s, INP < 200ms, CLS < 0.1)?

If a single checkbox fails, the page is not done. Fix it before delivering.
