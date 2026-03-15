# The AI Agent Workflow: Obsidian + Linear + OpenClaw

> **Give your AI agent memory, structure, and a voice.**

This is the exact system I use every day. Three tools, one AI agent, and a workflow that actually works — no theory, just the real setup.

📺 **Watch the full video:** [I Connected Obsidian, Linear, and an AI Agent — Here's What Happened](https://youtube.com/@Jason_Cyr)

---

## What This Is

Most AI assistants have no memory. Every conversation starts from zero. You end up pasting context into every prompt, and it doesn't scale.

This system fixes that by connecting three tools through a persistent AI agent:

| Layer | Tool | Purpose |
|-------|------|---------|
| 🧠 **Brain** | [Obsidian](https://obsidian.md) | Shared knowledge base — notes, projects, daily journals |
| ⚡ **Structure** | [Linear](https://linear.app) | Task management — assign work, track progress, close the loop |
| 💬 **Pulse** | [Slack](https://slack.com)* | Real-time communication — ad hoc requests, proactive check-ins |
| 🔗 **Glue** | [OpenClaw](https://openclaw.ai) | The agent platform — persistent identity, memory, tool connections |

The agent reads and writes to your Obsidian vault, picks up tasks from Linear, and communicates through Slack. It doesn't wait to be prompted — it checks in, flags things, and does work.

*\*I use Slack, but OpenClaw supports many communication channels — Discord, Telegram, WhatsApp, Signal, iMessage, and more. Use whichever one you already live in. The system works the same regardless of which channel you pick.*

---

## How It Works

```
┌─────────────────────────────────────────────────────┐
│                    YOU (Human)                       │
│                                                     │
│   Write notes ──► Obsidian ◄── Agent reads/writes   │
│   Create tasks ──► Linear  ◄── Agent picks up work  │
│   Quick chat  ──► Slack    ◄── Agent checks in      │
│                                                     │
│                  ┌──────────┐                        │
│                  │ OpenClaw │  (persistent agent)    │
│                  └──────────┘                        │
└─────────────────────────────────────────────────────┘
```

**The loop in action:**
1. You create a Linear issue: "Write the script for the next YouTube video"
2. Your agent picks it up, checks Obsidian for context (past videos, brand guidelines)
3. It writes a draft, saves it to the project folder in Obsidian
4. Updates the Linear issue to "In Review"
5. Sends you a Slack message: "Script draft is ready"
6. You review, leave notes, and the agent iterates

The whole thing happens across three tools but feels like one workflow.

---

## Prerequisites

- [Obsidian](https://obsidian.md) (free) — desktop app for notes
- [Linear](https://linear.app) (free tier works) — project management
- A messaging platform — Slack, Discord, Telegram, WhatsApp, Signal, or any [OpenClaw-supported channel](https://docs.openclaw.ai)
- [OpenClaw](https://openclaw.ai) — AI agent platform
- An AI model API key (Anthropic Claude recommended)

---

## Step 1: Set Up Obsidian (The Shared Brain)

### Create a Vault

If you don't have one, create a new Obsidian vault. This will be the shared knowledge base between you and your agent.

### Use the PARA Structure

Organize your vault using [PARA](https://fortelabs.com/blog/para/) — Projects, Areas, Resources, Archive:

```
My Vault/
├── 1. Projects/          ← Active projects with deadlines
│   └── Website Redesign/
│       └── PROJECT_CONTEXT.md
├── 2. Areas/             ← Ongoing responsibilities
│   └── Content Creation/
├── 3. Resources/         ← Reference material
│   └── Tools/
├── 4. Archive/           ← Completed/inactive items
├── Daily Notes/          ← Daily journal entries
│   ├── 2026-03-15.md
│   └── 2026-03-14.md
└── AGENTS.md             ← Standing instructions for your agent
```

You don't have to use PARA — any consistent structure works. The key is that your agent can navigate and find things.

### Create AGENTS.md

This is the most important file. It tells your agent how to behave in your vault. Copy the template from [`templates/AGENTS.md`](templates/AGENTS.md) and customize it.

The critical conventions:
- **Write it down.** The agent should never keep "mental notes" — everything goes to a file.
- **Update PROJECT_CONTEXT.md** every time work is done on a project.
- **Daily notes** capture what happened each day.
- **Memory files** persist context across sessions.

### Create a Project Folder

For each active project, create a folder under `1. Projects/` with a `PROJECT_CONTEXT.md` file. This becomes the shared document between you and your agent. See [`templates/PROJECT_CONTEXT.md`](templates/PROJECT_CONTEXT.md) for the template.

---

## Step 2: Set Up OpenClaw (The Agent)

OpenClaw gives your AI agent a persistent identity, memory, and the ability to connect to tools.

### Install OpenClaw

```bash
npm install -g openclaw
```

### Initialize Your Workspace

```bash
openclaw init
```

This creates a workspace with key files:
- `SOUL.md` — Your agent's personality and behavior
- `USER.md` — Information about you (timezone, preferences, etc.)
- `MEMORY.md` — The agent's long-term memory
- `AGENTS.md` — Standing instructions

### Configure Your Agent

Edit `SOUL.md` to define your agent's personality. See [`templates/SOUL.md`](templates/SOUL.md) for a starting point.

Edit `USER.md` with your details. See [`templates/USER.md`](templates/USER.md).

### Connect Your AI Model

```bash
openclaw config set anthropic.apiKey YOUR_API_KEY
```

OpenClaw supports Anthropic Claude, OpenAI, Google Gemini, and more. Claude is recommended for the best agent behavior.

### Give Your Agent Vault Access

Your agent needs to be able to read and write files in your Obsidian vault. Since Obsidian vaults are just folders on your filesystem, this works out of the box — your agent can access the vault path directly.

Set the vault path in your agent's configuration or `TOOLS.md`:

```markdown
### Obsidian Vault
- Path: /path/to/your/obsidian/vault
- System: PARA
- Daily Notes: Daily Notes/YYYY-MM-DD.md
```

---

## Step 3: Connect a Communication Channel (Real-Time Layer)

Your agent needs a real-time way to talk to you — and you to it.

OpenClaw supports multiple channels: **Slack, Discord, Telegram, WhatsApp, Signal, iMessage, IRC, Google Chat, LINE**, and more. Pick whichever one you already use. I chose Slack because it's where I already work, but the system works identically on any channel.

### Set Up Your Channel

Follow the [OpenClaw channels guide](https://docs.openclaw.ai) to connect your preferred channel.

### What You Get (on any channel)

- **DM your agent** for quick questions, brainstorming, ad hoc requests
- **Your agent DMs you** for proactive check-ins, task updates, and nudges
- **Thread-based conversations** keep topics organized (on platforms that support threads)
- **Reactions** for lightweight acknowledgments

### Pro Tips

- Tell your agent to always reply in threads (put this in AGENTS.md)
- Set up proactive check-ins — morning briefings, evening reflections
- Your agent can reference Obsidian notes in any conversation

---

## Step 4: Connect Linear (Structured Work)

Linear turns your agent into a real teammate that picks up work, updates status, and closes the loop.

### Create a Linear Workspace

If you don't have one, [create a Linear workspace](https://linear.app). The free tier works fine to start.

### Install Your Agent as a Linear App

This is the most powerful part. Your agent shows up as a team member in Linear — assignable, mentionable, and responsive.

The setup involves creating a Linear OAuth app, configuring webhooks, and wiring it to your agent. It's not complicated, but there are several steps and they depend on your specific setup.

**The easiest way to set this up:** Ask your OpenClaw agent to do it. It already knows your machine, your setup, and your tools. Just send it this:

```
Help me set up a Linear integration for OpenClaw. I want you to:
- Be assignable as a team member in Linear
- Respond when I @mention you in comments
- Update issue status (In Progress, In Review, Done)
- Post comments on issues with work summaries

Walk me through creating the OAuth app, setting up webhooks, 
and wiring everything together. Do as much of it as you can for me.
```

Your agent will walk you through it step by step — and handle most of the heavy lifting itself. That's the whole point of having an agent.

### The Workflow

Once connected, the workflow is simple:

1. **Create an issue** in Linear with a clear title and description
2. **Assign it to your agent**
3. Your agent moves it to **In Progress** and starts working
4. When done, it moves to **In Review** with a comment explaining what was done
5. You review, leave feedback, and the agent iterates

This creates a paper trail. You can see what's in progress, what's done, what's blocked — just like managing a real team.

### Recommended Status Workflow

```
Backlog → Todo → In Progress → In Review → Done
                  (agent)       (agent)     (you confirm)
```

---

## Step 5: Wire It All Together

The magic isn't in any single tool — it's that they're connected through one agent with persistent memory.

### The Triple-Update Rule

Every time your agent does work, it should update three places:

1. **Linear** — Issue status + comment with what was done
2. **Obsidian** — PROJECT_CONTEXT.md + any artifacts
3. **Slack** — Notification that work is ready for review

Put this in your AGENTS.md so it becomes automatic.

### Memory Conventions

Your agent wakes up fresh each session. These files are its continuity:

- **Daily notes** (`memory/YYYY-MM-DD.md`) — Raw logs of what happened
- **Long-term memory** (`MEMORY.md`) — Curated insights and context
- **Project context** (`PROJECT_CONTEXT.md` per project) — Shared project state

The agent should review and update MEMORY.md periodically, distilling daily notes into lasting knowledge.

### Proactive Check-Ins

Set up your agent to check in a few times a day:

- **Morning:** Calendar, tasks due today, overnight notifications
- **Afternoon:** Progress check, anything blocked?
- **Evening:** Reflection prompt, capture what happened today

This turns your agent from a reactive tool into a proactive teammate.

---

## Templates

All templates are in the [`templates/`](templates/) directory:

| File | Purpose |
|------|---------|
| [`AGENTS.md`](templates/AGENTS.md) | Standing instructions for your agent |
| [`SOUL.md`](templates/SOUL.md) | Agent personality and behavior |
| [`USER.md`](templates/USER.md) | Your profile and preferences |
| [`PROJECT_CONTEXT.md`](templates/PROJECT_CONTEXT.md) | Shared project state document |
| [`DAILY_NOTE.md`](templates/DAILY_NOTE.md) | Daily note template |
| [`MEMORY.md`](templates/MEMORY.md) | Long-term memory starter |

---

## Example: The Full Loop

Here's a real example of the system in action — making this very video:

**Linear:** Created issue "Write video script (10-12 min)" → assigned to agent

**Agent (working):**
1. Reads Obsidian vault for channel context — past video performance, brand guidelines
2. Writes 11-minute script draft
3. Saves to `1. Projects/YouTube Video/VIDEO-SCRIPT.md` in Obsidian
4. Updates Linear issue to "In Review"
5. Sends Slack message: "Script draft is ready"

**Me (reviewing):**
1. Open Obsidian, read the script
2. Leave inline notes (`JC: need more detail here`)
3. Agent sees the notes, makes revisions
4. Updates Linear, notifies via Slack
5. Repeat until done

The whole thing happened across three tools, but it felt like one workflow.

---

## FAQ

**Do I need all three tools?**
You can start with just Obsidian + OpenClaw for the memory layer, and add Linear and Slack as you get comfortable. Each layer adds value independently.

**What AI model should I use?**
Claude (Anthropic) works best for agent behavior — it follows conventions reliably and writes well. But OpenClaw supports multiple providers.

**Is this expensive to run?**
The main cost is the AI model API. For daily use with Claude, expect ~$20-50/month depending on usage. Obsidian is free, Linear has a free tier, Slack has a free tier.

**Can I use Notion instead of Obsidian?**
Yes — any note-taking tool your agent can read/write works. Obsidian is recommended because vaults are local files (easy agent access) and the graph/linking features are powerful.

**Can I use Asana/Jira instead of Linear?**
Any project management tool with an API works in principle. Linear is recommended for its clean API and modern design.

---

## Resources

- [OpenClaw Documentation](https://docs.openclaw.ai)
- [OpenClaw Discord](https://discord.com/invite/clawd)
- [Obsidian](https://obsidian.md)
- [Linear](https://linear.app)
- [My YouTube Channel](https://youtube.com/@Jason_Cyr) — more videos on AI agent workflows

---

## About

Built by [Jason Cyr](https://jasoncyr.ca) — VP Design at Cisco, building AI-augmented workflows.

If this helped you, [subscribe to my channel](https://youtube.com/@Jason_Cyr) for more.
