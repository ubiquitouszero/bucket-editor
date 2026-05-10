# Bucket Editor

A throwaway-style triage editor for daily prioritization. **Single self-contained HTML file**, opens in any browser, persists locally to `localStorage`. No install, no signup, no server.

**Try it:** [ubiquitouszero.github.io/bucket-editor](https://ubiquitouszero.github.io/bucket-editor/)

**Use it locally:** [Download `index.html`](https://raw.githubusercontent.com/ubiquitouszero/bucket-editor/main/index.html) (right-click → Save link as) — then double-click to open.

## Why it exists

Most TODO apps want you to commit to them. This is the opposite — a throwaway editor for one day's triage that you can use indefinitely or discard. State lives in your browser, not a service.

The trick: every column ends with an export button. **The HTML isn't the artifact you keep — it's the markdown or AI prompt you paste somewhere else.**

## How to use it

1. Download `index.html`
2. Double-click — it opens in your browser
3. Drag cards between columns. Add notes (pencil icon), tags, story-point estimates
4. When you're done, copy out:
   - **Copy as markdown** — paste into a note, doc, or message
   - **Copy as Claude prompt** — paste into Claude / ChatGPT to update a daily note or summarize the week
   - **Per-card copy icon** — grab a single item to drop into a thread

## Columns

| Column  | Purpose                                  |
|---------|------------------------------------------|
| Now     | What you're actively doing right now     |
| Next    | Today's actions, in priority order       |
| Later   | This week, not today                     |
| Cut     | Deprioritized — visible reminder of what you said no to |
| Done    | This week's wins. Drag here, don't delete |

## Features

- **Drag and drop** between columns and within a column
- **Inline notes** per card (Cmd/Ctrl+Enter to save)
- **Project tags** — color-coded chips you configure (default: Work / Side / Personal / Family / Health / Learning)
- **Story-point chips** with column sums — Fibonacci scale (1/2/3/5/8/13/21), use whatever cadence you want
- **Aging chips** on Later/Cut — cards older than 7 days get a warning chip; older than 14 a red one. Forces address-or-drop
- **WIP indicator** on Now — header turns amber at 5 cards, red at 8 (configurable)
- **Filter bar** — filter by tag, untagged, or text search
- **Settings panel** — edit tags, recolor, change thresholds, export full state JSON for backup

## The re-seed loop

You can use AI to populate the editor from your actual work. Click **Re-seed prompt** → it generates a prompt that asks the AI to scan your activity (git, notes, email, calendar) and return JSON. Click **Import JSON** to load the response.

This closes the loop both ways: the editor exports prompts for the AI, and accepts JSON back from it.

## Where state lives

- `localStorage` key `bucket-editor-share-v1` (board state)
- `localStorage` key `bucket-editor-share-config-v1` (tags, thresholds)
- Per-browser, per-file. Opening a copy at a different path starts fresh.
- For backup or hand-off, use **Settings → Export full state JSON**.

## Make it yours

The whole tool is one HTML file under 1000 lines. Open it in a text editor — change tags, colors, columns, copy text. The architecture is:

- HTML at the top defines the structure
- CSS in the `<style>` block uses CSS variables for colors
- JS at the bottom holds all the logic. The `DEMO` object is the seed data, `DEFAULT_TAGS` the starting tag set, and the `build*` functions handle exports.

## License

MIT. Do whatever you want with it.

## Credit

Pattern: "throwaway editor with copy-back-to-prompt export" — one of the [HTML output patterns](https://workiscode.com) for working with AI agents. Built by [Bert Carroll](https://workiscode.com) (`@BertCarroll`).
