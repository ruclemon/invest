# invest 迁移记录

更新日期：2026-11-16

> 本文保留迁移完成时的目录和验收快照，其中非链接路径为历史记录。当前目录见 [项目架构](../design/architecture.md)，后续工作见 [TODO](../TODO.md)。

状态：文档与元数据迁移已完成，核验结果见第 10 节。项目只保存知识、参考定义和私有凭据，没有恢复运行能力。前文保留迁移决策；实际目录、取舍和遗留项以第 10 节为准。

## 1. 目标与已确认边界

从 `/home/devops/investment-assistant` 提取有价值的投资知识、业务流程和资源信息，在 `/home/devops/invest` 建立轻量项目。

- 旧项目已无法运行，不恢复运行。
- 旧代码、测试、历史数据、日志和环境均不迁移。
- 保留投资方法、投资逻辑框架、研究与报告流程设计。
- 保留数据源资料、人工整理的订阅和资产映射，以及仍有用途的密钥、密码信息。
- 未实际使用的行情数据源只保留记录，不保留实现，也不因此安排重新接入。
- 微信公众号文章获取服务已永久下线并失效，此状态由用户确认。废弃相关代码、登录、抓取、重试、恢复及调度流程，不尝试修复旧服务。
- 保留公众号清单，记录后续补充文章下载的 TODO。
- 本次迁移不删除或修改旧项目。未迁移材料暂留原目录供追溯。

## 2. 分类原则

| 分类 | 处理方式 |
|---|---|
| 原文保留 | 先保留完整内容，调整链接；历史案例注明背景，不改写为当前判断 |
| 提炼保留 | 提取方法、公式、业务规则和设计理由，合并重复内容，去掉旧工程依赖 |
| 资料保留 | 保留来源、用途、地址、覆盖范围、限制、使用状态和必要参数 |
| 私有保留 | 凭据和个人账户信息单独保存，不写入普通文档或 Git |
| 不迁移 | 不进入新项目，不等于删除旧文件 |
| 待核对 | 先记录缺项，不猜测、不把示例当作真实配置 |

旧草案、默认参数及已实现规则不等于经过收益验证的方法。整理时区分投资原则、旧系统规则、研究假设和历史案例。

## 3. 投资知识与流程

本节来源均相对于旧项目根目录。

| 来源 | 决定 | 迁移内容 |
|---|---|---|
| `docs/notes/framework.md` | 原文保留 | 定价框架、主导变量、基本面、资金面、预期博弈、信息传播和价差 |
| `docs/notes/playbook.md` | 原文保留 | 操作纪律、交易执行、风险控制、退出条件和认知验证 |
| `docs/notes/strategy.md` | 原文保留 | 策略思路、适用环境、交易结构和失效条件 |
| `docs/drafts/strategy/ia_investment_philosophy_to_positions.md` | 提炼保留 | 投资理念到研究变量、信号、策略、仓位的映射 |
| `docs/drafts/strategy/ia_investment_philosophy_implementation_status.md` | 提炼保留 | 旧系统未充分表达的投资逻辑及其原因，去掉工程完成度记录 |
| `docs/drafts/strategy/ia_report_first_pipeline*.md` | 提炼保留 | 报告结构、时间窗口、证据、风险、失效条件；不迁移旧 schema 和实现方案 |
| `docs/review/report_first_pipeline_investor_review_2026-05-13.md` | 提炼保留 | 观点变化解释、反方证据、催化因素和复盘闭环 |
| `docs/agent/report_interpreter/AGENTS.md` | 提炼保留 | 区分事实与推断、不编造证据、解释策略各条腿的作用 |
| `docs/drafts/features/` 中成交量、基本面、搜索热度、反转和波动率设计 | 提炼保留 | 因子定义、公式、适用范围、限制及历史参数 |
| `docs/drafts/opinion/` 中评分、归一化、作者权重、分位数和 Prompt 设计 | 提炼保留 | 观点抽取、资产映射、时间衰减、聚合和可信度判断 |
| `docs/drafts/signals/ia_signal_pipeline.md`、`signal_engine/README.md` | 提炼保留 | 信号组合和权重含义；参数标为旧项目参考 |
| `docs/drafts/strategy/ia_strategy_engine*.md`、`strategy_engine/strategies/README_long_select.md`、`README_spot_swap_pair.md` | 提炼保留 | 精选做多、配对策略、预算、仓位和风险约束 |
| ETF monitor、发行商 AUM、资产热度报告相关设计 | 提炼保留 | 观察指标、聚合口径、资金与供给变化的研究用途 |
| `docs/architecture.md`、NC design、文章分类、筛选、聚类和去重设计 | 提炼保留 | 信息采集、筛选、研究、判断、报告与复盘的业务流程 |
| NC 日历、Polymarket 排名和主题配额设计 | 提炼保留 | 事件类别、时间语义、筛选标准和解释方法 |
| 两套 `IDEAS.md`、`backlog.md`、`TODO.md` 及 `docs/roadmap.md` | 筛选保留 | 有价值的产品与研究想法；不继承任务编号、排期和旧工程任务 |

