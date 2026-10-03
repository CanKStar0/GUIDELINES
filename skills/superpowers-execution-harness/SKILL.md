---
name: superpowers-execution-harness
description: "MANDATORY - Must execute view_file on this skill before task execution, multi-language i18n updates, verification gates, or QA auditing. Agent harness methodology, Hermes error memory, and 4-pillar QA."
---

# 🚀 Superpowers Execution Harness — Engineering Discipline, Memory & Verification Gates

This skill enforces high-discipline execution, eliminates shallow/hasty patching, prevents redundant tool loops, minimizes shell waste, and establishes strict empirical verification gates and multi-language parity.

---

# HARD BANS — UNFORGIVABLE HARNESS & EXECUTION ANTI-PATTERNS

The following AI habits and execution shortcuts are **STRICTLY PROHIBITED**:

### 1. Mocking Everything / Testing Nothing is BANNED
- ❌ **Prohibited:** Writing unit tests that mock the database, mock the service, mock the fetch call, and assert trivialities like `expect(true).toBe(true)`.
- 💣 **Failure Mode:** Code ships to production with passing tests, but fails immediately on runtime queries, real data payloads, or network serialization.
- ✅ **Mandatory:** Tests must validate real contracts, actual Zod schemas, real state transitions, and integration error cases.

### 2. Bypassing Type Errors with `@ts-ignore` or `any` is BANNED
- ❌ **Prohibited:** Silencing TypeScript compiler errors by slapping `// @ts-ignore`, `// @ts-nocheck`, or casting `(data as any)` onto broken code.
- 💣 **Failure Mode:** Destroys type safety guarantees across the codebase, resulting in catastrophic `TypeError: Cannot read properties of undefined` crashes in production.
- ✅ **Mandatory:** Type errors must be fixed properly via correct generics, strict interface definitions, discrimination unions, or Zod parsing.

### 3. Blind File Overwrites (No Pre-Read) are BANNED
- ❌ **Prohibited:** Rewriting an entire file from chat memory without inspecting the physical file first (`write_to_file` over existing files without prior `view_file`).
- 💣 **Failure Mode:** Silently wipes out sibling utility functions, imports, comments, and recent edits made in other branches (fatal regression).
- ✅ **Mandatory:** Always read the targeted file slice first (`view_file`), and execute surgical modifications using `replace_file_content`.

### 4. Claiming Completion Without Verification is BANNED
- ❌ **Prohibited:** Telling the user *"I have fixed the issue and everything works"* without actually executing the verification build command.
- 💣 **Failure Mode:** Hallucinated confidence. Broken imports and syntax errors remain unresolved until the user tries to run the project.
- ✅ **Mandatory:** The agent must physically execute `npm run build` or `npx tsc --noEmit` (or corresponding project verification command) and prove Exit Code 0 in the trajectory before claiming completion.

### 5. Partial Multi-Language Updates are BANNED
- ❌ **Prohibited:** Adding a new button or label to `en.json` while leaving `tr.json`, `nl.json`, or other locale dictionaries out of sync.
- 💣 **Failure Mode:** The application throws missing key runtime warnings or displays ugly raw variable identifiers (`SETTINGS_NAV_HEADER`) in foreign locales.
- ✅ **Mandatory:** All active locale translation files must be updated simultaneously with 100% key parity.

---

# THE 5 GOLDEN EXECUTION PILLARS

1. **Zero Guesswork & Live Code as SSOT:**
   - Never assume file paths, exports, or database columns exist without empirical verification. Always verify live files on disk using `view_file` before making edits.
2. **Terminal Discipline & Zero Waste:**
   - The shell (`run_command`) is reserved for package installation, compilation/testing (`npm run build`, `tsc --noEmit`, `test`), and targeted repo checks (`git status`, `git ls-files`). Aimless exploratory loops or raw file dumping (`cat`, `Get-Content`) are strictly forbidden.
3. **In-Session Read Cache:**
   - If a file has already been read in this conversation session, reuse working memory; never read the same file repeatedly.
4. **Root-Cause Remediation (Anti-Regression):**
   - Superficial patches are banned. Resolve null pointer risks, CSS overflow bounds, and API failure modes at the architectural root.
5. **Empirical Verification Gate:**
   - A task is NEVER complete until automated verification (TypeScript `npm run build` / `npx tsc --noEmit`, Python `pytest`, or project build command) passes with **Exit Code 0**.

---

# HERMES ERROR LEARNING MEMORY & SMART CONTEXT

- **4-Step Error Learning Cycle:**
  1. *Symptom:* Concrete error message or runtime stack trace.
  2. *Root Cause:* Underlying architectural or logic failure.
  3. *Permanent Fix:* Side-effect-free remediation.
  4. *Memory Record:* One-sentence actionable lesson logged to `output/<project>/memory.json` (Max 10 rules).
- **Smart Context Window:**
  - Never ingest 50 turns of stale transcripts; rely only on the immediate intent (last 1–2 turns) and live disk code.

---

# THE 4 VISUAL & INTERACTIVE QA PILLARS

1. **Pillar 1: Layout & CSS Integrity:** Zero horizontal scroll (`overflow-x`), WCAG AA contrast, consistent border-radius tokens.
2. **Pillar 2: DOM & Content Integrity:** Zero blank screens, meaningful and contextual Empty States on null data.
3. **Pillar 3: Asset & Resource Integrity:** Zero broken images (`img.complete && naturalWidth > 0`), zero 404 font or bundle errors.
4. **Pillar 4: Runtime & Interaction Integrity:** Zero uncaught `console.error` or `window.onerror`, fully tested interactive modals, dropdowns, and form submissions.

### 🔴 0-Token Root-Cause Clustering
- Do not dump 500+ lines of raw test logs into LLM context.
- Cluster errors into 5–8 high-level categories (`P0 Crash`, `API 401`, `Mobile Cutoff`, `Type Mismatch`) for actionable resolution.
