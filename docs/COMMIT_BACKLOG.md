# Daily Commit Backlog — dev

This repo is **submitted coursework** (an air-quality EDA notebook) and a public portfolio piece.
A scheduled agent takes the **top unchecked item** each time this repo comes up, does it, verifies it,
and commits. Changes must be **additive** — the work was graded.

## Rules

1. One item per run. Finish it or leave it uncommitted.
2. **Allowed:** READMEs, `.gitignore`, `requirements.txt`/environment notes, dataset provenance and
   licence notes, removing clearly accidental junk (`.DS_Store`, `.ipynb_checkpoints/`, duplicate files).
3. **Forbidden:** editing `air_quality_eda.ipynb` code or markdown, re-running it so stored outputs
   change, reformatting submitted source, or anything that alters what was assessed. If something looks
   wrong, record it under "Observations", do not fix it.
4. Verification for doc/additive commits: confirm no executable file changed, and that every command a
   README tells a reader to run was actually run or is plainly correct.
5. Never `git add -A` / `git add .`; stage named paths. Never fabricate a source, licence or result.
6. Conventional commit subject; end with the Co-Authored-By trailer. Tick the item and append to Log.

## Audit facts (verified 2026-10-28)

- Single commit in history ("hi", 2025-11-24). Tracked files: `air_quality_eda.ipynb`, five CSVs at the
  repo root, the same five under `Datasets/`, `city_day 2.csv`, `.DS_Store`.
- Notebook: 27 cells (Python 3.10.11 kernel), sections 1-10 (the "8. Additional Visualizations"
  heading sits at the very end, after section 10). Loads `city_day.csv`, `city_hour.csv`,
  `station_day.csv`, `station_hour.csv`, `stations.csv` by **relative path from the repo root** and, in
  its save cell, would write `city_day_cleaned.csv`.
- Recorded versions in stored output: pandas 2.3.2, NumPy 2.3.3, Matplotlib 3.10.6, Seaborn 0.13.2.
  Plotly is imported (cell 17) but no version is recorded.
- Row counts (excluding header): city_day 18,265; city_hour 438,245; station_day 36,530;
  station_hour 7,210; stations 10. `city_day` spans 2015-01-01 to 2024-12-31 and covers 5 cities
  (Bangalore, Chennai, Delhi, Kolkata, Mumbai); `city_hour` spans the same range.
- `Datasets/*.csv` are byte-identical (same md5) to the root copies; `city_day 2.csv` is byte-identical
  to `city_day.csv`.
- No README, `.gitignore`, requirements file, or licence/provenance note exists.
- ~54 MB of CSVs in the working tree (city_hour.csv alone is 46 MB), duplicated under `Datasets/`.

## Queue

- [ ] **B1 — .gitignore + remove accidental junk.** `git rm --cached` `.DS_Store` and `city_day 2.csv`
      (re-confirm still byte-identical to `city_day.csv` first); add ignore entries for `.DS_Store`,
      `.ipynb_checkpoints/`, `__pycache__/`, `.venv/`. Does not touch the notebook.
- [ ] **B2 — README.md.** Explain the problem, the five datasets and their columns, how to run the
      notebook (from the repo root, since paths are relative), the notebook's sections, and what is
      recorded in its stored output. Be explicit about the notebook's state (see Observations): which
      cells have stored outputs and which do not. Quote findings only as recorded.
- [ ] **B3 — requirements.txt.** Pin to the versions recorded in the stored output (pandas 2.3.2,
      numpy 2.3.3, matplotlib 3.10.6, seaborn 0.13.2) plus plotly (unpinned, say so) and jupyter.
      Verify by installing into a clean venv; if executing, run a **scratch copy** only.
- [ ] **B4 — Dataset provenance note.** Per-file columns, row counts, date range, derived from the
      files. Source and licence are **unverified** — see Observations; VB must supply them. If
      unconfirmed, record only what is derivable.
- [ ] **B5 — Document the root vs `Datasets/` duplication** in the README. Do not delete either
      without VB's decision.

## Observations / needs VB's decision (do not act)

- **`dev` vs `DEV-AAT` overlap.** Both hold `air_quality_eda.ipynb` and the same CSV layout; the
  notebooks differ (not byte-identical) and DEV-AAT has the later, extended history and recorded
  versions (pandas 2.0.3 there vs 2.3.2 here). VB to decide which is canonical; no repo should be
  merged or deleted by the agent.
- **The notebook as stored is incomplete.** Of its code cells, only those up to the first plot have
  execution counts; cell 14 (AQI distribution plot) stored a `NameError: name 'plt' is not defined`
  (executed out of order), and cells 15-17, 19, 20, 22, 24 have no outputs at all. The conclusions in
  section 10 are therefore not backed by stored results. Not re-run, since that would alter assessed
  output.
- **Column name mismatch.** The CSVs have a `Datetime` column; cell 9 converts `Datetime`, but cells
  17, 19, 20, 22 and 24 reference `Date`, which no cell creates — they would raise `KeyError` if run
  in order. Left as submitted.
- **Data looks synthetic.** `stations.csv` lists `Station_D1`, `Station_D2`, ... `Station_B2` (two per
  city, five cities), not real monitoring-station names, and `station_hour.csv` covers only
  2015-01-01 to 2015-01-31 (7,210 rows). Provenance should be confirmed by VB before any README calls
  it a public dataset.
- Large CSVs are in git history; slimming would need history rewriting and is out of scope.

## Log

2026-10-28 - audit - docs: add commit backlog from repo audit
