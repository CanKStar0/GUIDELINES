---
name: antigravity-guide
description: "Comprehensive guide, quick reference, and sitemap for Google Antigravity (AGY), CLI, IDE, subagents, and background scheduling."
---

# 🚀 Google Antigravity (AGY) Quick Reference & Guide

Google Antigravity (AGY) is an advanced agentic AI coding environment equipped with autonomous subagent delegation, background scheduling, multi-tiered rule hierarchies, and interactive generative UI rendering.

---

## 🛠️ 1. Subagent Orchestration (`invoke_subagent` & `manage_subagents`)

Utilized for complex, multi-step tasks or parallelized research workflows:
- **`define_subagent`:** Programmatically defines a specialized subagent for the conversation duration.
- **`invoke_subagent`:** Launches one or more background subagents concurrently (`Model: "inherit" | "flash" | "pro"`).
- **`manage_subagents`:** Inspects live subagent state (`list`) or cancels tasks (`kill | kill_all`).
- **`send_message`:** Coordinates two-way inter-agent communication.

---

## ⏰ 2. Background Scheduling & Timers (`schedule`)

- **One-Shot Timers:** Dispatches high-priority reminder notifications after a set delay (`DurationSeconds: 300`).
- **Recurring Cron Schedules:** Runs automated health checks, background polling, or recurring status audits (`CronExpression: "*/5 * * * *"`).

---

## 📑 3. Artifact & Generative UI Architecture

- Structured reports, architectural plans, and diagrams are saved in `<appDataDir>\brain\<conversation-id>/` as persistent artifacts.
- The `generative_ui` skill renders interactive HTML/Tailwind widgets directly inline in chat or standalone viewer panels.
