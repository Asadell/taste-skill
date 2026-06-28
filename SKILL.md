---
name: design-taste-full
description: >
  Merged synthesis of leonxlnx/taste-skill (anti-slop layout, typography, color, design systems,
  architecture, pre-flight) and emilkowalski/skill (animation decision framework, spring physics,
  clip-path, gesture interactions, component craft, performance). Full-stack frontend taste skill for
  landing pages, portfolios, redesigns, and production-grade UI components.
---

# Design Taste — Full Skill
> Landing pages, company profiles, portfolios, redesigns, and production-grade UI components.
> Not dashboards, not data tables, not multi-step product UI.
> Every rule below is **contextual**. None of it fires automatically. First read the brief, then pull only what fits.

---

## CORE PHILOSOPHY

### Taste is trained, not innate

Good taste is not personal preference. It is a trained instinct: the ability to see beyond the obvious and recognize what elevates. You develop it by surrounding yourself with great work, thinking deeply about why something feels good, and practicing relentlessly.

When building UI, don't just make it work. Study why the best interfaces feel the way they do. Reverse engineer animations. Inspect interactions. Be curious.

### Unseen details compound

Most details users never consciously notice. That is the point. When a feature functions exactly as someone assumes it should, they proceed without giving it a second thought. That is the goal.

> "All those unseen details combine to produce something that's just stunning, like a thousand barely audible voices all singing in tune." - Paul Graham

Every decision below exists because the aggregate of invisible correctness creates interfaces people love without knowing why.

### Beauty is leverage

People select tools based on the overall experience, not just functionality. Good defaults and good animations are real differentiators. Beauty is underutilized in software. Use it as leverage to stand out.

### LLM design output is bad because the model jumps to defaults

Most AI-generated design is bad because the model jumps to a default aesthetic instead of reading the room. This skill corrects that at every layer: layout, color, typography, motion, and copy.

---

## 0. BRIEF INFERENCE (Read the Room Before Anything Else)

Before touching code or tweaking dials, **infer what the user actually wants**.

### 0.A Read these signals first

1. **Page kind** - landing (SaaS / consumer / agency / event), portfolio (dev / designer / creative studio), redesign (preserve vs overhaul), editorial / blog, product UI component.
2. **Vibe words** the user used - "minimalist", "calm", "Linear-style", "Awwwards", "brutalist", "premium consumer", "Apple-y", "playful", "serious B2B", "editorial", "agency-y", "glassy", "dark tech".
3. **Reference signals** - URLs they linked, screenshots they pasted, products they named, brands they're competing with.
4. **Audience** - B2B procurement panel vs. design-conscious consumer vs. recruiter scanning a portfolio. The audience picks the aesthetic, not your taste.
5. **Brand assets that already exist** - logo, color, type, photography. For redesigns, these are starting material, not optional input (see Section 11).
6. **Quiet constraints** - accessibility-first audiences, public-sector, regulated industries, trust-first commerce, kids' products. These constraints OVERRIDE aesthetic preference.

### 0.B Output a one-line "Design Read" before generating

Before any code, state in one line: **"Reading this as: \<page kind> for \<audience>, with a \<vibe> language, leaning toward \<design system or aesthetic family>."**

Example reads:

- *"Reading this as: B2B SaaS landing for technical buyers, with a Linear-style minimalist language, leaning toward Tailwind utilities + Geist + restrained motion."*
- *"Reading this as: solo designer portfolio for hiring managers, with an editorial / kinetic-type language, leaning toward native CSS + scroll-driven animation + custom typography."*
- *"Reading this as: redesign of a public-sector service site, with a trust-first language, leaning toward GOV.UK Frontend or USWDS."*
- *"Reading this as: product UI component for a SaaS dashboard, with crisp and fast motion, leaning toward shadcn/ui + CSS transitions + spring physics."*

### 0.C If the brief is ambiguous, ask one question, do not guess

Ask exactly **one** clarifying question - never a multi-question dump - and only when the design read genuinely diverges. Example: *"Should this feel closer to Linear-clean or Awwwards-experimental?"*

If you can confidently infer from context, **do not ask**. Just declare the design read and proceed.

### 0.D Anti-Default Discipline

Do not default to: AI-purple gradients, centered hero over dark mesh, three equal feature cards, generic glassmorphism on everything, infinite-loop micro-animations everywhere, Inter + slate-900. These are the LLM defaults. Reach past them deliberately based on the design read.

---

## 1. THE THREE DIALS (Core Configuration)

After the design read, set three dials. Every layout, motion, and density decision below is gated by these.

- **`DESIGN_VARIANCE: 8`** - 1 = Perfect Symmetry, 10 = Artsy Chaos
- **`MOTION_INTENSITY: 6`** - 1 = Static, 10 = Cinematic / Physics
- **`VISUAL_DENSITY: 4`** - 1 = Art Gallery / Airy, 10 = Cockpit / Packed Data

**Baseline:** `8 / 6 / 4`. Use these unless the design read overrides them. Do not ask the user to edit this file - overrides happen conversationally.

### 1.A Dial Inference (design read → dial values)

| Signal | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| "minimalist / clean / calm / editorial / Linear-style" | 5-6 | 3-4 | 2-3 |
| "premium consumer / Apple-y / luxury / brand" | 7-8 | 5-7 | 3-4 |
| "playful / wild / Dribbble / Awwwards / experimental / agency" | 9-10 | 8-10 | 3-4 |
| "landing page / portfolio / marketing site (default)" | 7-9 | 6-8 | 3-5 |
| "trust-first / public-sector / regulated / accessibility-critical" | 3-4 | 2-3 | 4-5 |
| "product UI / SaaS dashboard / app component" | 4-6 | 3-5 | 5-7 |
| "redesign - preserve" | match existing | +1 | match existing |
| "redesign - overhaul" | +2 | +2 | match existing |

### 1.B Use-Case Presets

| Use case | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| Landing (SaaS, mainstream) | 7 | 6 | 4 |
| Landing (Agency / creative) | 9 | 8 | 3 |
| Landing (Premium consumer) | 7 | 6 | 3 |
| Portfolio (Designer / studio) | 8 | 7 | 3 |
| Portfolio (Developer) | 6 | 5 | 4 |
| Editorial / Blog | 6 | 4 | 3 |
| Public-sector service | 3 | 2 | 5 |
| Product UI component | 5 | 4 | 6 |
| Redesign - preserve | match | match+1 | match |
| Redesign - overhaul | +2 | +2 | match |

### 1.C How the Dials Drive Output

Use these (or user-overridden values) as global variables. Cross-references throughout this document refer to these exact variable names - never invent aliases like `LAYOUT_VARIANCE` or `ANIM_LEVEL`.

---

## 2. BRIEF → DESIGN SYSTEM MAP

Once you have the design read (Section 0) and dials (Section 1), pick the right foundation. Do not invent CSS for things that have an official package. Do not pretend an aesthetic trend is an official system.

### 2.A When to reach for a real design system (use official packages)

| Brief reads as… | Reach for | Why |
|---|---|---|
| Microsoft / enterprise SaaS / dashboards | `@fluentui/react-components` or `@fluentui/web-components` | Official Fluent UI, Microsoft tokens, accessibility done |
| Google-ish UI, Material-flavored product | `@material/web` + Material 3 tokens | Official, theme-able via Material Theming |
| IBM-style B2B / enterprise analytics | `@carbon/react` + `@carbon/styles` | Official Carbon, mature data-density patterns |
| Shopify app surfaces | `polaris.js` web components / Polaris React | Required for Shopify admin UI |
| Atlassian / Jira-style product | `@atlaskit/*` + `@atlaskit/tokens` | Official Atlassian DS |
| GitHub-style devtool / community page | `@primer/css` or `@primer/react-brand` | Official Primer; Brand variant for marketing |
| Public-sector UK service | `govuk-frontend` | Legally / regulatorily expected |
| US public-sector / trust-first | `uswds` | Same |
| Fast local-business / agency MVP | Bootstrap 5.3 | Boring, fast, works |
| Modern accessible React foundation | `@radix-ui/themes` | Primitives + polished theme |
| Modern SaaS where you own the components | shadcn/ui (`npx shadcn@latest add ...`) | You own the code, easy to customise; never ship default state |
| Tailwind-based modern SaaS / AI marketing | Tailwind v4 utilities + `dark:` variant | Default for indie + small team builds |

**Honesty rule:** if the brief reads as one of the systems above, install and use the **official** package. Do not recreate its CSS by hand. Do not import a system's tokens but then override 90% of them.

**One system per project.** Do not mix Fluent React with Carbon in the same tree. Do not import shadcn/ui components into a Material 3 app.

### 2.B When the brief is an aesthetic, not a system

For these directions, there is **no single official package**. Build with native CSS + Tailwind + a maintained component library. Be honest in code comments about what is borrowed inspiration vs. official material.

| Aesthetic | Honest implementation |
|---|---|
| Glassmorphism / "frosted glass" | `backdrop-filter`, layered borders, highlight overlays. Provide solid-fill fallback for `prefers-reduced-transparency`. |
| Bento (Apple-style tile grids) | CSS Grid with mixed cell sizes. No single library owns this. |
| Brutalism | Native CSS, monospace, raw borders. No library. |
| Editorial / magazine | Serif type, asymmetric grid, generous whitespace. No library. |
| Dark tech / hacker | Mono + accent neon, terminal motifs. No library. |
| Aurora / mesh gradients | SVG or layered radial gradients. No library. |
| Kinetic typography | Native CSS animations, scroll-driven animations, GSAP for hijacks. No library. |
| **Apple Liquid Glass** | Apple documents this for Apple platforms only. **There is no official `liquid-glass.css`.** Web implementations are approximations using `backdrop-filter` + layered borders + highlights. Label clearly as approximation. |

---

## 3. DEFAULT ARCHITECTURE & CONVENTIONS

Unless the design read picks a real design system (Section 2.A), these are the defaults:

### 3.A Stack

- **Framework:** React or Next.js. Default to Server Components (RSC).
  - **RSC SAFETY:** Global state works ONLY in Client Components. In Next.js, wrap providers in a `"use client"` component.
  - **INTERACTIVITY ISOLATION:** Any component using Motion, scroll listeners, or pointer physics MUST be an isolated leaf with `'use client'` at the top. Server Components render static layouts only.
- **Styling:** **Tailwind v4** (default). Tailwind v3 only if the existing project demands it.
  - For v4: do NOT use `tailwindcss` plugin in `postcss.config.js`. Use `@tailwindcss/postcss` or the Vite plugin.
- **Animation:** **Motion** (the library formerly known as Framer Motion). Import from `motion/react` (`import { motion } from "motion/react"`). The `framer-motion` package still works as a legacy alias - prefer `motion/react` in new code.
- **Fonts:** Always use `next/font` (Next.js) or self-host with `@font-face` + `font-display: swap`. Never link Google Fonts via `<link>` in production.

### 3.B State

