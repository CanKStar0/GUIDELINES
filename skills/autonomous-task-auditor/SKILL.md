---
name: autonomous-task-auditor
description: "MANDATORY - Must execute view_file on this skill on every task to perform dynamic requirement analysis, deep research, self-auditing, and autonomous self-healing. Dynamic prompt-aware task auditor and quality engine."
---

# 🧠 Autonomous Task Auditor — Dynamic Quality Engine & Self-Healing Loop

This skill completely eliminates AI complacency and premature "done" claims. It dynamically analyzes explicit and implicit requirements from user prompts, investigates global best practices, ruthlessly self-audits generated deliverables, verifies assumptions against **physical code on disk (Disk as SSOT)**, and autonomously resolves defects via **Self-Healing** before presenting work to the user.

---

## ⚡ 1. Core Philosophy: Zero Burden on the User

* **No User-Side Debugging:** The user must never be forced to hunt for edge cases, missing states, or prompt oversights.
* **Generous Reasoning & Research:** Leverage deep thinking, documentation lookups, security audits, and automated verification commands (`npm run build`, `tsc --noEmit`).
* **Disk Verification over Chat Memory:** Old conversation snippets or abandoned prototypes must never be assumed to be live code. Every assumption must be verified empirically via `view_file` or `grep_search` against the file system.

---

## 🔄 2. The 5-Stage Autonomous Loop

```
                       [User Prompt / Goal]
                                 │
                                 ▼
 1. [DYNAMIC INTENT & IMPLICIT REQUIREMENTS ANALYSIS]
    • Uncover unspoken yet essential architectural, resilience, and UX requirements.
                                 │
                                 ▼
 2. [GLOBAL BENCHMARK & DEEP RESEARCH]
    • Identify industry-standard patterns, security vulnerabilities, and accessibility baselines.
                                 │
                                 ▼
 3. [EXHAUSTIVE & PRODUCTION-READY EXECUTION]
    • Zero TODOs, zero fake mocks, zero placeholder architecture.
                                 │
                                 ▼
 4. [RUTHLESS AUDITING & AUTONOMOUS SELF-HEALING]
    • "Where will this break? What edge case crashes this? What state is missing?"
    • Auto-fix all discovered defects behind the scenes BEFORE presenting to user.
                                 │
                                 ▼
 5. [EMPIRICAL VERIFICATION & DELIVERABLE AUDIT CARD]
    • Validate via `build` / `typecheck` commands (Exit Code 0).
```

---

## 🔬 3. Critical Self-Audit Inquiries

Before finalizing any task, evaluate these diagnostic vectors and **fix any gaps immediately**:

### A. Scope & Edge Cases
1. Are all logical boundaries and edge cases handled?
2. How does the system respond to empty data, massive datasets (100k+ rows), or malformed inputs?
3. What is displayed when client/server connectivity drops or an external service times out?

### B. Security & Resilience
1. Are there any untyped inputs, skipped validations, or loose `any` types?
2. Are authentication, authorization (RBAC), and object-level isolation (IDOR protection) strictly enforced?
3. Do error responses leak sensitive database errors, stack traces, or internal server paths?
4. Are rate limits and quota guards in place to prevent resource exhaustion or token depletion?

### C. Design Integrity & User Experience (Anti-AI-Slop)
1. Does the interface honor the project's existing design system, or was a generic template pasted?
2. Are all semantically applicable states (Default, Loading/Skeleton, Empty, Error, Optimistic) implemented?
3. Is horizontal overflow (`overflow-x`) completely eliminated across all screen sizes (320px to 4K)?

---

## 🚪 4. Autonomous Self-Healing Protocol

```
[Defect or Edge Case Discovered During Audit]
                     │
                     ▼
 1. Identify root cause and regression risks.
 2. Edit target files directly (`replace_file_content` / `write_to_file`) without asking the user.
 3. Re-run verification commands (`npm run build`, `npx tsc --noEmit`).
 4. Do NOT deliver the task until all verification gates pass with Exit Code 0.
```

---

## 📋 5. Deliverable Audit Card

Conclude completed tasks with a concise audit summary:

```markdown
### 📋 Autonomous Task Audit Summary
* 🎯 **Dynamic Scope:** Fully satisfied explicit intent and implicit architectural requirements.
* 🛡️ **Security & Resilience:** Strict validation, rate limiting, timeout budgets, and sanitized error masking.
* 🎨 **UI/UX & States:** Conforms to project design tokens and applicable component states.
* 🔧 **Autonomous Fixes:** [List of issues automatically identified and resolved during self-audit].
* ✅ **Empirical Verification:** `npx tsc --noEmit` & `npm run build` (Exit Code 0).
```
