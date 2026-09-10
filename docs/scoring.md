# Scoring Model · 评分模型

Career Future Score (CFS): 0–100, computed **per scenario** (Modest /
Substantial / Extreme). Never report a single blended number without the
scenario spread.

## 1. Dimensions · 维度

| # | Dimension | 中文 | What it measures | Primary sources |
|---|---|---|---|---|
| 1 | Future Demand | 未来需求 | Official projection direction & magnitude | BLS EP, JSA, Job Bank, CEDEFOP, MOHRSS 缺工排行 |
| 2 | AI Resilience | AI韧性 | 100 − (automation-driven task loss risk); transformation-adjusted | ILO–NASK gradient, Anthropic Index, task model |
| 3 | Wage Potential | 工资潜力 | Current median + trajectory, local | BLS OEWS, ABS, StatCan, NBS, MHLW |
| 4 | Labor Scarcity | 劳动力稀缺 | Shortage lists, vacancy/unemployment ratio | JSA SPL, Job Bank, MOHRSS, Hello Work |
| 5 | Demographic Tailwind | 人口顺风 | Aging/care demand, working-age trends | OECD, World Bank, national stats |
| 6 | Entry Feasibility | 进入可行性 | Inverse of training time, cost, licensing barrier | Regulators, O*NET Job Zones, national qualification frameworks |
| 7 | Geographic Mobility | 跨国流动性 | Cross-border employability, migration-list presence | Home Affairs, IRCC, national lists |
| 8 | AI Complementarity | AI互补性 | Augmentation upside: does AI make this worker more productive? | Anthropic Index (augmentation share), task model |

## 2. Dimension rubric (0–100) · 评分标尺

Score each dimension on evidence. Anchor bands:

- **80–100**: Strong direct S/A evidence favorable (e.g. occupation on
  official shortage list AND positive official projection).
- **60–79**: Favorable evidence, partially indirect or Aging data.
- **40–59**: Mixed or neutral evidence.
- **20–39**: Unfavorable evidence (declining projection, high exposure
  gradient 3–4 with low augmentation).
- **0–19**: Strong unfavorable S/A evidence (e.g. official projection of
  steep decline).
- **Insufficient evidence**: do not score. Mark the dimension
  `"insufficient evidence"`, exclude it from the weighted sum, and renormalize
  the remaining weights. Report this renormalization.

## 3. Weights · 权重

Default profile (`balanced`):

```
Future Demand 25% · AI Resilience 20% · Wage Potential 15% ·
Labor Scarcity 10% · Demographic Tailwind 10% · Entry Feasibility 10% ·
Geographic Mobility 5% · AI Complementarity 5%
```

Goal-based profiles — apply these deltas, then renormalize to 100%:

| Goal | 中文 | Weight changes |
|---|---|---|
| `high-income` | 高收入 | Wage Potential +10, Future Demand +5; reduce Entry Feasibility −5, Demographic −5, Mobility −5 |
| `immigration` | 移民 | Mobility +15, Labor Scarcity +10, regulation check becomes a hard gate; reduce Demographic −5, AI Complementarity −5, Wage −5, Resilience −5, Demand −5 |
| `quick-employment` | 快速就业 | Entry Feasibility +15, Labor Scarcity +5; reduce Wage −5, Demographic −5, Mobility −5, Complementarity −5 |
| `ai-era-stability` | AI时代长期稳定 | AI Resilience +10, AI Complementarity +10; reduce Wage −5, Entry −5, Demographic −5, Mobility −5 |

Hard gates (applied before scoring): licensing/regulatory ineligibility,
physical constraint conflict, budget infeasibility → mark path `blocked` with
reason, do not score.

## 4. Scenario adjustment · 情景调整

Compute the CFS three times. Scenario affects primarily dimensions 1, 2, 4, 8
via the task-automation shares defined in `docs/scenarios.md`:

```
AI Resilience_scenario = 100 − 100 × AutomatedShare_scenario × SeverityFactor
```

where `SeverityFactor ∈ [0,1]` reflects how directly automated tasks translate
to employment risk in that occupation (accountability, licensing, physicality
lower it). `SeverityFactor` is `Model inference` — state it and its basis.

Demand-side: under Substantial/Extreme, apply the scenario's macro
assumptions (e.g. cognitive vs. other-occupation divergence in Anthropic's
model) as a qualitative up/down adjustment with reasoning shown — not as
invented percentages.

## 5. Worked example · 示例

Occupation: Electrician, Australia, goal `immigration`, evidence available
(S-level): JSA Skills Priority List presence, ABS earnings, Home Affairs
occupation list, ILO gradient ~1–2 (physical trade).

| Dimension | Score (Substantial) | Weight (immigration profile) | Basis |
|---|---|---|---|
| Future Demand | 75 | 20% | JSA projection positive |
| AI Resilience | 85 | 15% | Low GenAI exposure, physical tasks; robotics moderate |
| Wage Potential | 70 | 10% | ABS earnings data |
| Labor Scarcity | 85 | 20% | On Skills Priority List |
| Demographic Tailwind | 55 | 5% | Neutral-to-positive |
| Entry Feasibility | 50 | 10% | Licensing + apprenticeship length |
| Geographic Mobility | 85 | 20% | On skilled occupation lists |
| AI Complementarity | 40 | 0%→renormalized | Weak direct evidence |

CFS(Substantial) ≈ 0.20·75 + 0.15·85 + 0.10·70 + 0.20·85 + 0.05·55
+ 0.10·50 + 0.20·85 ≈ **76** (illustrative arithmetic only — real runs must
cite actual current figures).

## 6. Reporting rules · 报告规则

- Always show: the three scenario scores, the weight profile used, the
  dimension table with evidence levels, and dimensions excluded for
  insufficient evidence.
- Round to whole numbers; never show false precision (no 73.4).
- A score is a structured summary of cited evidence, not a measurement.
  Say so.
