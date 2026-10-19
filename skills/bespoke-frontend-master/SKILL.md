---
name: bespoke-frontend-master
description: "Project-first design constitution, 3-era AI slop eradication, 67-rule anti-pattern catalog, semantic design tokens, mechanical UI baseline, accessibility contracts, and 5-state UI modeling."
---

# 🏛️ BESPOKE FRONTEND MASTER — ANTI-SLOP CONSTITUTION & ENGINE

Eliminates the statistical mediocrity of AI-generated user interfaces ("AI Slop"). Enforces a strict, project-first design constitution, a 67-rule anti-pattern catalog across all three eras of AI slop, semantic design tokens, mechanical CSS execution, WCAG 2.2 AA accessibility, and resilient 5-state UI modeling.

---

# 0. PROJECT-FIRST DESIGN CONSTITUTION

This skill must never impose its own visual preferences or arbitrary pre-packaged design templates onto any project.

Labels such as "Modern UI", "SaaS UI", "Developer UI", or "Clean UI" can never justify visual decisions on their own.

Before generating any code or UI, the existing repository must be thoroughly inspected.

### Order of Precedence (Sovereignty Hierarchy & Escape Hatches):
1. **Explicit User Direction (Inversion of Control):** If the user deliberately requests a specific aesthetic (e.g., "Build a retro 80s neon synthwave theme", "I want a technical CAD grid background"), the explicit user instruction **overrides** the anti-slop defaults. Never block conscious creative choices.
2. **Existing Product Requirements & Brand Truth (`PRODUCT.md`):** Real corporate brand colors (e.g., Discord/Twitch purple, Spotify green, Linear dark aesthetic) are authentic brand identities, not AI slop.
3. **Domain Whitelists (Functional Architecture):**
   - **Breadcrumbs & Taxonomies:** Hierarchical paths (`DOCS / AUTH / API-KEYS` or `MEN / SHOES / RUNNING`) are essential navigation, NOT decorative kickers.
   - **Kanban & Issue Categorization:** Left-border status coding on task cards (Bug = Red, Feature = Green, Task = Blue) is industry-standard data encoding, NOT decorative side-tab slop.
   - **Canvas & Node Graphs:** Grid-line backgrounds on interactive canvases (React Flow, Figma/CAD tools, diagram editors) are functional measurement grids, NOT decorative background slop.
   - **B2B & High-Density Operational Screens:** Compact padding (4–8px), dense multi-row data tables, and grouped operational monitors are functional requirements for professionals, NOT "cramped layout" violations.
   - **Performance & Offline Typography:** When zero-latency, offline availability, or system-native neutrality is required, Inter, Geist, or SF Pro are pragmatic engineering choices, NOT slop.
4. **Existing Design System & Tokens (`DESIGN.md`):** Component tokens and established conventions.
5. **Anti-Slop 67-Rule Defense Baseline:** Protects against thoughtless, uncalibrated AI reflexes when no explicit brand or user constraint exists.

**Architecture must always precede decoration. Decoration must never obscure content.**

### Existing System First:
Inspect and identify the existing system in the project before generating any new patterns:
- Colors & Theme tokens
- Typography & Font pairings
- Spacing & Grid scale
- Border radius tiers
- Shadows & Elevation
- Containers & Max-widths
- Iconography
- Component primitives (Radix, Base UI, React Aria, etc.)
- Form & Table patterns

- **If the existing system is consistent:** Preserve it with zero drift.
- **If the existing system is fragmented:** Standardize it using semantic tokens first.
- **Do not rebrand or restyle the project** simply because of personal aesthetic bias.

---

# 1. THE 3 ERAS OF AI SLOP — DETECTION & IMMUNITY MATRIX

AI coding assistants default to predictable, clichéd aesthetics because training data centers on average, over-represented patterns. Every generated surface must be immune to all three historical eras of AI slop:

