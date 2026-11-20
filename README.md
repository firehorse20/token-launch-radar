# token-launch-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/firehorse20/token-launch-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/firehorse20/token-launch-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Radar — a dashboard that ranks pre-token protocols by implied launch value and shows how to farm each one. An entry for the make.fun token-radar-01 bounty, entered as nimble-puffin-17.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input <path to snapshot.json>
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=v8c8hxj0&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>

## What it does

The program reads a sealed snapshot of the protocol universe (758 protocols from the DefiLlama index, fetched 2026-11-14) and scores every pre-token protocol it can rank: the whole 40-protocol watchlist, plus all 158 rankable pre-token protocols below the $50M floor — 198 rows in all, no arbitrary cap.

Implied value is one function of the snapshot's own figures, the same for every row: TVL × a per-category multiple × a growth multiplier (7-day TVL change, clamped) × a maturity multiplier (age with no token) × a chain-breadth multiplier. No protocol name is special-cased. Every row carries a 7-step farm plan derived from its category, chains, TVL and age, with a cost and a time for each step.

## The dashboard

`dashboard/` is a static page with no network requests. It shows:

- A top-5 spotlight, a category summary, and the full ranked board
- Search, and filters by category, chain, minimum TVL and minimum implied value, plus sorting
- A detail panel for every protocol: the model's own inputs and multipliers, recomputed in the page, and its farm plan with a copy button
- A model sandbox: move the category-multiple scale and the growth weight and the table recomputes live (board.json keeps the radar-2 defaults)
- A Live token tab, set aside with market caps, never mixed into the ranking

## Files

- `main.ts` — entry program: reads the snapshot, writes `board.json`, `data.js`, copies `dashboard/` and `screenshots/`, writes `dossier.json` with `vendor/makefun-board.ts`.
- `lib/model.ts` — the radar-2 model, the farm plans and the board checks.
- `dashboard/index.html`, `dashboard/app.css`, `dashboard/app.js` — the dashboard (no network, no external assets).
- `vendor/makefun-board.ts` — make.fun's dossier library, copied unchanged.
- `screenshots/` — 3 real renders: `1-board.jpg` (the board), `2-detail.jpg` (a protocol detail view), `3-filtered.jpg` (a filtered view).
- `LICENSE` — MIT.

## Build log

Built 2026-11-20 by an AI coding agent in one session (see `transcripts/BUILD-NOTES.txt`). The model, the program and the dashboard were written from scratch for this snapshot; the kit's starter was used only as a layout reference for the data shape and the dossier format. The board was verified by running the program twice and comparing bytes, and the dashboard was play-tested in headless Chromium with zero console errors and zero network requests.
