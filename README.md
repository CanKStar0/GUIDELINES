# 🧠 GUIDELINES: Universal AI Agent Constitution & Skill Hub

<p align="center">
  <a href="https://findfreeapi.com" target="_blank" rel="noopener noreferrer">
    <img src="https://findfreeapi.com/api/badge/developer?style=flat" alt="FreeAPI Verified Developer" />
  </a>
  <a href="https://findfreeapi.com" target="_blank" rel="noopener noreferrer">
    <img src="https://findfreeapi.com/api/badge/directory?style=flat" alt="FreeAPI Directory" />
  </a>
  <img src="https://img.shields.io/badge/Antigravity-Supported-4285F4?logo=google&logoColor=white" alt="Antigravity" />
  <img src="https://img.shields.io/badge/Cursor-Compatible-000000?logo=cursor&logoColor=white" alt="Cursor" />
  <img src="https://img.shields.io/badge/Claude_Code-Ready-D97706?logo=anthropic&logoColor=white" alt="Claude Code" />
  <img src="https://img.shields.io/badge/OpenAI_Codex-Compliant-10A37F?logo=openai&logoColor=white" alt="Codex" />
  <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License MIT" />
</p>

> **Single Source of Truth (SSOT), Cross-Platform, and Tool-Agnostic AI Agent Constitution & Skill Library.**
>
> Equip any coding assistant (**Cursor, Claude Code, Antigravity, GitHub Copilot, OpenAI Codex**) with a battle-tested Principal Software Architect persona and specialized on-demand skills—**with zero project-level configuration bloat**.

---

## 🏛️ Architecture & Philosophy: The Zero-Pollution Mandate

Traditional agent workflows clutter project repositories with redundant configuration folders (`.cursor/rules/`, `.agents/skills/`, `.vscode/`, `.github/copilot-instructions.md`, etc.), creating tech debt and documentation debt.

**GUIDELINES** enforces a strict, clean architectural pattern:

1. **Single Source of Truth (SSOT):** All rules, engineering standards, and modular capabilities reside centrally in this single repository.
2. **Zero In-Project Pollution:** No local skill folders or repetitive rule sets are ever copied or committed into client repositories.
3. **Single-File Bridge (`AGENTS.md`):** A single, declarative `AGENTS.md` file placed at the client project root links the verified tech stack to the central capabilities dynamically.
4. **Cross-Platform & Tool-Agnostic:** Operates seamlessly across **Windows, macOS, and Linux**, directly supporting **Cursor, Claude Code, Antigravity, OpenAI Codex, and Windsurf**.

---

## 📂 Directory Structure

```text
GUIDELINES/
├── MASTER_AGENT_CONSTITUTION.md       # Core AI Constitution, System Persona & Execution Disciplines
├── PROJECT_AGENT_TEMPLATE.md          # Universal, cross-platform AGENTS.md template for projects
├── PROJECT_AGENT_GENERATOR_PROMPT.txt # Read-only prompt to inspect stacks and auto-generate AGENTS.md
├── skills/                            # On-Demand Specialized Engineering Skills
│   ├── master-orchestrator/           # Intent router & multi-skill orchestration engine
│   ├── bespoke-frontend-master/       # Bespoke design tokens, anti-AI-slop UI, a11y & motion
│   ├── resilient-backend-architect/   # Concurrency safety, rate limiting, idempotency & Zod contracts
│   ├── modern-data-engineer/          # Drizzle ORM, Prisma, PostgreSQL, pgvector & migrations
│   ├── fullstack-security-auditor/    # OWASP Top 10, Auth/RBAC, sanitization & DevSecOps
│   ├── ecommerce-payments-engine/     # Integer cent math, Stripe, Iyzico & order state machines
│   ├── seo-growth-architect/          # Technical SEO, JSON-LD schemas, Core Web Vitals & analytics
│   ├── autonomous-task-auditor/       # Autonomous research, dynamic self-auditing & self-healing
│   ├── superpowers-execution-harness/ # Multi-language i18n, 4-pillar QA auditing & verification gates
│   ├── create-design-md/              # 60-30-10 palettes, typography scales & DESIGN.md generation
│   ├── image-generation-studio/       # Text-free studio lighting asset generation directives
│   └── antigravity-guide/             # Antigravity CLI, subagents & background task orchestration
└── README.md
```

---

## 🧩 Specialized Skills Catalog