```
┌────────────────────────────────────────────────────────────────────────┐
│                        AI SLOP ERADICATION MATRIX                      │
├───────────────────┬──────────────────────────┬─────────────────────────┤
│ 2022-2023 DÖNEMİ  │     2024-2025 DÖNEMİ     │    2025-2026 DÖNEMİ     │
│ (Cyber / Neon)    │    (Beige Editorial)     │   (GPT Neobrutalism)    │
├───────────────────┼──────────────────────────┼─────────────────────────┤
│ • Purple/Cyan neon│ • Washed-out warm beige  │ • 2-3px pitch-black     │
│   gradients       │   backgrounds (#f5efe2)  │   borders (border-black)│
│ • Süs niyetine    │ • Italic serifs inserted │ • Zero-blur hard offset │
│   glassmorphism   │   inside sans headlines  │   shadows (4px 4px 0 #0)│
│   (backdrop-blur) │ • Uppercase kicker tags  │ • Arbitrary pastel      │
│ • Floating glowing│   above every heading    │   sticker tags & badges │
│   radial orbs     │ • Decorative side-tabs on│ • "Cardocalypse": 4     │
│ • Forced dark mode│   cards (border-l-4)     │   layers of cards in    │
│   with glowing    │ • "Status-chip soup":    │   cards, zero breath    │
│   borders/buttons │   colored pill on all    │ • 44px blob-like extreme│
│                   │ • Redundant, patronizing │   border-radii on cards │
│                   │   marketing copywriting  │ • Crude hand-coded SVGs │
└───────────────────┴──────────────────────────┴─────────────────────────┘
```

---

# 2. THE 67-RULE ANTI-PATTERN CATALOG (IMPECCABLE STANDARD)

Every line of code and rendered surface must pass these 67 deterministic checks:

### A. Visual Details (8 Rules)
1. `rule-codex-grid-background`: **BANNED.** Decorative grid-line backgrounds (`linear-gradient(...)` squares) are prohibited unless building an actual CAD canvas, graph editor, or map.
2. `rule-border-accent-on-rounded`: **BANNED.** Thick colored borders (2px-3px accent) on rounded cards (`rounded-2xl`) compete with content. Use subtle borders (`border-border/60`) or surface tinting.
3. `rule-glassmorphism`: **BANNED.** Decorative `backdrop-blur` and semi-transparent frosted cards without a functional layering/z-index need are forbidden.
4. `rule-side-tab`: **BANNED.** Decorative vertical stripe borders on one side of a card (`border-l-4 border-l-primary`) are strictly reserved for genuine Alert/Warning states. Never use on ordinary cards.
5. `rule-gpt-thin-border-wide-shadow`: **BANNED.** 1px hairline border + 24px-32px wide soft drop shadow used simultaneously is prohibited. Choose **either** a clean border **or** a subtle shadow.
6. `rule-repeating-stripes-gradient`: **BANNED.** 45-degree repeating gradient stripes used to fill empty space are forbidden. Use intentional whitespace.
7. `rule-over-round`: **BANNED.** Extreme border-radii (32px–44px) that warp cards into shapeless blobs are prohibited. Follow established radius tiers.
8. `rule-sketchy-svg`: **BANNED.** Crude, hand-coded wavy vector mascots or placeholder doodles are prohibited. Use high-fidelity assets or clean typography.

### B. Typography (11 Rules)
9. `rule-kicker-above-heading`: **STRICTLY PROHIBITED.** Uppercase, tracked-out label tags placed above headings (`FEATURES`, `OVERVIEW`, `WHY US`) are banned. Headings must stand strong on their own.
10. `rule-undersized-ui-text`: **BANNED.** Interactive controls, buttons, and navigation text smaller than 12px (e.g., `text-[9px]`, `text-[10px]`) are prohibited.
11. `rule-flat-type-hierarchy`: **BANNED.** Headings, subheadings, and body text rendered at near-identical sizes and weights (e.g., H2 at 17px, body at 15px) are prohibited. Establish clear optical scale.
12. `rule-icon-tile-stack`: **BANNED.** A rounded squircle with a colorful icon stacked directly above every feature heading is prohibited. Integrate icons inline with headings or let copy lead.
13. `rule-italic-serif-display`: **BANNED.** Randomly inserting an italic serif word inside a modern sans-serif headline (`Build the <em>future</em> today`) is prohibited.
14. `rule-hero-eyebrow-chip`: **BANNED.** Floating pill badges above the main hero headline (`✨ Introducing v2.0 →`) are prohibited. State value directly in the headline.
15. `rule-oversized-h1`: **BANNED.** Runaway 72px–96px headlines that swallow the entire viewport and push value propositions below the fold are prohibited.
16. `rule-extreme-negative-tracking`: **BANNED.** Crushed letter-spacing (`tracking-[-0.08em]` or tighter) that collides character glyphs is forbidden.
17. `rule-overused-font`: **BANNED.** Defaulting to Inter or Geist without evaluating brand identity is discouraged. Choose typography intentional for the domain.
18. `rule-all-caps-body`: **BANNED.** Uppercase styling on multi-line body paragraphs is prohibited. Use sentence case.
19. `rule-single-font`: **BANNED.** Monolithic single-weight typography without optical rhythm or contrast is prohibited.

