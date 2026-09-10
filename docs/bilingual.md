# Bilingual Design · 双语设计

## Language behavior · 语言行为

- User writes in Chinese → the **entire** output is in Chinese (section
  headers, tables, evidence notes). English canonical names may appear in
  parentheses on first use only.
- User writes in English → entirely English.
- Mixed input → use the dominant language of the user's last message.
- Never produce machine-translation-style interleaving (half-Chinese
  sentences with English clauses).
- Evidence source names stay in their original language (BLS, 国家统计局).

## Canonical field names · 规范字段名

All schemas and internal reasoning use English canonical names; Chinese
display names map 1:1:

| Canonical | 中文显示名 |
|---|---|
| AI Exposure | AI暴露程度 |
| Automation Potential | 自动化潜力 |
| Augmentation Potential | AI增强潜力 |
| Task Transformation | 任务结构变化 |
| Employment Demand / Future Demand | 就业需求 / 未来需求 |
| Wage Potential | 工资潜力 |
| Labor Shortage / Labor Scarcity | 劳动力短缺 / 稀缺度 |
| Entry Barrier / Entry Feasibility | 进入门槛 / 进入可行性 |
| Training Cost / Training Time | 培训成本 / 培训时间 |
| Geographic Mobility | 跨国就业能力 |
| Demographic Tailwind | 人口顺风 |
| Regulation Risk / Regulatory Barrier | 监管风险 / 监管门槛 |
| Offshoring Risk | 外包风险 |
| Robotics Exposure / Robotics Risk | 机器人暴露 / 机器人自动化风险 |
| AI Complementarity | AI互补性 |
| AI Resilience | AI韧性 |
| Career Future Score | 职业未来评分 |
| Career Transition Graph | 职业转型图 |
| Transition Cost / Difficulty / Expected Upside / Risk Reduction | 转型成本 / 难度 / 预期收益 / 风险降低 |
| Evidence Level | 证据等级 |
| Scenario, not forecast | 情景模拟，不是确定性预测 |
| Data unavailable / Evidence insufficient | 暂无数据 / 证据不足 |

New canonical terms added to the skill must extend this table in the same PR.
