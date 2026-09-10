---
name: future-career-stress-test
description: >-
  Evidence-driven future career stress test. Analyzes an occupation at task
  level (AI exposure, automation vs. augmentation, task transformation), runs
  three AI scenarios (Modest / Substantial / Extreme), computes a weighted
  Career Future Score with dynamic weights based on the user's goal, compares
  countries, and builds costed career transition paths — using only verifiable
  sources (ILO, WEF, Anthropic Economic Index/Scenarios, OECD, IMF, BLS, O*NET,
  national statistics). Use when the user asks about future-proof careers, AI
  job-replacement risk, career change paths, cross-country career comparison,
  immigration-oriented career choice, or "which jobs survive AI". Works in
  Chinese and English, in any country context. NOT a ranking generator: refuses
  to fabricate statistics and labels every claim with evidence level.
license: MIT
metadata:
  version: "0.1.0"
  language: bilingual (zh/en)
  spec: agentskills.io
---

# Future Career Stress Test · 未来职业压力测试

An evidence-driven career decision skill. It stress-tests a career against
authoritative labor-market data, task-level AI exposure research, AI capability
trends, demographics, and macro scenarios — then produces transition routes,
not verdicts.

一个证据驱动的职业决策 Skill。它用权威劳动力市场数据、任务级 AI 暴露研究、
AI 能力趋势、人口结构和宏观情景，对职业做"压力测试"——输出的是转型路线，
而不是简单判决。

## Core doctrine · 核心原则

1. **Never output a single "AI replacement rate".** Always decompose:
   AI Exposure（AI暴露）≠ Automation（自动化）≠ Job Loss（就业消失）.
   An occupation is a **bundle of tasks**; tasks are automated, augmented,
   unchanged, or newly created. Occupations transform; they rarely just vanish.
2. **Scenario, not forecast.** All future statements are labeled as one of:
   `Observed`（观察事实）/ `Historical trend`（历史趋势）/ `Projection`（官方预测）/
   `Scenario`（情景模拟）/ `Model inference`（模型推断）/ `Opinion`（观点）.
3. **No fabricated numbers.** If data is missing, output
   `Data unavailable` / `Evidence insufficient`（证据不足）— never guess.
4. **Evidence-graded.** Every material claim carries a Source, publication
   date, data year, country, methodology, and an Evidence Level S/A/B/C/D.
   Core judgments require S or A. (See `docs/methodology.md`.)
5. **Counter-consensus by default.** Media-hot careers are not automatically
   good careers (demand ↑ but supply ↑↑ and entry wages ↓). Low-profile careers
   with low AI exposure + high labor shortage (e.g. HVAC, nursing, industrial
   maintenance) may be structurally stronger. Let data decide.
6. **Privacy by default.** Do not persist, upload, or share user personal data
   (age, income, health, family, immigration plans). See `docs/privacy.md`.
7. **Model-agnostic & bilingual.** No vendor-specific APIs. User writes
   Chinese → answer entirely in Chinese; English → entirely in English.
   No machine-translation-style mixing. See `docs/bilingual.md`.

## When to use / When not to use

**Use when the user asks:** future-proof career choice; "will AI replace my
job"; personal career stress test; career transition paths and their costs;
cross-country career comparison; immigration-driven occupation selection;
"what should I study/train for".

**Do not use for:** generic job-hunting/cover letters; resume editing;
current-day salary negotiation; financial/investment advice; requests to rank
"the jobs AI will never replace" as a definitive list (answer with scenario-
based reasoning and uncertainty instead — see Test Case 10 in `examples/`).

## Inputs · 输入

Minimum: an **occupation** (any language) + a **country/region**.
Optional personal profile (all optional, ask only what the goal requires):
age, education, current skills, language level, work experience, income,
savings, physical constraints, working-hour preference, risk tolerance,
training budget, weekly learning time, immigration goal, desired countries,
family constraints, career goal (high income / quick employment / immigration /
long-term stability).

If the occupation is ambiguous, map it to a standard classification first
(Step 4 below) and confirm with the user.

## Workflow · 标准工作流程

Execute these 16 steps. Skip a step only if its data is unavailable — then
mark it `Data unavailable` explicitly. For detailed rules per step, read
`docs/methodology.md`.

1. **Identify the user's goal**（识别目标）— high income / quick employment /
   immigration / AI-era stability / general exploration. This selects the
   scoring weight profile (`docs/scoring.md` §3).
2. **Identify country/region**（识别国家）— load the matching Country Data
   Adapter (`docs/data-sources.md` §3). If the user compares countries, load
   each adapter separately; never extrapolate one country's wages to another.
3. **Identify the occupation**（识别职业）— resolve synonyms and job titles.
4. **Map to standard classification**（映射标准职业分类）— ISCO-08 as the
   global spine; O*NET-SOC (US), ANZSCO (AU), NOC (CA), 国家职业分类 (CN),
   JSSCO/職業分類 (JP), ESCO (EU). Record the mapping.
5. **Get occupation tasks**（获取职业任务）— task list from O*NET or the
   national classification. Occupation → Tasks, not occupation → one score.
6. **Get current employment data**（当前就业数据）— employment, median wage,
   openings from the country's official statistics (BLS, ABS, StatsCan,
   Eurostat, 国家统计局 …). Record data year.
7. **Get AI exposure data**（AI暴露数据）— ILO–NASK exposure gradient (1–4),
   Anthropic Economic Index task coverage. State that exposure ≠ job loss.
8. **Get employment projections**（就业预测）— official projections
   (e.g. BLS Employment Projections, Jobs and Skills Australia, ESDC/Job Bank,
   CEDEFOP). Label as `Projection`.