### C. Color & Contrast (7 Rules)
20. `rule-radial-halo`: **BANNED.** Ambient glowing radial gradient orbs behind dark surfaces are prohibited.
21. `rule-radial-spotlight-glow`: **BANNED.** Soft spotlights placed behind text sections to simulate depth are prohibited.
22. `rule-ai-color-palette`: **BANNED.** Default purple-to-blue gradients, neon violet, and electric cyan are strictly forbidden.
23. `rule-dark-glow`: **BANNED.** Neon glowing borders and buttons in dark mode (`shadow-[0_0_20px_theme(colors.cyan.500)]`) are prohibited.
24. `rule-gradient-text`: **BANNED.** Multi-color gradients applied to text (`bg-clip-text text-transparent`) are prohibited. Use high-contrast solid colors.
25. `rule-gray-on-color`: **BANNED.** Muted neutral gray text rendered over colored saturated backgrounds is prohibited (fails contrast).
26. `rule-cream-palette`: **BANNED.** Defaulting to warm washed-out beige/cream (`#f5efe2`) as a lazy substitute for a real color system is prohibited.

### D. Layout & Space (12 Rules)
27. `rule-nested-cards` (**CARDOCALYPSE BAN**): **STRICTLY PROHIBITED.** Wrapping every element in a card, and nesting cards inside cards (3–4 layers of borders and shadows) is forbidden. Use whitespace, dividers, and typography to structure hierarchy.
28. `rule-identical-card-grids`: **BANNED.** Copy-paste 3x3 identical card grids (icon + heading + 2-line text) are prohibited. Use varied, content-informed layouts (Bento, master-detail, asymmetric rhythm).
29. `rule-monotonous-spacing`: **BANNED.** Equal gaps everywhere (e.g., `gap-4` between everything regardless of relationship). Related items must be close (4–8px); distinct groups must be separated (24–32px).
30. `rule-numbered-section-labels`: **BANNED.** Placing `01`, `02`, `03` numbers beside headings when there is no sequential workflow is prohibited.
31. `rule-hero-metric-layout`: **BANNED.** Generic 3-card metric bars (`10M+ Users`, `99.9% Uptime`, `200ms Latency`) slapped under heros are prohibited.
32. `rule-line-length`: **BANNED.** Running body text lines exceeding 75–80 characters across wide screens are prohibited. Constrain via `max-w-prose` (65–75 chars).
33. `rule-heading-rhythm`: **BANNED.** Headings positioned closer to the preceding section than their own content are prohibited. Space above a heading must always exceed space below.
34. `rule-cramped-padding`: **BANNED.** Buttons or cards with cramped, suffocated padding (e.g., `py-0.5 px-2`).
35. `rule-body-text-viewport-edge`: **BANNED.** Text running flush against mobile viewport edges without gutter padding.
36. `rule-text-overflow`: **BANNED.** Single-line text overflowing containers or causing horizontal window scrolling.
37. `rule-clipped-overflow-container`: **BANNED.** Dropdowns, tooltips, or popovers getting clipped by parent containers with `overflow-hidden`.
38. `rule-edge-flush-cards`: **BANNED.** Cards touching horizontal carousel scroll edges without boundary padding.

### E. Motion (6 Rules)
39. `rule-pulsing-dot`: **BANNED.** Status dots pulsing continuously on static, unchanged states are prohibited. Motion is reserved for active live changes.
40. `rule-blinking-cursor`: **BANNED.** Blinking terminal cursors in static marketing copy are prohibited.
41. `rule-marquee`: **BANNED.** Auto-scrolling logo marquees that force users to wait or read at the machine's pace are prohibited unless pause controls exist.
42. `rule-bounce-easing`: **BANNED.** Bouncy, elastic, overshoot springs on dialogs, modals, and buttons are prohibited. Use crisp ease-out transitions.
43. `rule-layout-transition`: **BANNED.** Animating layout-triggering properties (`width`, `height`, `margin`, `padding`). Animate exclusively via `transform` and `opacity`.
44. `rule-image-hover-transform`: **BANNED.** Defaulting to 105% zoom or rotation on every image hover is prohibited.

### F. UX Writing & Copy (5 Rules)
45. `rule-marketing-buzzword`: **STRICTLY PROHIBITED.** Banned buzzwords: `Supercharge`, `Next-gen`, `Cutting-edge`, `State-of-the-art`, `Robust`, `Turnkey`, `End-to-end orchestration`, `Synergy`, `Paradigm shift`, `Holistic`, `Seamless integration`, `Hyper-scalable`, `Disruptive`, `Leverage`, `World-class`.
46. `rule-aphoristic-cadence`: **BANNED.** Slogan-like forced contrasts: *"Not a feature. A platform."*, *"Less noise. More signal."*
47. `rule-repeated-container-text`: **BANNED.** Repeating the exact same word in multiple slots of one card (e.g., Badge: "Ready", Title: "Ready", Button: "Ready").
48. `rule-em-dash-overuse`: **BANNED.** Inserting em-dashes (`—`) in every sentence as an AI writing tic.
49. `rule-theater-slop-phrase`: **BANNED.** Pretentious dismissals like *"We killed the growth theater."*

