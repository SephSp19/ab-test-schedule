---
name: ab-test-schedule
description: >-
  Generate a polished, on-brand A/B Test Schedule visual (an HTML page with a
  pastel lavender/pink gradient, a frosted "AI Beauty Chat" style card, colored
  locale + status pills, and section dividers with colored left bars). Use this
  skill whenever the user wants to build, remake, update, or restyle an A/B test
  schedule, experiment schedule, test roadmap, pilot/rollout schedule, or a
  feature-testing timeline table — especially in the AI Beauty Chat / iOS
  Frontend context, or any time they show a schedule table and ask to "make it
  look like this" or reference this style. Trigger even if they don't say the
  word "skill" or "template".
---

# A/B Test Schedule

Produce a single self-contained HTML file that renders a schedule exactly in the
established house style: a soft lavender-to-pink gradient background, a centered
header (pill badge → two-tone title → subtitle), and a frosted glass card holding
a table of features grouped into labeled sections. This is a fixed visual
identity — the job is to pour the user's data into it faithfully, not to redesign
it.

## How to build one

1. **Read the template.** `assets/template.html` is the source of truth for all
   styling. Copy it and fill in the four header placeholders plus the `{{ROWS}}`
   block. Never re-derive the CSS from scratch — keeping the CSS byte-identical is
   what makes every schedule look like part of the same family.

2. **Gather the data.** You need, per feature: the name, a locale (US/CA/etc.),
   a date range (or none), and a status/pilot value. Features are organized into
   ordered **sections** (e.g. STANDALONE, TEST 3, DYNAMIC ENTRY, IN REVIEW), and
   sections may carry a **note** row (an italic callout). If the user gives you a
   messy list, a screenshot, or a spreadsheet, extract this structure first. If a
   detail is genuinely ambiguous, ask — but prefer sensible defaults over stalling.

3. **Emit the rows** using the three building blocks documented inside the
   template (section header, note, data row). Preserve the user's ordering.

4. **Save** to a `.html` file in the working directory (default name
   `ab-test-schedule.html` unless the user names it) and open it with
   `open <file>` so they can see it.

## Header placeholders

| Placeholder      | Meaning                          | Example                |
|------------------|----------------------------------|------------------------|
| `{{PAGE_TITLE}}` | browser tab title                | `A/B Test Schedule`    |
| `{{BADGE}}`      | top pill, all-caps               | `✦ AI BEAUTY CHAT`     |
| `{{TITLE_MAIN}}` | dark part of the title           | `A/B Test`             |
| `{{TITLE_ACCENT}}`| purple part of the title        | `Schedule`             |
| `{{SUBTITLE}}`   | gray line under the title        | `iOS Frontend · 2026`  |

## Choosing pill colors

Locale pills are fixed: `loc-us` (blue) for US, `loc-ca` (amber) for CA. Add
analogous classes only if a new locale appears.

Status pills carry meaning through color — match intent, and keep the same value
the same color across the page so readers can scan it:

- **Solid pilot codes** (like `S−3783C`) use a saturated fill. Group features that
  share a pilot code under the same color so the shared code reads as a set —
  `st-purple`, `st-blue`, `st-green`, `st-red`, `st-amber` are the options.
- **Status words** use the softer "line" variants: `st-amberline` for pending /
  blocked (e.g. "Pending Eng"), `st-greenline` for shipping ("Launching − No
  Test"), `st-bluesoft` for scheduled/queued ("After Code Freeze"), `st-gray` for
  undecided ("Testing TBD").

Use a real minus/en dash `−` in pilot codes and `−` between dates, matching the
reference (not a hyphen). Use `—` in a dates cell when there is no date.

## Section bar colors

Each section header has a colored left bar (`--barcolor`) with a matching muted
label color. Reuse these; introduce a new hue only for a genuinely new section
type:

- Purple `#8b5cf6` / label `#7b6ba0` — default / standalone / numbered tests
- Blue `#5b8def` / label `#5f7bb5` — entry-point / dynamic groupings
- Red `#e05a6f` / label `#b05264` — higher-risk or later test waves
- Lilac `#b39ddb` / label `#8478a3` — review / backlog ("IN REVIEW")

## Fidelity notes

The look depends on small details: the frosted card (`backdrop-filter`), tabular
numbers on dates, the three footer dots (purple, purple, orange), and generous
row padding. Don't drop these. If the user asks for a PNG, render the HTML and
screenshot it at ~1400px wide to match the original proportions.
