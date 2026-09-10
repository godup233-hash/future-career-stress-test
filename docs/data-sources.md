# Data Sources Whitelist · 数据源白名单

Only sources on this list may ground scores and factual claims. Each entry
states what the source is authoritative **for** — and **not for**. Do not copy
datasets into this repository or into outputs; cite and link.

## 1. Global layer · 全球层

| Source | URL | Authoritative for | NOT for | Level |
|---|---|---|---|---|
| Anthropic Economic Index | https://www.anthropic.com/economic-index | Observed AI usage mapped to O*NET tasks; augmentation vs. automation shares; task coverage | Predicting employment outcomes | S |
| Anthropic Economic Scenarios (Institute) | https://www.anthropic.com/institute/econ-scenarios | Structured what-if macro scenarios for AI (task-based, O*NET-anchored) | Forecasts — explicitly "scenarios, not predictions"; also excludes robotics | S |
| ILO — Generative AI and Jobs (ILO–NASK refined index, WP140, 2025) | https://www.ilo.org/ | GenAI occupational exposure gradients (1–4), global employment shares exposed, gender/country-income differences | Actual job losses — exposure ≠ displacement | S |
| WEF Future of Jobs Report (latest: 2025) | https://www.weforum.org/publications/the-future-of-jobs-report-2025/ | Employer-survey expectations: fastest growing/declining roles and skills, macrotrend drivers | Precise counts for a single occupation; it is survey expectation data | S (survey) |
| OECD Employment/AI work | https://www.oecd.org/ | Cross-country labor markets, skills, wages, AI & work policy | Occupation-level wages in a single city | S |
| IMF analysis | https://www.imf.org/ | Macro impact of AI: productivity, GDP, labor share, inequality | Occupation-level analysis | S |
| World Bank | https://www.worldbank.org/ | Demographics, income classification, labor force context | Occupation task detail | S |
| Stanford AI Index | https://aiindex.stanford.edu/ | AI capability trends, cost, investment, adoption — the *speed* dimension | Direct occupation predictions | A |

## 2. Country layer · 国家层（Country Data Adapters）

A Country Data Adapter is an interface, not a hardcoded table. Each adapter
MUST provide: (a) occupation classification + crosswalk to ISCO-08,
(b) employment & wage statistics, (c) official projections or outlook,
(d) labor-shortage / priority lists, (e) licensing/regulation registers,
(f) immigration occupation lists where applicable. See `schemas/country.json`.

### United States
| Source | URL | For |
|---|---|---|
| BLS (OEWS, Employment Projections, OOH) | https://www.bls.gov/ | Employment, median wages, 10-year projections, openings |
| O*NET | https://www.onetonline.org/ | Occupation definitions, tasks, skills, abilities, work activities, technology skills, work context |
| Census Bureau | https://www.census.gov/ | Demographics, industry composition |
| U.S. Dept. of Labor | https://www.dol.gov/ | Regulation, apprenticeship (Apprenticeship.gov) |

### China · 中国
| Source | URL | For |
|---|---|---|
| 国家统计局 (NBS) | https://www.stats.gov.cn/ | Employment, wage statistics, industry data |
| 人力资源和社会保障部 (MOHRSS) | http://www.mohrss.gov.cn/ | 国家职业分类大典, 职业技能标准, 最缺工职业排行 (quarterly "最缺工" 100 occupations) |
| 中国就业培训技术指导中心 | http://www.cettic.gov.cn/ | Occupational standards, skill certification |
| 教育部 / 省级统计局 | — | Education pipeline, regional detail |

Note: China has no O*NET-equivalent public task database; use 职业分类大典
task descriptions and mark task-level AI exposure as `Model inference`
anchored to the ILO ISCO-08 gradient.

### Australia
| Source | URL | For |
|---|---|---|
| Jobs and Skills Australia | https://www.jobsandskills.gov.au/ | Labour Market Update, Skills Priority List, employment projections |
| Australian Bureau of Statistics | https://www.abs.gov.au/ | Labour Force, ANZSCO, earnings |
| Dept. of Home Affairs | https://immi.homeaffairs.gov.au/ | Skilled occupation lists (CSOL etc.), visa eligibility |
| Trades Recognition Australia / state regulators | https://www.tradesrecognitionaustralia.gov.au/ | Trade licensing and assessment |

### Canada
| Source | URL | For |
|---|---|---|
| Statistics Canada | https://www.statcan.gc.ca/ | Labour Force Survey, wages, NOC 2021 |
| Job Bank / ESDC | https://www.jobbank.gc.ca/ | Occupational outlooks (3-year), wage reports, shortages |
| IRCC | https://www.canada.ca/ | Express Entry categories, immigration occupation eligibility |
| Provincial regulators | — | Trade certification (e.g. Red Seal) |

### Europe
| Source | URL | For |
|---|---|---|
| Eurostat | https://ec.europa.eu/eurostat | EU labor force, wages, ISCO-based statistics |
| CEDEFOP | https://www.cedefop.europa.eu/ | Skills forecasts, occupational outlooks |
| ESCO | https://esco.ec.europa.eu/ | Occupation/skill taxonomy, task descriptions |
| National statistical offices | — | Country-level detail (Destatis, INSEE, …) |

### Japan
| Source | URL | For |
|---|---|---|
| Statistics Bureau (総務省統計局) | https://www.stat.go.jp/ | Labour Force Survey |
| MHLW (厚生労働省) | https://www.mhlw.go.jp/ | Wage census (賃金構造基本統計調査), labor policy |
| Hello Work | https://www.hellowork.mhlw.go.jp/ | Vacancies, job-seeker data |

### Other countries
Default fallback: ILOSTAT (https://ilostat.ilo.org/) for employment by
occupation (ISCO-08), plus the national statistical office. If neither yields
occupation-level data, say `Data unavailable` and run the analysis on the
global layer only, with `confidence: low`.

## 3. Acquisition policy · 获取方式

1. Prefer live retrieval (web search / fetch) of the source's official page or
   dataset at analysis time; record `retrieved_at`.
2. If the agent environment has no network access, state this limitation and
   use the model's knowledge with strict evidence labeling and freshness
   caveats — never present memorized figures as current.
3. Respect each source's terms of use; do not bulk-scrape; do not vendor
   datasets into this repo (`data/README.md`).
4. Wages: always local currency, always with data year; note gross vs. net
   and full-time basis when known.

## 4. Known limitations · 已知局限

- ILO gradients are occupation-level potential exposure, built from
  task-automation assessments — not measured displacement.
- Anthropic scenarios are US-economy macro models; applying their logic to
  other countries is `Model inference` requiring local anchoring.
- WEF figures are employer expectations, not outcomes.
- China/Japan task-level data is thinner than US O*NET; be explicit.
