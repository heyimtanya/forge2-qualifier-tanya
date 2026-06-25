# Forge 2 · Edition 1 Qualifier — Tanya

A two-agent AI system built for the Forge 2 · Edition 1 online qualifier. OpenClaw (the hands) and Hermes (the brain) are wired through Slack to plan, write, and ship a tiny Trello-style Kanban board — entirely on a free stack.

---

## 🤖 Agents

| Agent | Role | Model |
|-------|------|-------|
| **Hermes** | Orchestrator — plans tasks, holds memory, runs skills autonomously | Groq `openai/gpt-oss-120b` |
| **OpenClaw** | Coding agent — writes code, runs it, reports back in Slack | Groq `llama-3.3-70b-versatile` / Ollama `qwen2.5-coder` |

---

## 🧠 Model Routing

- **Hermes (brain / planning)** → Groq `openai/gpt-oss-120b` — stronger model for decomposing goals and making decisions
- **OpenClaw (hands / execution)** → Ollama `qwen2.5-coder` locally, fallback to Groq `llama-3.3-70b-versatile` — optimised for code generation

All models are free. No paid APIs used.

---

## 🚀 Live URL

> Frontend: [Add after deploying]  
> Backend API: [Add after deploying]

---

## 📦 How to Run Locally

### Prerequisites
- Node.js 22.19+
- PHP 8.2+ and Composer
- Git

### Backend (Laravel API)

```bash
cd backend
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan serve
API runs at http://localhost:8000
Frontend (React + Vite)
Bash
UI runs at http://localhost:5173
🗂️ What the App Does
A Trello-style Kanban board with the following features:
✅ Boards → Lists → Cards (full CRUD)
✅ Move cards between lists
✅ Card details — title and description (editable)
✅ Coloured tags / labels (e.g. bug, design, feature)
✅ Assign a member to a card
✅ Due dates — overdue cards are visually flagged
📁 Repo Structure
forge2-qualifier-tanya/
├── backend/              # Laravel REST API (SQLite)
├── frontend/             # React + Vite UI
├── skills/
│   └── status-report/
│       └── SKILL.md      # Reusable Hermes skill
├── slack-export/         # Slack screenshots and evidence
├── agent-log.md          # Unedited agent chat log
├── ARCHITECTURE.md       # Agent roles, Slack channels, model routing
├── .env.example          # Env vars (no real secrets)
└── README.md
💬 Slack Channel Scheme
Channel
Purpose
#sprint-main
Human talks to Hermes — goals, plans, decisions
#agent-coder
Hermes assigns tasks to OpenClaw — code work happens here
#agent-log
Raw agent activity and autonomous run output
🔑 Environment Variables
See .env.example for the full list. Key variables:
SLACK_BOT_TOKEN=xoxb-...
SLACK_APP_TOKEN=xapp-...
GROQ_API_KEY=...
GEMINI_API_KEY=...
Never commit real tokens. Rotate immediately if accidentally pushed.
🎥 Video Walkthrough
[Add Loom / Drive link here — 60 to 90 seconds]
👩‍💻 Builder
Tanya — CSE student, Pranveer Singh Institute of Technology, Kanpur
GitHub: @heyimtanya
---

Copy the whole thing, paste it into your `README.md`, then:

```bash
git add README.md
git commit -m "init: add README"
git push