| Skill | Domain & Key Responsibilities |
| :--- | :--- |
| **`master-orchestrator`** | Analyzes user prompt intent, automatically determines architectural requirements, and coordinates skill loading order. |
| **`bespoke-frontend-master`** | Rejects generic "AI slop" templates; enforces project-specific visual identity, semantic tokens, micro-interactions, and accessibility contracts. |
| **`resilient-backend-architect`** | Builds fault-tolerant, concurrency-safe, idempotent, rate-limited APIs with strict Zod schema validation. |
| **`modern-data-engineer`** | Designs production schemas with Drizzle ORM / Prisma, PostgreSQL indexing, migration safety, and pgvector pipelines. |
| **`fullstack-security-auditor`** | Inspects OWASP Top 10 vulnerabilities, session/JWT lifecycles, RBAC authorization gates, and sensitive secret hygiene. |
| **`ecommerce-payments-engine`** | Enforces integer cent math (preventing float precision loss), Stripe/Iyzico gateways, cart calculation, and reservation lifecycles. |
| **`seo-growth-architect`** | Audits Core Web Vitals, builds Schema.org JSON-LD structured data, dynamic OpenGraph assets, and crawl budgets. |
| **`autonomous-task-auditor`** | Independently verifies live file changes against implementation goals and triggers autonomous self-healing upon errors. |
| **`superpowers-execution-harness`** | Governs multi-language i18n completeness, strict type checking, and empirical compiler/test verification gates. |
| **`create-design-md`** | Bootstraps a comprehensive, accessible design token contract (`DESIGN.md`) using the 60-30-10 color rule. |
| **`image-generation-studio`** | Generates prompt matrices for commercial studio renders, clean floor shadows, and isolated product photography (zero text). |
| **`antigravity-guide`** | Reference manual for Google Antigravity, subagent delegation, and background daemon scheduling. |

---

## 🚀 Quick Start Guide

### 1. Clone the Central Hub
Clone this repository to a persistent local directory on your machine:

```bash
# Windows
git clone https://github.com/CanKStar0/GUIDELINES.git C:/GUIDELINES

# macOS / Linux
git clone https://github.com/CanKStar0/GUIDELINES.git ~/GUIDELINES
```

---

### 2. Connect Your Project (Zero Bloat)

Copy [PROJECT_AGENT_TEMPLATE.md](./PROJECT_AGENT_TEMPLATE.md) into your project root as **`AGENTS.md`**:

```markdown
# Developer Instructions (Project AI Constitution)

<!-- DCM_GLOBAL_GUIDELINES_ROOT: /path/to/GUIDELINES -->

## 📌 Scope & Project Definition
- **Project:** MyAwesomeProject
- **Root:** /path/to/project
- **Objective:** Production-grade web application

## 🏛️ Central Reference & Single Source of Truth
- **Master Constitution:** <GLOBAL_GUIDELINES_ROOT>/MASTER_AGENT_CONSTITUTION.md
- **Global Skills:** <GLOBAL_GUIDELINES_ROOT>/skills/

### Active Project Skills:
- Frontend & UI ➔ <GLOBAL_GUIDELINES_ROOT>/skills/bespoke-frontend-master/SKILL.md
- Backend & API ➔ <GLOBAL_GUIDELINES_ROOT>/skills/resilient-backend-architect/SKILL.md
- Security      ➔ <GLOBAL_GUIDELINES_ROOT>/skills/fullstack-security-auditor/SKILL.md
```

*(Alternatively, run the [PROJECT_AGENT_GENERATOR_PROMPT.txt](./PROJECT_AGENT_GENERATOR_PROMPT.txt) prompt in your AI tool to automatically inspect the tech stack and generate this file in 5 seconds).*

---

### 3. Tool Compatibility Matrix

* **Antigravity / Gemini CLI:** Automatically discovers `AGENTS.md` at root and applies the persona and skills.
* **Cursor:** Reads root `AGENTS.md` natively as the project-wide system instruction.
* **Claude Code:** Automatically indexes `AGENTS.md` on startup as project context.
* **GitHub Copilot / OpenAI Codex:** Uses `AGENTS.md` as the open-standard context baseline.

---

## 🌐 Developer Ecosystem & Live Free APIs

When prototyping or bootstrapping full-stack apps with your AI agents, utilize the [FindFreeAPI.com](https://findfreeapi.com) open infrastructure:

- **500+ Curated Public REST APIs:** [findfreeapi.com/explorer](https://findfreeapi.com/explorer)
- **Zero-Authentication Filter:** Instant access to APIs that require no API keys or setup.
- **Dynamic Status Badges:** Generate live SVG status badges at [findfreeapi.com/badge](https://findfreeapi.com/badge).

---

## 📄 License

Distributed under the [MIT License](LICENSE).
