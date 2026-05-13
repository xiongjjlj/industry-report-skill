# Module · 政策环境

> Module ID: `policy_environment`
> ⬜ **可选** — 适用 archetype: Regulated, Cross-border, Subsidized




## 这一章要回答什么问题

- 中 / 美 / 欧 各国政策时间表？
- 补贴规模？类比历史（如 EV 早期）？
- 出口管制 / 关税 / 实体清单？
- 政策博弈情景？

## 期望产出

- 政策对照表
- 补贴省级 / 国别分布
- 出口管制时间表

## 信息源

依 Phase 3 信息源策略

## 主要 pitfalls

中国补贴占 GDP 比例要算对。EV 早期类比不要硬套。

## Agent Prompt 模板

填入 `templates/agent_prompt.md.j2` 渲染时使用：

```
**章节**：政策环境

**这一章要回答的核心问题**：
- 中 / 美 / 欧 各国政策时间表？
- 补贴规模？类比历史（如 EV 早期）？
- 出口管制 / 关税 / 实体清单？
- 政策博弈情景？

**期望产出**：
- 政策对照表
- 补贴省级 / 国别分布
- 出口管制时间表

**主要 pitfalls**：
中国补贴占 GDP 比例要算对。EV 早期类比不要硬套。

**字数**：4000-8000 字

**关键纪律**：
- 每个数字 ≥ 1 URL 引用
- 不可追溯标 [UNSOURCED] / [INFERRED] / [UNDISCLOSED]
- 软化强判断
- 数学验算两次
- 不写元叙事（"应用 skill 模板"等）

**输出**：写入 `sections/policy_environment.md`
**在 reply**：摘要 ≤800 字 + 10 条关键发现
```
