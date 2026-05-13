# Module · 未解之问 + 可证伪假设

> Module ID: `open_questions`
> ✅ **必选（适用所有行业）**

## 适用场景
所有行业。最后一章。

## 这一章要回答什么问题

- 当前最大的不确定性是什么？
- 哪些"共识"实际上是 herding 共识，未被严肃证伪？
- 哪些假设崩塌会让整个 thesis 翻车？
- 5 年后回看本报告，最可能错在哪 3 件事？

## 期望产出

- 5-8 个 open questions
- 每个 question 的"如何 falsify"路径
- "如果我错了，最可能错在..." 反思

## 信息源

Critics、反方投资人、被忽略的边缘声音

## 主要 pitfalls

不要敷衍。这是报告诚实度的标志。

## Agent Prompt 模板

填入 `templates/agent_prompt.md.j2` 渲染时使用：

```
**章节**：未解之问 + 可证伪假设

**这一章要回答的核心问题**：
- 当前最大的不确定性是什么？
- 哪些"共识"实际上是 herding 共识，未被严肃证伪？
- 哪些假设崩塌会让整个 thesis 翻车？
- 5 年后回看本报告，最可能错在哪 3 件事？

**期望产出**：
- 5-8 个 open questions
- 每个 question 的"如何 falsify"路径
- "如果我错了，最可能错在..." 反思

**主要 pitfalls**：
不要敷衍。这是报告诚实度的标志。

**字数**：4000-8000 字

**关键纪律**：
- 每个数字 ≥ 1 URL 引用
- 不可追溯标 [UNSOURCED] / [INFERRED] / [UNDISCLOSED]
- 软化强判断
- 数学验算两次
- 不写元叙事（"应用 skill 模板"等）

**输出**：写入 `sections/open_questions.md`
**在 reply**：摘要 ≤800 字 + 10 条关键发现
```
