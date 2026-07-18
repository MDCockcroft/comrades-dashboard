# Comrades Dashboard

Self-contained training tracker for the 100th Comrades Marathon (Down Run, ~89 km).
Single-page, zero-dependency `index.html` PWA; all data lives in the browser
(localStorage). Deployed on GitHub Pages: https://mdcockcroft.github.io/comrades-dashboard/

## Project shape (durable)
- **Single file:** `index.html` (~977 lines, no framework/build/CDN) + a 15-line
  `sw.js` service worker (`comrades-cache-v1`) + `manifest.webmanifest`.
- **Persistence:** localStorage only (`comradesLogs`, `startDate`, `age`, `strava*`).
- **Plan:** 52 weeks hardcoded in JS (phases P0–P4, deloads, taper); runs Tue/Thu/Sat.
- ⚠️ **Strava is orphaned on the live site.** The Strava panel calls
  `/.netlify/functions/strava`, which only exists behind Netlify Functions — but the
  app is deployed to GitHub Pages, so Strava connect/sync is non-functional live
  (only `demoSync()` works). `netlify/`, `netlify.toml`, `DEPLOY.md` are gitignored
  as the abandoned approach.

## Persistent memory (Obsidian vault)

Cross-session memory for this project lives in the Obsidian vault:
`~/vault/Projects/Comrades-system/` (hub: `comrades-system.md`; durable decisions:
`architecture/decisions.md`). Vault-wide rules: `~/vault/CLAUDE.md`.

3-layer context rule — cheapest first, read source last:
1. **Graph** — `graphify query "<question>"` for code structure.
2. **Vault** — `architecture/decisions.md` + recent `~/vault/logs/*-comrades-dashboard-*.md`
   for decisions, context, and progress.
3. **Source** — read raw files only when editing, or when layers 1–2 fall short.

Session commands (real slash commands): `/mem-resume` at start, `/mem-save` at end.
The vault holds durable decisions + logs; **live status stays in the repo docs**
(never copy it into the vault). Never put secrets/PII in the vault (iCloud-synced).
The graphify Obsidian export lives at `~/vault/graphify/comrades-dashboard/`
(auto-generated — refresh with `/graphify . --obsidian --obsidian-dir ~/vault/graphify/comrades-dashboard`).
