# 宏观叙事整理

来源：旧项目 `news_collector/config/prompts.json` 的 `narratives`。保留旧规则供研究，不代表当前生效的程序接口。

占位符、资产标识和输出示例属于旧约定，使用前须按 [数据定义](../../../docs/design/data_definitions.md) 核对。

## header_template

请为 {dt} 生成 3-{max_narratives} 条中文宏观叙事。

## must_return

必须返回严格匹配以下 schema 的 JSON，不要加 markdown 代码块，不要加注释：
{"narratives": [{"sentence": "一句话叙事", "asset_ids": ["GC", "BITCOIN"], "asset_views": [{"asset_id": "GC", "view": "上涨"}, {"asset_id": "BITCOIN", "view": "下跌"}], "evidence_doc_ids": ["doc_id_1"]}]}

## rules

- 只能使用提供的 documents
- 每条 narrative 必须包含 1-5 个 evidence_doc_ids
- asset_ids 只能使用这些值: GC, SI, CL, US_TREASURY, DXY, US_TECH, CHINA_A_SHARE, BITCOIN, CHINA_BOND, LITHIUM, HK_TECH, JAPAN_EQUITY, KOREA_EQUITY, STAR50
- asset_views 必须给出每个 asset_id 的简化方向判断，view 只能是: 上涨 / 下跌 / 走平
- 如果文章里明确表达某类资产近期明显走强或上涨，标记为上涨；如果明确表达明显走弱或下跌，标记为下跌；如果只是小幅上涨、小幅下跌、波动不大、震荡、横盘、缺少明确方向，统一标记为走平
- 叙事要写成中文市场观点，不要写成文章摘要翻译
- 请在叙事里顺手概括 Macro Top-10 里的主要资产方向，不要只重复单篇文章标题
- 句子尽量简洁，避免空话和套话

## documents_header

Documents:
