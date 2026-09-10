# Scenario Model · 情景模型

**Scenario, not forecast. 情景模拟，不是确定性预测。**
No probabilities are attached to any scenario. This mirrors Anthropic's own
framing of its Economic Scenarios work (Korinek et al., Anthropic Institute
Working Paper 2026-02, Sept 2026) — scenarios are structured what-ifs anchored
to current data.

## 1. The three scenarios · 三种情景

Anchored to Anthropic's Economic Scenarios (US economy, task-based on O*NET).
Anchor figures below are from that model (data year 2025–2026, level S); they
describe the **macro** environment, not any single occupation. Verify against
the live explorer (https://www.anthropic.com/institute/econ-scenarios) at
analysis time and update if revised.

| | Scenario 1: Modest 渐进 | Scenario 2: Substantial 大规模普及 | Scenario 3: Extreme 极高速 |
|---|---|---|---|
| Framing | AI impact ≈ internet-scale, gradual | ~2× normal growth; agents significant | Growth beyond recorded history; recursive capability gains |
| AI-affected task share (economy-wide) | ~4% of tasks by 2030 | materially higher | ~half of cognitive-worker tasks |
| Cognitive employment (US, vs. mid-2026) | −0.5% | −3.9% | −21.5% |
| Economy-wide unemployment 2030 | 3.9% (baseline 3.8%) | 4.6% | 11.9% |
| Cognitive wages vs. no-AI | +0.4% | −0.3% | −11.5% |
| Other-occupation wages vs. no-AI | +1.1% | +5.9% | (model: divergence widens) |
| GDP 2030 vs. no-AI | +1.6% | +8.3% | +32.4% |

Key structural insight from the model: **cognitive/knowledge occupations bear
the downside in aggressive scenarios, while non-cognitive occupations may see
wage gains** — the analytical basis for counter-consensus findings (trades,
care work showing relative strength under Substantial/Extreme).

Model exclusions to always disclose: no robotics advances, no business-cycle
shocks, no financial-market disruptions, no new-task policy responses.

## 2. Applying scenarios to an occupation · 情景落到职业

For each scenario, derive task-level automation/augmentation shares:

| Scenario | Automated share of exposed tasks | Augmented share | Guidance |
|---|---|---|---|
| Modest | Low: adoption friction dominates; most exposed tasks only partially automated | Moderate | Use ILO gradient as ceiling; observed adoption (Anthropic Index) as floor |
| Substantial | Medium: exposed digital tasks largely automated; new tasks appear | High | Default reference scenario for planning |
| Extreme | High: ~90% of affected cognitive task instances automated (per Anthropic's extreme assumption); few replacement tasks | Saturates | Stress boundary, not a plan basis |

Occupation-level translation (`Model inference`, must be shown):
1. Start from the occupation's task table (`docs/methodology.md` §4).
2. Under each scenario, mark each task: automated / augmented / unchanged /
   newly created.
3. Aggregate shares → feed `docs/scoring.md` §4 (AI Resilience, Demand
   adjustments).
4. Physical-trade occupations: scenario deltas apply mainly via robotics,
   which the anchor model excludes — state this and treat robotics as a
   separate slow-moving risk with its own evidence.

## 3. Scenario spread as a signal · 情景差作为信号

Report CFS(Modest), CFS(Substantial), CFS(Extreme) together.

- Small spread (≤10 pts): robust occupation — resilience across AI paths.
- Large spread (≥25 pts): path-dependent occupation — recommendation must
  hedge (e.g. "enter, but build adjacent skills X, Y as options").
- Risk-averse users: weight the worst-case scenario more (see
  `docs/methodology.md` §6).

## 4. Non-US countries · 非美国国家

The anchor numbers are US-specific. For other countries, transfer the
*structure* (three speeds, task-based mechanism) and anchor the *magnitudes*
locally: exposure shares differ by income level (ILO: ~34% of employment
exposed in high-income countries vs ~11% in low-income). Label all transferred
magnitudes `Model inference`.

## 5. Update policy · 更新

Anthropic and ILO revise their indices. At each analysis, check for newer
editions; record the edition used in the Evidence section. If anchors in this
file conflict with a newer primary source, the primary source wins — and this
file should be updated via PR (see CONTRIBUTING).