- Local `useState` / `useReducer` for isolated UI.
- Global state ONLY for deep prop-drilling avoidance - Zustand, Jotai, or React context.
- **NEVER** use `useState` to track continuous values driven by user input (mouse position, scroll progress, pointer physics, magnetic hover). Use Motion's `useMotionValue` / `useTransform` / `useScroll`. `useState` re-renders the React tree on every change and collapses on mobile.

### 3.C Icons

- **Allowed libraries (priority order):** `@phosphor-icons/react`, `hugeicons-react`, `@radix-ui/react-icons`, `@tabler/icons-react`.
- **Discouraged:** `lucide-react`. Acceptable only when the user explicitly asks for it or the project already depends on it.
- **NEVER hand-roll SVG icons.** If a glyph is missing, install a second library or compose from primitives - do not draw icon paths from scratch.
- **One family per project.** Do not mix Phosphor with Lucide in the same component tree.
- **Standardize `strokeWidth` globally** (e.g. `1.5` or `2.0`).

### 3.D Emoji Policy

Discouraged by default in code, markup, and visible text. Replace symbols with icon-library glyphs. **Override:** allow emojis only when the user explicitly asks for a playful / chat-style / social-native vibe - and even then use them sparingly with intent.

### 3.E Responsiveness & Layout Mechanics

- Standardize breakpoints (`sm 640`, `md 768`, `lg 1024`, `xl 1280`, `2xl 1536`).
- Contain page layouts using `max-w-[1400px] mx-auto` or `max-w-7xl`.
- **Viewport Stability:** NEVER use `h-screen` for full-height Hero sections. ALWAYS use `min-h-[100dvh]` to prevent layout jumping on mobile (iOS Safari address bar).
- **Grid over Flex-Math:** NEVER use complex flexbox percentage math (`w-[calc(33%-1rem)]`). ALWAYS use CSS Grid (`grid grid-cols-1 md:grid-cols-3 gap-6`).

### 3.F Dependency Verification (mandatory)

Before importing ANY 3rd-party library, check `package.json`. If the package is missing, output the install command first. **Never** assume a library exists.

---

## 4. DESIGN ENGINEERING DIRECTIVES (Bias Correction)

LLMs default to clichés. Override these defaults proactively. Each rule has a context-aware override path.

### 4.1 Typography

- **Display / Headlines:** Default `text-4xl md:text-6xl tracking-tighter leading-none`.
- **Body / Paragraphs:** Default `text-base text-gray-600 leading-relaxed max-w-[65ch]`. Cap body text at about 65ch instead of stretching full width so line length stays comfortable to read.
- **Tabular numbers:** Apply `tabular-nums` to price columns and metrics so digits align and the column reads cleanly.
- **Ellipsis:** Use the `…` character instead of `...` in markup so truncation follows the container instead of snapping at a fixed character count.
- **Uppercase labels:** Loosen letter-spacing on uppercase labels; tight uppercase reads cramped.
- **Font loading:** Declare a fallback stack whose x-height and weight match the primary face so loading does not cause layout shift.
- **Underlines:** Reserve underlines for links; emphasize non-link text with weight or color so underline stays a reliable affordance.

- **Sans font choice:**
  - **Discouraged as default:** `Inter`. Pick `Geist`, `Outfit`, `Cabinet Grotesk`, `Satoshi`, or a brand-appropriate sans first.
  - **Override:** Inter is acceptable when the user explicitly asks for a neutral / standard / Linear-style feel, or when the brief is a public-sector / accessibility-first site.
- **Pairings to know:** `Geist` + `Geist Mono`, `Satoshi` + `JetBrains Mono`, `Cabinet Grotesk` + `Inter Tight`, `GT America` + `IBM Plex Mono`.

- **SERIF DISCIPLINE (VERY DISCOURAGED AS DEFAULT):**
  - Serif is **very discouraged as the default font for any project.** "It feels creative / premium / editorial" is NOT a reason to reach for serif. The agent's default mental model that "creative brief = serif" is the single most-tested AI tell in production rounds.
  - **Serif is only acceptable when ONE of these is explicitly true:**
    - The brand brief literally names a serif font, OR
    - The aesthetic family is genuinely editorial / luxury / publication / manuscript / heritage / vintage AND you can articulate why this specific serif fits this specific brand
  - For everything else (creative agency, design studio, modern brand, premium consumer, portfolio, lifestyle), **default sans-serif display** (Geist Display, ABC Diatype, Söhne Breit, Cabinet Grotesk Display, Migra Sans, GT Walsheim, Inter Display, PP Neue Montreal). Sans display fonts are not "boring" — they are the default for the same reason black is the default in fashion.
  - **EMPHASIS RULE (related):** When you want to emphasize a word within a headline (the kinetic "and `spatial` design" type move), use **italic or bold of the SAME font**. Do NOT inject a random serif word into a sans headline (or vice versa) just to add visual interest. Mixed-family emphasis is amateur. Italic/bold emphasis in the same family is the right move.
  - **Specifically BANNED as defaults:** `Fraunces` and `Instrument_Serif` (the two LLM-favorite display serifs).
  - **If a serif is justified** (rare, per the above), rotate from this pool, do NOT reuse the same serif across consecutive projects: PP Editorial New, GT Sectra Display, Cardinal Grotesque, Reckless Neue, Tiempos Headline, Recoleta, Cormorant Garamond, Playfair Display, EB Garamond, IvyPresto, Migra, Editorial Old, Saol Display, Söhne Breit Kursiv, Domaine Display, Canela, Schnyder, Tobias, NB Architekt, ITC Galliard.

- **ITALIC DESCENDER CLEARANCE (mandatory):** When italic is used in display type and the word contains a descender letter (`y g j p q`), `leading-[1]` or `leading-none` will clip the descender. Use `leading-[1.1]` minimum and add `pb-1` or `mb-1` reserve on the wrapping element. Audit every italic word in display headlines before shipping.

### 4.2 Color Calibration

- Max 1 accent color. Saturation < 80% by default.
- **THE LILA RULE:** The "AI Purple / Blue glow" aesthetic is discouraged as a default. No automatic purple button glows, no random neon gradients. Use neutral bases (Zinc / Slate / Stone) with high-contrast singular accents (Emerald, Electric Blue, Deep Rose, Burnt Orange, etc.).
- **Override:** if the brand or brief explicitly asks for purple / violet / lila, embrace it. But execute with intent: consistent palette, harmonised neutrals, restrained gradients. Not generic AI gradient slop.
- **One palette per project.** Do not fluctuate between warm and cool grays within the same project.
- **COLOR CONSISTENCY LOCK (mandatory):** Once an accent color is chosen for a page, it is used on the WHOLE page. A warm-grey site does not suddenly get a blue CTA in section 7. A rose-accented site does not get a teal status badge in the footer. Pick one accent, lock it, audit every component before shipping.

- **PREMIUM-CONSUMER PALETTE BAN (mandatory, second-most-recurring AI-tell):**
  - For premium-consumer briefs (cookware, wellness, artisan, luxury, heritage craft, DTC home goods, etc.) the LLM default is **warm beige/cream + brass/clay/oxblood/ochre + espresso/ink dark text**. Concretely banned hex families as default backgrounds and accents:
    - Backgrounds: `#f5f1ea`, `#f7f5f1`, `#fbf8f1`, `#efeae0`, `#ece6db`, `#faf7f1`, `#e8dfcb` (all "warm paper / cream / chalk / bone")
    - Accents: `#b08947`, `#b6553a`, `#9a2436`, `#9c6e2a`, `#bc7c3a`, `#7d5621` (all "brass / clay / oxblood / ochre")
    - Text: `#1a1714`, `#1a1814`, `#1b1814` (all "espresso / warm near-black")
  - This palette is BANNED as the default reach for premium-consumer briefs.
  - **Default alternatives (rotate, do not reuse):**
    - **Cold Luxury:** silver-grey + chrome + smoke
    - **Forest:** deep green + bone + amber accent
    - **Black and Tan:** true off-black + warm tan, sharp contrast, no beige
    - **Cobalt + Cream:** saturated blue against a single neutral, no brass
    - **Terracotta + Slate:** warm rust against cool grey, no brass
    - **Olive + Brick + Paper:** muted olive plus brick-red accent
    - **Pure monochrome + single saturated pop:** off-white + off-black + one bright accent (electric blue, emerald, hot pink, etc.)
  - **Override:** the beige+brass+espresso palette is acceptable ONLY when the brand brief explicitly names those colors, or when the brand identity is genuinely vintage / artisan / warm-craft AND you can articulate why this specific palette fits this specific brand.

### 4.3 Layout Diversification

- **ANTI-CENTER BIAS:** Centered Hero / H1 sections are avoided when `DESIGN_VARIANCE > 4`. Force "Split Screen" (50/50), "Left-aligned content / right-aligned asset", "Asymmetric white-space", or scroll-pinned structures.
- **Override:** centered hero is OK for editorial / manifesto / launch-announcement briefs where the message itself is the design.

### 4.4 Materiality, Shadows, Cards

- Use cards ONLY when elevation communicates real hierarchy. Otherwise group with `border-t`, `divide-y`, or negative space.
- When a shadow is used, tint it to the background hue. No pure-black drop shadows on light backgrounds.
- For `VISUAL_DENSITY > 7`: generic card containers are banned. Data metrics breathe in plain layout.
- **SHAPE CONSISTENCY LOCK (mandatory):** Pick ONE corner-radius scale for the page and stick to it. Options: all-sharp (radius 0), all-soft (radius 12-16px), all-pill (full radius for interactive). Mixed systems are allowed only when there is a documented rule (e.g. "buttons are full-pill, cards are 16px, inputs are 8px") and that rule is followed everywhere. Round buttons in a square layout, or square cards on a pill-button page, is broken design.

### 4.5 Interactive UI States

LLMs default to "static successful state only." Always implement full cycles:

- **Loading:** Skeletal loaders matching the final layout's shape. Avoid generic circular spinners.
- **Empty States:** Beautifully composed; indicate how to populate.
- **Error States:** Clear, inline (forms), or contextual (toasts only for transient).
- **Tactile Feedback:** On `:active`, use `scale(0.97)` or `scale(0.98)` to simulate a physical push. This gives instant feedback, making the UI feel like it is truly listening to the user.
- **BUTTON CONTRAST CHECK (mandatory, a11y):** Before shipping any button, verify the button text is readable against the button background. Audit every CTA: contrast ratio WCAG AA min (4.5:1 for body, 3:1 for large text 18px+).
- **CTA BUTTON WRAP BAN (mandatory):** Button text MUST fit on one line at desktop. Fix by EITHER shortening the label (3 words max for primary CTAs) OR widening the button.
- **NO DUPLICATE CTA INTENT (mandatory):** Two CTAs with the same intent on one page is a Pre-Flight Fail. Pick ONE label per intent and use it everywhere.
- **FORM CONTRAST CHECK (mandatory, a11y):** Form inputs, placeholder text, focus rings, helper text, and error text all pass WCAG AA contrast against the section background.

### 4.6 Data & Form Patterns

- Label ABOVE input. Helper text optional but present in markup. Error text BELOW input. Standard `gap-2` for input blocks.
- No placeholder-as-label. Ever.

### 4.7 Layout Discipline (Hard Rules)

- **Hero MUST fit in the initial viewport.** Headline max 2 lines on desktop, subtext max **20 words** AND max 3-4 lines, CTAs visible without scroll.
- **Hero font-scale discipline.** Plan font size and image size *together*. Default sensible range: `text-4xl md:text-5xl lg:text-6xl` for most heroes; `text-6xl md:text-7xl` only when the headline is 3-5 words.
- **HERO TOP PADDING CAP (mandatory):** Hero top padding max `pt-24` (≈6rem) at desktop.
- **HERO STACK DISCIPLINE (max 4 text elements):**
  1. Eyebrow (small uppercase label) OR brand strip OR neither
  2. Headline (max 2 lines)
  3. Subtext (max 20 words, max 4 lines)
  4. CTAs (1 primary + max 1 secondary)
  - **BANNED in the hero:** trust micro-strip, pricing teaser, feature bullet list, social-proof avatar row.
- **"Used by" / "Trusted by" logo wall belongs UNDER the hero, never inside it.**
- **Navigation MUST render on a single line on desktop.** Height cap: 80px max desktop, default 64-72px.
- **Bento grids MUST have rhythm, not one-sided repetition.**
- **BENTO CELL COUNT RULE (mandatory):** N items → N cells. No empty cells.
- **Section-Layout-Repetition Ban.** Each layout family at most ONCE per page. A landing page with 8 sections must use at least 4 different layout families.
- **ZIGZAG ALTERNATION CAP (mandatory).** Max 2 consecutive image+text-split sections. The 3rd is a Pre-Flight Fail.
- **EYEBROW RESTRAINT (mandatory):** Maximum 1 eyebrow per 3 sections. Hero counts as 1. Pre-flight is mechanical: count instances of `uppercase tracking`; if count > ceil(sectionCount / 3), the output fails.
- **SPLIT-HEADER BAN (mandatory).** "Left big headline + right small explainer paragraph" is banned as default. Stack them vertically instead.
- **Bento Background Diversity (mandatory).** At least 2-3 cells in any multi-cell grid need real visual variation.
- **Mobile collapse must be explicit per section.** Declare the `< 768px` fallback in the same component.

### 4.8 Image & Visual Asset Strategy

Landing pages and portfolios are **visual products**. Text-only pages with fake-screenshot divs are slop.

**Priority order for visual assets:**

1. **Image-generation tool first.** If ANY image-gen tool is available, use it.
2. **Real web images second.** `https://picsum.photos/seed/{descriptive-seed}/{w}/{h}` for placeholder photography.
3. **Last resort: tell the user.** Leave clearly-labeled placeholder slots and list what's needed.

**Real company logos for social proof.** Use real SVG logos from Simple Icons (`https://cdn.simpleicons.org/{slug}/ffffff`) or devicon. Never plain text wordmarks.

**LOGO-ONLY rule (mandatory):** logo wall = logos and nothing else. No industry / category labels below each logo.

**Div-based fake screenshots are banned.** Use a real screenshot, a generated image, or a real component preview.

**Hero needs a real visual.** Text + gradient blob is not a hero - it's a placeholder.

### 4.9 Content Density

- **Default content shape per section:** short headline (≤ 8 words) + short sub-paragraph (≤ 25 words) + one visual asset OR one CTA.
- **No data-dump sections.**
- **Long lists need a different UI component, not a longer list.** If you have > 5 items, reach for: 2-column split, card grid, tabs/accordion, horizontal scroll-snap pills, carousel, or marquee.
- **Spec sheets:** Banned in raw table form. Use 2-col card grid, scroll-snap pills, grouped chunks, or featured-vs-rest disclosure.
- **COPY SELF-AUDIT (mandatory before ship):** Re-read every visible string. Flag and rewrite: grammatically broken, unclear referents, AI hallucination, mock-poetic micro-meta.
- **Fake-precise numbers are flagged.** Numbers like `92%`, `4.1×`, `48k` must come from real data or be labeled as mock.
- **One copy register per page.**

### 4.10 Quotes & Testimonials

- **Max 3 lines** of quote body. Never 6.
- Attribution: name + role + (optionally) company. Never name only.
- Quote marks: use real typographic quotes ( " " ) or none at all. Not straight ASCII.

### 4.11 Page Theme Lock

The page has ONE theme. Sections do not invert.

- Pick light, dark, or auto (`prefers-color-scheme`) at the page level and lock it.
- Section-level background tints within the same theme family are fine (`bg-zinc-950` next to `bg-zinc-900`).
- When using a design system with built-in theming, set the theme ONCE in `layout.tsx` or the page root.

---

## 5. ANIMATION DECISION FRAMEWORK (Emil Kowalski)

Before writing any animation code, answer these questions in order. This framework applies to ALL animations in the project regardless of surface.

### 5.1 Should this animate at all?

**Ask:** How often will users see this animation?

| Frequency | Decision |
|---|---|
| 100+ times/day (keyboard shortcuts, command palette toggle) | No animation. Ever. |
| Tens of times/day (hover effects, list navigation) | Remove or drastically reduce |
| Occasional (modals, drawers, toasts) | Standard animation |
| Rare/first-time (onboarding, feedback forms, celebrations) | Can add delight |

**Never animate keyboard-initiated actions.** These actions are repeated hundreds of times daily. Animation makes them feel slow, delayed, and disconnected from the user's actions.

Raycast has no open/close animation. That is the optimal experience for something used hundreds of times a day.

### 5.2 What is the purpose?

Every animation must have a clear answer to "why does this animate?"

Valid purposes:

- **Spatial consistency**: toast enters and exits from the same direction, making swipe-to-dismiss feel intuitive
- **State indication**: a morphing feedback button shows the state change
- **Explanation**: a marketing animation that shows how a feature works
- **Feedback**: a button scales down on press, confirming the interface heard the user
- **Preventing jarring changes**: elements appearing or disappearing without transition feel broken

If the purpose is just "it looks cool" and the user will see it often, don't animate.

**MOTION MUST BE MOTIVATED (mandatory).** Before adding any animation, ask: "what does this animation communicate?" Valid answers: hierarchy, storytelling, feedback, state transition. Invalid answer: "it looked cool". GSAP everywhere because GSAP is available is amateur. Each ScrollTrigger, each marquee, each pinned section needs a reason. If you cannot articulate the reason in one sentence, drop the animation.

### 5.3 What easing should it use?

```
Is the element entering or exiting?
  Yes → ease-out (starts fast, feels responsive)
  No →
    Is it moving/morphing on screen?
      Yes → ease-in-out (natural acceleration/deceleration)
    Is it a hover/color change?
      Yes → ease
    Is it constant motion (marquee, progress bar)?
      Yes → linear
    Default → ease-out
```

**Critical: use custom easing curves.** The built-in CSS easings are too weak. They lack the punch that makes animations feel intentional.

```css
/* Strong ease-out for UI interactions */
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);

/* Strong ease-in-out for on-screen movement */
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);

/* iOS-like drawer curve (from Ionic Framework) */
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);
```

**Never use ease-in for UI animations.** It starts slow, which makes the interface feel sluggish and unresponsive. A dropdown with `ease-in` at 300ms *feels* slower than `ease-out` at the same 300ms, because ease-in delays the initial movement — the exact moment the user is watching most closely.

