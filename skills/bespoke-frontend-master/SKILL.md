---
name: bespoke-frontend-master
description: "MANDATORY - Must execute view_file on this skill before writing any frontend, UI, Next.js, or React code. Project-first design constitution, semantic design tokens, anti-AI-slop hard rules, mechanical baseline UI standards, accessibility contracts, motion performance, and contextual state modeling."
---

# 0. PROJECT-FIRST DESIGN CONSTITUTION

This skill must never impose its own visual preferences or arbitrary pre-packaged design styles onto any project.

Labels such as "Modern UI", "SaaS UI", "Developer UI", or "Premium UI" can never justify visual decisions on their own.

Before generating any code or UI, the existing repository must be thoroughly inspected.

### Order of Precedence:
1. Existing product requirements
2. Existing design system / design tokens
3. Existing brand identity
4. Existing component patterns
5. User workflow and information hierarchy
6. Accessibility (WCAG 2.1 AA compliance)
7. Responsive behavior & mobile viewports
8. Visual decoration

**Decoration must never precede architecture.**

## Existing System First

Inspect and identify the existing system in the project before generating any new patterns:
- Colors
- Typography
- Spacing
- Border radius
- Shadows & elevation
- Containers & layout grids
- Icons
- Existing components
- Form patterns
- Table patterns
- Navigation patterns

- **If the existing system is consistent and functional:** Preserve it.
- **If the existing system is fragmented or inconsistent:** Standardize it first.
- **Do not rebrand or restyle the project** simply because this skill mentions different values or examples.

---

# 1. GLOBAL DESIGN TOKENS — HARD REQUIREMENT

Never permit the repetition of raw, physical design values inside component or page templates.

**Hard-coded values in colors are STRICTLY PROHIBITED.**

Never produce the following within component or page files:
- Raw hex colors (`#ffffff`, `#0f1013`)
- `rgb(...)`
- `rgba(...)`
- `hsl(...)`
- Arbitrary Tailwind color utilities such as `bg-[#...]`, `text-[#...]`, `border-[#...]`
- Random framework palette utilities (e.g., `bg-purple-600`, `text-slate-400` scattered across components)
- One-off shadow color definitions

Actual physical color values must exist solely within the global theme / token configuration layer.

Components must consume **semantic tokens exclusively**.

### ❌ WRONG (Physical & Arbitrary Values):
```tsx
<div className="bg-[#0f1013] text-slate-400 border border-[#1e2025]">
```

### ✅ CORRECT (Semantic Tokens):
```tsx
<div className="bg-surface text-muted border border-border">
```

Create token names based on **purpose and semantic role**, never by visual color:
- `background`
- `foreground`
- `surface`
- `surface-subtle`
- `surface-elevated`
- `border`
- `border-subtle`
- `text-primary`
- `text-secondary`
- `text-muted`
- `primary`
- `primary-hover`
- `primary-foreground`
- `success`
- `warning`
- `destructive` (or `danger` alias)
- `info`

Domain-specific semantic tokens may be defined when required (e.g., for a developer tool):
- `terminal-background`
- `terminal-foreground`
- `terminal-prompt`
- `code-background`
- `http-get`
- `http-post`
- `http-delete`

Components must not be aware of physical light/dark color mappings. Light and dark theme resolutions must occur entirely at the global theme layer.

---

# 2. MECHANICAL CODE STANDARDS (BASELINE UI RULES)

To eliminate sloppy AI output and substandard CSS execution, every component must strictly conform to these mechanical rules:

### A. Viewports & Safe Areas
- **Use `h-dvh` instead of `h-screen` or `100vh`:** Standard `100vh` breaks on mobile Safari/Chrome due to dynamic address bars. Always use dynamic viewport height (`h-dvh`, `min-h-dvh`).
- **Respect mobile safe areas:** Use `pb-safe` (when `tailwindcss-safe-area` is configured) or standard CSS `padding-bottom: env(safe-area-inset-bottom)` for fixed bottom bars, modals, or sheets to avoid overlapping the iOS home indicator.

### B. Typography Mechanics
- **Headings (`h1`–`h4`):** Always apply `text-balance` (Tailwind v3.3+) to headings to prevent awkward single-word orphan wraps.
- **Body & Paragraphs:** Apply `text-pretty` (Tailwind v3.4+) to multiline paragraphs for clean typographic rags.
- **Numbers, Metrics & Timestamps:** Always apply `tabular-nums` (`font-variant-numeric: tabular-nums`) to tables, prices, counters, countdowns, timers, and KPI figures so digits don't jump horizontally on update.
- **Tight Headings:** Use tight leading (`leading-tight` or `tracking-tight`) on large display headings (`text-3xl` and above). Never leave default loose leading on giant text.

### C. Sizing & Spacing Mechanics
- **Square Elements:** Use `size-*` (Tailwind v3.4+) or `w-* h-*` on older releases (e.g., `size-4`, `size-8`, `size-10`).
- **Standard Scale:** Stick to the standardized spacing scale (`4`, `8`, `12`, `16`, `24`, `32px`). Never use arbitrary pixel classes like `p-[13px]` or `gap-[7px]`.

### D. Component Primitives First
- **No Div-Buttons:** Never use `<div onClick={...}>` or `<span onClick={...}>` as interactive triggers. Use native `<button>` or accessible unstyled primitives (`Base UI`, `Radix UI`, `React Aria`).
- **Accessible Primitives:** For dropdowns, dialogs, popovers, tabs, and tooltips, use established unstyled primitives that manage focus traps, keyboard navigation, and ARIA roles automatically.

---

# 3. ANTI-AI-SLOP — HARD RULES

The following patterns are **STRICTLY PROHIBITED as default solutions**:
- Purple / blue / cyan neon gradients
- Purely decorative gradients
- Gratuitous glassmorphism
- Decorative backdrop blur
- Glowing background blobs
- Glow effects on standard buttons or cards
- Wrapping every individual section inside a bordered card
- Nested cards inside cards
- Forcing 16–24px radius uniformly everywhere
- Drop shadows applied to every surface
- Colored rounded icon containers everywhere
- Forcing an icon onto every single button
- Emoji-based UI styling
- The generic template: Eyebrow + Huge Heading + Tiny Muted Subtitle
- Center-aligning everything by default
- Excessive, vacuous whitespace
- Fake social proof (e.g., generic avatar clusters `[M][S][K][B] ★★★★★ 4.9/5`)
- Benefit pill clusters under CTAs (`[⚡ 3 mins] [🛡️ Free]`)
- KPI metric cards by default
- Defaulting any dashboard to: KPI cards + Line Chart + Recent Activity list
- Bento grids by default
- Generic SaaS marketing buzzwords
- Fake metrics, fake latency, fake uptime, fake revenue charts

Any of these patterns may only be used if there is an **explicit product or brand requirement**.  
*"Looking modern"* is never a valid architectural justification.

---

# 4. ACCESSIBILITY CONTRACTS (WCAG 2.1 AA)

Accessibility is non-negotiable and must be built directly into the DOM structure:

### Priority Rules:
1. **Accessible Names:**
   - Every interactive control must have an accessible name.
   - Icon-only buttons **must** have `aria-label` or `aria-labelledby`.
   - Decorative SVGs and icons **must** have `aria-hidden="true"`.
2. **Keyboard Navigation:**
   - All interactive elements must be reachable via `Tab`.
   - Never remove focus rings without providing an intentional, high-contrast replacement (`focus-visible:ring-2 focus-visible:ring-primary`).
   - `Escape` must dismiss modals, dropdowns, and overlays.
   - Dialogs/modals must trap focus while open and restore focus to the triggering element upon closure.
3. **Forms & Validation:**
   - Every `<input>`, `<select>`, and `<textarea>` must have an associated `<label>`.
   - Input errors must be explicitly linked using `aria-describedby="field-error-id"`.
   - Invalid fields must programmatically set `aria-invalid="true"`.
4. **Color Contrast:**
   - Maintain minimum 4.5:1 contrast for regular text and 3:1 for large text / graphical UI components.

---

# 5. MOTION PERFORMANCE HARD RULES (ANTI-JANK)

Stuttering or sluggish animations degrade perceived product quality:

### Priority Rules:
1. **Compositor Properties Only:**
   - Animate exclusively via `transform` and `opacity`.
   - **Never animate layout properties** (`width`, `height`, `top`, `left`, `margin`, `padding`) continuously on large surfaces.
2. **Scroll-Driven Motion:**
   - Never drive animations by attaching raw listeners to `window.addEventListener('scroll')` or reading `scrollY` in loops.
   - Use CSS `animation-timeline: view()` or `IntersectionObserver` with visibility thresholds.
   - Pause or stop animations when elements are scrolled out of viewport.
3. **Micro-Interaction Budget:**
   - Standard UI state transitions (hover, active, expand) must not exceed **200ms**.
   - Do not use `transition-all`. Specify exact changing properties: `transition-colors`, `transition-opacity`, `transition-transform`.
4. **Blur Restrictions:**
   - Blur animations must be <= 8px.
   - Never animate blur continuously or over large layout surfaces.
5. **Reduced Motion:**
   - Always honor user system preferences via `prefers-reduced-motion`:
   ```css
   @media (prefers-reduced-motion: reduce) {
     *, ::before, ::after {
       animation-duration: 0.01ms !important;
       transition-duration: 0.01ms !important;
     }
   }
   ```

---

# 6. LAYOUT ARCHITECTURE & DENSITY

### No Default Bento
Select layouts based on **content relationships and user workflows**:
- **Comparable structured data:** Table
- **Browsable records:** List or grid, depending on scanning density requirements
- **System configuration:** Grouped settings with clear hierarchy
- **Sequential workflows:** Stepped wizard or structured form
- **Operational monitoring:** Dense operational layout
- **Independent showcase items:** Cards or grid, when contextually appropriate

### Card Rule
A card is an organizational boundary, not a decorative stamp.  
For section grouping, evaluate lighter separators first:
- Whitespace
- Typographic hierarchy
- Subtle horizontal dividers
- Clean 1px borders
- Subtle surface contrast

### Radius Baselines
- **Small (badges, tags):** 4px
- **Controls (inputs, buttons):** 6–8px
- **Surfaces (cards, panels):** 8–12px
- **Major Overlays (modals, dialogs):** 12–16px
- **Full:** Reserved strictly for true pills and circles  
*0px sharp corners are completely valid for dense developer/terminal tools.*

### Shadows
Shadows must be reserved for **real physical layering** (modals, popovers, tooltips, dropdown menus). Never apply default heavy drop shadows to standard flat cards.

---

# 7. REAL DATA ONLY

Never invent numbers, metrics, or telemetry that simulate operational credibility:
- Latency (e.g., "12ms")
- Uptime (e.g., "99.99%")
- SLA guarantees
- Revenue figures
- Conversion percentages
- Active user counts
- FPS benchmarks

Fake telemetry is classified as AI-slop. If test fixtures are required, structure them explicitly as mock test data (`fixtures/mockData.ts`).

---

# 8. CONTEXTUAL STATE MODELING

Implement only semantically applicable states for each specific component:
- **Default**
- **Loading / Pending** (Only use skeletons if they prevent layout shift and wait time warrants it)
- **Empty** (Single-line clean text preferred; avoid huge icon + CTA banners for simple lists)
- **Error** (Descriptive, actionable error messages with retry triggers)
- **Optimistic** (Only when mutation outcome is highly predictable with tested rollback)

---

# 9. FRAMEWORK VERSION SAFETY

Never trigger automatic migrations to newer framework versions.
- Inspect `package.json` and lockfiles first.
- Match existing repository APIs (React 18 vs 19, Next.js Pages vs App Router).
- Upgrades must only occur upon explicit user request.

---

# 10. THE BESPOKE AUDIT GATE

Before declaring any UI task complete, conduct this 10-point audit:

1. **Does the product workflow genuinely require this layout, or is it generic SaaS boilerplate?**
2. **Are headings using `text-balance` and multiline copy using `text-pretty`?**
3. **Are all numbers, metrics, and tabular data using `tabular-nums`?**
4. **Is viewport height handled via `h-dvh` with mobile safe-area protection (`pb-safe`)?**
5. **Are interactive elements native buttons or accessible primitives (zero unaccessible divs)?**
6. **Do icon-only buttons have `aria-label`, and decorative icons `aria-hidden="true"`?**
7. **Are animations compositor-only (`transform`/`opacity`) with <= 200ms duration?**
8. **Are all colors, borders, and surfaces resolving to global semantic tokens (zero raw hex)?**
9. **Is the UI free of fake metrics, fake reviews, avatar clusters, and neon gradients?**
10. **Does the implementation strictly preserve the existing repository's design system?**

> *If any check fails, resolve it before presenting the deliverable to the user.*
