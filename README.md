# ab-test-schedule

A Claude skill that generates a polished, on-brand **A/B Test Schedule** visual —
a self-contained HTML page in the "AI Beauty Chat" house style: a pastel
lavender-to-pink gradient, a frosted-glass card, colored locale + status pills,
and section dividers with colored left bars.

![style: AI Beauty Chat](https://img.shields.io/badge/style-AI%20Beauty%20Chat-b39ddb)

## What it does

Give it schedule data — a list, table, spreadsheet, screenshot, or set of Jira
epics — describing features/experiments with locales, dates, and statuses grouped
into sections, and it produces a ready-to-open `.html` file styled exactly like
the reference design.

## Install

Copy this folder into your Claude skills directory:

```bash
cp -r ab-test-schedule ~/.claude/skills/
```

Then just ask in plain language, e.g.:

- "make an A/B test schedule for these features…"
- "remake this schedule" (with a screenshot)
- "update the test schedule — Shade Matching slipped to October"

## Contents

| Path                   | Purpose                                            |
|------------------------|----------------------------------------------------|
| `SKILL.md`             | Skill instructions + the design system reference   |
| `assets/template.html` | The frozen HTML/CSS template with `{{placeholders}}` |

## How it works

`SKILL.md` documents the fixed visual identity: header placeholders, the locale
and status pill palette (solid pills for pilot codes, soft "line" pills for
status words), section bar colors, and fidelity notes. The template's CSS is kept
byte-identical across every schedule so they all read as one family.
