# data/ · 数据政策

**This directory intentionally contains no datasets.**

Rules (binding for contributors):

1. **No vendored third-party data.** Do not commit BLS, O*NET, ILO, WEF,
   OECD, Eurostat, ABS, StatCan, NBS or any other provider's datasets,
   extracts, or screenshots of data tables into this repository. Licensing
   and freshness both forbid it.
2. **Cite and link instead.** Analyses retrieve data at run time from the
   whitelisted sources in `docs/data-sources.md` and record `retrieved_at`.
3. **What MAY live here:** small, original, hand-authored reference tables
   created by this project's maintainers (e.g. a weight-profile preset, a
   classification crosswalk note) — clearly marked as project-authored,
   with no copied third-party content.
4. **Schemas are not data.** Machine-readable contracts live in `schemas/`.

If you need a dataset to develop against, download it from the official
source locally and keep it out of git (`.gitignore`d).
