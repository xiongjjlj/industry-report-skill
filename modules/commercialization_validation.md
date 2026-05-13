# Module · 商业化验证（DD 真实情况）

> Module ID: `commercialization_validation`
> ⬜ **可选** — 适用 archetype: 所有 (DD 视角)




## 这一章要回答什么问题

- 媒体头条 vs 真实 firm revenue 的 gap？
- 订单质量分级（已收款 / 不可撤销合同 / 框架 / PoC / LOI）？
- 替代方案（成熟方案）的 ROI 对比？
- 安全 / 合规 / 监管真实门槛？

## 期望产出

- 订单 Tier A-E 分级表（Top 10 公开订单重新评估）
- autonomy level / 真实部署 vs demo 评分卡
- 替代方案 ROI 对照（如 AMR vs 人形 / 同行竞品）
- 资产负债表 / 单位经济假设的 audit

## 信息源

依 Phase 3 信息源策略

## 主要 pitfalls

这是 PE DD 的灵魂章节。所有数字 PR 语言要剥离。

## Agent Prompt 模板

填入 `templates/agent_prompt.md.j2` 渲染时使用：

```
**章节**：商业化验证（DD 真实情况）

**这一章要回答的核心问题**：
- 媒体头条 vs 真实 firm revenue 的 gap？
- 订单质量分级（已收款 / 不可撤销合同 / 框架 / PoC / LOI）？
- 替代方案（成熟方案）的 ROI 对比？
- 安全 / 合规 / 监管真实门槛？

**期望产出**：
- 订单 Tier A-E 分级表（Top 10 公开订单重新评估）
- autonomy level / 真实部署 vs demo 评分卡
- 替代方案 ROI 对照（如 AMR vs 人形 / 同行竞品）
- 资产负债表 / 单位经济假设的 audit

**主要 pitfalls**：
这是 PE DD 的灵魂章节。所有数字 PR 语言要剥离。

**字数**：4000-8000 字

**关键纪律**：
- 每个数字 ≥ 1 URL 引用
- 不可追溯标 [UNSOURCED] / [INFERRED] / [UNDISCLOSED]
- 软化强判断
- 数学验算两次
- 不写元叙事（"应用 skill 模板"等）

**输出**：写入 `sections/commercialization_validation.md`
**在 reply**：摘要 ≤800 字 + 10 条关键发现
```
