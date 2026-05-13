# Phase 4-7 · Pipeline 编排详情

> 完整执行细节。前置：Phase 1-3 已完成并经 user 确认。

---

## Phase 4 · 并行 Agent 执行（~25 min）

### 4.1 编排原则
- 每个 Phase 2 选中的模块 → 1 个 `general-purpose` agent
- **所有 agent 并行**（一个 message 里多个 Task 调用）
- 每个 agent 输出独立 markdown 到 `sections/{module_name}.md`

### 4.2 每个 agent 的 prompt 模板
从 `templates/agent_prompt.md.j2` 渲染：

```markdown
**任务**：研究 {INDUSTRY} 行业的 {MODULE_NAME} 章节。

**Phase 1 诊断结果**：
- Archetype：{archetype}
- 核心矛盾：{core_tension}
- SHARPEST 问题：{sharp_questions}

**信息源策略**（必读）：
{phase3_sources_for_this_module}

**章节要求**（从 modules/{module}.md 读取）：
{module_specific_requirements}

**输出**：写入 `sections/{module}.md`，字数 4000-8000 字。
- 每个数字必须 ≥1 个 URL 引用
- 不可追溯标 [UNSOURCED] / [INFERRED] / [UNDISCLOSED]
- 软化强判断（必然 → 大概率，等）
- 在 reply 给摘要 ≤800 字 + 关键数字 10 条

**关键避坑**（必读 `methodology/05_pitfalls.md`）：
1. 不要表面模仿
2. 信息源 > 框架
3. PE deal-level 工具不进章节
4. 数字可追溯
5. 数学验算两次
6. 软化强判断
```

### 4.3 等所有 agent 返回后
1. 读所有 `sections/*.md` 的摘要
2. 找 gap：哪些 SHARPEST 问题没回答好？哪些数据 [UNSOURCED] 太多？
3. 决定是否 launch 1-2 个补强 agent

---

## Phase 5 · 验证 Agent（~15 min 并行，必跑）

**3 个验证 agent**，对所有行业都跑：

### 5.1 Top Voices Agent
**任务**：找出最顶尖 10-15 人对核心矛盾的真实公开观点。
**输出**：观点矩阵 + 10 条最具穿透力引语 + 5 条核心分歧线
**Prompt 模板**：见 `prompts/top_voices_agent.md`

**关键纪律**：
- 每条观点必须带 URL + 时间
- 包括反方声音（最珍贵）
- 找"业内最不愿说出口"的共识

### 5.2 DD Metrics Agent
**任务**：industry-specific 的"专业 DD 指标"
**因行业不同而异**：
- 硬科技：MTBF / autonomy level / 订单 Tier A-E / 替代方案 ROI
- AI 软件：cohort retention / NRR / SWE-bench / 真实用户活跃
- 消费品：单店模型 / 同店增长 / 翻台率 / 复购率
- 服务平台：take rate / GTV / unit economics / 网络效应饱和度
- 创新药：临床读出真实性 / FDA 通讯 / 适应症竞争密度
- 制造业：产能利用率 / 良率 / yield curve / capex 回报周期

**Prompt 模板**：见 `prompts/dd_metrics_agent.md`

### 5.3 Adversarial Critic Agent
**任务**：模拟"怀疑论 PE 合伙人 + 行业专家 + 反方投资人 + 数字审计员"四种视角
**输出**：
- Fatal flaws（致命，必修）
- Severe issues（严重，必修）
- Improvement suggestions（建议）
- Gaps（遗漏）
- Strengths kept（保留强项）

**Prompt 模板**：见 `prompts/adversarial_critic.md`

**注意**：subagent_type 用 `debate-critic` 如果可用，否则 `general-purpose` + critic prompt。

---

## Phase 5.5 · 应用验证发现

### Fatal Flaws
- **必须 inline 修复**
- 不在最终交付报告里写"自审与勘误"章节
- 写到 `WORKING/ERRATA.md`（内部留档）

### Severe Issues
- inline 修复

### Improvement Suggestions
- 选择性采纳，避免 bloat

### Gaps
- 决定是否补充章节或加 [UNSOURCED]

---

## Phase 6 · HTML 合成

### 6.1 文件
- 模板：`templates/html_skeleton.html`
- 输出：`<output_dir>/report.html`

### 6.2 包含
- Hero + 执行摘要（KPI 卡片 4-8 个）
- TOC（可点击）
- 各章节（用 `<section>` + `<h2>` + 表格 + Chart.js + Mermaid）
- 引用列表（来自 references.json）
- 附录（仅在用户要求时含 PE deal-level 工具）

### 6.3 视觉规范
- Tailwind CSS via CDN（不引入构建）
- Chart.js for 柱图 / 饼图 / 雷达 / 散点
- Mermaid for 流程图 / 决策树 / 时间轴
- @media print 优化（可打印为 PDF）

### 6.4 禁忌（PE 老板看的报告）
- ❌ 元叙事（"应用 Anthropic skill 模板""debate-critic 评审"）
- ❌ 自审章节
- ❌ "PE Checklist 31 条"放主报告
- ❌ "IC Memo 样本"放主报告
- ❌ "投委会必问 10 个问题 + 标准答案"
- ❌ "PE 组合配置建议（人民币 30% / 美元 15%）"
- ❌ "决策树"

这些 deal-level 工具只在用户**明确要求**时放附录。

---

## Phase 7 · References DB

### 7.1 结构
```json
data/references.json:
{
  "schema_version": "1.0",
  "generated_at": "...",
  "references": [
    {
      "id": "REF001",
      "title": "...",
      "type": "report|news|paper|blog|company_announcement|database|official_gov",
      "publisher": "...",
      "url": "...",
      "accessed_date": "YYYY-MM-DD",
      "tier": "tier1|tier2|tier3",
      "used_in_sections": ["..."]
    }
  ]
}

data/data_points.json:
{
  "data_points": [
    {
      "id": "DP001",
      "category": "...",
      "subject": "...",
      "fact": "...",
      "value": "...",
      "year": 2026,
      "source_ids": ["REF001"],
      "confidence": "high|medium|low",
      "notes": "..."
    }
  ]
}
```

### 7.2 用 Python 脚本生成
- Grep 所有 sections/*.md 找 URL → 入 references
- Grep 数字 + 单位 → 入 data_points

### 7.3 HTML 集成
- References 章节里渲染 references.json（按 tier 分组）
- 关键数字加 `[REF-XXX]` 锚点

---

## 最终交付清单

```
{output_dir}/
├── README.md                # 这份报告的快速导览
├── FULL_REPORT.md           # 主报告 markdown
├── report.html              # 单文件 HTML
├── sections/                # 每个模块独立 markdown
├── data/                    # references / data_points / companies
└── WORKING/                 # Phase 1-3 conclusions + ERRATA（内部留档）
```

WORKING/ 默认不分享，是 pipeline 的内部产物。
