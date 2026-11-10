---
name: master-orchestrator
description: "Master Autonomous Skill Router & Intent Dispatcher. Analyzes incoming user prompts, architectural context, and project goals; automatically loads and coordinates all necessary expert skills."
---

# 👑 Master Orchestrator — Autonomous Skill Router & Intent Dispatcher

Eliminates the friction of manual skill selection. Analyzes incoming user prompts, architectural context, and project goals to **autonomously dispatch required expert skills, enforce lean tool execution (Anti-Thrashing), eliminate stale context hallucinations via tiered hierarchy, and audit deliverables**.

---

## ⚡ 1. SPEED & EFFICIENCY PRINCIPLES

1. **Focused Exploration:** Shell commands are reserved for package management (`npm i`, `pnpm add`), builds (`npm run build`, `tsc`), test suites (`npm test`), and structured repository checks (`git status`, `git ls-files`). Avoid aimless terminal browsing loops.
2. **Context Efficiency:** Do not repeatedly re-read unchanged files. Rely on working memory and inspect only modified or unverified files.
3. **Targeted Reading:** Inspect specific line ranges or targeted symbols rather than blind full-file dumps.
4. **Fast-Track Bounds:** Fast-track applies strictly to single-file, under-15-line trivial cosmetic, typography, or copy adjustments. Never fast-track API, DB, Auth, Payments, or architectural state changes.

---

## ⚡ 2. 4-Tier Smart Context (Zero-Hallucination Tiering)

1. **Tier 1 (Immediate Intent):** Current prompt and immediate 1–2 turn follow-ups. Never scan 50-turn-old raw transcripts.
2. **Tier 2 (Active Project State):** Architectural decisions verified via `implementation_plan.md` or `.agent/roadmap.json`.
3. **Tier 3 (Physical Code as SSOT):** Live files on disk are the sole ground truth. Discard past chat code snippets; verify live code directly.
4. **Tier 4 (On-Demand Skills):** Reference required expert skills as needed for complex architectures.

---

## ⚡ 3. Skill Dispatch Matrix

| Task / Domain | Scope & Focus | Autonomous Skill |
| :--- | :--- | :--- |
| **All Tasks (Core Analysis Kernel)** | Intent Deconstruction, Implicit Requirements, Deep Research, Self-Healing | `autonomous-task-auditor` |
| **All Code Tasks (Execution & QA Kernel)** | Strict Type Safety, Compiler Exit Code 0, i18n Key Parity, Hermes Memory, 4-Pillar QA | `superpowers-execution-harness` |
| **Interface, UI/UX, React, Next.js** | Baseline UI (`h-dvh`, `text-balance`, `tabular-nums`), WCAG 2.2 AA, 3-Era Anti-AI-Slop (67-rule catalog), Anti-Jank Motion | `bespoke-frontend-master` |
| **Design System, Tokens, Surgical Refinement** | Dual-Context (`PRODUCT.md` + `DESIGN.md`), 60-30-10 Palette, 14 Surgical Playbooks (`/distill`, `/clarify`, `/polish`, `/harden`, etc.) | `create-design-md` |
| **Backend, API, Route Handlers** | Zero Happy-Path, Rate Limiting, Idempotency, Quota Guards, Zod DTOs | `resilient-backend-architect` |
| **Database, Schema, ORM, Vectors** | Drizzle/Prisma, pgvector (Gemini: 768, OpenAI: 1536), ACID Transactions, Pooling | `modern-data-engineer` |
| **Payments, Checkout, Orders** | Integer Cent Math, Stripe/İyzico 3DS, Webhook Signatures, State Machine | `ecommerce-payments-engine` |
| **Security, Auth, OWASP, Secrets** | OWASP Top 10, Argon2id, CSRF/XSS Sanitization, Security Headers, RBAC | `fullstack-security-auditor` |
| **SEO, Growth, CRO, Funnel** | Technical SEO, JSON-LD Schema, Core Web Vitals (INP/LCP/CLS), GA4 DataLayer | `seo-growth-architect` |
| **Image Generation, Assets** | Zero Text, 8K Studio Lighting, Floor Shadows, Studio Prompts | `image-generation-studio` |

---

## 🏛️ 4. Execution Workflow

1. **Active Skills Declaration:**
   ```markdown
   > 🛡️ **Devredeki Uzmanlıklar:** `master-orchestrator` + `autonomous-task-auditor` + `superpowers-execution-harness` + [`target-domain-skills`]
   ```
2. **Pre-Flight Tech-Stack Sniffing (Framework Alignment):**
   - In web projects, quickly inspect `package.json` before writing code:
     - **Next.js:** If >= 15, enforce async `await params` and Next 15 caching; if <= 14, preserve sync patterns.
     - **React:** If 19, support `useActionState` and `useOptimistic`; if 18, preserve standard state patterns.
     - **Tailwind CSS:** If v4, configure tokens in CSS via `@theme`; if v3, configure in `tailwind.config.*`.
3. **Architectural Alignment & Execution:**
   - Reference necessary domain skills when dealing with complex patterns.
   - Produce strictly typed, architectural solutions aligned with project guidelines.
4. **Superpowers Verification & Quality Gates:**
   - Enforce Superpowers hard bans: Zero empty mock tests, zero `@ts-ignore` / `any`, zero unverified completion claims, 100% i18n key parity.
   - Run verification commands (`npm run build`, `npx tsc --noEmit`, test suites) ensuring **Exit Code 0**.
   - Perform the 4-Pillar QA audit (Layout overflow, DOM completeness, Assets/images, Runtime errors).
   - If errors occur, auto-heal with root-cause fixes and log lessons to Hermes memory (`.agent/memory.json`).
5. **Deliverable Audit Card:**
   - Conclude with the `Autonomous Task Audit Summary` card.
