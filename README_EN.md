# Future Career Stress Test

[中文文档 → README.md](README.md)

An **evidence-driven** open-source AI Skill that stress-tests a career against
authoritative labor-market data, task-level AI-automation research, AI
capability trends, demographics, and macro scenarios — and produces
**costed career transition routes**, not verdicts.

It is not an "AI career leaderboard" and not a "will AI take my job" chatbot.

## What it answers

- Which of my occupation's **tasks** are automatable, which are AI-augmented,
  and which remain human-dependent?
- How does my career hold up under three AI scenarios — Modest, Substantial,
  Extreme?
- Which skills should I keep, upgrade, or stop investing in — and **where can
  I move**, at what cost, difficulty, upside, and risk reduction?
- Is the same occupation worth more in China, the US, Australia, Canada,
  Europe, or Japan?
- Given my age, budget, time, physical constraints, and immigration goal,
  which path is best **for me**?

## Core principles

1. **AI exposure ≠ automation ≠ job loss.** An occupation is a bundle of
   tasks; tasks get automated, augmented, left unchanged, or newly created.
   Occupations are restructured rather than simply eliminated (a core finding
   of ILO 2025).
2. **Scenarios, not forecasts.** All future statements run across three
   scenarios aligned with Anthropic's Economic Scenarios and are explicitly
   labeled "scenario, not forecast."
3. **No fabricated numbers.** Every material claim carries source, year, data
   period, evidence level (S/A/B/C/D), and freshness tier. Insufficient
   evidence is stated as such.
4. **Counter-consensus.** Data beats media hype: hot careers (demand ↑ but
   supply ↑↑) may be poor fits for ordinary people; low-profile occupations
   (low exposure + high shortage) may be structurally stronger.
5. **Privacy by default.** No personal data is persisted or uploaded.
6. **Model-agnostic & bilingual.** No vendor APIs. Chinese in → Chinese out;
   English in → English out. Compatible with any agent following the
   [Agent Skills open specification](https://agentskills.io) (Claude, Codex,
   Gemini CLI, Copilot, …) and usable as a plain Markdown prompt with any LLM.

## Quick start

### Install as a Skill (Agent Skills–compliant platforms)

```bash
# Claude Code (personal)
cp -r future-career-stress-test ~/.claude/skills/

# Project level
cp -r future-career-stress-test /path/to/project/.claude/skills/
```

For other compliant platforms (Codex CLI, Gemini CLI, Cursor, Copilot, …),
place the directory wherever that platform expects skills. The skill uses only
the standard structure (SKILL.md + references + schemas) — no
platform-specific dependencies.

### Use as a plain prompt

Paste the full contents of `SKILL.md` into any LLM conversation, then ask.

### Example prompts

```
I'm 23, a college student in China with no trade skills. Run a career stress
test for me — goals: quick employment and long-term stability.
```

```
US software developer, 25, worried about AI. Give me transition paths with costs.
```

```
Compare nursing in China, the US, Australia, and Canada — I want to immigrate.
```

## Repository structure

```
future-career-stress-test/
├── SKILL.md              # Skill entry point (Agent Skills spec)
├── README.md             # 中文文档
├── README_EN.md          # This file
├── LICENSE               # MIT
├── CONTRIBUTING.md
├── CHANGELOG.md
├── docs/
│   ├── methodology.md    # Full method: task model, transition graph, evidence levels
│   ├── data-sources.md   # Source whitelist: global layer + country adapters
│   ├── scoring.md        # Scoring: dimensions, weights, goal-based re-weighting
│   ├── scenarios.md      # Three-scenario model (anchored to Anthropic scenarios)
│   ├── privacy.md
│   └── bilingual.md      # Bilingual spec + canonical field mapping
├── schemas/              # JSON Schemas: career / occupation / country / evidence / scenario
├── examples/             # China / US / Australia / country comparison / transition
└── data/                 # Intentionally empty: no vendored third-party data
```

## Data sources (summary)

Global layer: Anthropic Economic Index & Economic Scenarios · ILO · WEF Future
of Jobs · OECD · IMF · World Bank · Stanford AI Index.
Country layer (adapter pattern, not hardcoded): BLS + O*NET (US) · NBS +
MOHRSS (CN) · Jobs and Skills Australia + ABS (AU) · StatCan + Job Bank +
IRCC (CA) · Eurostat + CEDEFOP + ESCO (EU) · Statistics Bureau + MHLW (JP).

Full whitelist and authority boundaries: [docs/data-sources.md](docs/data-sources.md).
**This repository vendors no third-party data** — analyses retrieve from
official sources at run time and record the retrieval date.

## Disclaimer

This project is an independent open-source project and is **not affiliated
with** Anthropic, ILO, WEF, OECD, IMF, BLS, O*NET, Stanford University, or
any other data provider.

Outputs are research aids, not employment, immigration, or investment advice.
All scenarios are conditional what-ifs, not predictions of the future.

## Contributing & License

See [CONTRIBUTING.md](CONTRIBUTING.md). License: [MIT](LICENSE).
