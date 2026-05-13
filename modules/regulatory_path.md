# Module · 监管路径

> Module ID: `regulatory_path`
> ⬜ **可选** — 适用 archetype: Healthcare, Fintech, Autonomous Driving, Medical Devices




## 这一章要回答什么问题

- FDA / SEC / CFDA 流程？
- 审批时间表？
- 关键 milestone 通讯（FDA Type B / End-of-Phase 2 会议等）？
- 类似产品历史审批路径？

## 期望产出

- 监管时间表
- 关键审批节点
- 类似产品历史 case

## 信息源

依 Phase 3 信息源策略

## 主要 pitfalls

临床数据真实读出 vs 公司 PR 必须分清。

## Agent Prompt 模板

填入 `templates/agent_prompt.md.j2` 渲染时使用：

```
**章节**：监管路径

**这一章要回答的核心问题**：
- FDA / SEC / CFDA 流程？
- 审批时间表？
- 关键 milestone 通讯（FDA Type B / End-of-Phase 2 会议等）？
- 类似产品历史审批路径？

**期望产出**：
- 监管时间表
- 关键审批节点
- 类似产品历史 case

**主要 pitfalls**：
临床数据真实读出 vs 公司 PR 必须分清。

**字数**：4000-8000 字

**关键纪律**：
- 每个数字 ≥ 1 URL 引用
- 不可追溯标 [UNSOURCED] / [INFERRED] / [UNDISCLOSED]
- 软化强判断
- 数学验算两次
- 不写元叙事（"应用 skill 模板"等）

**输出**：写入 `sections/regulatory_path.md`
**在 reply**：摘要 ≤800 字 + 10 条关键发现
```
