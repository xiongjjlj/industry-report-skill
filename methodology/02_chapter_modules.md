# Phase 2 · 章节模块库

> 16 个模块。**必选 4 个**（always）+ **可选 12 个**（按 archetype 选）。每个模块对应 `modules/` 目录下一份独立的 prompt 模板。

---

## 必选 4 个（任何行业都要）

### 1. `industry_essence` — 行业本质 + 拐点
**回答**：为什么是现在？拐点的底层驱动是什么？这个行业过去 12 个月发生了什么质变？
**核心产出**：3-5 个独立驱动曲线 + 拐点判断
**示例**：具身智能 = 技术拐点（VLA）+ 算力拐点 + 数据拐点 + 经济拐点 4 条曲线合流

### 2. `top_voices` — 顶尖人物 thesis
**回答**：业内最聪明的 10-15 人（创业者 + 投资人 + 学者 + 批评者）对核心问题的真实公开观点？分歧线在哪？
**核心产出**：10×5 观点矩阵 + 5 条核心分歧 + 10 条最具穿透力引语
**关键**：**每条观点必须带 URL + 时间**

### 3. `scenarios_catalysts` — 关键变量 + 情景 + Catalyst 日历
**回答**：未来 12-24 个月有哪些决定性事件？三种情景（牛/基/熊）概率分布？
**核心产出**：核心变量驱动表 + 情景对比 + 月度 catalyst 日历

### 4. `open_questions` — 未解之问 + 可证伪假设
**回答**：当前最大的不确定性？哪些假设可能崩？哪些是真共识哪些是 herding？
**核心产出**：5-8 个 open questions + 每个的"如何 falsify"

---

## 可选 12 个（按 archetype 选）

### 5. `tech_routes` — 技术路线之争
**适用**：早期硬科技 / AI 软件 / 创新药
**示例**：
- 具身智能：VLA vs 世界模型 / 真机 vs 仿真 vs 视频 / 必须双足
- AI 编程：Agent loop vs IDE-native / RAG vs 长上下文 / SWE-bench 路径
- 创新药 PD-1：单抗 vs 双抗 vs ADC / 联用方案

### 6. `business_model_routes` — 商业模式之争
**适用**：AI 软件 / B2B 工具 / 服务平台
**示例**：
- AI 编程：subscription vs usage-based / Enterprise vs PLG
- Vertical AI：SaaS vs Outcome-based pricing
- 服务平台：commission vs SaaS vs hybrid

### 7. `value_chain` — 价值链分层
**适用**：制造业 / 工业 / 能源
**示例**：
- 储能：上游矿物 + 中游电芯 + 下游 PCS/EMS + 终端应用
- 半导体：设计 + 制造 + 封装测试 + 设备 + 材料
- **不适用**：AI 软件 / 消费品（不要硬套）

### 8. `player_paths` — 玩家路径分化
**适用**：几乎所有 archetype
**示例**：
- 具身智能：6 种打法（Tesla / Figure-Apptronik / 1X / PI-Skild / 中国硬件派 / 中国场景派）
- AI 编程：4 种打法（Anthropic Code / Cursor IDE / Devin Agent / OpenAI Codex）
- 新茶饮：3 种打法（蜜雪低价 + 加盟 / 喜茶高端直营 / 茶颜悦色区域品牌）
**核心产出**：每条路径的核心 moat / 单位经济 / 退出路径 / 失败模式 / 失败概率

### 9. `commercialization_validation` — 商业化验证（DD 真实情况）
**适用**：所有 archetype（关键章节）
**核心**：用 DD 视角拆穿"PR 数字"，找真实经济模型
**示例**：
- 具身智能：Autonomy level / 订单 Tier A-E 分级 / 替代方案 ROI / MTBF
- AI 编程：付费用户留存 / cohort 续费 / 真实用户活跃
- 消费品：单店模型 + 同店增长 + 翻台率
- 创新药：临床数据真实读出 vs 公司 PR

