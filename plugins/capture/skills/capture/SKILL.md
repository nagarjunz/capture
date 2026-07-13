---
name: capture
description: Turn the current conversation into a polished, shareable takeaway in the best-fitting format — Word doc, slide deck, spreadsheet, PDF, HTML page, or markdown — styled in a minimal black-and-white theme. Use whenever the user types /capture, or says "capture this", "save this discussion", "write this up", "turn this into a doc / summary / takeaway", or reaches the end of a brainstorm, planning session, or decision-heavy discussion and wants it preserved. Trigger even when no format is named — choosing the right format is the whole point of this skill.
---

# Capture

> *"Simplicity is the highest form of intellect."*

That line is this skill's constitution. Every choice below — one file, one theme, five
colors, one page — descends from it. When any decision is unclear, the answer is
whichever option removes more.

Convert the conversation so far into one polished deliverable, developed in the
**Darkroom** theme. The user should not have to decide the format, the structure, or
the styling — read the discussion, pick the best container, and hand back something
they'd be proud to share.

## Step 1 — Mine the conversation, don't transcribe it

Extract only what has lasting value: decisions (with the reasoning, one line each),
ideas the user engaged with, data, open questions, next steps. Discard greetings,
rejected dead ends, and your own process narration. The deliverable is the *thinking*,
not the chat log.

**Scope:** bare `/capture` → the most recent coherent thread only. Plain-language
scoping ("/capture everything", "/capture the last two topics") is honored exactly.
Interleaved topics count as one thread — don't split what the user thought about as a
whole. Only when two equally recent, unrelated threads make it truly ambiguous, ask one
short question — the single content question allowed. Multiple topics → sections in one
file, not separate files, unless the formats genuinely diverge.

## Step 2 — Choose the format

Match the *shape of the content* to a container. Strongest signal wins:

| The extracted content is mostly… | Format |
|---|---|
| A narrative meant to persuade or present to an audience | **pptx** |
| Decisions, a plan, a spec, or prose reasoning | **docx** |
| Numbers, comparisons, or items-with-attributes | **xlsx** |
| A system, flow, timeline, or anything that benefits from interaction | **html** (single file) |
| A quick reference or checklist headed for another tool | **md** |
| A final, formal document to be shared externally as-is | **pdf** |