### G. Imagery (4 Rules)
50. `rule-shape-assembled-illustration`: **BANNED.** Meaningless arrangements of geometric shapes (rectangles, circles) posing as art.
51. `rule-organic-clip-path`: **BANNED.** Jagged, jagged-polygon clip paths trying to simulate torn paper or organic edges.
52. `rule-buried-raster`: **BANNED.** Images covered by 90%+ opaque color overlays that render the image invisible.
53. `rule-broken-image`: **BANNED.** Missing, empty, or unhandled image source paths.

### H. General Quality (10 Rules)
54. `rule-script-error`: Zero uncaught runtime JavaScript/TypeScript exceptions.
55. `rule-content-hidden-at-rest`: Content stuck at `opacity: 0` because an entrance animation failed to trigger is prohibited. Content must be visible by default.
56. `rule-justified-text`: Two-sided justified text (`text-justify`) on web is prohibited (causes whitespace rivers).
57. `rule-low-contrast`: All text must achieve WCAG 2.2 AA (4.5:1 normal, 3:1 large).
58. `rule-skipped-heading`: Skipping heading levels (H1 to H3) is prohibited.
59. `rule-tight-leading`: Body text leading less than 1.4 is prohibited.
60. `rule-tiny-text`: Body text under 14px is prohibited.
61. `rule-wide-tracking`: Letter spacing wider than `0.05em` on multi-line body text is prohibited.
62. `rule-fake-social-proof`: Banned avatar clusters with fake 5-star ratings (`[M][S][K][B] ★★★★★ 4.9/5`).
63. `rule-fake-telemetry`: Banned invented latency, uptime, and SLA statistics.

### I. Design System Fidelity (4 Rules)
64. `rule-design-system-font`: No fonts outside `DESIGN.md`.
65. `rule-design-system-color`: No colors outside semantic tokens in `DESIGN.md`.
66. `rule-design-system-radius`: No border radii outside the scale in `DESIGN.md`.
67. `rule-design-system-font-size`: No type sizes outside the scale in `DESIGN.md`.

---

# 3. GLOBAL DESIGN TOKENS — HARD REQUIREMENT

Never permit the repetition of raw, physical design values inside component or page templates.

**Hard-coded values in colors are STRICTLY PROHIBITED.**

Never produce within component or page files:
- Raw hex colors (`#ffffff`, `#0f1013`)
- `rgb(...)`, `rgba(...)`, `hsl(...)`
- Arbitrary Tailwind color utilities such as `bg-[#...]`, `text-[#...]`, `border-[#...]`
- Random framework palette utilities (`bg-purple-600`, `text-slate-400` scattered across files)
- One-off shadow color definitions

Actual physical color values must exist solely within the global theme / token configuration layer (`globals.css` with `@theme` or Tailwind config).

### ❌ WRONG (Physical & Arbitrary Values):
```tsx
<div className="bg-[#0f1013] text-slate-400 border border-[#1e2025]">
```

### ✅ CORRECT (Semantic Tokens):
```tsx
<div className="bg-surface text-muted border border-border">
```

### Mandatory Semantic Roles:
- `background`: Canvas background
- `foreground`: Primary high-contrast text
- `surface`: Standard cards and surface panels
- `surface-subtle`: Subtle background contrast
- `surface-elevated`: Floating modals, popovers, menus
- `border`: Structural dividers and borders
- `border-subtle`: Secondary faint boundaries
- `text-primary`: Primary body and heading text
- `text-muted`: Secondary metadata and captions
- `primary`: Interactive brand accent (buttons, active states)
- `primary-hover`: Hover state for primary actions
- `primary-foreground`: Text rendered on primary accent
- `destructive` / `danger`: Error states, danger alerts, destructive triggers
- `warning`: Attention, pending, cautionary states
- `success`: Completed, verified, positive states
- `info`: Non-critical informational cues

---

# 4. MECHANICAL CODE STANDARDS (BASELINE UI RULES)

To guarantee flawless execution, every component must strictly conform to these mechanical rules:

### A. Viewports & Safe Areas
- **Use `h-dvh` instead of `h-screen` or `100vh`:** Standard `100vh` breaks on mobile Safari/Chrome due to dynamic address bars. Always use dynamic viewport height (`h-dvh`, `min-h-dvh`).
- **Respect mobile safe areas:** Use `pb-safe` or `padding-bottom: env(safe-area-inset-bottom)` for fixed bottom bars, modals, or sheets to avoid overlapping the iOS home indicator.

### B. Typography Mechanics
- **Headings (`h1`–`h4`):** Always apply `text-balance` to headings to prevent awkward single-word orphan wraps.
- **Body & Paragraphs:** Apply `text-pretty` to multiline paragraphs for clean typographic rags.
- **Numbers, Metrics & Timestamps:** Always apply `tabular-nums` (`font-variant-numeric: tabular-nums`) to tables, prices, counters, countdowns, timers, and KPI figures so digits don't jump horizontally on update.
- **Tight Headings:** Use tight leading (`leading-tight` or `tracking-tight`) on large display headings (`text-3xl` and above). Never leave default loose leading on giant text.

### C. Sizing & Spacing Mechanics
- **Square Elements:** Use `size-*` as modern baseline (e.g., `size-4`, `size-8`, `size-10`).
- **Standard Scale:** Stick to the standardized spacing scale (`4`, `8`, `12`, `16`, `24`, `32px`). Never use arbitrary pixel classes like `p-[13px]` or `gap-[7px]`.
- **Tailwind Version Awareness:** In Tailwind CSS v4, define tokens in CSS via `@theme` directives; in Tailwind v3, define tokens in `tailwind.config.*`. Never inject obsolete v3 config files into v4 setups.

### D. Component Primitives First
- **No Div-Buttons:** Never use `<div onClick={...}>` or `<span onClick={...}>` as interactive triggers. Use native `<button>` or accessible unstyled primitives (`Base UI`, `Radix UI`, `React Aria`).
- **Accessible Primitives:** For dropdowns, dialogs, popovers, tabs, and tooltips, use established unstyled primitives that manage focus traps, keyboard navigation, and ARIA roles automatically.

---

# 5. ACCESSIBILITY CONTRACTS (WCAG 2.2 AA)

1. **Accessible Names:** Every interactive control must have an accessible name. Icon-only buttons **must** have `aria-label` or `aria-labelledby`. Decorative icons **must** have `aria-hidden="true"`.
2. **Keyboard Navigation & Visible Focus:** All interactive elements must be reachable via `Tab`. Never remove focus rings without providing an intentional, high-contrast replacement (`focus-visible:ring-2 focus-visible:ring-primary focus-visible:ring-offset-2`).
3. **Modal Focus Traps:** `Escape` must dismiss modals, dropdowns, and overlays. Dialogs must trap focus while open and restore focus to the trigger upon closure.
4. **Forms & Validation:** Every input must have an associated `<label>`. Errors must link via `aria-describedby`. Invalid fields must set `aria-invalid="true"`.
5. **Touch Targets:** Minimum 44x44px for mobile devices (`min-h-11 min-w-11`), minimum 24x24px for compact desktop controls.

---

# 6. RESILIENT 5-STATE UI MODELING

Never ship a component that only handles the ideal "happy path". Every data-backed UI surface must explicitly implement:

1. **Default / Populated:** Standard operational state with clean typographic hierarchy.
2. **Loading / Pending:** Skeleton screens matching exact rendered geometry to eliminate layout shift (CLS).
3. **Empty / Zero-State:** Helpful, single-line guide with direct action trigger (avoid giant cartoon illustrations for simple tables).
4. **Error / Failed:** Human-readable explanation with explicit retry trigger (`onClick={refetch}`).
5. **Partial / Overflow:** Long text truncated gracefully (`truncate` / `line-clamp-2`), numerical figures formatted via `tabular-nums`.

---

# 7. THE MASTER ANTI-SLOP AUDIT GATE

Before declaring any UI deliverable complete, audit against this checklist:
- [ ] 0 nested cards (Cardocalypse check passed)
- [ ] 0 eyebrow labels / kicker tags above headings
- [ ] 0 decorative badges or fake feature pills
- [ ] 0 neon/purple/cyan gradients or decorative glassmorphism
- [ ] 0 hairline borders combined with wide blurry drop shadows
- [ ] 0 corporate buzzwords; copy is 100% human and outcome-focused
- [ ] `text-balance` on all headings, `text-pretty` on all paragraphs
- [ ] `tabular-nums` on all metrics, counters, and prices
- [ ] `h-dvh` used for dynamic viewports, safe-area paddings respected
- [ ] 100% semantic design tokens (0 raw hex colors)
- [ ] 5-state resilience verified (Default, Loading, Empty, Error, Overflow)
