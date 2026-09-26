# Antidote Reference

Emergency toxicology antidote reference — 115 entries across 18 categories.
Offline-first, no server, no accounts, no patient data.

**Live:** https://choij1104.github.io/antidotes-referense/

## What this is

A bedside decision-support reference for trained clinicians. Every entry is structured
as toxin → antidote → dose → **pitfall**, because in poisoning the antidote is rarely the
hard part; the timing, the endpoint, and the contraindication are.

Not a protocol. Not a substitute for a regional poison center — 1-800-222-1222.

## Architecture

Data and presentation are separate. One canonical dataset, one view on top of it.

```
index.html          view; carries an embedded baseline copy of the data
antidotes.json      canonical dataset — edit here
version.json        version, review dates, changelog
sw.js               service worker — offline shell
manifest.json       installable to the home screen
QA-log.md           verification record
```

**Offline behaviour.** The full dataset ships inside `index.html`, so the app opens with
no network on first launch, from any origin, even off the filesystem. When online it
fetches `version.json` (a few hundred bytes); if the version differs it pulls the
newer dataset in the background and updates silently. A failed or blocked fetch changes
nothing — the embedded baseline stands. The app never waits on the network to render.

There is no API and no backend. `version.json` served as a static file is the entire
update mechanism.

## Updating the data

1. Edit `antidotes.json`.
2. Bump `version` and `lastReviewed` in `version.json`, set `nextReviewDue`, add a changelog line.
3. Rebuild `index.html` so its embedded baseline matches, and bump `CACHE` in `sw.js`.

Entry schema:

```json
{
  "id": "039-cyanide-smoke-inhalation-hcn-nitroprusside",
  "category": "Gases & asphyxiants",
  "tier": "A",
  "toxin": "...",
  "antidote": "...",
  "dose": "...",
  "pitfall": "...",
  "brands": ["Cyanokit", "vitamin B12a"],
  "window": "...",
  "sources": [{ "label": "Cyanokit prescribing information", "type": "FDA label" }],
  "lastReviewed": "2026-08-02"
}
```

`brands` feeds the search index, so a trade name finds the entry.
`window` renders as a red time-critical bar where minutes or hours are lost by hesitating.
`sources` is the provenance line; filling the remaining entries is the next task.

## Evidence tiers

| Tier | Meaning |
|---|---|
| A | FDA-approved specific antidote, strong or definitive evidence |
| B | Approved or guideline-endorsed standard of care, moderate evidence |
| C | Off-label; case series and expert consensus |
| D | Investigational, contested, or not obtainable in the US |
| — | No specific antidote exists; supportive care is the treatment |

## Review cadence

Quarterly. The review date and the next due date are printed at the top of the app; once
the due date passes, the indicator turns amber and the app tells the reader to verify
against current labelling. Supply-volatile agents — physostigmine, glucagon, antivenoms,
DTPA — are checked every cycle.

Current status is recorded in `version.json` and the verification record in `QA-log.md`.

---

Compiled by **Jae Hyek Choi, MSc, PhD, DVSc**
© 2026 Jae Hyek Choi. All rights reserved.
