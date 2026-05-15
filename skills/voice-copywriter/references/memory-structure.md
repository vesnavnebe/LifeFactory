# Memory File Structure

## Three-Tier Architecture

The agent's memory is split into three layers. Read them in order each session.

| Tier | File | Purpose | Lifetime |
|------|------|---------|---------|
| **HOT** | `memory/hot/HOT_MEMORY.md` | Active drafts, current session tasks | Session only — clear at end |
| **WARM** | `memory/warm/WARM_MEMORY.md` | Stable facts: author, channels, rules | Long-term — change rarely |
| **COLD** | `MEMORY.md` | Session archive, feedback log | Permanent — append only |

## Full Directory Map

```
{workspace}/
├── MEMORY.md                        COLD: session log + feedback loop
│
└── memory/
    ├── ideas-{channel}.md           Idea bank per channel
    ├── ideas.md                     Navigator across all idea banks
    │
    ├── scripts/
    │   ├── TEMPLATE-script.md       Full video script template
    │   ├── TEMPLATE-shorts.md       Short-form video template
    │   └── YYYY-MM-DD-slug.md       Finished scripts
    │
    ├── hot/
    │   └── HOT_MEMORY.md            Session drafts and tasks
    │
    └── warm/
        ├── WARM_MEMORY.md           Author profile + channels + golden rules
        ├── channels.md              Channel registry (names, URLs, platforms)
        ├── channel-{name}.md        Per-channel style guide (one file per channel)
        ├── REFERENCES.md            External content saved for inspiration
        ├── MY_STANCE.md             Author's opinions and positions by topic
        │
        └── prince/
            ├── library/             Original author texts (add on command only)
            ├── tone/
            │   └── TONE_OF_VOICE.md Global style rules distilled from the library
            └── stance/              Author's long-term strategy and views
```

## What Goes Where — Decision Table

| Incoming content | Route to |
|---|---|
| Author's original published text | `memory/author/library/` (on command) |
| Style feedback ("I never write X") | `memory/warm/channel-{name}.md` (append) |
| External post / article / screenshot | `memory/warm/REFERENCES.md` |
| Author's opinion on a topic | `memory/warm/MY_STANCE.md` |
| Content idea (any channel) | `memory/ideas-{channel}.md` |
| Active draft in progress | `memory/hot/HOT_MEMORY.md` |
| Post approved without edits | Offer to add to `library/` |
| Post approved with edits | Log in `MEMORY.md` COLD |

## MEMORY.md (COLD) Format

```markdown
## Feedback Log
_Format: date | channel | original → revised | lesson_

- 2024-03-01 | main | "This is not magic" → "The mechanism is simple" | avoid metaphors, prefer direct statements

## TOV Counter
- **Posts since TOV review:** 0
- **TOV last updated:** —

_(increment when author adds text to library; at 5 → trigger Tone of Voice Review)_

## Session Archive
- 2024-03-01: Wrote 3 posts for main channel. Author revised tone in post 2 (too casual).
```

## WARM_MEMORY.md Format

```markdown
## Author
- Name, handle, timezone
- Projects and affiliations

## Channels
| File | Channel | Platform | Topics |
|------|---------|----------|--------|

## What Goes Where
(brief routing reminder)

## Golden Rules
- Never publish without approval
- Always offer 1–2 variants
- YouTube: get outline approved before full script
```

## ideas-{channel}.md Format

```markdown
## New Ideas
- [date] Idea title — brief description — format (short/long/video)

## In Progress
- [date] Idea title — started YYYY-MM-DD

## Published
- [date] Idea title — published YYYY-MM-DD
```
