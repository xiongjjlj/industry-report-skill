# Module · 单位经济（LTV / CAC / Payback / NDR）

> Module ID: `unit_economics`
> ⬜ **可选** — 适用 archetype: SaaS, Services, Consumer




## 这一章要回答什么问题

- 单位获客成本 CAC 多少？
- 单位 LTV / 合约期 LTV？
- Payback 多久？
- NDR / Gross Retention？
- 毛利率 / contribution margin？
- Cohort 留存曲线？

## 期望产出

- 单位经济表（CAC / LTV / Payback / NDR / GM）
- Best-in-class benchmark 对比
- Cohort 表（如有）

## 信息源

依 Phase 3 信息源策略

## 主要 pitfalls

数学验算两次。所有定价公式当场算。

## Agent Prompt 模板

填入 `templates/agent_prompt.md.j2` 渲染时使用：

```
**章节**：单位经济（LTV / CAC / Payback / NDR）

**这一章要回答的核心问题**：
- 单位获客成本 CAC 多少？
- 单位 LTV / 合约期 LTV？
- Payback 多久？
- NDR / Gross Retention？
- 毛利率 / contribution margin？
- Cohort 留存曲线？

**期望产出**：
- 单位经济表（CAC / LTV / Payback / NDR / GM）
- Best-in-class benchmark 对比
- Cohort 表（如有）

**主要 pitfalls**：
数学验算两次。所有定价公式当场算。

**字数**：4000-8000 字

**关键纪律**：
- 每个数字 ≥ 1 URL 引用
- 不可追溯标 [UNSOURCED] / [INFERRED] / [UNDISCLOSED]
- 软化强判断
- 数学验算两次
- 不写元叙事（"应用 skill 模板"等）

**输出**：写入 `sections/unit_economics.md`
**在 reply**：摘要 ≤800 字 + 10 条关键发现
```
