---
name: create-design-md
description: "Design system architect, dual-context engine (PRODUCT.md + DESIGN.md), and 14 surgical design playbooks (distill, clarify, polish, typeset, harden, critique, etc.)."
---

# 🏛️ DESIGN SYSTEM ARCHITECT & SURGICAL DESIGN ENGINE (`create-design-md`)

Establishes, calibrates, and enforces a repository-level design contract. Prevents AI hallucinations, arbitrary styling, and generic slop through the **Dual-Context Protocol (`PRODUCT.md` + `DESIGN.md`)** and provides **14 surgical design playbooks** (`/distill`, `/clarify`, `/polish`, `/typeset`, `/harden`, etc.) for targeted, non-destructive UI refinement.

---

# 📜 PART 1: THE DUAL-CONTEXT PROTOCOL

AI models revert to statistical slop when they lack durable context. Before generating or refactoring any interface, two binding context files must govern decisions:

```
┌────────────────────────────────────────────────────────────────────────┐
│                        THE DUAL-CONTEXT SHIELD                         │
├───────────────────────────────────┬────────────────────────────────────┤
│          PRODUCT.md               │             DESIGN.md              │
│       (The Human Why)             │        (The Structural How)        │
├───────────────────────────────────┼────────────────────────────────────┤
│ • Product thesis & target user    │ • 60-30-10 semantic token palette  │
│ • Primary task of each view       │ • Modular typography scale         │
│ • Brand archetype & emotional tone│ • Spacing, density & container grid│
│ • Anti-Goals (What it must NEVER  │ • Elevation, radius & shadow tiers │
│   look, sound, or behave like)    │ • Motion budgets & physics easing  │
└───────────────────────────────────┴────────────────────────────────────┘
```

---

## 1. PRODUCT CONTEXT SPECIFICATION (`PRODUCT.md`)

When bootstrapping or formalizing a project, generate or update a root `PRODUCT.md` containing:

```markdown
# Product Context: <Product Name>

## 1. Purpose & Audience
- **Target User:** Who specifically uses this interface (e.g., "Independent café owners during morning rush", "Senior DevOps engineers managing cluster alerts")?
- **Core Problem:** What real-world friction does this tool eliminate?
- **Primary View Action:** What is the single most important action on the main screen?

## 2. Brand Archetype & Tone
- **Archetype:** (e.g., "Dense High-Performance Terminal", "Warm Scandinavian Craft", "Calm Institutional FinTech")
- **Voice:** Direct, human, outcome-focused, zero-pretension.

## 3. Anti-Goals (Strict Prohibitions)
Explicitly list what the product must NEVER look, sound, or feel like:
- ❌ Must NEVER look like a generic crypto/web3 dashboard (zero neon cyan, zero dark glow).
- ❌ Must NEVER use patronizing marketing jargon ("Supercharge", "Next-gen").
- ❌ Must NEVER wrap every single element in nested bordered cards ("Cardocalypse").
- ❌ Must NEVER use playful bouncy cartoon animations.
```

---

## 2. DESIGN SYSTEM SPECIFICATION (`DESIGN.md`)

Generate or update a root `DESIGN.md` conforming to this concrete contract:

### 1. The 60-30-10 Color System
Never pick random palette colors. Distribute visual weight strictly:
- **60% Dominant (Base Surface & Canvas):** Canvas backgrounds, app shells, high-surface panels (`background`, `surface`, `surface-subtle`).
- **30% Secondary (Structure & Typography):** Text hierarchy, borders, separators, secondary containers (`foreground`, `text-muted`, `border`, `surface-elevated`).
- **10% Accent (Interactive Focus):** Primary buttons, active tabs, focus rings, status indicators (`primary`, `primary-hover`, `accent`).

```markdown
## Semantic Token Palette
- `background`: Canvas background (Light / Dark hex or OKLCH)
- `surface`: Elevated cards and panels
- `surface-subtle`: Secondary tinted surfaces
- `surface-elevated`: Floating modals and popovers
- `border`: Structural dividers and borders (subtle contrast)
- `foreground`: Primary high-contrast body text
- `text-muted`: Supporting metadata and secondary text
- `primary`: Interactive brand accent (buttons, active states)
- `primary-foreground`: Text rendered on top of primary accent
- `destructive`: Error states, danger alerts, destructive actions
- `warning`: Attention, pending, or cautionary alerts
- `success`: Completed, verified, or positive status
- `info`: Non-critical informational cues
```

### 2. Typography Hierarchy & Copy Contract
- **Primary Typeface:** Body copy and interface controls (e.g., Geist, Inter, SF Pro, or custom brand font).
- **Secondary Typeface (Optional):** Editorial display headings or monospace for code/metrics.
- **Type Scale:**
  - Display (`text-4xl` / `text-5xl`): Tight leading (`leading-none`), tracking tight (`tracking-tight`), `text-balance`.
  - Heading 1 (`text-2xl` / `text-3xl`): `leading-tight`, `tracking-tight`, `text-balance`.
  - Heading 2 & 3 (`text-lg` / `text-xl`): `leading-snug`, `text-balance`.
  - Body (`text-sm` / `text-base`): `leading-relaxed`, `text-pretty`.
  - Metadata / Caption (`text-xs`): `leading-normal`.
  - Tabular / Numeric (`tabular-nums`): Mandatory for metrics, prices, timestamps.

#### 🚫 Strict Anti-Slop Typography Laws:
- **ZERO EYEBROWS & ZERO KICKERS:** Uppercase tracked kicker tags placed above headings (`FEATURES`, `OVERVIEW`, `WHY US`) are strictly prohibited.
- **PLAIN HUMAN LANGUAGE:** Copy must explain real human outcomes in everyday words. Zero corporate buzzwords (`Next-gen`, `Cutting-edge`, `State-of-the-art`, `Robust`, `Turnkey`, `Synergy`).

### 3. Sizing, Spacing & Density Tiers
- **Base Grid:** Standard 4px / 8px scale (`4`, `8`, `12`, `16`, `24`, `32`, `48`, `64px`).
- **Density Profile:**
  - *Compact / Dense:* Developer tools, data tables, monitoring dashboards (padding 6–8px).
  - *Standard:* Typical SaaS, management portals, e-commerce admin (padding 12–16px).
  - *Spacious:* Marketing landing pages, editorial showcases (padding 24–32px).

### 4. Surfaces, Radius & Elevation
- **Border Radius Scale:**
  - `radius-sm` (4px): Subtle control indicators, small inputs.
  - `radius-md` (6–8px): Form inputs, buttons, control triggers.
  - `radius-lg` (8–12px): Standard cards, content panels.
  - `radius-xl` (12–16px): Modals, dialogs, popovers.
  - `radius-full`: True circular buttons and avatar circles.
- **Elevation / Shadows:**
  - `shadow-none`: Flat cards, bordered containers.
  - `shadow-sm`: Subtle hover lifts.
  - `shadow-md`: Dropdown menus, tooltips.
  - `shadow-xl`: Modal overlays, floating drawer panels.
  - **Rule:** Never combine a hairline 1px border with a wide 30px soft shadow simultaneously.

---

# ⚡ PART 2: THE 14 SURGICAL DESIGN PLAYBOOKS

When modifying existing UI, never trigger a blind, chaotic redesign. Select and execute the exact surgical playbook required for the user's intent:

```
┌────────────────────────────────────────────────────────────────────────┐
│                      14 SURGICAL DESIGN PLAYBOOKS                      │
├────────────────────────────────────────────────────────────────────────┤
│ 1. /distill   - Strip clutter, nested cards, and visual noise          │
│ 2. /clarify   - Plain human copywriting, eliminate marketing buzzwords │
│ 3. /polish    - Refine spacing, typography alignment, and token drifts │
│ 4. /typeset   - Fix type scales, line lengths, and font pairings       │
│ 5. /bolder    - Amplify confident hierarchy and contrast               │
│ 6. /quieter   - Tone down overstimulating, neon, or noisy layouts      │
│ 7. /harden    - Complete 5-state resilience (empty, error, loading)    │
│ 8. /colorize  - Apply OKLCH scales, semantic tokens, and contrast      │
│ 9. /layout    - Establish reading flow and asymmetric visual rhythm    │
│ 10. /animate  - Purposeful physics-based micro-interactions (<= 200ms) │
│ 11. /delight  - Memorable, tactile, brand-reinforcing micro-details    │
│ 12. /critique - Design Director evaluation of cognitive load & purpose │
│ 13. /audit    - Technical QA (WCAG 2.2 AA contrast, touch targets)     │
│ 14. /shape    - Pre-code conceptual design framing                     │
└────────────────────────────────────────────────────────────────────────┘
```