### 10. `unit_economics` — 单位经济
**适用**：SaaS / 服务业 / 消费品
**核心产出**：LTV / CAC / payback / contribution margin / NDR
**关键纪律**：所有定价公式当场验算两次（× 小时 / × 天 / × 月）

### 11. `user_demand_insight` — 用户洞察
**适用**：消费品 / B2C
**核心产出**：用户画像 / 真实需求场景 / 替代方案分析 / 价格敏感度
**信息源**：尼尔森 / 凯度 / 招股书用户调研 / 一手访谈

### 12. `channel_distribution` — 渠道与分销
**适用**：消费品 / B2B 销售
**核心产出**：渠道地图 / 渠道利润分配 / 直营 vs 加盟 vs 平台 / 海外渠道
**示例**：新茶饮直营 vs 加盟模型对比；POP MART 直营 + 机器人店 + 出海

### 13. `policy_environment` — 政策环境
**适用**：监管行业 / 跨境玩家 / 补贴行业
**核心产出**：政策时间表 / 补贴规模 / 政策博弈

### 14. `regulatory_path` — 监管路径
**适用**：创新药 / Fintech / 自动驾驶 / 医疗器械
**核心产出**：FDA / SEC / CFDA 流程 + 时间表 + 不确定性

### 15. `geopolitics` — 国际竞争 + 地缘
**适用**：跨境玩家 / 中美博弈相关
**核心产出**：出口管制 / 关税 / 实体清单 / 反制 / 路径选择

### 16. `store_cohort_model` — 单店/cohort 模型
**适用**：连锁零售 / 餐饮 / SaaS cohort 分析
**核心产出**：单店投入回报 / 同店增长 / cohort 留存曲线 / 海外开店 ROI

---

## 不同 archetype 的推荐组合

### 早期硬科技 (具身智能 / 脑机接口 / 量子)
- 必选 4 + `tech_routes` + `player_paths` + `commercialization_validation` + `value_chain` (if has physical layer) + `geopolitics` (if cross-border)
- **8 章左右**

### AI 软件 (LLM / AI 编程 / Vertical AI)
- 必选 4 + `tech_routes` + `business_model_routes` + `unit_economics` + `player_paths` + `commercialization_validation`
- **9 章左右**

### 制造业 (储能 / 光伏 / 半导体)
- 必选 4 + `value_chain` + `player_paths` + `policy_environment` + `geopolitics`
- **8 章左右**

### 消费品 (新茶饮 / SHEIN / POP MART)
- 必选 4 + `user_demand_insight` + `channel_distribution` + `store_cohort_model` + `player_paths` + `unit_economics`
- **9 章左右**

### 服务业 (滴滴 / 美团)
- 必选 4 + `business_model_routes` + `unit_economics` + `player_paths` + `regulatory_path`
- **8 章左右**

### 创新药 (PD-1 / GLP-1 / ADC)
- 必选 4 + `tech_routes` + `regulatory_path` + `player_paths` + `commercialization_validation`
- **8 章左右**

### 能源 (储能 / 氢能)
- 必选 4 + `value_chain` + `tech_routes` + `policy_environment` + `unit_economics`
- **8 章左右**

### Fintech (稳定币 / 跨境支付)
- 必选 4 + `regulatory_path` + `business_model_routes` + `unit_economics` + `player_paths` + `geopolitics`
- **9 章左右**

---

## 章节顺序原则

不是固定 1-2-3-4 顺序。一般原则：
1. **本质先行**：`industry_essence` 必在第一章（先讲为什么是现在）
2. **共识与分歧**：`top_voices` 紧随其后（让读者知道业内怎么想）
3. **核心矛盾展开**：根据 Phase 1 诊断，把最重要的 2-3 个模块放前面
4. **价值链 / 玩家**：靠后（如果不是核心矛盾）
5. **变量 / 情景 / 未解之问**：最后压轴
