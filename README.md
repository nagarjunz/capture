# /capture

> *"Simplicity is the highest form of intellect."*

**Stop losing your best conversations.**

You brainstorm something great with Claude. Decisions get made, numbers get thrown around, a plan takes shape — and then it all dies in the scrollback.

Type `/capture` and Claude turns the discussion into a polished, shareable takeaway. It picks the right format for you:

| Your conversation was… | You get |
|---|---|
| A pitch or story with a narrative arc | A slide deck (`.pptx`) |
| Decisions, a plan, a spec | A Word doc (`.docx`) |
| Numbers, comparisons, tiers | A spreadsheet (`.xlsx`) |
| A flow, system, or timeline | A single-file interactive HTML page |
| A quick checklist or reference | Markdown |
| Something final and formal | A PDF |

Everything is developed in **Darkroom** — the skill's design system, named for where captures have always been developed: black and white, whitespace, hairline rules, Helvetica. The content is the design.

And captures compound: every one appends a line to an `index.md` in your Capture folder — date, file, one line of what was decided. Ten captures in, you own a searchable log of every decision you've made with AI. The archive is the real product.

## Install

**Claude Code** — add this repo as a marketplace, then install:

```
/plugin marketplace add nagarjunz/capture
/plugin install capture@capture-marketplace
```

**Claude Desktop / Cowork** — download [`capture.skill`](./capture.skill) and open it, or copy `plugins/capture/skills/capture/` into your skills folder.

## Use

Have a conversation. Then:

```
/capture
```

That's it. No flags, no options. If you wanted a different format than the one it chose, just say so — it'll rebuild.

## Doesn't read like AI

Captures apply anti-AI-writing rules distilled from [blader/humanizer](https://github.com/blader/humanizer) (MIT) and Wikipedia's "Signs of AI writing" guide — plus voice-matching from your own wor