---

### Playbook 1: `/distill` (Declutter & Simplify)
**Trigger:** User asks to "simplify", "declutter", "clean up the noise", or when a page feels overwhelming.
1. **Detect & Flatten Nested Cards:** Identify cards nested inside cards (`rule-nested-cards`). Remove the outer wrapper; use subtle dividers or pure whitespace instead.
2. **Eliminate Status-Chip Soup:** Count badges and pills. If more than 2 items in a row have colored pills, replace them with plain typographic labels or subtle status dots.
3. **Consolidate Redundant KPI Boxes:** Replace 4 equal-sized small metric boxes with 1 dominant primary KPI and inline secondary details.
4. **Remove Purely Decorative Artifacts:** Delete decorative grid-lines, background orbs, and empty SVG doodles.
5. **🛡️ Playbook Symbiosis Invariant (CRITICAL):** `/distill` strips away *decorative fat* only. It **must NEVER delete functional operational states** generated by `/harden` (e.g., empty state instructions, error boundary banners, retry triggers, pagination controls, or aria accessibility labels).

---

### Playbook 2: `/clarify` (Human Copywriting & UX Clarity)
**Trigger:** User asks to "improve copy", "make headlines clearer", "fix messaging", or when text sounds like generic marketing slop.
1. **Kill Corporate Buzzwords:** Audit text against `rule-marketing-buzzword`. Replace abstract claims with concrete human verbs.
   - *Before:* "Supercharge your team's workflow with our next-gen orchestration engine."
   - *After:* "Assign tasks, track deadlines, and review team progress in one view."
2. **Contextualize Action Buttons:** Audit buttons against vague labels (`Submit`, `Continue`, `Go`). Replace with explicit outcomes (`Create Invoice`, `Send Invitation`, `Download PDF`).
3. **Eliminate Redundant Field Explanations:** If a form label says "Email Address", remove the helper text below that says "Enter your email address here".
4. **Friendly Error States:** Rewrite cryptic errors into actionable instructions.

---

### Playbook 3: `/polish` (Non-Destructive Craft Refinement)
**Trigger:** User asks to "polish", "tighten up", "finalize", or "clean up the UI".
1. **Preserve Structure:** Do NOT change the layout structure, brand colors, or functional behavior.
2. **Snap Spacing to Scale:** Convert arbitrary values (`p-[13px]`, `gap-[7px]`) to the standard 4/8px spacing grid.
3. **Check Optical Alignment:** Ensure icons and text baseline-align (`items-center`, `gap-2`). Ensure headings have more space above than below (`rule-heading-rhythm`).
4. **Fix Border/Shadow Clashes:** Eliminate 1px borders combined with 30px blurry shadows.

---

### Playbook 4: `/typeset` (Typographic Rhythm & Contrast)
**Trigger:** User asks to "fix typography", "improve readability", or when text looks flat and unformatted.
1. **Enforce Modular Scale:** Guarantee visible optical distinction between Display, H1, H2, Body, and Caption.
2. **Apply Mechanical Text Rules:**
   - Headings: Add `text-balance` and `tracking-tight`.
   - Paragraphs: Add `text-pretty`, `leading-relaxed`, and constrain width via `max-w-prose` (65–75 chars).
   - Numerical data & tables: Add `tabular-nums`.
3. **Eradicate Eyebrows:** Remove all uppercase kicker labels above headings.

---

### Playbook 5: `/bolder` & Playbook 6: `/quieter`
**`/bolder`:**
- When an interface feels timid, washed-out, or generic:
- Elevate primary CTA contrast with strong semantic color.
- Increase display heading weight and size (`text-3xl font-bold tracking-tight`).
- Add authoritative dark/light contrast between canvas and cards.

**`/quieter`:**
- When an interface feels loud, overstimulating, or aggressive:
- Strip away neon glow effects, pulsing dots, and competing accent colors.
- Reduce high-contrast card borders to subtle tinted dividers.
- Remove bouncy hover animations and simplify the palette to 60-30-10 distribution.

