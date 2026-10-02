---
name: master-orchestrator
description: "Master Autonomous Skill Router & Intent Dispatcher. Analyzes incoming user prompts, architectural context, and project goals; automatically loads and coordinates all necessary expert skills."
---

# 👑 Master Orchestrator — Autonomous Skill Router & Intent Dispatcher

Eliminates the friction of manual skill selection. Analyzes incoming user prompts, architectural context, and project goals to **autonomously dispatch required expert skills, enforce lean tool execution (Anti-Thrashing), eliminate stale context hallucinations via tiered hierarchy, and audit deliverables**.

---

## ⚡ 1. SPEED, EFFICIENCY & ANTI-THRASHING PRINCIPLES

1. **Terminal Discipline (`run_command` Restriction):**
   - Shell commands are strictly reserved for package management (`npm i`, `pnpm add`), builds (`npm run build`, `tsc`), and test suites (`npm test`).
   - Using terminal commands to search files (`dir`, `ls`, `Get-ChildItem`) or read file contents (`cat`, `type`, `Get-Content`) is STRICTLY PROHIBITED. Use built-in fast tools (`grep_search`, `find_by_name`, `view_file`).
2. **In-Session Read Cache:**
   - If a file has already been read during this conversation session, its content is already present in working memory. Re-reading the same file repeatedly in loops is forbidden.
3. **Targeted Slice Reads:**
   - Avoid blind 800-line full-file dumps. Use `grep_search` to pinpoint the exact code symbol, then load only the relevant line range (`StartLine / EndLine`).
4. **Fast-Track for Minor Edits:**
   - For trivial styling, typo corrections, single-line adjustments, or minor config changes, bypass bulky skill manuals. Edit the target file directly and verify.

---

## 🛑 2. STEP 0: PRE-FLIGHT `view_file` PROTOCOL (NEW / MAJOR WORK)

> ⚠️ **MANDATORY FOR AGENTS:**
> When executing major features or new architectures: if the corresponding skill's `SKILL.md` has **not yet been read in the active session**, the very first tool call before touching code must be `view_file` on that skill's `SKILL.md`. (If already read previously in this session, Rule 1.2 applies: do not re-read).

### 📌 Direct Skill Paths for `view_file`:

| Domain / Expertise | Absolute File Path for `view_file` |
| :--- | :--- |
| **🧠 Dynamic Task Auditor** | `C:\Users\canpo\.gemini\config\skills\autonomous-task-auditor\SKILL.md` |
| **🎨 Bespoke Frontend UI/UX** | `C:\Users\canpo\.gemini\config\skills\bespoke-frontend-master\SKILL.md` |
| **📐 Design System & Audit** | `C:\Users\canpo\.gemini\config\skills\create-design-md\SKILL.md` |
| **🏗️ Resilient Backend Architect** | `C:\Users\canpo\.gemini\config\skills\resilient-backend-architect\SKILL.md` |
| **🗄️ Modern Data & Vector** | `C:\Users\canpo\.gemini\config\skills\modern-data-engineer\SKILL.md` |
| **🛒 E-Commerce & Payments** | `C:\Users\canpo\.gemini\config\skills\ecommerce-payments-engine\SKILL.md` |
| **🛡️ Fullstack Security Auditor** | `C:\Users\canpo\.gemini\config\skills\fullstack-security-auditor\SKILL.md` |
| **🔍 SEO & Growth Architect** | `C:\Users\canpo\.gemini\config\skills\seo-growth-architect\SKILL.md` |
| **🚀 Superpowers Harness & QA** | `C:\Users\canpo\.gemini\config\skills\superpowers-execution-harness\SKILL.md` |
| **📸 Image Generation Studio** | `C:\Users\canpo\.gemini\config\skills\image-generation-studio\SKILL.md` |
| **🚀 Antigravity Guide** | `C:\Users\canpo\.gemini\config\skills\antigravity-guide\SKILL.md` |

---

## ⚡ 3. 4-Tier Smart Context (Zero-Hallucination Tiering)

1. **Tier 1 (Immediate Intent):** Current prompt and immediate 1–2 turn follow-ups. Never scan 50-turn-old raw transcripts.
2. **Tier 2 (Active Project State):** Architectural decisions verified via `output/roadmap.json` or `implementation_plan.md`.
3. **Tier 3 (Physical Code as SSOT):** Live files on disk are the sole ground truth. Discard past chat code snippets; verify live code via `view_file` / `grep_search`.
4. **Tier 4 (On-Demand Skills):** Load required expert skills via `view_file` only when needed.

---

## ⚡ 4. Skill Dispatch Matrix

| Task / Domain | Scope & Focus | Autonomous Skill |
| :--- | :--- | :--- |
| **All Tasks (Unconditional)** | Intent Deconstruction, Implicit Requirements, Deep Research, Self-Healing | `autonomous-task-auditor` + `superpowers-execution-harness` |
| **Interface, UI/UX, React, Next.js** | Baseline UI (`h-dvh`, `text-balance`, `tabular-nums`), WCAG A11y, Anti-Jank Motion, Anti-AI-Slop | `bespoke-frontend-master` |
| **Design System, Tokens, UI Audit** | Generating/Updating `DESIGN.md`, 60-30-10 Palette, UI Audit & Handoff Plans | `create-design-md` |
| **Backend, API, Route Handlers** | Zero Happy-Path, Rate Limiting, Idempotency, Quota Guards, Zod DTOs | `resilient-backend-architect` |
| **Database, Schema, ORM, Vectors** | Drizzle/Prisma, pgvector Embeddings, ACID Transactions, Connection Pooling | `modern-data-engineer` |
| **Payments, Checkout, Orders** | Integer Cent Math, Stripe/İyzico 3DS, Webhook Signatures, State Machine | `ecommerce-payments-engine` |
| **Security, Auth, OWASP, Secrets** | OWASP Top 10, Argon2id, CSRF/XSS Sanitization, Security Headers, RBAC | `fullstack-security-auditor` |
| **SEO, Growth, CRO, Funnel** | Technical SEO, JSON-LD Schema, Core Web Vitals, AIDA Copy, GA4 DataLayer | `seo-growth-architect` |
| **Image Generation, Assets** | Zero Text, 8K Studio Lighting, Floor Shadows, `generate_image` | `image-generation-studio` |

---

## 🏛️ 5. Execution Workflow

1. **Active Skills Declaration:**
   ```markdown
   > 🛡️ **Active Skills:** `master-orchestrator` + `autonomous-task-auditor` + [`target-domain-skills`]
   ```
2. **Lean Ingestion:**
   - Ingest unread skills via `view_file`. Reuse cached memory if previously read.
3. **Dynamic Execution:**
   - Produce strictly typed, architectural solutions aligned with project guidelines.
4. **Self-Healing & Verification:**
   - Auto-fix any discovered defects; verify with build/typecheck commands (`npm run build`, `tsc --noEmit`).
5. **Deliverable Audit Card:**
   - Conclude with the `Autonomous Task Audit Summary` card.