**Easing curve resources:** Use [easing.dev](https://easing.dev/) or [easings.co](https://easings.co/) to find stronger custom variants of standard easings.

### 5.4 How fast should it be?

| Element | Duration |
|---|---|
| Button press feedback | 100-160ms |
| Tooltips, small popovers | 125-200ms |
| Dropdowns, selects | 150-250ms |
| Modals, drawers | 200-500ms |
| Marketing/explanatory | Can be longer |

**Rule: UI animations should stay under 300ms.** A 180ms dropdown feels more responsive than a 400ms one. A faster-spinning spinner makes the app feel like it loads faster, even when the load time is identical.

### 5.5 Perceived performance

Speed in animation is not just about feeling snappy — it directly affects how users perceive your app's performance:

- A **fast-spinning spinner** makes loading feel faster (same load time, different perception)
- A **180ms select** animation feels more responsive than a **400ms** one
- **Instant tooltips** after the first one is open (skip delay + skip animation) make the whole toolbar feel faster

The perception of speed matters as much as actual speed. Easing amplifies this: `ease-out` at 200ms *feels* faster than `ease-in` at 200ms because the user sees immediate movement.

---

## 6. SPRING ANIMATIONS

Springs feel more natural than duration-based animations because they simulate real physics. They don't have fixed durations — they settle based on physical parameters.

### 6.A When to use springs

- Drag interactions with momentum
- Elements that should feel "alive" (like Apple's Dynamic Island)
- Gestures that can be interrupted mid-animation
- Decorative mouse-tracking interactions
- Magnetic micro-physics when `MOTION_INTENSITY > 5`

### 6.B Spring-based mouse interactions

Tying visual changes directly to mouse position feels artificial because it lacks motion. Use `useSpring` from Motion to interpolate value changes with spring-like behavior instead of updating immediately.

```jsx
import { useSpring } from 'framer-motion';

// Without spring: feels artificial, instant
const rotation = mouseX * 0.1;

// With spring: feels natural, has momentum
const springRotation = useSpring(mouseX * 0.1, {
  stiffness: 100,
  damping: 10,
});
```

This works because the animation is **decorative** — it doesn't serve a function. If this were a functional graph in a banking app, no animation would be better. Know when decoration helps and when it hinders.

Implement magnetic micro-physics EXCLUSIVELY with Motion's `useMotionValue` / `useTransform` outside the React render cycle. Never `useState`. See Section 3.B.

### 6.C Spring configuration

**Apple's approach (recommended — easier to reason about):**

```js
{ type: "spring", duration: 0.5, bounce: 0.2 }
```

**Traditional physics (more control):**

```js
{ type: "spring", mass: 1, stiffness: 100, damping: 10 }
```

Keep bounce subtle (0.1-0.3) when used. Avoid bounce in most UI contexts. Use it for drag-to-dismiss and playful interactions.

### 6.D Interruptibility advantage

Springs maintain velocity when interrupted — CSS animations and keyframes restart from zero. This makes springs ideal for gestures users might change mid-motion. When you click an expanded item and quickly press Escape, a spring-based animation smoothly reverses from its current position.

---

## 7. COMPONENT ANIMATION PRINCIPLES

### 7.A Buttons must feel responsive

Add `transform: scale(0.97)` on `:active`. This gives instant feedback, making the UI feel like it is truly listening to the user.

```css
.button {
  transition: transform 160ms ease-out;
}

.button:active {
  transform: scale(0.97);
}
```

This applies to any pressable element. The scale should be subtle (0.95-0.98).

### 7.B Never animate from scale(0)

Nothing in the real world disappears and reappears completely. Elements animating from `scale(0)` look like they come out of nowhere.

Start from `scale(0.9)` or higher, combined with opacity. Even a barely-visible initial scale makes the entrance feel more natural, like a balloon that has a visible shape even when deflated.

```css
/* Bad */
.entering {
  transform: scale(0);
}

/* Good */
.entering {
  transform: scale(0.95);
  opacity: 0;
}
```

### 7.C Make popovers origin-aware

Popovers should scale in from their trigger, not from center. The default `transform-origin: center` is wrong for almost every popover.

**Exception: modals.** Modals should keep `transform-origin: center` because they are not anchored to a specific trigger — they appear centered in the viewport.

```css
/* Radix UI */
.popover {
  transform-origin: var(--radix-popover-content-transform-origin);
}

/* Base UI */
.popover {
  transform-origin: var(--transform-origin);
}
```

Whether the user notices the difference individually does not matter. In the aggregate, unseen details become visible. They compound.

### 7.D Tooltips: skip delay on subsequent hovers

Tooltips should delay before appearing to prevent accidental activation. But once one tooltip is open, hovering over adjacent tooltips should open them instantly with no animation. This feels faster without defeating the purpose of the initial delay.

```css
.tooltip {
  transition: transform 125ms ease-out, opacity 125ms ease-out;
  transform-origin: var(--transform-origin);
}

.tooltip[data-starting-style],
.tooltip[data-ending-style] {
  opacity: 0;
  transform: scale(0.97);
}

/* Skip animation on subsequent tooltips */
.tooltip[data-instant] {
  transition-duration: 0ms;
}
```

### 7.E Use CSS transitions over keyframes for interruptible UI

CSS transitions can be interrupted and retargeted mid-animation. Keyframes restart from zero. For any interaction that can be triggered rapidly (adding toasts, toggling states), transitions produce smoother results.

```css
/* Interruptible - good for UI */
.toast {
  transition: transform 400ms ease;
}

/* Not interruptible - avoid for dynamic UI */
@keyframes slideIn {
  from { transform: translateY(100%); }
  to { transform: translateY(0); }
}
```

### 7.F Use blur to mask imperfect transitions

When a crossfade between two states feels off despite trying different easings and durations, add subtle `filter: blur(2px)` during the transition.

**Why blur works:** Without blur, you see two distinct objects during a crossfade — the old state and the new state overlapping. Blur bridges the visual gap by blending the two states together, tricking the eye into perceiving a single smooth transformation.

```css
.button-content {
  transition: filter 200ms ease, opacity 200ms ease;
}

.button-content.transitioning {
  filter: blur(2px);
  opacity: 0.7;
}
```

Keep blur under 20px. Heavy blur is expensive, especially in Safari.

### 7.G Animate enter states with @starting-style

The modern CSS way to animate element entry without JavaScript:

```css
.toast {
  opacity: 1;
  transform: translateY(0);
  transition: opacity 400ms ease, transform 400ms ease;

  @starting-style {
    opacity: 0;
    transform: translateY(100%);
  }
}
```

Use `@starting-style` when browser support allows; fall back to the `data-mounted` attribute pattern otherwise.

```jsx
// Legacy pattern (still works everywhere)
useEffect(() => {
  setMounted(true);
}, []);
// <div data-mounted={mounted}>
```

### 7.H Asymmetric enter/exit timing

Pressing should be slow when it needs to be deliberate (hold-to-delete: 2s linear), but release should always be snappy (200ms ease-out). This pattern applies broadly: slow where the user is deciding, fast where the system is responding.

```css
/* Release: fast */
.overlay {
  transition: clip-path 200ms ease-out;
}

/* Press: slow and deliberate */
.button:active .overlay {
  transition: clip-path 2s linear;
}
```

### 7.I Stagger animations

When multiple elements enter together, stagger their appearance. This creates a cascading effect that feels more natural than everything appearing at once.

```css
.item {
  opacity: 0;
  transform: translateY(8px);
  animation: fadeIn 300ms ease-out forwards;
}

.item:nth-child(1) { animation-delay: 0ms; }
.item:nth-child(2) { animation-delay: 50ms; }
.item:nth-child(3) { animation-delay: 100ms; }
.item:nth-child(4) { animation-delay: 150ms; }

@keyframes fadeIn {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

Keep stagger delays short (30-80ms between items). Long delays make the interface feel slow. Stagger is decorative — never block interaction while stagger animations are playing.

### 7.J The Sonner Principles (Building Loved Components)

These principles come from building Sonner (13M+ weekly npm downloads) and apply to any component:

1. **Developer experience is key.** No hooks, no context, no complex setup. Insert `<Toaster />` once, call `toast()` from anywhere.
2. **Good defaults matter more than options.** Ship beautiful out of the box. Most users never customize.
3. **Naming creates identity.** "Sonner" (French for "to ring") feels more elegant than "react-toast". Sacrifice discoverability for memorability when appropriate.
4. **Handle edge cases invisibly.** Pause toast timers when the tab is hidden. Fill gaps between stacked toasts with pseudo-elements to maintain hover state. Users never notice these, and that is exactly right.
5. **Use transitions, not keyframes, for dynamic UI.** Toasts are added rapidly. Keyframes restart from zero on interruption. Transitions retarget smoothly.
6. **Build a great documentation site.** Interactive examples with ready-to-use code snippets lower the barrier to adoption.

**Cohesion matters.** Sonner's animation feels satisfying partly because the whole experience is cohesive. The easing and duration fit the vibe of the library. Match the motion to the mood.

---

## 8. CSS TRANSFORM MASTERY

### 8.A translateY with percentages

Percentage values in `translate()` are relative to the element's own size. Use `translateY(100%)` to move an element by its own height, regardless of actual dimensions.

```css
/* Works regardless of drawer height */
.drawer-hidden {
  transform: translateY(100%);
}

/* Works regardless of toast height */
.toast-enter {
  transform: translateY(-100%);
}
```

Prefer percentages over hardcoded pixel values. They are less error-prone and adapt to content.

### 8.B scale() scales children too

Unlike `width`/`height`, `scale()` also scales an element's children. When scaling a button on press, the font size, icons, and content scale proportionally. This is a feature, not a bug.

### 8.C 3D transforms for depth

`rotateX()`, `rotateY()` with `transform-style: preserve-3d` create real 3D effects in CSS. Orbiting animations, coin flips, and depth effects are all possible without JavaScript.

```css
.wrapper {
  transform-style: preserve-3d;
}

@keyframes orbit {
  from {
    transform: translate(-50%, -50%) rotateY(0deg) translateZ(72px) rotateY(360deg);
  }
  to {
    transform: translate(-50%, -50%) rotateY(360deg) translateZ(72px) rotateY(0deg);
  }
}
```

### 8.D transform-origin

Every element has an anchor point from which transforms execute. The default is center. Set it to match where the trigger lives for origin-aware interactions.

---

## 9. CLIP-PATH FOR ANIMATION

`clip-path` is not just for shapes. It is one of the most powerful animation tools in CSS.

### 9.A The inset shape

`clip-path: inset(top right bottom left)` defines a rectangular clipping region. Each value "eats" into the element from that side.

```css
/* Fully hidden from right */
.hidden {
  clip-path: inset(0 100% 0 0);
}

/* Fully visible */
.visible {
  clip-path: inset(0 0 0 0);
}

/* Reveal from left to right */
.overlay {
  clip-path: inset(0 100% 0 0);
  transition: clip-path 200ms ease-out;
}
.button:active .overlay {
  clip-path: inset(0 0 0 0);
  transition: clip-path 2s linear;
}
```

### 9.B Tabs with perfect color transitions

Duplicate the tab list. Style the copy as "active" (different background, different text color). Clip the copy so only the active tab is visible. Animate the clip on tab change. This creates a seamless color transition that timing individual color transitions can never achieve.

### 9.C Hold-to-delete pattern

Use `clip-path: inset(0 100% 0 0)` on a colored overlay. On `:active`, transition to `inset(0 0 0 0)` over 2s with linear timing. On release, snap back with 200ms ease-out. Add `scale(0.97)` on the button for press feedback.

### 9.D Image reveals on scroll

Start with `clip-path: inset(0 0 100% 0)` (hidden from bottom). Animate to `inset(0 0 0 0)` when the element enters the viewport. Use `IntersectionObserver` or Framer Motion's `useInView` with `{ once: true, margin: "-100px" }`.

### 9.E Comparison sliders

Overlay two images. Clip the top one with `clip-path: inset(0 50% 0 0)`. Adjust the right inset value based on drag position. No extra DOM elements needed, fully hardware-accelerated.

---

## 10. GESTURE AND DRAG INTERACTIONS

### 10.A Momentum-based dismissal

Don't require dragging past a threshold. Calculate velocity: `Math.abs(dragDistance) / elapsedTime`. If velocity exceeds ~0.11, dismiss regardless of distance. A quick flick should be enough.

```js
const timeTaken = new Date().getTime() - dragStartTime.current.getTime();
const velocity = Math.abs(swipeAmount) / timeTaken;

if (Math.abs(swipeAmount) >= SWIPE_THRESHOLD || velocity > 0.11) {
  dismiss();
}
```

### 10.B Damping at boundaries

When a user drags past the natural boundary (e.g., dragging a drawer up when already at top), apply damping. The more they drag, the less the element moves. Things in real life don't suddenly stop; they slow down first.

### 10.C Pointer capture for drag

Once dragging starts, set the element to capture all pointer events. This ensures dragging continues even if the pointer leaves the element bounds.

### 10.D Multi-touch protection

Ignore additional touch points after the initial drag begins. Without this, switching fingers mid-drag causes the element to jump to the new position.

```js
function onPress() {
  if (isDragging) return;
  // Start drag...
}
```

### 10.E Friction instead of hard stops

Instead of preventing upward drag entirely, allow it with increasing friction. It feels more natural than hitting an invisible wall.

---

## 11. PERFORMANCE RULES

### 11.A Only animate transform and opacity

These properties skip layout and paint, running on the GPU. Animating `padding`, `margin`, `height`, or `width` triggers all three rendering steps.

### 11.B CSS variables are inheritable

Changing a CSS variable on a parent recalculates styles for all children. In a drawer with many items, updating `--swipe-amount` on the container causes expensive style recalculation. Update `transform` directly on the element instead.

```js
// Bad: triggers recalc on all children
element.style.setProperty('--swipe-amount', `${distance}px`);

// Good: only affects this element
element.style.transform = `translateY(${distance}px)`;
```

### 11.C Framer Motion hardware acceleration caveat

Framer Motion's shorthand properties (`x`, `y`, `scale`) are NOT hardware-accelerated. They use `requestAnimationFrame` on the main thread. For hardware acceleration, use the full `transform` string:

```jsx
// NOT hardware accelerated (convenient but drops frames under load)
<motion.div animate={{ x: 100 }} />

// Hardware accelerated (stays smooth even when main thread is busy)
<motion.div animate={{ transform: "translateX(100px)" }} />
```

This matters when the browser is simultaneously loading content, running scripts, or painting.

### 11.D CSS animations beat JS under load

CSS animations run off the main thread. When the browser is busy loading a new page, Framer Motion animations (using `requestAnimationFrame`) drop frames. CSS animations remain smooth. Use CSS for predetermined animations; JS for dynamic, interruptible ones.

### 11.E Use WAAPI for programmatic CSS animations

The Web Animations API gives you JavaScript control with CSS performance. Hardware-accelerated, interruptible, and no library needed.

```js
element.animate(
  [{ clipPath: 'inset(0 0 100% 0)' }, { clipPath: 'inset(0 0 0 0)' }],
  {
    duration: 1000,
    fill: 'forwards',
    easing: 'cubic-bezier(0.77, 0, 0.175, 1)',
  }
);
```

### 11.F Hardware Acceleration

- Animate ONLY `transform` and `opacity`. Never animate `top`, `left`, `width`, `height`.
- Use `will-change: transform` sparingly - only on elements that will actually animate.

### 11.G DOM Cost

- Apply grain / noise filters EXCLUSIVELY to fixed, `pointer-events-none` pseudo-elements. NEVER on scrolling containers - continuous GPU repaints destroy mobile FPS.
- Be aware of bundle size. Motion is not tiny. Three.js is large. Lazy-load anything that's not above-the-fold.

### 11.H Z-Index Restraint

NEVER spam arbitrary `z-50` or `z-10`. Use z-index strictly for systemic layer contexts (sticky navbars, modals, overlays, grain). Document the z-index scale in a project constants file.

---

## 12. ACCESSIBILITY

### 12.A prefers-reduced-motion (mandatory)

Animations can cause motion sickness. Reduced motion means fewer and gentler animations, not zero. Keep opacity and color transitions that aid comprehension. Remove movement and position animations.

**Any motion above `MOTION_INTENSITY > 3` MUST honor `prefers-reduced-motion`.**

```css
@media (prefers-reduced-motion: reduce) {
  .element {
    animation: fade 0.2s ease;
    /* No transform-based motion */
  }
}
```

```jsx
const shouldReduceMotion = useReducedMotion();
const closedX = shouldReduceMotion ? 0 : '-100%';
```

In Motion: wrap with `useReducedMotion()` and degrade to static.

Infinite loops, parallax, scroll-hijack, and magnetic physics MUST collapse to static / instant under reduced motion.

### 12.B Touch device hover states

Touch devices trigger hover on tap, causing false positives. Gate hover animations behind this media query.

```css
@media (hover: hover) and (pointer: fine) {
  .element:hover {
    transform: scale(1.05);
  }
}
```

### 12.C Dark Mode (mandatory for any consumer-facing page)

- Design for **both modes from the start**. Never ship light-only or dark-only without explicit user instruction.
- Use Tailwind `dark:` variant OR CSS variables for tokens. Pick one strategy per project.
- Respect `prefers-color-scheme: dark`. Default to system preference unless the brand insists on one mode.
- **No pure `#000000` and no pure `#ffffff`** - use off-black (zinc-950, near-black warm gray) and off-white. Pure values kill depth.
- Test in both modes before finishing. Do not ship a page you've only seen in one mode.

### 12.D Core Web Vitals Targets

- **LCP** < 2.5s. Hero image must be `next/image priority` or preloaded.
- **INP** < 200ms. Heavy work off main thread.
- **CLS** < 0.1. Reserve space for images, fonts, embeds.

---

## 13. CONTEXT-AWARE PROACTIVITY

These are tools, not defaults. Use them when the design read calls for them. **None of these fire automatically.**

- **Liquid Glass / Glassmorphism:** Appropriate for premium consumer, Apple-adjacent, luxury brand, or media-overlay vibes. Inappropriate for dashboards, public-sector, or "boring B2B." When used, go beyond `backdrop-blur`: add a 1px inner border (`border-white/10`) and a subtle inner shadow (`shadow-[inset_0_1px_0_rgba(255,255,255,0.1)]`). Provide a solid-fill fallback under `prefers-reduced-transparency`.
- **Magnetic Micro-physics:** Use when `MOTION_INTENSITY > 5` AND the brief reads premium / playful / agency. Implement EXCLUSIVELY with Motion's `useMotionValue` / `useTransform`. Never `useState`.
- **Perpetual Micro-Interactions** (Pulse, Typewriter, Float, Shimmer, Carousel): Use when `MOTION_INTENSITY > 5` AND the section actively benefits from motion. **Not every card needs an infinite loop.** Apply Spring Physics (`type: "spring", stiffness: 100, damping: 20`) - no linear easing.
- **"Motion claimed, motion shown."** If `MOTION_INTENSITY > 4`, the page must actually move. A static page that claims `MOTION_INTENSITY: 7` is broken.
- **MARQUEE MAX-ONE-PER-PAGE (mandatory).** Horizontal scrolling text marquees are appropriate at most ONCE per page.

---

## 14. ADVANCED SCROLL PATTERNS

### 14.A Sticky-Stack - Canonical Skeleton

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
          start: "top top",                              // pin at viewport top
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
        <div
          key={i}
          className="stack-card sticky top-0 min-h-[100dvh] flex items-center justify-center"
        >
          {card}
        </div>
      ))}
    </div>
  );
}
```

Critical points: `start: "top top"`, `pin: true`, every card except the last is pinned, the scale/opacity transform is driven by the NEXT card's scroll trigger.

### 14.B Horizontal-Pan - Canonical Skeleton

```tsx
"use client";
import { useRef, useEffect } from "react";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { useReducedMotion } from "motion/react";

