# 数据源资料

本页和 [资源清单](../resources/sources.json) 保存旧项目资料，不证明服务当前可用。本次没有联网检查、下载数据或验证凭据。所有行情源使用状态暂为待核对；未使用的源只留记录，不保留实现或自动安排接入。

## 行情与基本面

| 服务 | 旧用途 | 认证与限制 |
|---|---|---|
| Tushare | A 股、国内期货、ETF；基本面草案使用 daily_basic | token；具体接口权限未验证，旧配置含自定义 HTTP 入口，不应当成官方默认地址 |
| Alpha Vantage | 美股日线，TIME_SERIES_DAILY | API key；旧配置 compact 模式，不代表完整历史覆盖 |
| Polygon | 美股行情 | API key；套餐、覆盖和当前服务状态未验证 |
| Yahoo Finance / yfinance | 美股与海外期货；旧配置选为两者 provider | 旧配置未含密钥；复权设定为 false，后续使用应明确价格口径 |
| Bitget | 股票代币或合约行情 | 旧配置为 USDT-FUTURES、1Dutc；合约与标的股票不等同 |
| Binance | 加密现货、永续与资金费率 | 旧 crypto provider 选项；现货和合约入口分开 |
| OKX | 永续资金费率、财经日历 | 行情入口和日历认证要求不同；旧日历认证文件本机不存在 |
| Futu | 港美股、ETF 列表和快照；基本面草案使用 get_market_snapshot | 旧连接为本机 OpenD；服务、账户权限与实时性未验证 |

入口与原有连接参数见资源清单。`legacy_selected_for` 仅说明旧配置的 provider 选择，不证明实际运行过。股票基本面设计还保留 PE、PE_TTM、PB，以及未来 ROE、EPS、市值等字段；不能把这些指标混作日线 OHLCV。

国内期货要区分连续价格与具体交易合约。美股/海外期货的 Yahoo 符号、加密现货与永续标识各有语义，见 [数据定义](design/data_definitions.md)。

## 文章与研究来源

RSS 保留 64 条记录，包含原标识、名称、作者、标签、语言、优先级和订阅地址。旧运行统计 `articles_7d` 与每次抓取数量限制未迁移。旧条目若没有启停字段，保持缺省，不推断为启用。

公众号保留 34 条订阅信息，包括名称、搜索关键词、标签、优先级和原显式启停状态。用户已确认旧文章获取服务永久下线，因此新项目没有微信服务地址、认证 Cookie、登录、抓取或恢复流程。后续下载需求见 [待办](TODO.md)。

其他来源设计保留为历史资料：

- Substack：旧方案通过出版物的 `/feed` 订阅，保留作者和主题信息；RSS 可能只有摘要，不等于拥有全文。
- Odaily：旧资料记录 `https://rss.odaily.news/rss/post` 与 `https://rss.odaily.news/rss/newsflash`，旧默认订阅偏重文章而非快讯。
- PANews：旧资料记录中英文 RSS 生成页面，精选中文 feed 当时默认停用。当前条目以资源清单为准。
- 金色财经：旧研究未确认稳定的第一方 RSS，保留待研究记录，不声称当前不存在。
- RSSHub：保留作为扩展来源的思路，旧方案处于延后状态；不迁移部署方式或采集实现。
- 人工资料：可补充研究文章与事件，但本次没有迁移旧手动投递目录或文章正文。

这些都是旧资料摘要，没有进行当前可用性核查。

## 搜索热度、ETF、日历与预测市场

Google Trends 关键词映射保存在资产资料中；旧设计通过 pytrends 取得周频相对搜索量。保留口径和关键词，不引入依赖。

ETF 资料包括资产与行业映射、过滤规则和发行商数据入口。发行商状态是旧记录，不表示本轮检查结果。数据覆盖不足时不能把部分 AUM 当成全市场规模。

日历来源设计覆盖中美宏观事件、企业/行业会议、政治事件、指数调整及衍生品到期。官方公告、时间表和估计窗口的精度不同；十二条旧人工日程仅用于保留设计样本与来源，不作为最新提醒。

Polymarket 保留事件筛选、主题配额和概率变化解释方法。成交量、概率、观察窗口和结算规则应同时记录，不能把市场概率当成保证发生的事实。

## 凭据索引

真实值仅在 `private/`，不在此页展示。

| 私有位置 | 保存内容 | 状态 |
|---|---|---|
| `credentials.json:market_data` | Tushare、Alpha Vantage、Polygon 凭据字段 | 已迁移，未验证 |
| `credentials.json:llm` 与 `llm_connection` | 主备用 API key、关联 provider 和 API 入口 | 已迁移，未验证；不继承旧模型名单和重试链 |
| `credentials.json:feishu_reference` | 项目引用的飞书 helper 所需认证字段 | 仅保存明确引用的字段，未登录或发送消息 |
| `credentials.json:delivery_reference` | 旧投递目标和外部 helper 位置 | 私有资料，不是启用投递 |
| `accounts.reference.json` | 7 条原账户配置，含初始资金字段 | 不确认是实际余额，不公开复制资金值 |

外部飞书凭据按 `news_collector/feishu_delivery.py` → `lark_doc/config.py` → 明确指定的配置文件定位，没有扫描无关凭据。其精确源位置保留在私有资料中。

当前进程没有提供所引用的行情环境变量值或 `FEISHU_WEBHOOK`；不能断言它们在其他启动环境中不存在。未找到独立密码清单。旧配置引用的 OKX 日历认证、市场日历修正和政治日历修正文件均不存在，没有用示例文件替代。微信失效服务凭据明确不迁移。

私有目录权限为 `700`，文件为 `600`，并被 `.gitignore` 排除。将来备份或复制项目时，需要单独保管私有资料；只复制公开文件不会包含凭据。

## 来源

旧 `config/data_sources.json`、两个 config README、RSS/微信配置；数据源目录 README；funding rate、CN futures auto roll、ETF issuer AUM、equity fundamentals 设计；NC crypto media、Substack、RSSHub、calendar 与 Polymarket 设计。私人配置迁移不表示任何来源已获重新调用授权。
