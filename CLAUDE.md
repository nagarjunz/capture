# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A Claude Code **plugin marketplace** repo containing one plugin: `/capture`, a skill that turns a conversation into a polished deliverable (docx, pptx, xlsx, html, pdf, or md) styled in the "Darkroom" black-and-white theme. There is no build, lint, or test tooling — the entire product is markdown and JSON.

## Structure

- `.claude-plugin/marketplace.json` — marketplace manifest; points to `./plugins/capture`.
- `plugins/capture/.claude-plugin/plugin.json` — plugin manifest (name, **version**, description).
- `plugins/capture/skills/capture/SKILL.md` — the skill itself. This is the only substantive file; everything else is packaging.
- `capture.skill` — a zip of the skill directory, distributed for Claude Desktop/Cowork users. **It is a build artifact**: after editing SKILL.md, re-zip `plugins/capture/skills/capture/` and replace this file, or the two copies drift.

## When editing

- Bump `version` in `plugin.json` whenever SKILL.md changes.
- Keep README.md's format table and install instructions in sync with SKILL.md.
- `YOUR_GITHUB_USERNAME` placeholders exist in README.md, plugin.json (`homepage`), and SKILL.md (the credit-line URL). If the repo has a real GitHub home, replace all of them together — SKILL.md deliberately renders the credit line without a link while the placeholder remains.
- SKILL.md's frontmatter `description` doubles as the skill's trigger conditions — edit it carefully, since it controls when the skill fires.
