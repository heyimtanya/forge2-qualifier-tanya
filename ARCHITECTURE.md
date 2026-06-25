# Architecture — Forge 2 · Edition 1 Qualifier

## 🧠 Agent Roles

| Agent | Type | Responsibility |
|-------|------|---------------|
| **Hermes** | Brain / Orchestrator | Receives goals from human in `#sprint-main`, decomposes into tasks, holds memory across sessions, runs the status-report skill, posts autonomous updates |
| **OpenClaw** | Hands / Coder | Receives coding tasks in `#agent-coder`, writes and runs code, reports back with What I Did / What's Left / What Needs Your Call |

---

## 🔁 The Loop
Human (you)
↓  posts goal in #sprint-main
Hermes
↓  posts plan + task breakdown
Hermes
↓  assigns task to OpenClaw in #agent-coder
OpenClaw
↓  writes code, runs it, reports back
Human (you)
↓  reviews, approves or corrects
↑  loop continues

No agent works in private DMs. Everything is visible in channels.

---

## 💬 Slack Channel Scheme

| Channel | Who posts | What lands here |
|---------|-----------|-----------------|
| `#sprint-main` | Human + Hermes | Goals, plans, decisions, status updates |
| `#agent-coder` | Hermes + OpenClaw | Task assignments, code output, reports |
| `#agent-log` | Both agents | Raw activity, autonomous run output, audit trail |

---

## 🧠 Model Routing

| Agent | Provider | Model | Reason |
|-------|----------|-------|--------|
| Hermes | Groq | `openai/gpt-oss-120b` | Stronger model needed for planning, memory, and decision-making |
| OpenClaw | Ollama (local) | `qwen2.5-coder` | Unlimited, offline, optimised for code generation |
| OpenClaw (fallback) | Groq | `llama-3.3-70b-versatile` | Fallback if Ollama is slow or unavailable |

**Fallback ladder on rate limit (429):** Groq → Gemini `gemini-2.5-flash` → OpenRouter `:free` → Ollama

---

## 🗂️ Skill

One reusable skill committed at `skills/status-report/SKILL.md`.  
Fires automatically when Hermes is asked for a status update — structured as:
- **What I Did**
- **What's Left**
- **What Needs Your Call**

---

## 🏗️ App Architecture
- Backend exposes a REST API for Boards, Lists, Cards, Tags, Members
- Frontend consumes the API and renders the Kanban UI
- SQLite used as the database — zero server setup required

---

*Forge 2 · Edition 1 · NMG Labs · June 2026*
