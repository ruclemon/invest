# 预测市场事件解读

来源：旧项目 `news_collector/config/prompts.json` 的 `polymarket_summary`。保留旧规则供研究，不代表当前生效的程序接口。

占位符、资产标识和输出示例属于旧约定，使用前须按 [数据定义](../../../docs/design/data_definitions.md) 核对。

## header_template

请为 {dt} 的 Polymarket Top-{count} 事件生成中文结构化解读，供 summary 单行展示。

## must_return

必须返回严格匹配以下 JSON，不要加 markdown 代码块，不要加注释：
{"items":[{"event_no":1,"price_direction":"上涨","price_move_explainer":"一句中文，40字内，解释事件在交易什么"}]}

## rules

- 只能使用提供的事件，不要引入外部事实
- price_direction 只能是: 上涨 / 下跌 / 走平
- price_move_explainer 必须是单句中文，控制在40字内
- 必须点出事件本身在交易什么，例如候选人、政策、战争、降息、并购、监管，不要只写概率上涨/下跌/稳定/不变
- 即使走势平稳，也要说明市场仍在押注什么，而不是只写稳定、持平、变化有限
- 不要只写 YES 概率、市场预期、市场定价 这类空话；不要复述 price_direction
- 只保留变化解释，不要输出 why_it_matters、看点、成交量、方向复述
- 输出用于 summary 单行展示，尽量压缩，避免空话和重复标题
