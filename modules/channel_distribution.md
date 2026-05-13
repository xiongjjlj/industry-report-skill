# Module · 渠道与分销

> Module ID: `channel_distribution`
> ⬜ **可选** — 适用 archetype: Consumer, B2B Sales




## 这一章要回答什么问题

- 渠道地图（直营 / 加盟 / 平台 / 海外）？
- 渠道利润分配？
- 渠道 moat 在哪？
- 海外扩张的渠道差异？

## 期望产出

- 渠道地图
- 每个渠道的占比 + 利润分配
- 直营 vs 加盟模型对比

## 信息源

依 Phase 3 信息源策略

## 主要 pitfalls

不要写成"渠道分布"。要写"渠道之争"和"为什么 winning"。

## Agent Prompt 模板

填入 `templates/agent_prompt.md.j2` 渲染时使用：

```
**章节**：渠道与分销

**这一章要回答的核心问题**：
- 渠道地图（直营 / 加盟 / 平台 / 海外）？
- 渠道利润分配？
- 渠道 moat 在哪？
- 海外扩张的渠道差异？

**期望产出**：
- 渠道地图
- 每个渠道的占比 + 利润分配
- 直营 vs 加盟模型对比

**主要 pitfalls**：
不要写成"渠道分布"。要写"渠道之争"和"为什么 winning"。

**字数**：4000-8000 字

**关键纪律**：
- 每个数字 ≥ 1 URL 引用
- 不可追溯标 [UNSOURCED] / [INFERRED] / [UNDISCLOSED]
- 软化强判断
- 数学验算两次
- 不写元叙事（"应用 skill 模板"等）

**输出**：写入 `sections/channel_distribution.md`
**在 reply**：摘要 ≤800 字 + 10 条关键发现
```