重复或已弃用的草案只提取独有的设计理由，不整份复制。发现文档冲突时记录差异和来源，不擅自选定投资口径。

## 4. 数据源、订阅与资源

数量来自本轮配置结构盘点，表示配置条目数，不表示启用数量或可用数量。

| 来源 | 已确认内容 | 处理方式 |
|---|---|---|
| `config/data_sources.json` | Tushare、Alpha Vantage、Polygon、Yahoo Finance、Bitget、Binance、OKX、Futu | 保留资料，先拆出凭据；不迁移任何适配器 |
| `news_collector/config/sources_rss.json` | 64 条 feed 配置 | 保留订阅、地址、用途和原启停状态 |
| `news_collector/config/sources_wechat.json` | 34 条订阅配置 | 保留公众号身份和订阅信息；移除旧服务连接、认证和抓取配置 |
| `config/asset_registry.json` | 15 条资产定义 | 保留资产分类与标识 |
| `config/asset_class_etf_map.json` | 130 条 canonical 映射及分类规则 | 保留人工映射、分类与排除依据 |
| `config/us_etf_aum_issuer_registry.json` | 6 条发行商配置 | 保留发行商与数据获取资料 |
| `config/search_heat_asset_classes.json` | 15 组资产搜索配置 | 保留关键词和映射 |
| `config/asset_heat_universe.json` | 10 条配置 | 保留观察范围 |
| `news_collector/config/asset_aliases.json` | 资产别名与宏观资产范围 | 与资产注册表核对、合并 |
| `news_collector/config/market_event_schedules.json` | 12 条事件配置 | 保留事件规则，具体日期注明时效 |
| `config/opinion_prompts.json`、`news_collector/config/prompts.json` | 观点抽取、叙事及预测市场总结 Prompt | 保留有价值的正文和输入输出含义，合并重复版本 |
| `curation.json`、`polymarket.json`、`summary.json` | 筛选、排名、摘要规则 | 提炼业务规则；不保留并发、重试、旧路径等运行参数 |
| 数据源研究文档 | RSSHub、Substack、加密媒体、资金费率、期货换月、ETF 等 | 保留服务资料与数据口径；移除旧代码操作步骤 |

数据源记录至少包含：名称、用途、覆盖范围、入口、认证要求、已知限制、使用状态、资料来源。

使用状态区分“已确认使用过”“已确认未使用”“永久停用”“待核对”。配置存在或 `enabled` 为真，都不能单独证明实际使用过。尚未确认各行情源的实际使用情况，迁移时不能擅自归类。

### 微信公众号的明确取舍

保留公众号名称、标识、原订阅状态及有研究价值的来源说明。只记录旧文章获取服务已永久下线，不复制旧接入方案。

以下内容不迁移：

- remote exporter 的代码和服务连接配置。
- 扫码登录、Cookie 轮换、认证健康检查和凭据。
- 抓取、限流退避、重复抓取跳过、故障恢复及定时任务。
- `nc_sources_wechat.md`、`nc_wechat_login_remote.md`、`nc_wechat_skip_existing_fetch.md`、`wechat_recovery.md` 中的旧服务流程。
- 微信恢复用的文章 URL 标注和跳过清单，以及旧抓取历史数据。

## 5. 凭据与个人配置

