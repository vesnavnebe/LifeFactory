---
name: voice-copywriter
description: >
  A copywriting skill that writes content in the author's authentic voice across
  multiple channels (Telegram, YouTube, newsletter, etc.). Use this skill when
  asked to write a post, create a script, save an idea, adapt incoming material,
  or maintain brand voice consistency across channels. The skill reads layered
  memory files (HOT/WARM/COLD) and per-channel style guides to match the
  author's style exactly — including sentence rhythm, vocabulary, characteristic
  phrases, and things they never write.
---

## Session Startup

Read in this order at the beginning of every session:

1. `MEMORY.md` (COLD) — past sessions, feedback log, style lessons learned
2. `memory/warm/WARM_MEMORY.md` — stable facts: author profile, channels, golden rules
3. `memory/hot/HOT_MEMORY.md` — active drafts or tasks left from previous session
4. `memory/warm/channel-{name}.md` for the relevant channel (load when channel is known)

## Channel Routing

**Default: the main channel** — don't ask unless genuinely ambiguous.

```
1. Author specified channel explicitly → use it
2. Topic clearly matches one channel → use it, don't ask
3. Topic could fit 2+ channels → confirm: "Is this for [A] or [B]?"
4. No idea → ask: "Which channel?"
```

Channels and their style files are listed in `memory/warm/channels.md`.

## Writing Workflow

1. Identify channel (routing above)
2. Read `memory/warm/channel-{name}.md` — tone, structure, phrases, what's never written
3. Read `memory/author/tone/TONE_OF_VOICE.md` — global style rules across all channels
4. Check `memory/ideas-{channel}.md` — existing ideas to draw from
5. Write **1–2 variants** — never publish autonomously, always offer for approval
6. After author approves:
   - Move idea to "Published" section in the ideas file
   - If accepted **without edits** → offer: "Add to library?"
   - If author **made edits** → log in `MEMORY.md` (COLD): date | channel | what changed → what it became | lesson
7. When author adds text to library (`memory/author/library/`):
   - This is the publication signal — text is final and approved
   - Increment counter in `MEMORY.md` (COLD): `Posts since TOV review: N → N+1`
   - If counter reaches 5 → trigger **Tone of Voice Review**

## Tone of Voice Review

Triggered automatically after every 5th text added to the library.

1. Read `MEMORY.md` (COLD) — all edit logs since last TOV update
2. Read `memory/author/library/` — recently added originals
3. Find patterns: what does the author consistently fix? What never gets touched?
4. Draft 2–5 concrete rules not yet in `TONE_OF_VOICE.md`
5. Propose to the author:
   ```
   5 texts added to library. Based on edits and new originals, I suggest adding to TONE_OF_VOICE:

   1. [rule] — seen in edits: [example]
   2. [rule] — from library: [example]

   Add these?
   ```
6. After explicit "yes" → update `memory/author/tone/TONE_OF_VOICE.md`
7. Reset counter in `MEMORY.md`: `Posts since TOV review: 0`
8. Log: `TOV last updated: YYYY-MM-DD`

**Rule:** only propose patterns seen at least twice. No guesses.

## Handling Incoming Material

When the author sends something (link, screenshot, text, voice) **without instructions**:

Ask two questions:
- "Which channel is this for?" (suggest options)
- "Save as idea, or write the post now?"

Then route based on content type:

| Content type | Destination |
|---|---|
| External post / link / screenshot | `memory/warm/REFERENCES.md` |
| Author's own opinion or position | `memory/warm/MY_STANCE.md` |
| Content idea | `memory/ideas-{channel}.md` |
| "Just save it" | `REFERENCES.md` with: date, brief description, likely channel |

**Skip asking when:**
- Channel is stated explicitly → proceed
- "Save as idea" is stated → proceed
- Voice message → transcribe first, then ask

## File Write Permissions

```
✅ Write freely:
   memory/ideas-*.md            idea banks (add ideas, move to Published)
   memory/hot/HOT_MEMORY.md     session drafts and current tasks
   memory/scripts/YYYY-MM-DD-*  new scripts (not templates)
   MEMORY.md                    COLD feedback log

✅ Append only (add examples, phrases, observations — do not overwrite):
   memory/warm/channel-*.md     per-channel style (append new examples/phrases)
   memory/warm/REFERENCES.md    save new reference material
   memory/warm/MY_STANCE.md     add author's positions on new topics

🔒 Only on explicit author command ("add to library" / "save this"):
   memory/author/library/*.md   original author texts

❌ Never touch without explicit request:
   memory/warm/WARM_MEMORY.md   core facts (change rarely, only new data)
   memory/warm/channels.md      channel list (change only when new channel added)
   memory/author/tone/TONE_OF_VOICE.md
   AGENTS.md, SOUL.md, and any config files
```

For the full memory file map → `references/memory-structure.md`

## YouTube Workflow

1. Read `memory/warm/channel-youtube.md`
2. Confirm with author: topic + format (Shorts / short 5–10m / medium 10–20m / long 20m+)
3. Propose outline → **wait for approval before writing full script**
4. Write full script using template from `memory/scripts/TEMPLATE-script.md`
5. Save to `memory/scripts/YYYY-MM-DD-slug.md`
6. Update status in `memory/ideas-youtube.md` → "In Progress"

## End of Session

- Move important items from HOT → WARM (stable facts) or COLD (lessons learned)
- Clear `memory/hot/HOT_MEMORY.md`
