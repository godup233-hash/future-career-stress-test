# Future Career Stress Test · 未来职业压力测试

[English README → README_EN.md](README_EN.md)

一个**证据驱动**的开源 AI Skill：基于权威劳动力市场数据、任务级 AI 自动化研究、
AI 能力趋势、人口结构与宏观情景，对个人职业做**未来压力测试**，并给出
**可计算成本的职业转型路线**。

它不是一个"AI 职业排行榜"，也不是"AI 会不会取代我"的问答机器人。

## 它回答什么问题

- 我的职业中，**哪些任务**容易被自动化、哪些会被 AI 增强、哪些仍依赖人类？
- 在 AI 渐进 / 大规模普及 / 极高速发展三种情景下，我的职业分别什么处境？
- 我该保留、升级、放弃哪些技能？**可以转去哪**，每条路的成本、难度、收益、
  风险降低是多少？
- 同一个职业，在中国 / 美国 / 澳大利亚 / 加拿大 / 欧洲 / 日本哪个更值得做？
- 以我的年龄、预算、时间、身体状况和移民目标，哪条路径**对我**最优？

## 核心理念

1. **AI 暴露 ≠ 自动化 ≠ 失业。** 职业是一束任务；任务被自动化、增强、不变
   或新生，职业被**重构**而不是简单消失（ILO 2025 的核心结论）。
2. **情景，不是预测。** 所有未来判断分三种情景（对齐 Anthropic Economic
   Scenarios），并显式标注"情景模拟，不是确定性预测"。
3. **没有编造的数字。** 每个关键结论标注来源、年份、数据期、证据等级
   （S/A/B/C/D）与新鲜度；证据不足就直说"证据不足"。
4. **反共识。** 数据优先于媒体热度：媒体热门职业（需求↑但供给↑↑）不一定
   适合普通人；低讨论度职业（低暴露 + 高短缺）可能更具长期韧性。
5. **隐私默认。** 不保存、不上传任何个人资料。
6. **模型无关 + 双语。** 不依赖任何厂商 API；中文提问全程中文，英文提问
   全程英文。兼容所有遵循 [Agent Skills 开放规范](https://agentskills.io)
   的 Agent（Claude、Codex、Gemini CLI、Copilot 等），也可作为普通
   Markdown 提示词在任何大模型上使用。

## 快速开始

### 作为 Skill 安装（支持 Agent Skills 规范的平台）

将整个 `future-career-stress-test/` 目录放入你的 Agent 技能目录，例如：

```bash
# Claude Code（个人级）
cp -r future-career-stress-test ~/.claude/skills/

# 项目级
cp -r future-career-stress-test /path/to/project/.claude/skills/
```

其他兼容平台（Codex CLI、Gemini CLI、Cursor、Copilot 等）按其技能目录
约定放置即可——本 Skill 仅使用规范标准结构（SKILL.md + references +
schemas），无平台特有依赖。

### 作为普通提示词使用

把 `SKILL.md` 全文粘贴给任何大模型，然后直接提问。

### 提问示例

```
我 23 岁，大专在读，没什么技能，帮我做一次职业压力测试，目标快速就业+长期稳定。
```

```
我是美国 software developer，25 岁，担心被 AI 替代，给我转型路径和成本。
```

```
比较一下护理在中国、美国、澳大利亚、加拿大哪个更值得做，我想移民。
```

## 项目结构

```
future-career-stress-test/
├── SKILL.md              # Skill 主文件（Agent Skills 规范）
├── README.md             # 本文档
├── README_EN.md          # English documentation
├── LICENSE               # MIT
├── CONTRIBUTING.md       # 贡献指南
├── CHANGELOG.md          # 版本历史
├── docs/
│   ├── methodology.md    # 完整方法论（任务级模型、转型图、证据等级）
│   ├── data-sources.md   # 数据源白名单（全球层 + 各国适配器）
│   ├── scoring.md        # 评分模型（维度、权重、目标化动态调权）
│   ├── scenarios.md      # 三情景模型（锚定 Anthropic 情景参数）
│   ├── privacy.md        # 隐私规则
│   └── bilingual.md      # 双语规范与字段对照表
├── schemas/              # JSON Schema：career / occupation / country / evidence / scenario
├── examples/             # 中国 / 美国 / 澳大利亚 / 多国比较 / 转型 示例
└── data/                 # 有意为空：不内置第三方数据，仅运行时引用
```

## 数据源（摘要）

全球层：Anthropic Economic Index & Economic Scenarios · ILO · WEF Future of
Jobs · OECD · IMF · World Bank · Stanford AI Index。
国家层（适配器模式，非硬编码）：BLS + O*NET（美）· 国家统计局 + 人社部（中）·
Jobs and Skills Australia + ABS（澳）· StatCan + Job Bank + IRCC（加）·
Eurostat + CEDEFOP + ESCO（欧）· 总务省统计局 + 厚劳省（日）。

完整白名单与使用边界见 [docs/data-sources.md](docs/data-sources.md)。
**本仓库不内置任何第三方数据**，分析时从官方来源实时检索并标注检索日期。

## 免责声明

This project is an independent open-source project and is **not affiliated
with** Anthropic, ILO, WEF, OECD, IMF, BLS, O*NET, Stanford University, or
any other data provider.（本项目为独立开源项目，与上述任何数据机构无隶属
或背书关系。）

本 Skill 输出为研究辅助信息，不构成就业、移民或投资决定建议；所有情景
均为条件假设推演，不是对未来的预测。

## 贡献与许可

欢迎贡献：见 [CONTRIBUTING.md](CONTRIBUTING.md)。License: [MIT](LICENSE)。