**🛡️ Anti-Oscillation Guard:** Do not oscillate back and forth between extreme high-contrast and extreme washed-out neutrals. Always anchor adjustments to the documented 60-30-10 palette in `DESIGN.md`. If moving between louder and quieter, settle at the **30% structure / 10% accent** baseline.

---

### Playbook 7: `/harden` (5-State Resilience & Edge Cases)
**Trigger:** User asks to "handle edge cases", "prepare for production", or when error/loading states are missing.
1. **Loading State:** Build zero-CLS skeleton loaders matching exact layout geometries.
2. **Empty State:** Provide helpful zero-state instructions with a clear primary action button.
3. **Error State:** Wrap boundaries with descriptive error alerts and a retry trigger.
4. **Overflow & Long Text:** Wrap long text in `truncate` or `line-clamp-2`; verify layout with 50-character strings.
5. **Mobile Viewport Test:** Check `h-dvh` usage and safe-area padding (`pb-safe`).

---

### Playbook 8: `/critique` & Playbook 9: `/audit`
**`/critique` (Design Director Review):**
1. Evaluate primary visual focus: Does the eye immediately know where to look first?
2. Evaluate cognitive load: Are there more than 7 distinct concepts competing for attention?
3. Evaluate brand resonance: Does the design feel bespoke to the `PRODUCT.md` archetype?

**`/audit` (Technical Quality Verification):**
1. Verify WCAG 2.2 AA contrast ratios (4.5:1 text, 3:1 components).
2. Verify touch target sizes (minimum 44x44px for touchable controls).
3. Verify zero layout shift (CLS) during transitions.
4. Verify keyboard accessibility (`Tab`, `Escape`, visible focus rings).

---

# 🔍 PART 3: UI REFURBISHMENT PROTOCOL (`improve-ui`)

Before refactoring any existing UI, do not dive into raw code editing. Execute this 3-proof protocol:

### Step 1: Trace the Rendered Path
1. Identify the exact route and layout file.
2. Trace imports through compositions, shared components, and resolved tokens.
3. Exclude untouched surfaces; audit only the coherent task surface.

### Step 2: The 3-Proof Gate
A visual finding is valid only if all three proofs exist:
1. **Contract Proof:** Cite the specific clause in `PRODUCT.md`, `DESIGN.md`, or the 67-rule anti-slop catalog that is violated.
2. **Runtime Proof:** Prove that the invalid property, nested card, or jargon reaches the rendered DOM.
3. **Correction Proof:** Provide the exact replacement semantic token, primitive, plain copy, or layout fix.

### Step 3: Write Isolated Design Plan (`design-plans/<plan-name>.md`)
When proposing non-trivial UI improvements, record them in a structured plan:

```markdown
# Design Plan: <Surface Name>

## Evidence Chain
- Surface: `<route or component path>`
- Playbook Selected: `<e.g. /distill, /clarify, /polish, /harden>`
- Anti-Pattern Violations: `<e.g. rule-nested-cards, rule-marketing-buzzword>`
- Contract Proof: `<clause in PRODUCT.md or DESIGN.md>`

## Proposed Changes
1. `<file path>`:
   - Replace: `<offending nested card, raw hex, or corporate jargon>`
   - With: `<semantic token, clean typography, or plain outcome copy>`
   - Verification: `<expected visual/audited result>`

## Scope Boundaries
- Affected: `<components inheriting change>`
- Excluded: `<unrelated components kept intact>`
```

---

## ⚡ Execution Protocol

1. **If `PRODUCT.md` or `DESIGN.md` does not exist in the project root:**
   - Scan existing styling configurations: inspect Tailwind CSS v4 `@theme` in `globals.css` or Tailwind v3 `tailwind.config.*`, CSS root variables, and theme providers.
   - Generate `PRODUCT.md` (defining user, task, anti-goals) and `DESIGN.md` (defining tokens, typography scale, radius tiers).
2. **If `PRODUCT.md` and `DESIGN.md` exist:**
   - Treat them as the binding visual and copywriting law of the repository.
   - Deny any UI change that contradicts either contract.
