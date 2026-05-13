# Module · 商业模式之争

> Module ID: `business_model_routes`
> ⬜ **可选** — 适用 archetype: AI Software, B2B Tools, Service Platforms




## 这一章要回答什么问题

- 当前有哪些商业模式（SaaS / usage-based / outcome-based / marketplace / freemium）？
- 每种模式的真实单位经济？
- 哪种模式 winning？为什么？
- PLG vs Enterprise 之争？

## 期望产出

- 商业模式对照表（含 ARR / NRR / CAC / payback）
- PLG / Enterprise / Hybrid 玩家分布
- 订阅 vs 用量 vs Outcome 经济模型对比

## 信息源

依 Phase 3 信息源策略

## 主要 pitfalls

所有数字必须验算。RaaS / SaaS 定价公式不能错。

## Agent Prompt 模板

填入 `templates/agent_prompt.md.j2` 渲染时使用：

```
**章节**：商业模式之争

**这一章要回答的核心问题**：
- 当前有哪些商业模式（SaaS / usage-based / outcome-based / marketplace / freemium）？
- 每种模式的真实单位经济？
- 哪种模式 winning？为什么？
- PLG vs Enterprise 之争？

**期望产出**：
- 商业模式对照表（含 ARR / NRR / CAC / payback）
- PLG / Enterprise / Hybrid 玩家分布
- 订阅 vs 用量 vs Outcome 经济模型对比

**主要 pitfalls**：
所有数字必须验算。RaaS / SaaS 定价公式不能错。

**字数**：4000-8000 字

**关键纪律**：
- 每个数字 ≥ 1 URL 引用
- 不可追溯标 [UNSOURCED] / [INFERRED] / [UNDISCLOSED]
- 软化强判断
- 数学验算两次
- 不写元叙事（"应用 skill 模板"等）

**输出**：写入 `sections/business_model_routes.md`
**在 reply**：摘要 ≤800 字 + 10 条关键发现
```