gsap.registerPlugin(ScrollTrigger);

export function HorizontalPan({ children }: { children: React.ReactNode }) {
  const wrap = useRef<HTMLDivElement>(null);
  const track = useRef<HTMLDivElement>(null);
  const reduce = useReducedMotion();

  useEffect(() => {
    if (reduce || !wrap.current || !track.current) return;
    const ctx = gsap.context(() => {
      const distance = track.current!.scrollWidth - window.innerWidth;
      gsap.to(track.current, {
        x: -distance,
        ease: "none",
        scrollTrigger: {
          trigger: wrap.current,
          start: "top top",
          end: () => `+=${distance}`,
          pin: true,
          scrub: 1,
          invalidateOnRefresh: true,
        },
      });
    }, wrap);
    return () => ctx.revert();
  }, [reduce]);

  return (
    <section ref={wrap} className="relative overflow-hidden">
      <div ref={track} className="flex h-[100dvh] items-center">
        {children}
      </div>
    </section>
  );
}
```

Critical points: `start: "top top"`, `pin: true`, `end: "+=${distance}"`, `scrub: 1`.

### 14.C Scroll-Reveal Stagger - Canonical Skeleton

For simple "items appear as they enter viewport" (no pinning), prefer Motion's `whileInView` over GSAP:

```tsx
"use client";
import { motion, useReducedMotion } from "motion/react";

export function RevealStagger({ items }: { items: string[] }) {
  const reduce = useReducedMotion();
  return (
    <ul className="grid gap-6">
      {items.map((item, i) => (
        <motion.li
          key={item}
          initial={reduce ? false : { opacity: 0, y: 24 }}
          whileInView={{ opacity: 1, y: 0 }}
          viewport={{ once: true, amount: 0.3 }}
          transition={{
            duration: 0.6,
            delay: i * 0.06,
            ease: [0.16, 1, 0.3, 1],
          }}
        >
          {item}
        </motion.li>
      ))}
    </ul>
  );
}
```

Use this for: feature lists, testimonial grids, logo walls, anything that just needs "enter on scroll." Save GSAP for actual pin/scrub work.

### 14.D Forbidden Animation Patterns

- **`window.addEventListener("scroll", ...)`** is banned. Use Motion's `useScroll()`, GSAP's `ScrollTrigger`, IntersectionObserver, or CSS `scroll-driven animations`.
- **Custom scroll progress calculations using `window.scrollY`** in React state. Same reason.
- **`requestAnimationFrame` loops that touch React state.** Use motion values instead.
- **Layout Transitions:** Use Motion's `layout` and `layoutId` props for visible state changes.
- **Staggered Orchestration:** Use `staggerChildren` (Motion) or CSS cascade for reveal moments.
- **NEVER mix GSAP / Three.js with Motion in the same component tree.** They fight over the same frames.

---

## 15. ANIMATION REVIEW FORMAT (Required)

When reviewing UI code for animation quality, you MUST use a markdown table with Before/After columns. Do NOT use a list with "Before:" and "After:" on separate lines.

| Before | After | Why |
|---|---|---|
| `transition: all 300ms` | `transition: transform 200ms ease-out` | Specify exact properties; avoid `all` |
| `transform: scale(0)` | `transform: scale(0.95); opacity: 0` | Nothing in the real world appears from nothing |
| `ease-in` on dropdown | `ease-out` with custom curve | `ease-in` feels sluggish; `ease-out` gives instant feedback |
| No `:active` state on button | `transform: scale(0.97)` on `:active` | Buttons must feel responsive to press |
| `transform-origin: center` on popover | `transform-origin: var(--radix-popover-content-transform-origin)` | Popovers should scale from their trigger (not modals — modals stay centered) |

**Animation Review Checklist:**

| Issue | Fix |
|---|---|
| `transition: all` | Specify exact properties: `transition: transform 200ms ease-out` |
| `scale(0)` entry animation | Start from `scale(0.95)` with `opacity: 0` |
| `ease-in` on UI element | Switch to `ease-out` or custom curve |
| `transform-origin: center` on popover | Set to trigger location or use Radix/Base UI CSS variable (modals exempt) |
| Animation on keyboard action | Remove animation entirely |
| Duration > 300ms on UI element | Reduce to 150-250ms |
| Hover animation without media query | Add `@media (hover: hover) and (pointer: fine)` |
| Keyframes on rapidly-triggered element | Use CSS transitions for interruptibility |
| Framer Motion `x`/`y` props under load | Use `transform: "translateX()"` for hardware acceleration |
| Same enter/exit transition speed | Make exit faster than enter (e.g., enter 2s, exit 200ms) |
| Elements all appear at once | Add stagger delay (30-80ms between items) |

### Debugging Animations

**Slow motion testing:** Play animations at reduced speed to spot issues invisible at full speed. Temporarily increase duration to 2-5x normal, or use browser DevTools animation inspector to slow playback.

Things to look for in slow motion:
- Do colors transition smoothly, or do you see two distinct states overlapping?
- Does the easing feel right, or does it start/stop abruptly?
- Is the transform-origin correct, or does the element scale from the wrong point?
- Are multiple animated properties (opacity, transform, color) in sync?

**Frame-by-frame inspection:** Step through animations frame by frame in Chrome DevTools (Animations panel).

**Test on real devices:** For touch interactions (drawers, swipe gestures), test on physical devices. Connect your phone via USB, visit your local dev server by IP address, and use Safari's remote devtools. The Xcode Simulator is an alternative but real hardware is better for gesture testing.

---

## 16. DIAL DEFINITIONS (Technical Reference)

### DESIGN_VARIANCE (Level 1-10)

- **1-3 (Predictable):** Symmetrical CSS Grid (12-col, equal fr-units), equal paddings, centered alignment.
- **4-7 (Offset):** `margin-top: -2rem` overlaps, varied image aspect ratios (4:3 next to 16:9), left-aligned headers over center-aligned data.
- **8-10 (Asymmetric):** Masonry layouts, CSS Grid with fractional units (`grid-template-columns: 2fr 1fr 1fr`), massive empty zones (`padding-left: 20vw`).
- **MOBILE OVERRIDE:** For levels 4-10, asymmetric layouts above `md:` MUST collapse to strict single-column (`w-full`, `px-4`, `py-8`) on viewports `< 768px`.

### MOTION_INTENSITY (Level 1-10)

- **1-3 (Static):** No automatic animations. CSS `:hover` and `:active` states only.
- **4-7 (Fluid CSS):** `transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1)`. `animation-delay` cascades for load-ins. Focus on `transform` and `opacity`.
- **8-10 (Advanced Choreography):** Complex scroll-triggered reveals, parallax, scroll-driven animation (CSS `animation-timeline` or GSAP ScrollTrigger). Use Motion hooks. **NEVER use `window.addEventListener('scroll')`** - hard ban.

### VISUAL_DENSITY (Level 1-10)

- **1-3 (Art Gallery):** Lots of white space. Huge section gaps (`py-32` to `py-48`). Expensive, clean.
- **4-7 (Daily App):** Standard web app spacing (`py-16` to `py-24`).
- **8-10 (Cockpit):** Tight paddings. No card boxes; 1px lines separate data. Mandatory: `font-mono` for all numbers.

---

## 17. DARK MODE PROTOCOL

Dual-mode by default. Never assume light-only unless the brief is print-emulating editorial.

### 17.A Token Strategy (pick one, stick to it)

- **Tailwind `dark:` variant** (default for utility-first projects): every color utility paired with its dark variant (`bg-white dark:bg-zinc-950`, `text-gray-900 dark:text-gray-100`).
- **CSS variables** (for shadcn/ui, Radix Themes, or component libraries with theming): define semantic tokens (`--surface`, `--surface-elevated`, `--text-primary`, `--accent`) and swap values under `[data-theme="dark"]` or `@media (prefers-color-scheme: dark)`.

### 17.B Enforcement

- **Contrast** - WCAG AA minimum for body text, AAA target for hero copy.
- **Hierarchy parity** - visual hierarchy that works in light must work in dark.
- **Brand fidelity** - primary brand color stays recognisable. Don't desaturate the brand into a dark mode.
- **No pure `#000000` and no pure `#ffffff`** - use off-black (zinc-950) and off-white.

