# Module · 技术路线之争

> Module ID: `tech_routes`
> ⬜ **可选** — 适用 archetype: Pre-PMF Tech, AI Software, Healthcare R&D




## 这一章要回答什么问题

- 当前有哪 2-4 条主要技术路线？
- 每条路线的核心假设、代表玩家、性能 SOTA？
- 路线之争的可证伪 benchmark 是什么？时间表？
- 中美技术路线分歧（如适用）？

## 期望产出

- 技术路线对比表（路线 / 代表玩家 / 假设 / SOTA / 风险）
- Scaling Law / Benchmark 现状
- 路线分歧的中美 / 学术界图谱

## 信息源

依 Phase 3 信息源策略

## 主要 pitfalls

避免技术细节堆砌。重点是 strategic implications。

## Agent Prompt 模板

填入 `templates/agent_prompt.md.j2` 渲染时使用：

```
**章节**：技术路线之争

**这一章要回答的核心问题**：
- 当前有哪 2-4 条主要技术路线？
- 每条路线的核心假设、代表玩家、性能 SOTA？
- 路线之争的可证伪 benchmark 是什么？时间表？
- 中美技术路线分歧（如适用）？

**期望产出**：
- 技术路线对比表（路线 / 代表玩家 / 假设 / SOTA / 风险）
- Scaling Law / Benchmark 现状
- 路线分歧的中美 / 学术界图谱

**主要 pitfalls**：
避免技术细节堆砌。重点是 strategic implications。

**字数**：4000-8000 字

**关键纪律**：
- 每个数字 ≥ 1 URL 引用
- 不可追溯标 [UNSOURCED] / [INFERRED] / [UNDISCLOSED]
- 软化强判断
- 数学验算两次
- 不写元叙事（"应用 skill 模板"等）

**输出**：写入 `sections/tech_routes.md`
**在 reply**：摘要 ≤800 字 + 10 条关键发现
```
