# 逐资产观点抽取

来源：旧项目 `config/opinion_prompts.json` 的 `article_import_zh_cn`。保留旧规则供研究，不代表当前生效的程序接口。

占位符、资产标识和输出示例属于旧约定，使用前须按 [数据定义](../../../docs/design/data_definitions.md) 核对。

## header_template

阅读文章，识别其中重点讨论的相关资产，并输出结构化的逐资产观点结果，观点有看多/看空/中性。

## must_return

请只返回严格匹配输出 schema 的 JSON，不要添加 Markdown 代码块或额外说明。

## rules

- 步骤 1：先识别文章中重点 actively discusses 的可交易金融资产，并写入 related_assets。
- 只有当 len(related_assets)<=3 时，输出才是有效的。
- 如果文章讨论的资产超过 3 个，按文章讨论篇幅排序，只保留讨论最多的前 3 个可交易资产。
- 每个 related_asset 都要输出：asset_id、raw_name、asset_classes、score、stance、rationale。
- 不要输出重复的 related_assets。同一个 canonical asset_id 最多只能出现一次；同一个非空 asset_classes 集合也不能换别名或换 symbol 重复出现。
- 只有当文章内容能明确映射到提供的 candidate asset context 时，才使用 canonical asset_id。raw_name 保留文章里最容易识别的原始叫法，asset_classes 保持数组结构。
- 步骤 2：再分别对每个相关资产进行独立评分，依据作者对该资产“当前可交易立场”的表达。
- score 只能取 -1、0、1；stance 只能取 bullish、bearish、neutral、mixed；rationale 必须是一句简短解释。
- 应优先判断作者的短期可交易视角，而不是长期结构性看法。如果长期看好与短期看空、悲观、担忧、谨慎、兑现、降风险、等待、或“现在不要买/不要追”同时出现，必须优先按当前可交易立场判断。长期 bullish + 短期 bearish/悲观/担忧，应该把该资产当前可交易分数记为 bearish。
- 不要要求文章必须出现“bearish”“卖出”“做空”等显式词汇，才能把某个资产判为 bearish。像“估值过高、赔率差、不追高、先兑现、降仓位、先防守、等确认、暂不参与”等委婉表达，通常都意味着该资产当前可交易立场偏 bearish。
- 例子：如果作者长期看多黄金，但当前对黄金表达担忧、不安、不追高、或短期偏空，那么黄金在当前可交易视角下应记为 bearish。

## few_shot_header

最小合法 JSON 示例：

## few_shot_example

```json
{
  "related_assets": [
    {
      "asset_id": "AU",
      "raw_name": "黄金",
      "asset_classes": [
        "GOLD"
      ],
      "score": -1,
      "stance": "bearish",
      "rationale": "作者当前对黄金明显担忧，并明确表达不追高。"
    },
    {
      "asset_id": "COPPER",
      "raw_name": "铜",
      "asset_classes": [
        "COPPER"
      ],
      "score": -1,
      "stance": "bearish",
      "rationale": "作者对铜表达了偏谨慎、偏负面的短期看法。"
    }
  ],
  "has_author_view": true,
  "article_base_score": -1,
  "unknown_tradable_assets": []
}
```

## candidate_asset_context_header

候选资产上下文：

## article_header

文章：