### 17.C Default Mode

Respect `prefers-color-scheme` unless the brand insists. Add a manual toggle if either mode would lose key brand expression.

---

## 18. AI TELLS (Forbidden Patterns)

Avoid these signatures unless the brief explicitly asks for them.

### 18.A Visual & CSS

- **NO neon / outer glows** by default. Use inner borders or subtle tinted shadows.
- **NO pure black (`#000000`).** Off-black, zinc-950, or charcoal.
- **NO oversaturated accents.** Desaturate to blend with neutrals.
- **NO excessive gradient text** for large headers.
- **NO custom mouse cursors.** Outdated, accessibility-hostile, perf-hostile.

### 18.B Typography

- **AVOID Inter as default.** See Section 4.1.
- **NO oversized H1s** that just scream. Control hierarchy with weight + color, not raw scale.
- **Serif constraints:** Serif for editorial / luxury / publication. Not for dashboards.

### 18.C Layout & Spacing

- **Mathematically perfect** padding and margins. No floating elements with awkward gaps.
- **NO 3-column equal feature cards.** The generic "three identical cards horizontally" feature row is banned.

### 18.D Content & Data ("Jane Doe" Effect)

- **NO generic names.** "John Doe", "Sarah Chan", "Jack Su" → use creative, realistic, locale-appropriate names.
- **NO generic avatars.** No SVG "egg" or Lucide user icons.
- **NO fake-perfect numbers.** Avoid `99.99%`, `50%`, `1234567`. Use organic, messy data (`47.2%`, `+1 (312) 847-1928`).
- **NO startup-slop brand names.** "Acme", "Nexus", "SmartFlow", "Cloudly" → invent contextual, premium names.
- **NO filler verbs.** "Elevate", "Seamless", "Unleash", "Next-Gen", "Revolutionize" → concrete verbs only.

### 18.E External Resources & Components

- **NO hand-rolled SVG icons.** Use Phosphor / HugeIcons / Radix / Tabler.
- **NO div-based fake screenshots.**
- **NO broken Unsplash links.** Use `https://picsum.photos/seed/{descriptive-string}/{w}/{h}`.
- **shadcn/ui customization:** Allowed, but NEVER in default state.

### 18.F Production-Test Tells (banned outright)

**Hero & top-of-page**
- **NO version labels in the hero.** `V0.6`, `v2.0`, `BETA`, `INVITE-ONLY PREVIEW`, `EARLY ACCESS`, `ALPHA` - banned as default eyebrows.
- **NO "Brand · No. 01"-style sub-eyebrows.**

**Section numbering & micro-labels**
- **NO section-number eyebrows.** `00 / INDEX`, `001 · Capabilities`, `06 · how it works` - banned.
- **NO `01 / 4`-style pagination on images or bento tiles.**
- **NO "Index of Work, 2018 - 2026"-style range labels** as eyebrows.

**Separators & dots**
- **The middle-dot (`·`) is rationed.** Maximum 1 per line in metadata strips.
- **NO decorative colored status dots on every list/nav/badge.**

**Em-dashes & typography flourishes**
- **NO em-dash (`—`) as a design element OR anywhere else.** See Section 18.G.
- **NO `<br>`-broken-and-italicized headlines** as a default "design move."
- **NO vertical rotated text.**
- **NO crosshair / hairline grid lines as decoration.**

**Fake product previews**
- **NO div-based fake product UI in the hero.**
- **NO fake version footers** ("v0.6.2-rc.1", "last sync 4s ago · main") inside fake screenshots.

**Marketing-copy Tells**
- **NO "Quietly in use at" / "Quietly trusted by"** social-proof headers.
- **NO "From the field" / "Field notes"** style poetic labels.
- **NO weather / locale strips** ("LIS 14:23 · 18°C") unless the brief is explicitly place-focused.
- **NO micro-meta-sentences under eyebrows.**
- **NO generic step labels.** "Stage 1 / Stage 2 / Stage 3" - banned. Use verb-noun directly.

**Pills, labels and version stamps**
- **NO pills/labels/tags overlaid on images.**
- **NO photo-credit captions as decoration.**
- **NO version footers on marketing pages.** (`v1.4.2`, `Build 0048`)
- **NO "Reservation 412 of 800"-style live-stock counters** as decoration.

**Decoration text strips**
- **NO decoration text strip at hero bottom.** (`BRAND. MOTION. SPATIAL.`)
- **NO floating top-right sub-text in section headings.**

**Lists, dividers and scoring**
- **NO `border-t` + `border-b` on every row** of a long list / spec table.
- **NO scoring/progress bars with filled background tracks** as comparison visuals.

**Locale, time, scroll cues**
- **Locale / city-name / time / weather strips are banned for 99% of briefs.**
- **Scroll cues are banned.** `Scroll`, `↓ scroll`, `Scroll to explore` - if the user hasn't scrolled yet, they're looking at the hero. They know what scroll is.
- **ZERO decorative status dots by default.**

### 18.G EM-DASH BAN (the single most-violated Tell)

**Em-dash (`—`) is COMPLETELY banned.** It is the LLM's signature stylistic crutch and it is the #1 visual Tell in production tests. There is no "limited use" allowance, no "natural language frequency" allowance, no "in body copy is fine" allowance. None.

- **Banned in headlines.** Use a period or a comma.
- **Banned in eyebrows / labels / pills / button text / image captions / nav items.** Replace with line breaks, columns, or hairlines.
- **Banned in body copy.** Restructure the sentence: two sentences with a period, OR a comma, OR parentheses, OR a colon.
- **Banned in quote attribution.** Use a normal hyphen with spaces (` - `) or a line break + smaller-weight name.
- **Banned in en-dash form too (`-`) when used as a separator.** Date ranges (`2018-2026`) use a hyphen. Number ranges use a hyphen.

The ONLY permitted dash characters on the page are:
- Regular hyphen `-` (for compound words, ranges, line dividers in markup)
- Minus sign in math (`-5°C`)

If your output contains a single `—` or `–` anywhere visible to the user, the output fails the Pre-Flight Check and must be rewritten. This rule is non-negotiable. The agent has historically ignored em-dash limits when phrased as "use sparingly." The phrasing here is binary: zero em-dashes.

---

## 19. REFERENCE VOCABULARY (Pattern Names)

This is a vocabulary, not a library. The agent should KNOW these pattern names to communicate about them, design with them in mind, and reach for them when the design read calls for them.

### Hero Paradigms

- **Asymmetric Split Hero** - Text on one side, asset on the other, generous white space.
- **Editorial Manifesto Hero** - Large type, no asset, almost-poster.
- **Video / Media Mask Hero** - Type cut out as mask over video background.
- **Kinetic-Type Hero** - Animated typography as the primary visual.
- **Curtain-Reveal Hero** - Hero parts on scroll like a curtain.
- **Scroll-Pinned Hero** - Hero stays pinned while content scrolls behind.

### Navigation & Menus

- **Mac OS Dock Magnification** - Edge nav, icons scale fluidly on hover.
- **Magnetic Button** - Pulls toward cursor.
- **Gooey Menu** - Sub-items detach like viscous liquid.
- **Dynamic Island** - Morphing pill for status / alerts.
- **Contextual Radial Menu** - Circular menu expanding at click point.
- **Floating Speed Dial** - FAB springing into curved secondary actions.
- **Mega Menu Reveal** - Full-screen dropdown, stagger-fade content.

### Layout & Grids

- **Bento Grid** - Asymmetric tile grouping (Apple Control Center).
- **Masonry Layout** - Staggered grid, no fixed row height.
- **Chroma Grid** - Borders / tiles with subtle animating gradients.
- **Split-Screen Scroll** - Two halves sliding in opposite directions.
- **Sticky-Stack Sections** - Sections that pin and stack on scroll.

### Cards & Containers

