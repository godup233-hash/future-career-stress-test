# Methodology · 方法论

> Canonical language: English. Chinese display names follow each term on first use.
> 规范字段名为英文，首次出现附中文显示名。

This document is the full procedure behind the 16-step workflow in `SKILL.md`.
Load it when executing a stress test.

---

## 1. Statement-type taxonomy · 陈述类型学

Every sentence in an output that makes a claim about the world MUST be
classifiable into exactly one type, and must be labeled when it is not
obviously `Observed`:

| Type | 中文 | Definition | Example |
|---|---|---|---|
| `Observed` | 观察事实 | Directly measured, published data | "Median annual wage was $X in May 2024 (BLS OEWS)." |
| `Historical trend` | 历史趋势 | Pattern in past observed data | "Employment grew ~Y%/yr over 2019–2024." |
| `Projection` | 官方预测 | Forecast published by an official/statistical body | "BLS projects +Z% employment 2024–2034." |
| `Scenario` | 情景模拟 | Conditional what-if under stated assumptions | "Under the Extreme AI scenario, demand for task T could fall sharply." |
| `Model inference` | 模型推断 | This skill's own computed judgment from inputs | "We infer medium automation potential from the task mix." |
| `Opinion` | 观点 | Arguable interpretation | "We judge this path underrated relative to media attention." |

Rules:
- Never let a `Scenario` read as a fact. Prefix: "Under this scenario… / 在该情景下…".
- Never upgrade `Model inference` to `Observed` by omitting the label.
- WEF employer-survey expectations are `Projection`-class survey data — say
  "employers surveyed by WEF expect…", not "jobs will…".

## 2. Evidence levels · 证据等级

| Level | Class | Examples |
|---|---|---|
| **S** | Official government / international organization / primary research with published methodology | BLS, O*NET, ILO, OECD, Eurostat, ABS, Statistics Canada, 国家统计局, Anthropic Economic Index & Economic Scenarios, WEF Future of Jobs |
| **A** | Major research institution / peer-reviewed or recognized academic research | Stanford AI Index, NBER/working papers by established researchers, IMF analysis |
| **B** | Industry research with stated methodology | LinkedIn Economic Graph, Indeed Hiring Lab, major consultancy reports |
| **C** | Secondary media / aggregators | News articles summarizing any of the above |
| **D** | Unverified / anecdotal | Forum posts, unsourced claims — never usable as a basis |

Requirements:
- Core judgments (score dimensions 1–5) require ≥ one S or A source, or must be
  reported with `confidence: low` and an explicit note.
- C-level evidence may inform commentary only, never scores.
- Every evidence entry records: `source`, `url`, `published_at`,
  `data_period`, `retrieved_at`, `country`, `methodology_note`, `level`.
  See `schemas/evidence.json`.

## 3. Data freshness · 数据新鲜度

| Tier | 中文 | Age of data period (from today) | Policy |
|---|---|---|---|
| Fresh | 新鲜 | 0–1 year | Use freely |
| Aging | 偏旧 | 1–3 years | Use; note the year |
| Old | 较旧 | 3–5 years | Use only with explicit year labels; prefer checking for updates |
| Historical | 历史 | >5 years | Use only for long-run trend context, never for current-state claims |

Old data is not deleted or hidden — it is labeled. Trend analysis across
Historical + Fresh is legitimate and encouraged; presenting Old data as
current is a violation.

## 4. Task-level occupation model · 职业任务级分析模型

The atomic unit is the **task**, not the occupation.

### 4.1 Decompose
For the mapped occupation, obtain its task list:
1. US or global fallback → O*NET (Tasks, Work Activities, Technology Skills).
2. Otherwise → national classification (ANZSCO, NOC, ESCO, 国家职业分类大典)
   or ISCO-08 4-digit unit-group tasks.
3. If no structured list exists, derive 5–10 tasks from official occupation
   descriptions and mark them `Model inference`.

### 4.2 Score each task on four axes (0–4 ordinal, evidence-anchored)

| Axis | 中文 | Anchors |
|---|---|---|
| AI Exposure | AI暴露 | Map to ILO–NASK gradient (1 = none … 4 = highest). Anthropic Economic Index task coverage corroborates. |
| Automation Potential | 自动化潜力 | 0 = requires physical presence/dexterity or legal human accountability; 4 = digital, rule-based, verifiable output (e.g. data entry). |
| Augmentation Potential | AI增强潜力 | 0 = AI adds little; 4 = AI clearly raises quality/speed while human remains in loop (e.g. drafting, analysis, monitoring). |
| Human Dependency | 人类依赖 | 0 = no human needed in principle; 4 = requires trust, accountability, physicality, or licensed judgment (e.g. bathing a patient, signing off a wiring installation). |

