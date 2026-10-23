# Football Scout AI

Personal learning and portfolio project. Not a production recruitment system.

## Goal

Build a **reproducible** football scouting application that:

1. Finds **statistically similar** players from legally available event data.
2. Helps **explore** potential transfer candidates.
3. Documents **data limitations** so results are not oversold.

Statistical similarity is a starting point for exploration. It does **not** prove that a player is a suitable transfer.

## Background

The developer has several years of BI / Data Engineering experience (SQL, Azure, Power BI, some Python) and is transitioning toward **Applied AI Engineering**, ideally in football analytics.

**Time budget:** 2–3 hours per week for about six months (~50–75 hours). Design every phase to fit that constraint.

## MVP (in scope)

- Data: [StatsBomb Open Data](https://github.com/statsbomb/open-data) only (public, legally usable under StatsBomb terms).
- Processing: Python + pandas on player event data.
- Features: meaningful **per-90** and **position-specific** metrics.
- Ranking: simple similarity with **scikit-learn** (e.g. scaled features + cosine / nearest neighbours).
- UI: **Streamlit** to search a player and inspect similar candidates.

## Explicitly later (only with approval)

- DuckDB for local analytical queries.
- LLM features (explanations, Q&A over results).
- Extra data sources, scouting reports, or production APIs.

## Engineering principles

- Start small. Prefer a working slice over a complete platform.
- Reproducibility first: pinned dependencies, documented data version, repeatable scripts.
- Data quality over model complexity. Validate minutes, positions, and sample size before ranking.
- Avoid premature complexity (no extra services, no LLM, no DuckDB until they clearly help).
- Include **basic tests** for feature logic and similarity inputs.
- Document what the data cannot tell us (context, role, wages, injuries, tactics, availability).
- Never claim transfer suitability from similarity scores alone.

## Proposed roadmap

Phases are sequential. Do not start the next phase without explicit approval.

| Phase | Focus | Outcome |
| --- | --- | --- |
| 0 | Project docs | `PROJECT.md`, `AGENTS.md`, `README.md` |
| 1 | Environment and data | Python env, StatsBomb download notes, raw data inventory |
| 2 | Feature engineering | Per-90, position-aware feature table |
| 3 | Similarity | Simple scikit-learn ranking + sanity checks |
| 4 | UI | Streamlit: pick a player, see similar candidates |
| 5 | Quality and portfolio | Tests, limitation docs, short write-up |
| 6+ | Optional | DuckDB and/or LLM, only if they add clear value |

### Phase details

**Phase 1 — Environment and data.** Create a minimal project layout, `requirements.txt` / lockfile, and a documented way to obtain StatsBomb Open Data. Inventory competitions, seasons, and event types. Do not design a full feature set yet.

**Phase 2 — Feature engineering.** Aggregate events to player-season (or similar) grain. Compute per-90 rates. Split or weight features by position group. Drop or flag players with too few minutes.

**Phase 3 — Similarity.** Scale features. Rank nearest neighbours. Keep the model simple and inspectable. Add a few tests that a known profile does not collapse (e.g. empty minutes, all-zero vectors).

**Phase 4 — Streamlit.** One screen: select competition/season/player, show top-N similar players with key features and a short caveat.

**Phase 5 — Portfolio hardening.** Tests for transforms, README usage, a limitations page, and a short narrative of what was learned.

**Phase 6+ — Optional.** DuckDB if local query speed or SQL-style exploration becomes a bottleneck. LLM only as explanation on top of computed numbers, never as a substitute for features.

## Success criteria (MVP)

- A third party can recreate the pipeline from the repo docs.
- Similarity results are driven by documented features, not opaque magic.
- The UI states data coverage and that similarity ≠ transfer fit.
- Basic automated tests cover feature and ranking assumptions.

## Non-goals

- Live recruitment, player valuation, or club decision support.
- Scraping or using data without a clear licence.
- Matching commercial scouting platforms.
