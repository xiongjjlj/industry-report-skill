# Module · 单店 / Cohort 模型

> Module ID: `store_cohort_model`
> ⬜ **可选** — 适用 archetype: Retail, Restaurants, SaaS Cohorts




## 这一章要回答什么问题

- 单店投入回报周期？
- 同店增长率？
- 翻台率 / 复购率？
- Cohort 留存曲线（SaaS）？
- 海外开店 ROI vs 国内？

## 期望产出

- 单店模型（投资 / 收入 / 毛利 / payback）
- 同店增长 trend
- Cohort 留存表

## 信息源

依 Phase 3 信息源策略

## 主要 pitfalls

不同地区 / 不同年份 cohort 必须分开。

## Agent Prompt 模板

填入 `templates/agent_prompt.md.j2` 渲染时使用：

```
**章节**：单店 / Cohort 模型

**这一章要回答的核心问题**：
- 单店投入回报周期？
- 同店增长率？
- 翻台率 / 复购率？
- Cohort 留存曲线（SaaS）？
- 海外开店 ROI vs 国内？

**期望产出**：
- 单店模型（投资 / 收入 / 毛利 / payback）
- 同店增长 trend
- Cohort 留存表

**主要 pitfalls**：
不同地区 / 不同年份 cohort 必须分开。

**字数**：4000-8000 字

**关键纪律**：
- 每个数字 ≥ 1 URL 引用
- 不可追溯标 [UNSOURCED] / [INFERRED] / [UNDISCLOSED]
- 软化强判断
- 数学验算两次
- 不写元叙事（"应用 skill 模板"等）

**输出**：写入 `sections/store_cohort_model.md`
**在 reply**：摘要 ≤800 字 + 10 条关键发现
```