Heuristic anchors (must be stated as `Model inference` unless directly
sourced): routine cognitive digital tasks → high automation; judgment +
communication → augmentation; physical/embodied → low automation, check
robotics separately.

### 4.3 Robotics Exposure · 机器人暴露
Score separately from AI exposure (0–4). Drivers: physical task share,
environment structuredness (factory floor vs. unstructured homes/sites),
robot cost curve vs. local wage. Note: Anthropic's scenario model explicitly
excludes robotics advances — flag this gap when robotics matters.

### 4.4 Aggregate to occupation
- Compute time-weighted task shares if the source provides them (O*NET gives
  task importance; use as proxy weights, labeled `Model inference`).
- Produce: share of tasks automated / augmented / unchanged / newly-created
  under each scenario (`docs/scenarios.md`).
- State the transformation narrative: which tasks leave the bundle, which grow,
  what the job plausibly becomes. **Occupations transform; do not write
  "this job will disappear" without S/A evidence of actual employment decline.**

## 5. Career Transition Graph · 职业转型模型

### 5.1 Candidate generation
Generate 3–8 adjacent occupations via:
1. Skill/task overlap with the origin occupation (O*NET skills, national
   classification descriptions).
2. Published shortage lists / growing-occupations lists in the target country
   (see `docs/data-sources.md`).
3. Known ladders (e.g. IT Support → Cloud Support → Cybersecurity;
   Electrician → Automation Technician → Robotics Maintenance).
Mark ladder suggestions as `Model inference` unless sourced.

### 5.2 Edge metrics (per transition origin → target)
| Metric | 中文 | How to estimate |
|---|---|---|
| Skill overlap | 技能重合度 | 0–100%; from shared tasks/skills in classification data; else inferred |
| Training time | 培训时间 | Months to reach target entry level, from licensing/official training info |
| Training cost | 培训成本 | Local-currency direct cost (tuition/certification), local source only |
| Salary change | 薪酬变化 | Target median − origin median, same country, same year basis |
| Risk reduction | 风险降低 | Origin Career Future Score − target score (same scenario) |
| Demand delta | 需求增量 | Official projection difference |
| Mobility | 流动性 | Whether target appears on destination-country shortage/migration lists |

### 5.3 Transition Score (0–100, default)
```
TransitionScore = 0.30 × SkillOverlap
                + 0.25 × (1 − NormalizedTrainingBurden)   # time+cost combined
                + 0.20 × NormalizedSalaryUpside
                + 0.15 × RiskReduction
                + 0.10 × DemandDelta
```
Re-weight if the user goal says otherwise (immigration → raise mobility;
budget-constrained → raise training burden term). Always show the raw
metrics, not just the score. Output per path: **Transition Cost, Transition
Difficulty, Expected Upside, Risk Reduction** plus evidence.

## 6. Personal fit filtering · 个人适配

Apply hard constraints as filters, soft preferences as ranking adjustments:
- Hard filters: physical/health constraints vs. job physicality (use O*NET Work
  Context or national equivalents); available hours vs. shift patterns;
  training budget < required training cost; licensing age/language minimums.
- Soft adjustments: risk tolerance scales weight of scenario spread
  (risk-averse → penalize high variance across scenarios); time horizon
  (needs income in <6 months → Entry Feasibility dominates).
- State every assumption made for missing profile fields.

## 7. Country comparison · 国家比较

For "is occupation X better in country A or B": load each Country Data
Adapter independently; fill the comparison table from each country's own
sources; add a row for each of: Demand, Wage, AI Risk, Labor Shortage,
Training Cost, Regulation, Immigration Value, Long-term Resilience.
Never convert purchasing-power or assume wage transferability; show local
currency + local context. Note data-year mismatches between countries.

## 8. Uncertainty reporting · 不确定性

The final section of every output must list:
- which dimensions rest on B/C evidence or inference,
- where country data years diverge,
- which scenario assumptions drive the conclusion most (sensitivity),
- what would change the recommendation (falsifiability).
