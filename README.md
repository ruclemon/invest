# invest

定期生成有证据、可解释、可复盘的投资研究报告，供投资判断参考。不输出仓位或调仓计划，不做自动化交易。

当前保存投资知识、流程设计和少量参考资料，尚未实现数据采集、LLM 报告生成或定时发布。后续围绕具体报告按需实现，见 [TODO](docs/TODO.md)。

## 当前目录

```text
invest/
├── README.md
├── AGENTS.md
├── docs/
│   ├── investment/       # 投资框架、纪律、策略和旧评分方法
│   ├── design/           # 架构、研究流程和数据定义
│   ├── sources.md        # 数据源与凭据说明
│   ├── TODO.md           # 已确认工作
│   ├── ideas.md          # 尚未排期的研究想法
│   └── archive/          # 迁移历史记录
├── resources/
│   ├── sources.json      # 数据源、RSS、公众号清单
│   ├── assets.json       # 资产、别名、关注列表
│   ├── etf_mapping.json  # ETF 映射及发行商资料
│   └── legacy/           # 旧参数、日历和 Prompt 参考
├── private/              # 私有凭据和账户资料，不进 Git
└── .agent/tmp/           # Agent 临时脚本，不进 Git
```

后续代码、运行配置、提示词、模板和运行产物的目录边界见 [项目架构](docs/design/architecture.md)，实际使用时再创建。

## 阅读入口

| 文档 | 内容 |
|---|---|
| [分析框架](docs/investment/framework.md) | 定价、主导变量、资金、预期与传播 |
| [操作手册](docs/investment/playbook.md) | 投资纪律、执行、风险与退出的个人笔记 |
| [交易策略](docs/investment/strategies.md) | 策略思路与交易结构，仅供研究 |
| [因子、观点与组合](docs/investment/signals.md) | 旧评分方法、参数、组合规则及局限 |
| [研究与报告流程](docs/design/workflow.md) | 筛选信息、整理证据、形成判断、报告与复盘 |
| [数据定义](docs/design/data_definitions.md) | 字段、身份、时间、缺失值及旧口径冲突 |
| [数据源资料](docs/sources.md) | 行情、文章、日历、Polymarket 与私有凭据索引 |
| [研究想法](docs/ideas.md) | 尚未排期的研究问题 |

## 资源与历史参考

- [数据源与订阅](resources/sources.json)：8 类行情服务、64 条 RSS、34 条公众号订阅。
- [资产与关注列表](resources/assets.json)：资产分类、别名、28 个关注标的、搜索关键词。
- [ETF 映射](resources/etf_mapping.json)：130 条显式映射、分类规则及 6 条发行商资料。
- [旧参数](resources/legacy/research_parameters.json) 与 [旧日历](resources/legacy/calendar.json)：研究参考，不是生效配置或当前日程。
- 旧 Prompt：[观点抽取](resources/legacy/prompts/article_import_zh_cn.md)、[宏观叙事](resources/legacy/prompts/narratives.md)、[Polymarket 解读](resources/legacy/prompts/polymarket_summary.md)。

资料存在不代表服务可用或实际使用过。旧仓位规则不进入新报告实现。微信公众号旧服务已永久下线，保留订阅清单和未来下载需求。

凭据仅存于 `private/`，目录权限为 `700`、文件为 `600`，已配置 Git 忽略；没有验证有效性。旧项目的代码、测试和历史数据未迁入，来源与取舍见 [迁移记录](docs/archive/migration.md)。
