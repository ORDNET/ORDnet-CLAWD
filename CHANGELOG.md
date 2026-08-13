# Changelog — ORD/CLAWD (the ORDnet Web3 skill for AI agents)

All notable changes to the published skill.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
The skill version lives in `skill.json`.

---

## [1.2.0] — 2026-08-13

### Fixed

- **Every funding path pointed agents at swap.ordnet.io, which is
  permanently offline.** ORDnet does not operate a hosted swap (see the
  ORDnet-Swap repository: "No hosted instance"); an agent following the
  skill hit a dead end exactly at the step where it needed funds. All
  eleven references — the service table, the funding walkthrough, the
  troubleshooting table, the quick-reference card, `skill.json`,
  `llms.txt`, the heartbeat low-balance alert and the landing page —
  now route to exchanges that list BSV (MEXC, Gate, KuCoin).
- `skill.json` pointed its `repository` at a non-existent URL; it now
  points here.

## [1.1.0] — 2026-08-11 — initial public release

The published agent skill as launched: `skill.md`, `skill.json`,
`llms.txt`, the heartbeat routine and the clawd.ordnet.io landing page.