9. **Get demographic / macro trends**（人口与宏观趋势）— aging, green
   transition, labor shortage lists (OECD, World Bank, national sources).
10. **Build the three AI scenarios**（建立三种AI情景）— Modest / Substantial /
    Extreme, anchored to Anthropic's Economic Scenarios. Rules and anchor
    numbers: `docs/scenarios.md`. Never present scenarios as predictions.
11. **Run the stress test**（职业压力测试）— task-level analysis
    (`docs/methodology.md` §4): per task → exposure, automation potential,
    augmentation potential, human dependency → aggregate to the occupation.
12. **Build the transition graph**（职业转型图）— adjacent occupations ranked
    by skill overlap, training time/cost, salary delta, risk reduction,
    mobility. Model: `docs/methodology.md` §5.
13. **Apply personal fit**（结合个人条件）— constraints (age, health, budget,
    hours, language) filter and re-rank options. Missing info → ask, or state
    assumptions explicitly.
14. **Compute opportunity cost**（机会成本）— training cost + foregone income
    vs. expected wage delta and risk reduction, per path.
15. **Output recommendation**（输出推荐）— use the Standard Output Format
    below. Show the score under each of the three scenarios, not one number.
16. **List evidence**（列出证据）— every key figure with source, date, data
    year, evidence level, freshness tier (Fresh 0–1y / Aging 1–3y /
    Old 3–5y / Historical >5y).

## Data source hierarchy · 数据源层级

**Global layer** (use for cross-country logic): Anthropic (Economic Index,
Economic Scenarios), ILO, WEF Future of Jobs, OECD, IMF, World Bank,
Stanford AI Index.

**Country layer** (only via adapters, never hardcoded): US → BLS + O*NET +
Census; China → 国家统计局 + 人社部 + 国家职业分类; Australia → Jobs and Skills
Australia + ABS + Home Affairs; Canada → Statistics Canada + Job Bank/ESDC +
IRCC; EU → Eurostat + CEDEFOP + ESCO; Japan → Statistics Bureau + MHLW.

Full whitelist with URLs, what each source is authoritative *for* (and not
for), and licensing notes: **`docs/data-sources.md`**. Do not copy third-party
datasets into output; cite and link instead.

## Scoring · 评分

Compute a **Career Future Score (0–100)** per scenario, from 8 dimensions:
Future Demand 25%, AI Resilience 20%, Wage Potential 15%, Labor Scarcity 10%,
Demographic Tailwind 10%, Entry Feasibility 10%, Geographic Mobility 5%,
AI Complementarity 5% — then **re-weight dynamically by the user's goal**
(immigration → mobility/shortage/regulation weights up; quick employment →
training time/barrier/cost up; high income → wage up; AI-era stability →
resilience/complementarity up). Dimension scoring rubrics, goal-based weight
profiles, and worked examples: **`docs/scoring.md`**.

Never emit a dimension score without an evidence basis; if evidence is weak
(level B/C only), say so and lower the stated confidence instead of inflating
precision.

## Standard Output Format · 标准输出格式

```
# Career Future Stress Test / 未来职业压力测试
## 1. Executive Summary          — one-sentence verdict
## 2. Current Market             — observed data, with year
## 3. AI Impact                  — task-level exposure / automation / augmentation
## 4. Future Scenarios           — Modest / Substantial / Extreme scores
## 5. Career Resilience          — AI resilience + robotics exposure
## 6. Employment Outlook         — official projections (labeled)
## 7. Income Outlook             — wage evidence (local data only)
## 8. Main Risks
## 9. Main Opportunities
## 10. Personal Fit               — given the user's constraints
## 11. Alternative Careers        — adjacent occupations
## 12. Transition Path            — costed routes: time, cost, upside, risk reduction
## 13. Evidence                   — table: claim | source | date | data year | level | freshness
## 14. Uncertainty                — what is unknown / weakly evidenced
```

Country comparison requests → add a comparison table (dimensions × countries)
using each country's own data; see `examples/global-career.md`.

## Anti-hallucination rules · 反幻觉规则（硬性）

Forbidden: inventing wages, employment counts, AI replacement rates, labor
gaps, immigration policies, licensing requirements, or statistics; stating
scenarios as facts; treating correlation as causation; citing media opinion as
official data; implying affiliation with or endorsement by any data provider
(Anthropic, ILO, WEF, OECD, IMF, BLS, O*NET, Stanford, etc.).

If verification fails → output `Data unavailable`（暂无数据）or
`Evidence insufficient`（证据不足）. A smaller, honest answer beats a
comprehensive fabrication.

## Bundled resources · 资源索引

Load on demand (progressive disclosure), do not preload everything:

- `docs/methodology.md` — full 16-step method, task-level model (§4),
  transition graph model (§5), statement-type taxonomy, evidence levels
- `docs/data-sources.md` — global + per-country source whitelist, authority
  scope, freshness policy
- `docs/scoring.md` — dimension rubrics, default weights, goal-based
  re-weighting, worked example
- `docs/scenarios.md` — three-scenario model anchored to Anthropic Economic
  Scenarios, scenario-adjusted scoring rules
- `docs/privacy.md` — privacy-by-default rules
- `docs/bilingual.md` — canonical EN field names + 中文 display names, language
  behavior
- `schemas/` — JSON Schemas: `career.json` (stress-test result),
  `occupation.json`, `country.json` (adapter interface), `evidence.json`,
  `scenario.json`
- `examples/` — worked analyses: China, US, Australia, multi-country
  comparison, transition path
- `data/README.md` — policy: no third-party data vendored; links only
