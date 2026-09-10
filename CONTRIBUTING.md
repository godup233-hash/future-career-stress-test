# Contributing · 贡献指南

Thanks for helping keep this skill honest, current, and useful.
感谢贡献。本项目的最高价值是**证据质量**，请按以下规则参与。

## Ground rules · 基本规则

1. **Evidence first.** Any change to scoring anchors, scenario parameters, or
   data-source claims must cite the primary source (URL + publication date).
   PRs without sources for factual claims will not be merged.
2. **No vendored data.** Never commit third-party datasets or copied data
   tables (see `data/README.md`). Link, don't copy.
3. **No invented numbers.** Do not add occupation wages, employment counts,
   or exposure percentages unless they come from a whitelisted source with a
   recorded data year.
4. **No affiliation claims.** Do not imply endorsement by or partnership with
   any data provider.
5. **Bilingual parity.** If you add a canonical term, update
   `docs/bilingual.md` with its Chinese display name in the same PR.
6. **Spec compliance.** `SKILL.md` must stay valid per
   https://agentskills.io/specification: `name`/`description` frontmatter,
   body under ~500 lines, progressive disclosure (details go to `docs/`,
   not into SKILL.md).

## How to contribute · 贡献方式

### Updating data anchors (most common)
When Anthropic, ILO, WEF, BLS, etc. publish new editions:
1. Verify against the primary source.
2. Update the anchor in the relevant `docs/` file, replacing (not
   accumulating) figures, with the new edition noted.
3. Add a CHANGELOG entry.

### Adding a country adapter
1. Research the country's official occupation classification, its ISCO-08
   crosswalk, and its official sources for: employment/wages, projections,
   shortage lists, licensing, immigration lists.
2. Add a section to `docs/data-sources.md` following the existing table
   format; only official sources (evidence level S).
3. Optionally add an `examples/<country>-career.md` following the existing
   example structure (fictional persona, `[RETRIEVE]` markers for live data).

### Adding an example
Examples must use fictional personas, follow the Standard Output Format
(`SKILL.md`), mark every figure as retrieved-with-date or `[RETRIEVE]`, and
include Evidence + Uncertainty sections.

### Improving the methodology
Open an issue first describing the problem with the current model (scoring,
scenarios, transitions). Methodology changes need: rationale, at least one
external methodological reference, and an updated worked example.

## PR checklist · 提交前自查

- [ ] Factual claims cite whitelisted sources with dates
- [ ] No copied datasets; links only
- [ ] `docs/bilingual.md` updated for new terms
- [ ] SKILL.md still < 500 lines; details delegated to `docs/`
- [ ] JSON Schemas still validate (run any JSON Schema validator against
      the example snippets)
- [ ] CHANGELOG.md entry added
- [ ] No personal data, no affiliation claims

## Code of conduct

Be precise, be civil, argue with sources. Disagreements are resolved by
evidence quality (S > A > B > C), not by who writes more.