| 位置 | 盘点结果 | 迁移决定 |
|---|---|---|
| `config/data_sources.json` | Tushare token、Alpha Vantage 和 Polygon API key 字段非空 | 私有保留，普通资料只引用凭据名称；不据此推断有效性 |
| `config/openai_compat.local.json` | 主、备用 API key 字段非空 | 私有保留，同时记录关联服务和用途 |
| `news_collector/config/wechat_remote_cookie.local.json` | 旧服务 Cookie 字段非空 | 不迁移，服务已永久失效 |
| 配置引用的环境变量 | 包括飞书 webhook 等 | 沿明确引用核对实际存放位置，不输出真实值 |
| `config/accounts.json` | 7 条账户配置 | 提炼账户类别、预算和风控规则；个人信息如有则私有保存 |

尚未确认独立密码清单，也未完成外部凭据位置盘点。后续仅沿项目明确引用查找，不扫描无关个人文件。

私有材料计划存入 `private/`，目录权限为 `700`，文件权限为 `600`，整个目录加入 Git 忽略。普通文档、资源清单和迁移日志中不得出现密钥、密码、Cookie 或带认证参数的地址。

本轮不调用服务验证凭据，不刷新登录，不触发付费请求。有效性统一标为未验证，明确停用的微信旧服务除外。

## 6. 不迁移清单

- 全部实现代码、测试、golden fixtures、依赖环境和安装产物。
- 行情、文章、报告、数据库、回测等历史数据，以及日志和缓存。
- DuckDB 迁移、历史补数、重跑、对账和数据清理方案。
- CLI 标准化、模块拆分、配置拆分、HTTP client 和 Pydantic 改造文档。
- Prefect、systemd、cron 的旧部署和调度方案。
- 模型价格与延迟 benchmark、旧模型选择结果。
- 版本迁移、历史重算、兼容层切换和旧 schema 实施记录。
- 大部分工程架构评审、代码精简报告、质量评分。
- `CHANGELOG.md`、旧文档索引、工程任务状态原件和项目体量统计。
- 旧项目整套 AGENTS 规则。新项目只建立适用的简短协作规则。

## 7. 目标目录

实际结构如下。为减少文件与目录层级，资源收拢为五份 JSON，提示词作为文档保存。

```text
invest/
├── README.md
├── AGENTS.md
├── MIGRATION_PLAN.md
├── .gitignore
├── docs/
│   ├── framework.md
│   ├── playbook.md
│   ├── strategies.md
│   ├── signals.md
│   ├── workflow.md
│   ├── sources.md
│   ├── data_definitions.md
│   └── ideas.md
├── resources/
│   ├── sources.json
│   ├── assets.json
│   ├── etf_mapping.json
│   ├── research_parameters.json
│   ├── calendar.json
│   └── prompts/               # 三份 Markdown 提示词
└── private/                   # 两份私有 JSON，不进入 Git
```

投资笔记保留正文，流程和规则经过合并。各文档和元数据记录旧来源，日常阅读不依赖旧项目。后续需求统一记在 `docs/ideas.md`，本页只记录迁移状态。

## 8. 执行顺序与验收

1. 核对边界项：真实 watchlist、各行情源使用状态、外部凭据位置、重复与冲突设计。
2. 迁移三份投资笔记，保留原意并整理链接。
3. 提炼信号、策略、新闻处理和报告流程；历史参数单独标注。
4. 整理数据源、订阅、资产映射和 Prompt；拆分普通资料与私有内容。
5. 建立新项目入口与简短规则，核对来源映射和遗漏。

验收条件：

- 阅读 `invest` 即可理解投资框架、业务流程和资源用途，无需运行旧项目。
- 保留的投资规则、公式和参数可追溯；原理、假设、历史案例和旧默认值有明确区别。
- 64 条 RSS、34 条公众号订阅等资源逐项核对，删除或合并条目有理由。
- 微信旧服务没有被作为可用依赖迁入，后续文章下载需求有明确 TODO。
- 未使用行情源只保留记录，未引入实现或自动接入任务。
- 普通文件不含凭据，私有文件权限和 Git 忽略配置正确。
- 没有迁入旧代码、测试和历史数据；旧项目保持不变。

## 9. 待办与待核对项

- [x] 定位配置引用的 watchlist：主配置明确引用 `config/watchlists.example.json`，保留其中 28 项；不声称实际运行或交易过。
- [x] 沿项目明确引用迁移行情、LLM 和飞书凭据，并记录缺项；未验证有效性。
- [x] 核对重点方法和设计的重复及冲突，归入 `docs/signals.md` 与 `docs/data_definitions.md`。没有把所有工程草案逐篇复制或迁入。
- [x] 迁移文档、少量元数据和参考定义，记录实际路径与取舍。
- 行情源的实际使用状态和当前可用性保留为待核对，不以配置选项推断。
- 后续公众号文章下载和其他研究需求统一见 [研究想法与待办](../ideas.md)。微信旧服务永久停用，不恢复旧链路。

