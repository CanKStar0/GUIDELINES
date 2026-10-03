---
name: create-design-md
description: "MANDATORY - Must execute view_file on this skill when bootstrapping a design system, generating/updating DESIGN.md, or auditing project UI against design contracts. Establishes 60-30-10 color palettes, typography scales, elevation tiers, and design handoff plans."
---

# Design System Architect & Audit Engine (`create-design-md`)

Generate, calibrate, and enforce a repository-level `DESIGN.md` specification. Establish an unambiguous visual contract so agents never hallucinate styles, introduce arbitrary colors, or produce disjointed AI-slop interfaces.

---

## 🏛️ PART 1: THE DESIGN SYSTEM SPECIFICATION (`DESIGN.md`)

When bootstrapping a new project or formalizing an existing project's visual identity, generate or update a root `DESIGN.md` conforming to this exact structure:

### 1. Brand Identity & Design Direction
- **Archetype & Tone:** Define the personality (e.g., "Dense High-Performance Developer Terminal", "Clean Scandinavian FinTech", "Warm Editorial Culinary Studio").
- **Visual Thesis:** 1–2 sentences defining what the product looks like and what it **strictly avoids**.

### 2. The 60-30-10 Color System
Never pick random palette colors. Distribute visual weight strictly:
- **60% Dominant (Base Surface & Canvas):** Canvas backgrounds, app shells, high-surface cards (`background`, `surface`, `surface-subtle`).
- **30% Secondary (Structure & Typography):** Text hierarchy, borders, separators, secondary containers (`foreground`, `text-muted`, `border`, `surface-elevated`).
- **10% Accent (Interactive Focus):** Primary buttons, active tabs, focus rings, status indicators (`primary`, `primary-hover`, `accent`).

```markdown
## Semantic Token Palette
- `background`: Canvas background (Light / Dark hex)
- `surface`: Elevated cards and panels
- `surface-elevated`: Floating modals and popovers
- `border`: Structural dividers and borders (subtle contrast)
- `foreground`: Primary high-contrast body text
- `text-muted`: Supporting metadata and secondary text
- `primary`: Interactive brand accent (buttons, active states)
- `primary-foreground`: Text rendered on top of primary accent
- `destructive`: Error states, danger alerts, destructive actions (or `danger` alias)
- `warning`: Attention, pending, or cautionary alerts
- `success`: Completed, verified, or positive status
```

### 3. Typography Hierarchy
- **Primary Typeface:** Body copy and interface controls (e.g., Inter, Geist, SF Pro).
- **Secondary Typeface (Optional):** Editorial display headings or monospace for code/metrics.
- **Type Scale:**
  - Display (`text-4xl` / `text-5xl`): Tight leading (`leading-none`), tracking tight (`tracking-tight`), `text-balance`.
  - Heading 1 (`text-2xl` / `text-3xl`): `leading-tight`, `tracking-tight`, `text-balance`.
  - Heading 2 & 3 (`text-lg` / `text-xl`): `leading-snug`, `text-balance`.
  - Body (`text-sm` / `text-base`): `leading-relaxed`, `text-pretty`.
  - Metadata / Caption (`text-xs`): `leading-normal`.
  - Tabular / Numeric (`tabular-nums`): Mandatory for metrics, prices, timestamps.

### 4. Sizing, Spacing & Density Tiers
- **Base Grid:** Standard 4px / 8px scale (`4`, `8`, `12`, `16`, `24`, `32`, `48`, `64px`).
- **Layout Max-Widths:** Container constraints (`max-w-7xl` for apps, `max-w-5xl` for marketing, `max-w-prose` for longform).
- **Density Profile:**
  - *Compact / Dense:* Developer tools, data tables, monitoring dashboards (padding 6–8px).
  - *Standard:* Typical SaaS, management portals, e-commerce admin (padding 12–16px).
  - *Spacious:* Marketing landing pages, editorial showcases (padding 24–32px).

### 5. Surfaces, Radius & Elevation
- **Border Radius Scale:**
  - `radius-sm` (4px): Badges, tags, small pills.
  - `radius-md` (6–8px): Form inputs, buttons, control triggers.
  - `radius-lg` (8–12px): Standard cards, content panels.
  - `radius-xl` (12–16px): Modals, dialogs, popovers.
  - `radius-full`: True pill buttons and avatar circles.
- **Elevation / Shadows:**
  - `shadow-none`: Flat cards, bordered containers.
  - `shadow-sm`: Subtle hover lifts.
  - `shadow-md`: Dropdown menus, tooltips.
  - `shadow-xl`: Modal overlays, floating drawer panels.

---

## 🔍 PART 2: UI AUDIT & DESIGN PLAN ENGINE (`improve-ui`)

Before refactoring, restyling, or updating any existing UI, do not dive into raw code editing. Execute this 4-step proof protocol:

### Step 1: Trace the Rendered Path
1. Identify the exact route and layout file.
2. Trace imports through compositions, shared components, and resolved tokens.
3. Exclude untouched surfaces; audit only the coherent task surface.

### Step 2: The 3-Proof Gate
A visual finding is valid only if all three proofs exist:
1. **Contract Proof:** Cite the specific line in `DESIGN.md` or global tokens that is violated.
2. **Runtime Proof:** Prove that the invalid property reaches the rendered DOM element.
3. **Correction Proof:** Provide the exact replacement semantic token, primitive, or class (e.g., replace `bg-[#1e2025]` with `bg-surface`).

### Step 3: Write Isolated Design Plan (`design-plans/<plan-name>.md`)
When proposing non-trivial UI improvements, record them in a structured plan:

```markdown
# Design Plan: <Surface Name>

## Evidence Chain
- Surface: `<route or component path>`
- Problem: <direct observation>
- Contract Violated: `<token, rule, or DESIGN.md clause>`

## Proposed Changes
1. `<file path>`:
   - Replace: `<exact offending code>`
   - With: `<concrete token or primitive>`
   - Verification: `<expected visual result>`

## Scope Boundaries
- Affected: `<consumers inheriting the change>`
- Excluded: `<unrelated components kept intact>`
```

---

## ⚡ Execution Protocol

1. If `DESIGN.md` does not exist in the project root:
   - Scan existing styling configurations (`tailwind.config.*`, `globals.css`, theme providers).
   - Generate `DESIGN.md` in the project root capturing the real active tokens.
2. If `DESIGN.md` exists:
   - Treat it as the binding visual law.
   - Deny any UI change that contradicts `DESIGN.md`.
