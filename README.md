# Canvas Breach Customer Lookup

A simple, self-contained search tool for the list of education institutions named in the **ShinyHunters Instructure / Canvas data leak**.

🔎 **Live site:** https://jrsherlock.github.io/canvas-breach/

## What this is

In early 2026, the ShinyHunters group published a data-leak-site (DLS) file naming **8,790 Instructure / Canvas customer instances** — universities, K-12 districts, community colleges, and corporate / government training tenants — whose data was allegedly exfiltrated and published after the victim org did not pay or cooperate.

That list circulates as a flat text file with no search, no structure, and a lot of duplicates and noise. This tool makes it useful: paste any partial name (e.g. `texas`, `county`, `community college`, `australia`) and instantly see every match.

## Features

- ⚡ **Instant filter** — substring search across all 8,790 entries as you type
- 🎯 **Match highlighting** — the matched portion of each result is highlighted
- 🔢 **Live match count** — see exactly how many institutions match your query
- 🔒 **Local only** — the entire dataset is embedded in the page; nothing is uploaded, queried, or tracked
- 📦 **Single file** — `index.html` is fully self-contained (~244 KB), no build step, no dependencies, no backend
- 🌙 **Dark UI** — easy on the eyes for long lookups

## Usage

### Online

Just visit **https://jrsherlock.github.io/canvas-breach/** and start typing.

### Offline

Clone the repo (or download `index.html`) and open it directly in any modern browser:

```bash
git clone https://github.com/jrsherlock/canvas-breach.git
open canvas-breach/index.html      # macOS
xdg-open canvas-breach/index.html  # Linux
start canvas-breach/index.html     # Windows
```

No server, no install, no Node.js — just a static HTML file.

## Search tips

- Search is **case-insensitive substring** match — `UTAH`, `utah`, and `Utah` all return the same results.
- Try broad terms first to scope the space:
  - `university` → ~1,500+ matches
  - `county` → school districts
  - `community college` → community colleges
  - `qld doe` → Queensland Dept. of Education instances
  - country/region keywords like `australia`, `sweden`, `brasil`, `chile`
- Results are capped at 500 visible at a time for performance — the count is accurate, just refine the query to see all matches.

## Data source & caveats

- **Source:** the ShinyHunters DLS leak file, exported from a publicly-shared Google Doc as plain text.
- **Entries:** 8,790 unique names after whitespace-trimming and dedup.
- **Encoding:** the upstream file has some encoding artifacts — accented characters in Swedish, Spanish, and Portuguese institution names sometimes appear as `?` (e.g. `G?teborgs universitet`, `Ume? University`). This reflects the source data, not a corruption introduced here.
- **Internal / test instances:** entries like `Root`, `katydummy`, `Unit Canvas`, `*MVS: Root Account` are leftover internal/sandbox tenants. They are kept verbatim for fidelity to the source rather than filtered out.
- **No verification:** inclusion in this list does not necessarily mean an institution's user data was successfully exfiltrated, only that it appeared in the published list. Treat it as a **starting point for due diligence**, not a confirmation of breach impact.

## Why this exists

If you're at an affected institution, vendor, partner, or counsel — or you're just trying to figure out whether your alma mater is on the list — the official communications around the incident have been slow and uneven. A quick searchable index helps people self-serve that question in seconds.

## Tech

- Vanilla HTML / CSS / JavaScript — zero frameworks, zero build step
- Data embedded as a JSON literal in a `<script>` block
- Debounced input (60 ms) + `Array.includes` filter — fast enough for 8,790 entries on any laptop or phone
- Hosted on GitHub Pages from the `main` branch

## Contributing

Spot a clear data issue (e.g. a misencoded character that maps cleanly to a known institution)? Open an issue or PR.

## Disclaimer

This repository hosts a **searchable index of names already published by the threat actor in their public DLS post**. It does not host, link to, or facilitate access to the leaked data itself. If you believe an entry should be removed, please open an issue.

## License

The tool code (`index.html`) is released into the public domain under the [Unlicense](https://unlicense.org/). The underlying institution names are factual data drawn from the public DLS post.
