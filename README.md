# 🐾 PocketPaw

> **Hi, I'm PocketPaw! The AI agent that lives on YOUR laptop, not some corporate datacenter.**

[![PyPI version](https://img.shields.io/pypi/v/pocketpaw.svg)](https://pypi.org/project/pocketpaw/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Downloads](https://img.shields.io/pypi/dm/pocketpaw.svg)](https://pypi.org/project/pocketpaw/)

```bash
pip install pocketpaw && pocketpaw
```

**That's it.** One command. 30 seconds. Your own AI agent.

I'm your self-hosted, cross-platform personal AI agent. The **web dashboard** opens automatically — talk to me right in your browser, or connect me to **Discord**, **Slack**, **WhatsApp**, or **Telegram** and control me from anywhere. I run on _your_ machine, respect _your_ privacy, and I'm always here.

**No subscription. No cloud lock-in. Just you and me.**

---

## 🎬 What Can I Do?

```
You: "Find all the PDFs in my Downloads and organize them by date"
Me:  *runs commands, moves files around*
Me:  "Done! I moved 23 PDFs into dated folders. Your Downloads is clean now!"

You: "Go to GitHub and star the PocketPaw repo"
Me:  *opens browser, navigates, clicks star*
Me:  "Starred! Thanks for the support 🐾"

You: "What's eating up my disk space?"
Me:  *analyzes filesystem*
Me:  "Found it! You have 47GB of node_modules. Want me to clean them up?"
```

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🖥️ **Web Dashboard** | Browser-based control panel — the default mode, no setup needed |
| 💬 **Multi-Channel** | Discord, Slack, WhatsApp (Personal + Business), Telegram — run any combo |
| 🤖 **Claude Agent SDK** | Default backend — official Claude SDK with built-in tools (Bash, Read, Write) |
| 🧠 **Smart Model Router** | Auto-selects Haiku / Sonnet / Opus based on task complexity |
| 🔧 **Tool Policy** | Fine-grained allow/deny control over which tools the agent can use |
| 📋 **Plan Mode** | Require approval before the agent runs shell commands or edits files |
| 🌐 **Browser Control** | Browse the web, fill forms, click buttons via accessibility tree |
| 📧 **Gmail Integration** | Search, read, and send emails via OAuth (no app passwords) |
| 📅 **Calendar Integration** | List events, create meetings, meeting prep briefings |
| 🔍 **Web Search & Research** | Tavily/Brave search + multi-step research with source synthesis |
| 🎨 **Image Generation** | Google Gemini image generation, saved locally |
| 🔊 **Voice / TTS** | Text-to-speech via OpenAI or ElevenLabs |
| 🧠 **Memory & Compaction** | Long-term facts + session history with smart compaction |
| ⏰ **Cron Scheduler** | Recurring reminders with natural language time parsing |
| 🛡️ **Security Suite** | Injection scanner, audit CLI, Guardian AI, self-audit daemon |
| 🔒 **Local-First** | Runs on YOUR machine — your data never leaves your computer |
| 🖥️ **Cross-Platform** | macOS, Windows, Linux |
| 🧩 **Skill System** | Create reusable agent skills at runtime |
| 🤝 **Task Delegation** | Delegate complex sub-tasks to Claude Code CLI |

---

## 🚀 One-Command Install

### Option 1: pip (Recommended)
```bash
pip install pocketpaw
pocketpaw
```

### Option 2: pipx (Isolated Install)
```bash
pipx install pocketpaw
pocketpaw
```

### Option 3: uvx (Run Without Installing)
```bash
uvx pocketpaw
```

### Option 4: From Source
```bash
git clone https://github.com/pocketpaw/pocketpaw.git
cd pocketpaw
uv run pocketpaw
```

**That's it!** No Docker. No config files. No YAML. No dependency hell.

I'll automatically:
1. Set up everything I need
2. Open the web dashboard in your browser
3. Be ready to help in 30 seconds!

---

## 🖥️ Web Dashboard

The browser-based dashboard is the default mode — just run `pocketpaw` and it opens at `http://localhost:8888`.

**What you get:**
- Real-time streaming chat via WebSocket
- Activity panel showing tool calls, thinking, and system events
- Settings panel for LLM, backend, and tool policy configuration
- **Channel management** — configure, start, and stop Discord/Slack/WhatsApp/Telegram from the sidebar
- Plan Mode approval modal for reviewing tool calls before execution

### Channel Management

All configured channel adapters auto-start on launch. Use the sidebar "Channels" button to:
- Configure tokens and credentials per channel
- Start/stop adapters dynamically
- See running status at a glance

Headless mode is also available for running without the dashboard:

```bash
uv run pocketpaw --discord              # Discord only
uv run pocketpaw --slack                # Slack only
uv run pocketpaw --whatsapp             # WhatsApp only
uv run pocketpaw --discord --slack      # Multiple channels
uv run pocketpaw --telegram             # Legacy Telegram mode
```

See [Channel Adapters documentation](documentation/features/channels.md) for full setup guides.

---

## 🌐 Browser Superpowers

I can control a web browser for you! I see pages as a semantic tree and can:

- **Navigate** to any URL
- **Click** buttons and links
- **Type** into forms
- **Scroll** through pages
- **Take screenshots**

```
You: "Log into my GitHub and check my notifications"
Me:  *navigates to GitHub, sees login form*
Me:  "I see the login page. I found: textbox [ref=1], password field [ref=2],
      and Sign In button [ref=3]. Should I proceed?"
```

I use your existing Chrome if you have it — no extra downloads. If you don't have Chrome, I'll download a small browser automatically on first use.

---

## 🤖 Agent Backends

### Claude Agent SDK (Default, Recommended)

Uses Anthropic's official Claude Agent SDK with built-in tools (Bash, Read, Write, Edit, Glob, Grep, WebSearch). Supports `PreToolUse` hooks for dangerous command blocking.

### PocketPaw Native

Custom orchestrator: Anthropic SDK for reasoning + Open Interpreter for code execution.

### Open Interpreter

Standalone Open Interpreter supporting Ollama, OpenAI, or Anthropic as the LLM provider. Good for fully local setups with Ollama.

Switch anytime in settings or config!

---

## 🧠 Memory System

I can remember things about you across conversations!

```
You: "Remember that I prefer dark mode and my project is called PocketClaw"
Me:  "Got it! I'll remember your preference for dark mode and that you're
      working on PocketClaw."

[Next day...]

You: "What project am I working on?"
Me:  "You're working on PocketClaw!"
```

### File-based Memory (Default)
Stores memories as readable markdown in `~/.pocketclaw/memory/`:
- `MEMORY.md` — Long-term facts about you
- `sessions/` — Conversation history with smart compaction

### Session Compaction

Long conversations are automatically compacted to stay within budget:
- **Recent messages** kept verbatim (configurable window)
- **Older messages** compressed to one-liner extracts (Tier 1) or LLM summaries (Tier 2, opt-in)

### USER.md Profile

PocketPaw creates identity files at `~/.pocketclaw/identity/` including `USER.md` — a profile loaded into every conversation so the agent knows your preferences.

### Optional: Mem0 (Semantic Memory)
For smarter memory with vector search and automatic fact extraction:

```bash
pip install pocketpaw[memory]
```

See [Memory documentation](documentation/features/memory.md) for details.

---

## ⚙️ Configuration

I store my config in `~/.pocketclaw/config.json`:

```json
{
  "agent_backend": "claude_agent_sdk",
  "anthropic_api_key": "sk-ant-...",
  "anthropic_model": "claude-sonnet-4-5-20250929",
  "tool_profile": "full",
  "memory_backend": "file",
  "smart_routing_enabled": false,
  "plan_mode": false,
  "injection_scan_enabled": true,
  "self_audit_enabled": true,
  "web_search_provider": "tavily",
  "tts_provider": "openai"
}
```

Or use environment variables (all prefixed with `POCKETCLAW_`):

```bash
# Core
export POCKETCLAW_ANTHROPIC_API_KEY="sk-ant-..."
export POCKETCLAW_AGENT_BACKEND="claude_agent_sdk"

# Channels
export POCKETCLAW_DISCORD_BOT_TOKEN="..."
export POCKETCLAW_SLACK_BOT_TOKEN="xoxb-..."
export POCKETCLAW_SLACK_APP_TOKEN="xapp-..."

# Integrations
export POCKETCLAW_GOOGLE_OAUTH_CLIENT_ID="..."
export POCKETCLAW_GOOGLE_OAUTH_CLIENT_SECRET="..."
export POCKETCLAW_TAVILY_API_KEY="..."
export POCKETCLAW_GOOGLE_API_KEY="..."
```

See the [full configuration reference](documentation/features/) for all available settings.

---

## 🔐 Security

I take your safety seriously:

- **Guardian AI** — Secondary LLM safety check before running dangerous commands
- **Injection Scanner** — Two-tier detection (regex heuristics + optional LLM deep scan) blocks prompt injection attacks
- **Tool Policy** — Restrict agent tool access with profiles (`minimal`, `coding`, `full`) and allow/deny lists
- **Plan Mode** — Require human approval before executing shell commands or file edits
- **Security Audit CLI** — Run `pocketpaw --security-audit` to check 7 security aspects (config permissions, API key exposure, audit log, etc.)
- **Self-Audit Daemon** — Daily automated health checks (12 checks) with JSON reports at `~/.pocketclaw/audit_reports/`
- **Audit Logging** — Append-only log at `~/.pocketclaw/audit.jsonl`
- **Single User Lock** — Only authorized users can control the agent
- **File Jail** — Operations restricted to allowed directories
- **Local LLM Option** — Use Ollama and never phone home

See [Security documentation](documentation/features/security.md) for details.

---

## 🧑‍💻 Development

Want to make me better? Here's how:

```bash
# Clone
git clone https://github.com/pocketpaw/pocketpaw.git
cd pocketpaw

# Install with dev tools
uv sync --dev

# Run my tests
uv run pytest

# Check my code style
uv run ruff check .

# Format
uv run ruff format .
```

### Optional Extras

```bash
pip install pocketpaw[discord]             # Discord support
pip install pocketpaw[slack]               # Slack support
pip install pocketpaw[whatsapp-personal]   # WhatsApp Personal (QR scan)
pip install pocketpaw[image]               # Image generation (Google Gemini)
pip install pocketpaw[memory]              # Mem0 semantic memory
```

---

## 📖 Documentation

Full documentation lives in [`documentation/`](documentation/README.md):

- [Channel Adapters](documentation/features/channels.md) — Discord, Slack, WhatsApp, Telegram setup
- [Tool Policy](documentation/features/tool-policy.md) — Profiles, groups, allow/deny
- [Web Dashboard](documentation/features/web-dashboard.md) — Browser UI overview
- [Security](documentation/features/security.md) — Injection scanner, audit CLI, audit logging
- [Model Router](documentation/features/model-router.md) — Smart complexity-based model selection
- [Plan Mode](documentation/features/plan-mode.md) — Approval workflow for tool execution
- [Integrations](documentation/features/integrations.md) — OAuth, Gmail, Calendar
- [Tools](documentation/features/tools.md) — Web search, research, image gen, voice, delegation, skills
- [Memory](documentation/features/memory.md) — Session compaction, USER.md profile
- [Scheduler](documentation/features/scheduler.md) — Cron scheduler, self-audit daemon

---

## 🤝 Join the Pack

- 🐦 Twitter: [@PocketPawAI](https://twitter.com/PocketPawAI)
- 💬 Discord: [Coming Soon]
- 📧 Email: hello@pocketpaw.ai

PRs welcome! Let's build the future of personal AI together.

---

## 📄 License

MIT © PocketPaw Team

---

<p align="center">
  <b>🐾 Made with love for humans who want AI on their own terms 🐾</b>
</p>
