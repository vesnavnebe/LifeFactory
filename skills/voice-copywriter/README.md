# voice-copywriter

A [skills.sh](https://skills.sh) skill that turns an AI agent into a copywriter that sounds like **you** — not like an AI.

Works across multiple channels (Telegram, YouTube, newsletters) with a self-learning feedback loop that improves over time.

---

## The problem

LLMs forget everything between sessions. Every time you open a new chat, the agent has no idea:
- How you write
- What words you never use
- That you have three channels with different tones
- What you fixed in last week's post

This skill solves that by storing your voice in structured memory files the agent reads every session.

---

## How it works

### Three-tier memory

```
COLD  →  WARM  →  HOT
────────────────────────────────────────────────
Archive     Stable facts    Current session
Feedback    Author profile  Active drafts
TOV counter Channels        Tasks
            Style rules
```

The agent reads them in order at startup: COLD → WARM → HOT → channel file for the current task.

### Three style layers

```
library/            Real texts you've written — the primary voice signal
                    The agent imitates rhythm, transitions, vocabulary directly from these.

TONE_OF_VOICE.md    Universal rules distilled from the library:
                    what's always done, what's never done, formatting rules.
                    Updated every 5 published posts (see below).

channel-{name}.md   Per-channel style guide: tone, structure, characteristic phrases,
                    real post examples, things never written in this channel.
                    Each channel can have a different mode (analytical / diary / curious).
```

**Without the library:** the agent follows rules but sounds generic.
**Without TONE_OF_VOICE:** rules are duplicated or missing across channels.
**Without channel files:** the agent writes everywhere in the same tone.

All three together = text indistinguishable from the original author.

### Self-learning loop

Every time you edit a generated post, the agent logs the change in COLD memory:

```
date | channel | "original phrase" → "revised phrase" | lesson
```

Every 5th text added to the library triggers a **Tone of Voice Review**:

```
Agent reads:  COLD feedback log + library originals
              ↓
Finds:        patterns seen at least twice
              ↓
Proposes:     2–5 new rules for TONE_OF_VOICE.md
              ↓
You say yes → TONE_OF_VOICE updated, counter resets to 0
```

This means the agent gets measurably better every 5 published posts, without any manual work from you.

### Write permissions

The agent has strict rules about what it can and cannot write:

| Permission | Files |
|---|---|
| ✅ Write freely | `ideas-*.md`, `HOT_MEMORY.md`, `scripts/`, `MEMORY.md` (COLD) |
| ✅ Append only | `channel-*.md`, `REFERENCES.md`, `MY_STANCE.md` |
| 🔒 Only on your explicit command | `library/*.md` |
| ❌ Never touch | `WARM_MEMORY.md`, `channels.md`, `TONE_OF_VOICE.md`, config files |

**Why this matters:** without these rules, the agent will gradually overwrite your style files with its own interpretations. After 10 sessions, it's writing in *its* voice, not yours.

---

## File structure

```
your-workspace/
│
├── MEMORY.md                         COLD: feedback log + TOV counter
│
└── memory/
    │
    ├── ideas-{channel}.md            Idea bank per channel (New / In Progress / Published)
    │
    ├── hot/
    │   └── HOT_MEMORY.md             Session drafts and tasks (cleared at end of session)
    │
    ├── warm/
    │   ├── WARM_MEMORY.md            Author profile, channel list, golden rules
    │   ├── channels.md               Channel registry: names, URLs, platforms
    │   ├── channel-{name}.md         Per-channel style guide (one file per channel)
    │   ├── REFERENCES.md             External content saved for inspiration
    │   └── MY_STANCE.md              Author's opinions and positions by topic
    │
    └── author/
        ├── library/                  Original author texts (add on "save to library" command)
        └── tone/
            └── TONE_OF_VOICE.md      Distilled style rules — updated every 5 library additions
```

---

## Setup (step by step)

**1. Install the skill**
```
skills install voice-copywriter
```

**2. Create the memory structure**

Copy the directory layout from above into your agent's workspace. Use the starter templates in `templates/`:

```
templates/
├── WARM_MEMORY.md      → copy to memory/warm/WARM_MEMORY.md
├── TONE_OF_VOICE.md    → copy to author/tone/TONE_OF_VOICE.md
└── MEMORY.md           → copy to MEMORY.md (COLD)
```

**3. Fill in your author profile**

Edit `memory/warm/WARM_MEMORY.md`:
- Your name and handle
- Your channels (name, URL, platform, topics)
- The golden rules you never want broken

**4. Set up your first channel**

Copy `references/channel-template.md` to `memory/warm/channel-{your-channel}.md` and fill in:
- Tone and character
- Post structure
- What's never in your posts
- Characteristic phrases

**5. Add real posts**

This is the most important step. Paste 3–5 of your real posts into the channel file as examples. Then add them to `library/` one by one using the "save to library" command.

**The more originals in the library, the better the style match.**

**6. Set TONE_OF_VOICE baseline**

Fill in `author/tone/TONE_OF_VOICE.md` with the rules you already know about your style. The agent will expand this automatically over time.

---

## Training your agent (ongoing)

| Action | What it does |
|---|---|
| Send a post to the agent | It generates 1–2 variants in your style |
| Edit the output | Change logged in COLD: agent learns what to avoid |
| Say "add to library" | Post saved as training data, TOV counter +1 |
| Every 5th library addition | Agent proposes new style rules based on patterns |
| Say "yes" to the proposal | TONE_OF_VOICE updated, counter resets |

You don't need to maintain anything manually. The system accumulates your preferences through normal use.

---

## Multiple channels

Create one `channel-{name}.md` file per channel. The agent routes automatically:

- **Default:** your main channel — no confirmation needed
- **Clear match:** agent detects the right channel from the topic
- **Ambiguous:** agent asks "Is this for [A] or [B]?"

Each channel can have a completely different tone. Same author voice, different mode.

---

## Skill files in this repo

```
voice-copywriter/
├── SKILL.md                     Main skill file — agent behavior and workflows
├── README.md                    This guide
├── references/
│   ├── memory-structure.md      Detailed memory file map and formats
│   └── channel-template.md      Template for setting up a new channel
└── templates/
    ├── WARM_MEMORY.md           Starter: author profile + golden rules
    ├── TONE_OF_VOICE.md         Starter: global style rules template
    └── MEMORY.md                Starter: COLD memory with TOV counter
```

---

## License

MIT