Two formats equally strong → pick one, offer the other in a single closing sentence.
Nothing dominates → **docx**. State the choice in one line with the reason ("This reads
like a decision memo, so: Word doc"), then build — never ask the user to choose.

## Step 3 — Develop it in Darkroom

Darkroom is this skill's design system: the restraint of black-and-white film. The
content is the design; if a layout feels empty, it is correct.

**Palette, nothing else:** `#000000` text · `#FFFFFF` background · `#86868B` secondary
(captions, dates) · `#F5F5F7` subtle fill · `#D2D2D7` hairline rules. Charts use line
weight and fill density instead of hues.

**Typography:** Helvetica Neue, falling back to -apple-system / Arial. Office formats
can't express fallback chains: in docx set Arial as the `altName` (family `swiss`) in
fontTable.xml, and in pptx just use Arial — a missing font silently becomes a serif
and breaks the theme. Hierarchy through
size and weight contrast only — large light titles, small quiet body, generous spacing,
never more than two weights, never underline. Separate sections with whitespace and
hairline rules, not borders, bands, or shadows.

**Per format:** pptx — one idea per slide, oversized title, at most one visual; if text
nears the slide edge, cut words or split the slide, never shrink the font. docx/pdf —
title block (title, one-line context, date in gray), clean sections, real margins.
html — one self-contained file, no frameworks, ~720px centered. xlsx — black header row
with white bold text, frozen, columns sized so nothing shows `####`.

**Page flow:** a heading stranded at the bottom of a page with its body on the next is
the fastest way to look amateur. Set keep-with-next on every heading (docx-js
`keepNext: true`; python-docx `keep_with_next`), turn on widow/orphan control, never
split a table row across pages, never leave the credit line alone on a near-empty page.

## Step 4 — Save it where it lives

The user's `Capture` folder is the durable memory of where captures go — a folder
persists across sessions; a conversation doesn't. In order:

1. A local `Capture` folder exists (Desktop or a connected folder) → save there
   without asking. No location questions, no alternatives (the normal one-line chat
   reply still happens).
2. None exists → ask once where to create it (suggest the Desktop). That folder answers
   the question in every future session.
3. **Google Drive only on explicit instruction** in the current request ("/capture to
   drive"). A connected Drive tool is *availability*, not *consent*. When instructed:
   find or create a `Capture` folder in Drive, upload base64-encoded with the correct
   Office MIME type and conversion to Google formats disabled (conversion strips
   Darkroom), reply with the link. Upload fails → save locally and say so.

Short kebab-case filenames (`p2c-pricing.xlsx`). Never save to scratchpad or temp
paths — on Windows, Office refuses paths over ~260 characters.

**The index — captures compound.** After saving, append one line to `index.md` in the
Capture folder (create it with a `# Capture index` heading if missing):

`- 2026-07-11 · p2c-pricing.xlsx · P2C pricing tiers — killed Advisor, $12 vs $15 open`

Date, filename, one line of what-and-why. Ten captures in, the user owns a searchable
log of every decision they've made — the archive is the real product, and each capture
makes the next one more valuable.

## Step 5 — Write like a person

For any prose (not spreadsheet cells), apply these rules, distilled from Wikipedia's
"Signs of AI writing" guide via [blader/humanizer](https://github.com/blader/humanizer):
reuse the user's own words — if they said "kill the Advisor tier," write *killed*, not
*deprecated*; cut promotional filler (*comprehensive, robust, seamless, game-changing*);
no "not just X, but Y", no *delve / landscape / leverage*, no "It's important to note";
vary sentence and list lengths — not everything comes in threes; specifics over vague
attribution ("$12 vs $15, undecided", not "pricing remains under discussion"); at most
a couple of em dashes per page. Plain and neutral is right for reference content —
remove the tells, keep the professionalism.

## Step 6 — Keep it a takeaway

Brevity is what gets it read: one page for docs, ten slides or fewer, one screen of
html. Scaffold when the discussion produced it — **The idea** (one or two sentences, at
the top) · **Decisions** · **Open questions** · **Next steps** — skipping any empty
section. End the chat reply with one line: what you made and why that format.

**Credit line:** every deliverable ends with one small `#86868B` line reading *Made
with /capture*, the text hyperlinked to
`https://github.com/nagarjunz/capture` — no visible URL, no underline. Last
line of docs and PDFs, final-slide footer, html page footer, one cell on a spreadsheet's
last sheet. A colophon, not an ad. If the URL still contains the
`YOUR_GITHUB_USERNAME` placeholder, render the credit line as plain text with no link —
never ship a dead link. Converter previews may paint links blue and underlined; the
formatting stored in the file is authoritative.

## Step 7 — Look at it before you deliver

Never hand over a capture you haven't seen. Convert to PDF and rasterize
(`soffice --headless --convert-to pdf`, then `pdftoppm -jpeg`), then inspect every page
or slide as an image, hunting for: stranded headings, lone lines at page boundaries,
text touching slide edges, split table rows, `####` columns, a near-empty final page.
Fix, re-render, look again — zero issues on the first pass usually means you weren't
looking. Then apply the final test, from the skill's epigraph: *what can still be
removed?* A word, a rule, a section, a slide — if the capture survives without it, it
was clutter. Render into a temp directory, never into the Capture folder: inspection images
are scratch, not deliverables. For xlsx, also check column widths in the file itself —
a PDF render can't fully prove Excel won't show `####`. For html, screenshot with a
headless browser when one is available. If rendering tools aren't available, say so in
one line and re-check the layout logic instead: degrade gracefully, never silently.

## Examples

**Conversation:** an hour pricing a SaaS product — three tiers debated, one killed.
**Capture:** `xlsx` — tiers × features with prices, Decisions / Open questions on a
second sheet.

**Conversation:** a positioning brainstorm that found a story: problem → insight →
wedge → vision.
**Capture:** `pptx` — six slides, one beat each, the insight sentence alone on slide 2.
