# home

A static website exported from Rahat Site Builder. No server, no build step — every `.html` file in this folder is complete and self-contained; open one directly in a browser or host the whole folder as-is.

## Pages
- `index.html` — Home

## Hosting on GitHub Pages
This is a plain static site, so GitHub Pages works with no extra setup: commit this folder to a repo, enable Pages in the repo's Settings → Pages, and point it at the branch/folder containing these files. There is no build/CI step required.

**Important — this is a one-way export, not a live sync.** Editing these files with a code editor (or `git`) does *not* update the project inside Rahat Site Builder, and editing inside the builder does not update files already committed to your repo. Each time you want your published site to reflect changes made in the builder, re-export and re-commit/push the updated files — there is currently no automatic two-way connection between a cloned repo folder and the builder app.

## Re-importing into the builder
Every exported `.html` file has the full project data embedded in an HTML comment near the top (safe, invisible when the page is viewed normally). Use "Import Project" in the builder and select either that `.html` file or a `.rsb.json` export to restore the full editable project — including any custom blocks, which are also automatically added to your personal Custom Block library for reuse in other projects.

## Theme colors
Three colors drive the whole site's look, set in Theme → Brand Colors:

| Role | Current value | Used for |
|---|---|---|
| Primary | `#ffb347` | Accents only — selection states, one CTA, a drop-cap. Not a default text color. |
| Warning | `#e07a7a` | Errors, required-field markers, destructive actions only. |
| Base (white) | `#ffffff` | The default color for nearly all text on the site — headings, body copy, labels. |

All built-in blocks read these through CSS variables (`--theme-primary`, `--theme-warning`, `--theme-white`, plus derived `--theme-text2`/`--theme-text3` for secondary/tertiary text) rather than hardcoding colors, so changing any of the three above updates the whole site consistently. If you (or an AI) ever add a custom block with a hardcoded color instead of `var(--theme-primary)` etc., it will not follow future color changes — that is the one thing to watch for.

## Custom blocks on this site
(none on this site)

## Known engineering rules (do not reintroduce these bugs)
- The shared glass-blur filter (`#frosted`) is one expensive resource for the whole page — keep it to 1-2 elements per block; never resize/redeclare the filter itself.
- Any data embedded inside this page's own `<style>` tag must have its closing-tag sequences escaped, or a custom block containing its own `<style>` block will truncate the real page CSS.
- Custom block code is run through the browser's own parser to auto-repair malformed markup before being embedded — still, keep custom block code to just the block's own snippet, not a whole page.
