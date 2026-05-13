# Module · 玩家路径分化

> Module ID: `player_paths`
> ⬜ **可选** — 适用 archetype: 几乎所有




## 这一章要回答什么问题

- 行业有几种本质上不同的玩法（path）？
- 每条 path 的核心 moat / 单位经济 / 失败模式？
- 不是按"国别"分（这是民族主义视角），是按"打法"分

## 期望产出

- 4-7 条 player paths
- 每条 path：核心假设 / 单位经济 / 退出路径 / 失败概率 / 代表公司
- 6 path 对照矩阵

## 信息源

依 Phase 3 信息源策略

## 主要 pitfalls

不要写成"中 vs 美"二分。真实分歧在打法层面。

## Agent Prompt 模板

填入 `templates/agent_prompt.md.j2` 渲染时使用：

```
**章节**：玩家路径分化

**这一章要回答的核心问题**：
- 行业有几种本质上不同的玩法（path）？
- 每条 path 的核心 moat / 单位经济 / 失败模式？
- 不是按"国别"分（这是民族主义视角），是按"打法"分

**期望产出**：
- 4-7 条 player paths
- 每条 path：核心假设 / 单位经济 / 退出路径 / 失败概率 / 代表公司
- 6 path 对照矩阵

**主要 pitfalls**：
不要写成"中 vs 美"二分。真实分歧在打法层面。

**字数**：4000-8000 字

**关键纪律**：
- 每个数字 ≥ 1 URL 引用
- 不可追溯标 [UNSOURCED] / [INFERRED] / [UNDISCLOSED]
- 软化强判断
- 数学验算两次
- 不写元叙事（"应用 skill 模板"等）

**输出**：写入 `sections/player_paths.md`
**在 reply**：摘要 ≤800 字 + 10 条关键发现
```