- **Parallax Tilt Card** - 3D tilt tracking mouse coordinates.
- **Spotlight Border Card** - Borders illuminate under cursor.
- **Glassmorphism Panel** - Frosted glass with inner refraction.
- **Holographic Foil Card** - Iridescent rainbow shift on hover.
- **Tinder Swipe Stack** - Physical card stack, swipe-away.
- **Morphing Modal** - Button expands into its own dialog.

### Scroll Animations

- **Sticky Scroll Stack** - Cards stick and physically stack.
- **Horizontal Scroll Hijack** - Vertical scroll → horizontal pan.
- **Locomotive / Sequence Scroll** - Video / 3D sequence tied to scrollbar.
- **Zoom Parallax** - Central background image zooming on scroll.
- **Scroll Progress Path** - SVG line drawing along scroll.
- **Liquid Swipe Transition** - Page transition like viscous liquid.

### Galleries & Media

- **Dome Gallery** - 3D panoramic gallery.
- **Coverflow Carousel** - 3D carousel with angled edges.
- **Drag-to-Pan Grid** - Boundless draggable canvas.
- **Accordion Image Slider** - Narrow strips expanding on hover.
- **Hover Image Trail** - Mouse leaves popping image trail.
- **Glitch Effect Image** - RGB-channel shift on hover.

### Typography & Text

- **Kinetic Marquee** - Endless text bands reversing on scroll.
- **Text Mask Reveal** - Massive type as transparent window to video.
- **Text Scramble Effect** - Matrix-style decoding on load / hover.
- **Circular Text Path** - Text curving along spinning circle.
- **Gradient Stroke Animation** - Outlined text with running gradient.
- **Kinetic Typography Grid** - Letters dodging the cursor.

### Micro-Interactions & Effects

- **Particle Explosion Button** - CTA shatters into particles on success.
- **Liquid Pull-to-Refresh** - Reload indicator like detaching droplets.
- **Skeleton Shimmer** - Shifting light reflection across placeholders.
- **Directional Hover-Aware Button** - Fill enters from cursor's exact side.
- **Ripple Click Effect** - Wave from click coordinates.
- **Animated SVG Line Drawing** - Vectors drawing themselves in real time.
- **Mesh Gradient Background** - Organic lava-lamp blobs.
- **Lens Blur Depth** - Background UI blurred to focus foreground action.
- **Hold-to-Delete Button** - clip-path overlay fills on hold, snaps back on release.
- **Comparison Slider** - Draggable clip-path reveal between two images.
- **Tab Color Transition** - Duplicate + clip-path for seamless tab color swap.
- **Origin-Aware Popover** - Scales from trigger position, not center.

### Animation Library Choice

- **Motion (`motion/react`)** - default for UI / Bento / state-change motion.
- **GSAP + ScrollTrigger** - for full-page scrolltelling and scroll hijacks. Isolate in dedicated leaf components with `useEffect` cleanup.
- **Three.js / WebGL** - for canvas backgrounds and 3D scenes. Same isolation rule.
- **WAAPI** - Web Animations API for programmatic CSS animations with JS control and GPU performance.
- **NEVER mix GSAP / Three.js with Motion in the same component tree.** They fight over the same frames.

---

## 20. REDESIGN PROTOCOL

This skill handles **greenfield builds AND redesigns**. Misclassifying the mode is the single biggest source of bad redesign output.

### 20.A Detect the Mode (first action)

- **Greenfield** - no existing site, or full overhaul approved. Dial baseline from Section 1.
- **Redesign - Preserve** - modernise without breaking the brand. Audit first, extract brand tokens, evolve gradually.
- **Redesign - Overhaul** - new visual language on top of existing content. Treat as greenfield for visuals; preserve content and IA.

If ambiguous, ask **once**: *"Should this redesign preserve the existing brand, or are we starting visually from scratch?"*

### 20.B Audit Before Touching

Document the current state before proposing changes:

- **Brand tokens** - primary / accent colors, type stack, logo treatment, radii.
- **Information architecture** - page tree, primary nav, key conversion paths.
- **Content blocks** - what exists, what's doing work, what's filler.
- **Patterns to preserve** - signature interactions, recognisable hero, copy voice.
- **Patterns to retire** - AI-slop tells, broken layouts, dead links, generic stock imagery, perf traps.
- **Dial reading of the existing site** - infer current `DESIGN_VARIANCE` / `MOTION_INTENSITY` / `VISUAL_DENSITY`. That's your starting point, not the baseline.
- **SEO baseline** - current ranking pages, meta titles, structured data, OG cards. **SEO migration is the #1 redesign risk.**

### 20.C Preservation Rules

- **Do not change information architecture** unless asked.
- **Extract brand colors before applying Section 4.2.**
- **Preserve copy voice** unless asked for a rewrite. Visual modernisation ≠ content rewrite.
- **Honor existing accessibility wins.**
- **Respect existing analytics events.** Do not rename buttons, form fields, section IDs that downstream tracking depends on.

### 20.D Modernisation Levers (priority order)

1. **Typography refresh** - biggest visual lift per unit of risk.
2. **Spacing & rhythm** - increase section padding, fix vertical rhythm.
3. **Color recalibration** - desaturate, unify neutrals, keep brand accent.
4. **Motion layer** - add `MOTION_INTENSITY`-appropriate micro-interactions to existing components.
5. **Hero & key-section recomposition** - restructure top-of-funnel using Section 19 vocabulary.
6. **Full block replacement** - only when the existing block is unsalvageable.

### 20.E Decision Tree

- IA, content, and SEO sound → **targeted evolution** (Levers 1-4). ~70% of value at ~40% of risk.
- Visual debt is structural → **full redesign** with strict content preservation.
- Brand itself is changing → **greenfield**.

### 20.F What Never Changes Silently

Never modify without explicit user approval:

- URL structure / route slugs.
- Primary nav labels.
- Form field names or order (breaks analytics + autofill).
- Brand logo or wordmark.
- Existing legal / consent / cookie copy.

---

## 21. OUT OF SCOPE

This skill is NOT for:

- Dashboards / dense product UI / admin panels (use Fluent, Carbon, Atlassian, or Polaris from Section 2.A).
- Data tables (use TanStack Table or AG Grid).
- Multi-step forms / wizards.
- Code editors (use Monaco / CodeMirror with their official skinning).
- Native mobile (use Apple HIG / Material directly).
- Realtime collab UIs (presence, cursors, OT-aware).

If the brief is one of the above, **say so explicitly**, point to the right tool, and only apply this skill's marketing-page / about-page / landing-page / component parts to the surfaces where they apply.

---

## 22. FINAL PRE-FLIGHT CHECK

Run this matrix before outputting code. This is the last filter.

**THIS IS NOT OPTIONAL. Run every box. If any box fails, the output is not done.**

### Page & Layout
- [ ] **Brief inference** declared (Section 0.B one-liner)?
- [ ] **Dial values** explicit and reasoned from the brief, not silently using baseline?
- [ ] **Design system** chosen from Section 2 if applicable, or aesthetic labeled honestly?
- [ ] **Redesign mode** detected and audit performed (if applicable, Section 20)?
- [ ] **Page Theme Lock**: ONE theme (light, dark, or auto) for the whole page. No section flips to inverted mode mid-page (Section 4.11)?
- [ ] **Color Consistency Lock**: one accent color used identically across all sections (Section 4.2)?
- [ ] **Shape Consistency Lock**: one corner-radius system applied consistently (Section 4.4)?
- [ ] **Navigation on ONE line** at desktop, height ≤ 80px?
- [ ] **Section-Layout-Repetition** check: no two sections share the same layout family?
- [ ] **Bento has rhythm AND exact cell count** (N items → N cells, no empty cells)?
- [ ] **Bento Background Diversity**: at least 2-3 bento cells have real visual variation?
- [ ] **EYEBROW COUNT (mechanical)**: count ≤ ceil(sectionCount / 3)?
- [ ] **Split-Header Ban**: no "left big headline + right small explainer paragraph" as a section header?
- [ ] **Zigzag Alternation Cap**: no 3+ consecutive sections with the same image+text-split layout?

### Hero
- [ ] **Hero fits the viewport**: headline ≤ 2 lines, subtext ≤ 20 words AND ≤ 4 lines, CTA visible without scroll?
- [ ] **Hero top padding**: max `pt-24` at desktop?
- [ ] **Hero stack discipline**: max 4 text elements? No tiny tagline below CTAs, no trust micro-strip?
- [ ] **"Used by / Trusted by" logo wall** lives UNDER the hero, not inside it?

### Typography & Copy
- [ ] **ZERO em-dashes (`—`) anywhere on the page.** Zero. (Section 18.G - non-negotiable.)
- [ ] **Serif discipline**: if a serif is used, it is NOT Fraunces or Instrument_Serif?
- [ ] **Italic descender clearance**: every italic word with `y g j p q` has `leading-[1.1]` min + `pb-1` reserve?
- [ ] **Copy Self-Audit**: every visible string re-read, no grammatically-broken or AI-hallucinated phrases?
- [ ] **Quotes ≤ 3 lines** of body, attribution clean (no em-dash)?

### Color & Palette
- [ ] **Premium-consumer palette check**: if brief is premium-consumer, NOT the AI-default beige+brass family?

### Buttons, Forms & A11y
- [ ] **Button Contrast Check**: every CTA text is readable against its background (WCAG AA 4.5:1)?
- [ ] **CTA Button Wrap**: no CTA label wraps to 2+ lines at desktop?
- [ ] **No Duplicate CTA Intent**: no two CTAs with the same intent on the page?
- [ ] **Form Contrast Check**: form inputs, placeholders, focus rings, labels all pass WCAG AA?

### Images & Media
- [ ] **Real images used** (gen-tool first, then Picsum-seed, then explicit placeholder slots)?
- [ ] **No div-based fake screenshots, no hand-rolled decorative SVGs, no pure-text minimalism?**
- [ ] **Logo wall = logo only**: no industry / category labels printed below logos?
- [ ] **"Used by / Trusted by" logo wall** uses REAL SVG logos (Simple Icons / devicon)?
- [ ] **No pills/labels overlaid on images**?
- [ ] **No photo-credit captions as decoration**?

### Content & Lists
- [ ] **Long lists use the right UI component** (not default `<ul>` with `divide-y` for > 5 items)?
- [ ] **No `border-t` + `border-b` on every row** of long lists / spec tables?
- [ ] **Content density** sane: no 20-row data tables, no fake-precise specs?

### AI Tells (banned patterns)
- [ ] **No version footers** (`v1.4.2`, `Build 0048`) on marketing pages?
- [ ] **No micro-meta-sentences** under eyebrows?
- [ ] **No decoration text strip at hero bottom** (`BRAND. MOTION. SPATIAL.`)?
- [ ] **No floating top-right sub-text** in section headings?
- [ ] **No scoring/progress bars with filled background tracks** as comparison visuals?
- [ ] **No locale / city-name / time / weather strips** unless brief is genuinely place-focused?
- [ ] **No scroll cues** (`Scroll`, `↓ scroll`, `Scroll to explore`)?
- [ ] **No version labels in hero** (V0.6, BETA, INVITE-ONLY) unless the brief is a launch?
- [ ] **No section-numbering eyebrows** (`00 / INDEX`, `001 · Capabilities`)?
- [ ] **No decorative dots** (zero by default, only for real semantic state)?
- [ ] **No AI Tells** from Section 18 (Inter as default, AI-purple, three-equal cards, Jane Doe, Acme)?

