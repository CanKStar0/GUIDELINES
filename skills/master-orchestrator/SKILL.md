---
name: master-orchestrator
description: "Ultra-lean Skill Router. Lists every skill by name and one-line purpose so agents load ONLY relevant SKILL.md files on demand with zero token waste."
---

# 👑 Master Orchestrator — On-Demand Skill Router

> **Token Discipline (SSOT):** Never preload all skills. Match the user's intent to the index below and read **only** the relevant `SKILL.md` file(s) from `~/.gemini/config/skills/<name>/SKILL.md` (or `<GLOBAL_GUIDELINES_ROOT>/skills/<name>/SKILL.md`).

---

## 📋 Skill Index (Name & Purpose Only)

| Skill | Purpose |
| :--- | :--- |
| `autonomous-task-auditor` | Deconstructs implicit requirements, self-audits edge cases, and runs cumulative self-healing loops. |
| `superpowers-execution-harness` | Enforces strict TypeScript (`tsc`), build Exit Code 0, i18n key parity, Hermes memory, and 4-pillar QA. |
| `bespoke-frontend-master` | Enforces Anti-AI-Slop UI (67 rules), semantic tokens, Tailwind v4/Next 15+, WCAG 2.2 AA, and 5-state UI. |
| `create-design-md` | Generates root `PRODUCT.md` + `DESIGN.md` contracts and runs 14 surgical UI refurbishment playbooks. |
| `resilient-backend-architect` | Builds concurrency-safe, rate-limited, idempotent APIs with Zod DTOs, timeouts, and quota guards. |
| `modern-data-engineer` | Designs Drizzle/Prisma schemas, pooled serverless Postgres connections, ACID locks, and `pgvector` RAG. |
| `ecommerce-payments-engine` | Enforces integer-cent math, atomic stock reservation, Stripe/İyzico signed webhooks, and order state machines. |
| `fullstack-security-auditor` | Enforces OWASP Top 10, Auth.js v5/Better-Auth/Argon2id, XSS/CSRF/IDOR defense, headers, and secret hygiene. |
| `seo-growth-architect` | Implements Next.js metadata, JSON-LD Schema, Core Web Vitals, AEO/GEO structure, and typed GA4 DataLayer. |
| `image-generation-studio` | Generates text-free 8K commercial product and hero image prompts with studio lighting and floor shadows. |
| `simple-issue-description` | Converts rough bug reports, PRs, or feature notes into short, behavior-focused plain-language issues. |
| `humanizer` | Strips 26 structural/lexical AI writing tells while preserving facts, voice, and code blocks. |
| `antigravity-guide` | Reference for Antigravity subagent orchestration (`invoke_subagent`), `schedule` timers, and artifacts. |

---

## ⚡ Lean Execution Rules

1. **Declare Active Skills:** Start non-trivial responses with:
   `> 🛡️ **Devredeki Uzmanlıklar:** master-orchestrator + [loaded-skills]`
2. **Pre-Flight Sniffing:** Inspect `package.json` / `tsconfig.json` / `git status` once to align Next.js (`>=15` async `params`), React (`19` `useActionState`), and Tailwind (`v4` `@theme` vs `v3`).
3. **Fast-Track Anti-Evasion:** Fast-track (concise reply, no full audit card) applies **only** to <15-line single-file cosmetic/copy edits or direct Q&A—never to API, DB, Auth, Payments, async data, or state logic.
4. **Tiered Context:** Prioritize current intent + live files on disk (`Tier 3`) over chat history. Never re-read unchanged files.
