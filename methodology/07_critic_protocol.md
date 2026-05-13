# 对抗性评审协议 · Critic Protocol

> v1 报告完成后**强制**跑这一轮。所有行业都适用。

---

## 调用方式

Subagent type：`debate-critic`（如果可用）/ `general-purpose`（否则）

Prompt（适配后）：

```
**任务**：对一份 {INDUSTRY} 行业研究报告做最严厉的对抗性评审。

**报告位置**：
- 主报告：{path}/FULL_REPORT.md
- 各章节：{path}/sections/*.md
- HTML：{path}/report.html

**核心论点**（让 critic 知道要 attack 什么）：
{summary_of_main_claims}

**评审视角**：模拟 4 种 PE 内部角色：

1. **怀疑论 PE 合伙人**
   - 数字可信吗？引用经得起追溯吗？
   - 类比（vs 历史 EV 周期、AI 周期）是否过于轻率？
   - 概率分布的依据是什么？还是拍脑袋？

2. **行业专家**
   - 技术判断是否准确？
   - 玩家清单是否漏掉重要公司？是否过度乐观看待某家？
   - 关键 benchmark 数字是否反映真实通用能力？
   - 是否被公司 PR 语言带偏？

3. **反方投资人**（认为是泡沫）
   - 真实部署 vs 媒体宣传的 gap 在哪？
   - 哪些"PMF 信号"是补贴 / 政府订单催生，不是 ROI 驱动？
   - 估值 vs 真实营收的合理性？
   - 退出路径假设是否过于乐观？

4. **数字 / 事实审计员**
   - 每个核心数字独立审计：是否前后矛盾？口径一致？
   - 引用链接是否可访问（抽查 10-15 个）？
   - 时间口径混淆（出货 vs 装机 vs 交付 vs 累计）
   - 货币换算（USD vs RMB）
   - 数学错误（公式 / 占比 / 增长率）

**输出**：写入 `{path}/WORKING/ADVERSARIAL_REVIEW.md`：

1. **致命漏洞**（fatal）：会让 PE 投委会拒绝的问题，每个具体到段落 / 数字
2. **严重问题**（severe）：影响核心判断可信度但可修复
3. **改进建议**（improvements）：让报告更专业的细节
4. **遗漏**（gaps）：报告未覆盖但应该有的角度
5. **强项保留**（strengths）：哪些是真正立得住的论点，修订时不要丢

每条问题必须：
- 引用具体位置（章节 + 段落 + 原话）
- 为什么是问题
- 具体修复建议

**不要客气**。
**不要 generic**。不要说"数字应该交叉验证"这种空话；说"X 章节的 Y 数字仅有 Z 一个来源，应该用 W 验证"。

在 reply 给摘要（≤1000 字）+ Top 10 致命漏洞清单。
```

---

## 应用 Critic 输出的纪律

### Fatal Flaws
- **必须 inline 修复**——直接改原文
- 修复内容**不写注释**（如 "[已修正]"）
- 修复后跑一遍 grep 验证
- **不**在最终报告里加"自审与勘误"章节

### Severe Issues
- inline 修复
- 如果修复涉及概念性大改，标注到 `WORKING/ERRATA.md`（内部）

### Improvements
- 选择性采纳
- 避免 bloat（不是每个建议都要采纳）

### Gaps
- 决定：补章节 / 补段落 / 加 [UNSOURCED] / 显式声明 out-of-scope

### Strengths
- 修订时**不要丢**
- Critic 没攻击的部分往往是 v1 真正的价值所在

---

## 内部 ERRATA 模板（不在交付报告里）

写到 `WORKING/ERRATA.md`：

```markdown
# Internal ERRATA · {INDUSTRY} 报告

> 不交付。仅用于 PE 内部 audit 追溯。

## v1 → v2 修复的 Fatal Flaws

### #1 {flaw}
- **位置**：{location}
- **原表述**：{original}
- **修订后**：{revised}
- **依据**：{source}

### #2 ...

## v2 仍存在的 Known Limitations

- {limitation 1}
- {limitation 2}

## 不接受的 Critic 建议（理由）

- {建议 X，未采纳，因为...}
```

---

## 自动化迭代规则

如果 Critic 找出：
- ≥ 3 fatal flaws → **必须再跑一次 v2 critic**（验证修复有效）
- 0-2 fatal flaws → v2 自评足够

最多迭代 3 次（v1 → v2 → v3）；之后承认 known limitations 交付。