### Animation & Motion
- [ ] **Motion motivated**: every animation can be justified in one sentence?
- [ ] **Animation Decision Framework** applied (Section 5): should it animate? purpose? easing? duration?
- [ ] **Never animate from scale(0)**: using scale(0.95) + opacity as entry?
- [ ] **Popovers are origin-aware** (not centered)?
- [ ] **No ease-in** on any UI element?
- [ ] **UI animation durations ≤ 300ms** (except modals/drawers)?
- [ ] **Keyboard actions have NO animation**?
- [ ] **Hover animations gated behind** `@media (hover: hover) and (pointer: fine)`?
- [ ] **Rapidly-triggered elements** use CSS transitions, not keyframes?
- [ ] **Framer Motion shorthand** (`x`, `y`) replaced with `transform: "translateX()"` for GPU-critical animations?
- [ ] **Motion claimed = motion shown**: if `MOTION_INTENSITY > 4`, page actually animates?
- [ ] **GSAP sticky-stack / horizontal-pan** implemented per Section 14.A / 14.B canonical skeleton?
- [ ] **No `window.addEventListener('scroll')`** - using Motion `useScroll()` / ScrollTrigger / IntersectionObserver?
- [ ] **Marquee max-one-per-page**: no two horizontal marquees on the same page?
- [ ] **Reduced motion** wrapped for everything `MOTION_INTENSITY > 3`?
- [ ] **`useEffect` animations** have strict cleanup functions?

### Responsive & Performance
- [ ] **Viewport stability**: `min-h-[100dvh]`, never `h-screen`?
- [ ] **Mobile collapse** explicit (`w-full`, `px-4`, `max-w-7xl mx-auto`) for high-variance layouts?
- [ ] **Dark mode** tokens defined and tested in both modes?
- [ ] **Core Web Vitals** plausibly hit (LCP < 2.5s, INP < 200ms, CLS < 0.1)?

### Components & Architecture
- [ ] **Empty / loading / error** states provided?
- [ ] **Cards omitted** in favor of spacing where possible?
- [ ] **Icons** from an allowed library only (Phosphor / HugeIcons / Radix / Tabler)?
- [ ] **Motion** isolated in client-leaf components with `'use client'` at the top?
- [ ] **One design system** per project (no Material + shadcn mixed)?
- [ ] **CSS variables** NOT used to track per-frame animation values on containers with many children?

If a single checkbox cannot be honestly ticked, the page is not done. Fix it before delivering.

---

## APPENDIX A - Install Commands per Design System

```bash
# Material Web (Material 3)
npm install @material/web

# Fluent UI React (v9)
npm install @fluentui/react-components

# Fluent UI Web Components (framework-free)
npm install @fluentui/web-components @fluentui/tokens

# IBM Carbon
npm install @carbon/react @carbon/styles

# Radix Themes
npm install @radix-ui/themes

# shadcn/ui (open code, owned components)
npx shadcn@latest init
npx shadcn@latest add button card badge separator input

# Primer CSS (GitHub product/devtool UI)
npm install --save @primer/css

# Primer Brand (GitHub marketing UI)
npm install @primer/react-brand

# GOV.UK Frontend
npm install govuk-frontend

# USWDS (US Web Design System)
npm install uswds

# Atlassian Design System (Atlaskit)
yarn add @atlaskit/css-reset @atlaskit/tokens @atlaskit/button @atlaskit/badge @atlaskit/section-message @atlaskit/card

# Bootstrap 5.3
npm install bootstrap

# Shopify Polaris Web Components (Shopify apps only)
# Add this to your app HTML head:
#   <meta name="shopify-api-key" content="%SHOPIFY_API_KEY%" />
#   <script src="https://cdn.shopify.com/shopifycloud/polaris.js"></script>

# Motion (formerly Framer Motion)
npm install motion

# GSAP (for scroll animations)
npm install gsap

# Icon libraries
npm install @phosphor-icons/react
npm install hugeicons-react
npm install @tabler/icons-react
npm install @radix-ui/react-icons

# Fonts (self-hosted)
npm install @fontsource/geist
npm install @fontsource/geist-mono
```

---

## APPENDIX B - Canonical Sources

### Design Systems

**Material Web:** https://github.com/material-components/material-web | https://material-web.dev/theming/material-theming/ | https://m3.material.io/develop/web

**Fluent UI:** https://fluent2.microsoft.design/get-started/develop | https://fluent2.microsoft.design/components/web/react/ | https://github.com/microsoft/fluentui

**Carbon:** https://carbondesignsystem.com/ | https://github.com/carbon-design-system/carbon

**Shopify Polaris:** https://shopify.dev/docs/api/app-home/web-components | https://polaris-react.shopify.com/components

**Atlassian:** https://atlassian.design/get-started/develop | https://atlassian.design/tokens/design-tokens

**Primer:** https://primer.style/ | https://github.com/primer/css | https://github.com/primer/brand

**GOV.UK:** https://design-system.service.gov.uk/components/button/ | https://github.com/alphagov/govuk-frontend

**USWDS:** https://designsystem.digital.gov/documentation/developers/ | https://github.com/uswds/uswds

**Bootstrap:** https://getbootstrap.com/docs/5.3/layout/grid/

**Tailwind:** https://tailwindcss.com/docs/dark-mode | https://tailwindcss.com/blog/tailwindcss-v4

**Radix:** https://www.radix-ui.com/themes/docs/components/theme | https://github.com/radix-ui/themes

**shadcn/ui:** https://ui.shadcn.com/docs | https://github.com/shadcn-ui/ui

### Animation Resources

**Motion (Framer Motion):** https://motion.dev/docs/react-quick-start

**GSAP:** https://gsap.com/docs/v3/ | https://gsap.com/docs/v3/Plugins/ScrollTrigger/

**Easing curves:** https://easing.dev/ | https://easings.co/

**Emil Kowalski:** https://emilkowal.ski/ | https://animations.dev/

### Native CSS / W3C standards

https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/backdrop-filter
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@media/prefers-color-scheme
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@media/prefers-reduced-motion
https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout
https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Scroll-driven_animations
https://drafts.csswg.org/scroll-animations-1/

### Apple Liquid Glass (Apple platforms only)

https://developer.apple.com/design/human-interface-guidelines/materials
https://developer.apple.com/documentation/TechnologyOverviews/liquid-glass
https://developer.apple.com/documentation/TechnologyOverviews/adopting-liquid-glass
https://developer.apple.com/documentation/SwiftUI/Material

---

## APPENDIX C - Apple Liquid Glass: Honest Web Approximation

Do **not** treat random CSS snippets as official Apple Liquid Glass.

Apple documents Liquid Glass for **Apple platforms only**. There is no `liquid-glass.css` from Apple for normal websites.

A web approximation can use `backdrop-filter`, transparent backgrounds, layered borders, highlight overlays, gradients, motion, and strong contrast fallbacks. But that is **web glassmorphism / frosted-glass approximation**, not official Apple Liquid Glass. Label it as such in comments.

```css
.liquid-glass-web-approx {
  position: relative;
  isolation: isolate;
  overflow: hidden;
  border-radius: 999px;
  border: 1px solid rgb(255 255 255 / .32);
  background:
    linear-gradient(135deg, rgb(255 255 255 / .30), rgb(255 255 255 / .08)),
    rgb(255 255 255 / .12);
  backdrop-filter: blur(24px) saturate(180%) contrast(1.05);
  -webkit-backdrop-filter: blur(24px) saturate(180%) contrast(1.05);
  box-shadow:
    inset 0 1px 0 rgb(255 255 255 / .48),
    inset 0 -1px 0 rgb(255 255 255 / .12),
    0 18px 60px rgb(0 0 0 / .18);
}

.liquid-glass-web-approx::before {
  content: "";
  position: absolute;
  inset: 0;
  z-index: -1;
  border-radius: inherit;
  background:
    radial-gradient(circle at 20% 0%, rgb(255 255 255 / .55), transparent 34%),
    linear-gradient(90deg, rgb(255 255 255 / .18), transparent 42%, rgb(255 255 255 / .14));
  pointer-events: none;
}

.liquid-glass-web-approx::after {
  content: "";
  position: absolute;
  inset: 1px;
  border-radius: inherit;
  border: 1px solid rgb(255 255 255 / .14);
  pointer-events: none;
}

@media (prefers-color-scheme: dark) {
  .liquid-glass-web-approx {
    border-color: rgb(255 255 255 / .18);
    background:
      linear-gradient(135deg, rgb(255 255 255 / .16), rgb(255 255 255 / .04)),
      rgb(15 23 42 / .42);
    box-shadow:
      inset 0 1px 0 rgb(255 255 255 / .22),
      0 18px 60px rgb(0 0 0 / .42);
  }
}

@media (prefers-reduced-transparency: reduce) {
  .liquid-glass-web-approx {
    background: rgb(255 255 255 / .96);
    backdrop-filter: none;
    -webkit-backdrop-filter: none;
  }
}
```

**Important:** `prefers-reduced-transparency` has uneven browser support; test it. Always provide enough contrast even without blur.

---

## APPENDIX D - Custom Easing Reference

```css
:root {
  /* Strong ease-out - for entering UI elements */
  --ease-out-strong: cubic-bezier(0.23, 1, 0.32, 1);

  /* Strong ease-in-out - for on-screen morphing */
  --ease-in-out-strong: cubic-bezier(0.77, 0, 0.175, 1);

  /* iOS-like drawer - for drawers and sheets */
  --ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);

  /* Snappy enter - for quick UI feedback */
  --ease-snappy: cubic-bezier(0.16, 1, 0.3, 1);

  /* Spring feel - for hover and magnetic interactions */
  --ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

**Framer Motion / Motion equivalents:**

```js
// Easing arrays for Motion
const easeOutStrong = [0.23, 1, 0.32, 1];
const easeInOutStrong = [0.77, 0, 0.175, 1];
const easeDrawer = [0.32, 0.72, 0, 1];
const easeSnappy = [0.16, 1, 0.3, 1];

// Spring configs
const springSubtle = { type: "spring", duration: 0.4, bounce: 0.1 };
const springPlayful = { type: "spring", duration: 0.5, bounce: 0.25 };
const springPhysics = { type: "spring", mass: 1, stiffness: 100, damping: 10 };
```

---

*End of skill. This is a merged synthesis of leonxlnx/taste-skill (anti-slop layout, typography, color, design systems, architecture) and emilkowalski/skill (animation decision framework, spring physics, clip-path, gesture interactions, component craft, performance). Apply both bodies of knowledge together.*