## 10. 本次迁移结果

### 来源与目标

| 来源 | 实际目标 | 处理 |
|---|---|---|
| 三份 `docs/notes/` 投资笔记 | `docs/framework.md`、`playbook.md`、`strategies.md` | 保留正文，仅调整项目名并增加历史背景说明 |
| 因子、观点、信号、策略设计与配置 | `docs/signals.md`、`resources/research_parameters.json` | 提炼方法，保留参数；标明草案与配置差异 |
| 架构、报告设计、投资者评审、新闻筛选与解读规范 | `docs/workflow.md` | 合并为人工也可使用的业务流程，去掉旧执行路径 |
| 来源研究及数据源配置 | `docs/sources.md`、`resources/sources.json` | 保留资料与订阅，去掉旧运行参数和敏感字段 |
| 资产注册、别名、watchlist、观点映射、搜索词和观察范围 | `resources/assets.json` | 合并成一份资料，保留不同命名空间，不强行统一歧义 |
| ETF 映射与发行商资料 | `resources/etf_mapping.json` | 保留 130 条显式映射、分类规则和 6 条发行商记录 |
| 原市场事件配置 | `resources/calendar.json` | 保留 12 条人工日程资料及来源，不作为当前日历 |
| 资产身份、资金费率、报告和时间语义设计 | `docs/data_definitions.md` | 定义字段含义、空值、时间、身份和冲突处理，不迁移可执行 schema |
| 三类中文 Prompt | `resources/prompts/` 三份 Markdown | 保留规则、输出含义与示例；中文观点版保留，英文同用途版本不重复迁入 |
| 两套想法、任务与路线图 | `docs/ideas.md` | 提取投资与产品问题，合并重复项，去掉工程队列 |
| 本地行情、LLM 及明确引用的飞书凭据 | `private/credentials.json` | 私有保留；未调用服务验证 |
| 原账户配置 | `private/accounts.reference.json` | 原始资金字段仅私有保存，不确认是真实余额 |

### 具体取舍与缺项

- 64 条 RSS、34 条公众号订阅、28 个关注标的全部保留；删除 RSS 的近期文章数量统计和每次抓取限制。原显式启停状态保留为 `legacy_enabled`。
- 微信旧服务的连接、Cookie、登录、抓取、恢复和调度资料均未迁入。
- 资产别名不直接扁平合并，避免把主题、研究资产与可交易标的混为同一身份。
- 行情源均标记实际使用待核对；旧 provider 选择另行记录，未迁移任何实现。
- 私有资料保存飞书 helper 明确引用的三个认证配置字段，不复制外部配置全文，也未发送消息。
- 当前进程未提供相关行情环境变量值及 `FEISHU_WEBHOOK`。未找到独立密码清单，不推断其他启动环境中也不存在。
- 旧引用的 OKX 日历认证、市场日历修正、政治日历修正本地文件不存在，没有拿示例替代。
- 原账户初始资金字段仅私有保存；公开资源只保留账户分类与风险约束。
- 旧日历的两种优先级、资产选择标准、评分衰减和权重差异已记录，未擅自设定新投资口径。
- 未复制旧代码、测试、历史数据、缓存、数据库、运行日志、模型 benchmark 或工程任务队列。

### 验证范围

迁移验收检查 JSON 可解析、条目数量及保留字段一致、笔记正文完整、内部链接、凭据未出现在公开文件、私有权限和 Git 忽略规则。只验证迁移质量，不验证服务连通性、市场资料时效或投资方法有效性。

2026-11-16 核验通过：三份笔记正文与源文一致（除项目名和新增背景说明）；订阅、资产及 ETF 等保留字段逐项一致；所有 JSON 可解析，Markdown 内部链接有效；公开文件未发现已迁移凭据值及常见密钥字段或认证 URL；私有权限与 Git 忽略规则通过检查。旧项目 Git 工作区保持干净。交付共 22 个文件：14 份 Markdown、5 份公开 JSON、2 份私有 JSON 和 `.gitignore`，约 226 KiB。
