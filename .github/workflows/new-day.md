---
emoji: "📅"
name: new-day
description: Add today's UTC date to Daily Updates in index.html with a matching accessible confirmation dialog.
engine: copilot
on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit: true
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day

## Task

Use the workflow run date in UTC (the date at run time in UTC) and update only `index.html`.

In `index.html`, add one new daily update entry for that UTC date by following the existing Daily Updates conventions exactly:

- Add one new navigation button in `.daily-updates-list` with:
  - `class="daily-update-trigger"`
  - `type="button"`
  - `aria-haspopup="dialog"`
  - `aria-controls` pointing to the new dialog ID
  - `data-dialog-trigger`
  - date text wording that matches existing style (for example, `1st of August`)
  - the trailing right-arrow span used by existing entries
- Add one matching `<dialog class="daily-update-dialog">` with:
  - ID, `aria-labelledby`, and `aria-describedby` following existing ID conventions
  - header line in the same format as existing dialogs (`Daily Update / <date wording>`)
  - a close button matching the existing structure
  - a short, accessible confirmation message that the daily update ran for that UTC date

## Rules

- Follow the existing HTML structure, ID conventions, date wording, and styling patterns already present in `index.html`.
- Preserve every existing daily update, navigation control, and dialog.
- Do not modify `styles.css`.
- Do not duplicate a date, navigation control, or dialog.
- If the UTC date is already present in Daily Updates, make no file changes and call `noop` with a brief reason.

## Safe Outputs

- If `index.html` changes are needed, use `create-pull-request`.
- If no changes are needed, use `noop`.