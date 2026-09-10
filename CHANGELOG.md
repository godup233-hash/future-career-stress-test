# Changelog

All notable changes to this project are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/).

## [0.1.0] - 2026-09-10

### Added
- Initial release.
- `SKILL.md` compliant with the Agent Skills open specification
  (agentskills.io): 16-step workflow, data-source hierarchy, scoring and
  scenario entry points, standard 14-section output format, anti-hallucination
  rules, bilingual behavior.
- `docs/methodology.md`: statement-type taxonomy (Observed / Historical trend /
  Projection / Scenario / Model inference / Opinion), evidence levels S–D,
  freshness tiers, task-level occupation model (exposure / automation /
  augmentation / human dependency / robotics), career transition graph model
  with Transition Score.
- `docs/data-sources.md`: global-layer whitelist (Anthropic Economic Index &
  Economic Scenarios, ILO–NASK WP140 2025, WEF Future of Jobs 2025, OECD, IMF,
  World Bank, Stanford AI Index) and country adapters for US, China,
  Australia, Canada, Europe, Japan, plus ILOSTAT fallback.
- `docs/scoring.md`: Career Future Score (0–100) with 8 dimensions, default
  weights, goal-based re-weighting profiles (high-income / immigration /
  quick-employment / ai-era-stability), hard gates, insufficient-evidence
  renormalization.
- `docs/scenarios.md`: three-scenario model (Modest / Substantial / Extreme)
  anchored to Anthropic Economic Scenarios (Institute WP 2026-02, Sep 2026),
  including anchor figures and occupation-level translation rules.
- `docs/privacy.md`, `docs/bilingual.md`.
- JSON Schemas: `career`, `occupation`, `country`, `evidence`, `scenario`.
- Examples: China (entry-level trade), US (software developer), Australia
  (electrician), 4-country nursing comparison, graphic-designer transition
  incl. Test-Case-10 handling (refusing deterministic rankings).
- README (中文) and README_EN; MIT license; contributing guide.
