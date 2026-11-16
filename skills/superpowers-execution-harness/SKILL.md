---
name: superpowers-execution-harness
description: "Enforces strict compiler verification gates (Exit Code 0), multi-language i18n key parity, Hermes error memory, and 4-pillar QA auditing."
---

# 🚀 Superpowers Execution Harness — Engineering Discipline, Memory & Verification Gates

This skill enforces high-discipline execution, eliminates shallow/hasty patching, prevents redundant tool loops, minimizes shell waste, and establishes strict empirical verification gates and multi-language parity.

---

# HARD BANS — UNFORGIVABLE HARNESS & EXECUTION ANTI-PATTERNS

The following AI habits and execution shortcuts are **STRICTLY PROHIBITED**:

### 1. Mocking Everything / Code-Only Testing is BANNED
- ❌ **Prohibited:** Writing unit tests that mock the database, mock the service, mock the fetch call, and assert trivialities like `expect(true).toBe(true)` — OR treating `tsc --noEmit` / `npm run build` as proof that the feature works at runtime.
- 💣 **Failure Mode:** Code compiles and "unit tests" pass, while real users hit 500 errors, broken UI clicks, failed DB writes, hydration crashes, or unauthenticated leaks in production.
- ✅ **Mandatory:** Test real behavior end-to-end: real HTTP requests against live endpoints + real DB persistence for backend, and Playwright E2E or live browser (`browser` subagent / `browsermcp`) interaction + reload persistence for UI.

### 2. Bypassing Type Errors with `@ts-ignore` or `any` is BANNED
- ❌ **Prohibited:** Silencing TypeScript compiler errors by slapping `// @ts-ignore`, `// @ts-nocheck`, `// @ts-expect-error`, `/* eslint-disable */`, or casting `(data as any)` / `(data as unknown as SpecificType)` onto broken code.
- 💣 **Failure Mode:** Destroys type safety guarantees across the codebase, resulting in catastrophic `TypeError: Cannot read properties of undefined` crashes in production.
- ✅ **Mandatory:** Type errors must be fixed properly via correct generics, strict interface definitions, discrimination unions, or Zod parsing.

### 3. Blind File Overwrites (No Pre-Read) are BANNED
- ❌ **Prohibited:** Rewriting an entire file from chat memory without inspecting the actual live file first.
- 💣 **Failure Mode:** Silently wipes out sibling utility functions, imports, comments, and recent edits made in other branches (fatal regression).
- ✅ **Mandatory:** Always inspect the target file context first, and execute surgical modifications rather than blind whole-file clobbering.

### 4. Claiming Completion Without Verification is BANNED
- ❌ **Prohibited:** Telling the user *"I have fixed the issue and everything works"* without actually executing the verification build command.
- 💣 **Failure Mode:** Hallucinated confidence. Broken imports and syntax errors remain unresolved until the user tries to run the project.
- ✅ **Mandatory:** Run `npm run build` or `npx tsc --noEmit` (or corresponding project verification command) and verify success before claiming completion.

### 5. Partial Multi-Language Updates are BANNED
- ❌ **Prohibited:** Adding a new button or label to `en.json` while leaving `tr.json`, `nl.json`, or other locale dictionaries out of sync.
- 💣 **Failure Mode:** The application throws missing key runtime warnings or displays ugly raw variable identifiers (`SETTINGS_NAV_HEADER`) in foreign locales.
- ✅ **Mandatory:** All active locale translation files must be updated simultaneously with 100% key parity.

---

# THE 6 GOLDEN EXECUTION PILLARS

1. **Zero Guesswork & Live Code as SSOT:**
   - Never assume file paths, exports, or database columns exist without empirical verification. Always verify live files on disk before making edits.
2. **Terminal Discipline & Zero Waste:**
   - The shell (`run_command`) is reserved for package installation, compilation/testing (`npm run build`, `tsc --noEmit`, `test`), and targeted repo checks (`git status`, `git ls-files`). Aimless exploratory loops or raw file dumping (`cat`, `Get-Content`) are strictly forbidden.
3. **In-Session Read Cache:**
   - If a file has already been read in this conversation session, reuse working memory; never read the same file repeatedly.
4. **Root-Cause Remediation (Anti-Regression):**
   - Superficial patches are banned. Resolve null pointer risks, CSS overflow bounds, and API failure modes at the architectural root.
5. **2-Stage Verification Gate (Static + Real Runtime) & Cumulative Circuit Breaker:**
   - **Stage 1 (Static):** `npm run build` / `npx tsc --noEmit` must pass with **Exit Code 0** (necessary, never sufficient on its own).
   - **Stage 2 (Real Runtime & E2E):** Start the app/server and verify real behavior:
     - *UI / Full-Stack:* Run Playwright E2E or live browser (`browser` subagent / `browsermcp`) checks: real clicks, form submissions, post-reload persistence, zero `console.error`/`pageerror`, zero unexpected 4xx/5xx network responses, and 375px mobile overflow check.
     - *Backend / API:* Send real HTTP requests (happy path + `400/401/403/422` failure paths) and verify real DB persistence.
     - *CLI / Library / Script:* Execute the actual binary/script with real arguments and fixture inputs, verifying stdout/stderr, generated files, and exit codes (never rely on static `tsc` alone).
     - *Honest Scope:* If runtime/browser verification cannot run in the current environment, explicitly report runtime behavior as `UNVERIFIED` rather than claiming it works.
   - **Cumulative Circuit Breaker (`attempts <= 3`):** If verification fails 3 cumulative times across the task, halt immediately. Do NOT reset the counter when error messages or target files change. Report findings and logs to the user.
6. **Expanded Destructive Command Ban:**
   - The shell must NEVER execute destructive git, package, or filesystem commands (`git reset --hard`, `git clean -fd`, `git checkout -- .`, `git restore .`, `rm -rf`, `DROP TABLE`, `npm install --force`), nor blindly overwrite unread files via `write_file`. Uncommitted user code must never be overwritten.

---

# HERMES ERROR LEARNING MEMORY & SMART CONTEXT

- **4-Step Error Learning Cycle:**
  1. *Symptom:* Concrete error message or runtime stack trace.
  2. *Root Cause:* Underlying architectural or logic failure.
  3. *Permanent Fix:* Side-effect-free remediation.
  4. *Memory Record:* One-sentence actionable lesson logged to `.agent/memory.json` (Max 10 rules).
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
