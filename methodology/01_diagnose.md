# Phase 1 · 行业诊断方法

> 这是 pipeline 第一步。**强制**。诊断结果决定后面所有章节、信息源、agent 编排。

---

## 诊断 5 个问题

### 1. 行业 archetype（基础类型）

回答：本行业属于以下哪一类（可叠加，但要主导类型）：

| Archetype | 特征 | 决定胜负的核心 |
|---|---|---|
| **早期硬科技 (Pre-PMF Tech)** | AI 模型、量子计算、脑机接口、具身智能、可控核聚变 | 技术路线 + PMF 时间 + 玩家路径 |
| **成熟硬科技 (Mature Tech)** | 半导体设备、新能源车、储能、光伏 | 供应链 + 成本 + 规模 + 政策 |
| **AI 软件 / SaaS** | LLM / Vertical AI / Coding Agents | 模型能力 + 分销 + 单位经济 + 数据 moat |
| **消费品 (Consumer)** | 新茶饮、POP MART、SHEIN、运动品牌 | 品牌 + 渠道 + 用户洞察 + 单店模型 + 出海 |
| **服务业 / 平台** | 滴滴、美团、Uber Eats、Airbnb | 双边市场 + 网络效应 + 单位经济 |
| **创新药 / 医疗** | 创新药、CXO、医疗器械 | 管线 + 临床 + 适应症 + 支付方 + 监管 |
| **能源 / 公用事业** | 储能、氢能、电网、地热 | 技术 + 规模 + 政策 + 单位经济 |
| **Fintech / 金融科技** | 稳定币、跨境支付、券商科技 | 监管 + 单位经济 + 风险模型 + 网络效应 |
| **B2B 工具 / 工业软件** | EDA、CAD、CRM、ERP | 替换成本 + 生态 + 行业 know-how |
| **传统产业升级** | 农业科技、建筑科技、矿业 | 落地能力 + 客户教育 + 经济性 |

### 2. 行业成熟度

- **Pre-PMF**：尚未有公司明确跑通商业化（多数 AI Agent / 具身智能 / 量子）
- **Early Growth**：少数玩家有真实 ROI 案例（早期 SaaS / 新茶饮初期）
- **Growth**：行业整体高增速、玩家分化（当前 AI 编程 / 新茶饮中期）
- **Mature**：增速放缓、洗牌完成（消费电子 / 传统 SaaS）
- **Decline**：被替代品挤压（PC 板载市场 / 传统燃油车）

成熟度直接影响：
- Pre-PMF → 报告应该重点写"为什么是现在"+"技术路线之争"+"玩家路径"
- Mature → 重点写"市占率 + 单位经济 + 竞争壁垒 + 估值"

### 3. THE 核心矛盾（最关键的一问）

**问自己**：如果只能用一句话回答"这个行业现在最重要的事是什么"，会说什么？

例子：
- 具身智能：**技术拐点 + 商业化悬崖的双重张力**——VLA 模型能否真到 GPT 时刻？
- AI 编程：**Agent 是否会取代 IDE**——Claude Code/Cursor/Devin 谁是 winning form？
- 新茶饮：**海外能不能跑出来**——蜜雪冰城/霸王茶姬出海是否颠覆国内格局？
- 创新药 PD-1：**适应症拓展边际收益**——已饱和的赛道如何差异化？
- 稳定币：**监管落地 + USDT/USDC 双寡头会不会被打破**

**操作纪律**：核心矛盾必须用一句话写出来。如果写不出，说明诊断没做透，重做。

### 4. SHARPEST 分析师视角

**问自己**：业内最聪明的分析师 / 投资人会问什么？

例子：
- 具身智能：Tesla 100 万台是否兑现？1X 60-70% autonomy 是否能 scale？真实 MTBF 是多少？
- AI 编程：Anthropic vs OpenAI 谁先到 SWE-bench 80%？Cursor 用户留存如何？
- 新茶饮：单店 payback 月数？海外开店 ROI？
- 创新药：FDA 加速审批通道是否打开？医保谈判结果如何？
- 稳定币：GENIUS 法案落地时间表？储备金审计透明度？

**3-5 个 sharpest 问题**——这些是后面"商业化验证 + 玩家路径"章节的灵魂。

### 5. 章节模块选择

读 `02_chapter_modules.md`，从 16 个模块库里选 5-8 个本行业适用的。

**必选 4 个**（适用所有行业）：
- `industry_essence.md` — 行业本质 + 拐点驱动
- `top_voices.md` — 顶尖人物 thesis
- `scenarios_catalysts.md` — 关键变量 + 三情景 + 24 月日历
- `open_questions.md` — 未解之问

**可选 12 个**（按 Phase 1 archetype 选）：
| 模块 | 适用 archetype |
|---|---|
| `tech_routes.md` | 早期硬科技 / AI 软件 / 创新药 |
| `business_model_routes.md` | AI 软件 / B2B 工具 / 服务平台 |
| `value_chain.md` | 制造业 / 工业 / 能源 |
| `player_paths.md` | 所有 archetype（几乎必选） |
| `commercialization_validation.md` | 所有 archetype（DD 验证） |
| `unit_economics.md` | SaaS / 服务业 / 消费品 |
| `user_demand_insight.md` | 消费品 / B2C |
| `channel_distribution.md` | 消费品 / B2B 销售 |
| `policy_environment.md` | 监管行业 / 跨境 |
| `regulatory_path.md` | 创新药 / Fintech |
| `geopolitics.md` | 跨境玩家 / 中美博弈 |
| `store_cohort_model.md` | 零售 / SaaS cohort |

---

## 诊断输出模板

把诊断结果写到 `WORKING/phase1_diagnosis.md`：

```markdown
# 行业诊断：{INDUSTRY}

**诊断时间**：{DATE}
**Archetype**：{Primary} (+ {Secondary if any})
**成熟度**：{Pre-PMF / Early Growth / Growth / Mature}

## 核心矛盾（一句话）
{Single sentence}

## SHARPEST 分析师视角的 5 个问题
1. ...
2. ...
3. ...
4. ...
5. ...

## 推荐章节（5-8 个模块）
- ✅ industry_essence (always)
- ✅ top_voices (always)
- ✅ scenarios_catalysts (always)
- ✅ open_questions (always)
- ✅ {conditional 1}
- ✅ {conditional 2}
- ...

## 推荐信息源策略
{Brief plan, detail in Phase 3}

## 关键避坑
{如果对标了 X 行业报告，提醒避开哪些不适用的章节}
```

**用户必须确认 Phase 1 诊断结果，再进入 Phase 2。**

---

## 反诊断（什么是 BAD 诊断）

❌ "和电池产业一样按上游 / 中游 / 下游分" —— 对 AI 软件 / 消费品根本不适用
❌ "做 ABCDE 五大块"——没有 archetype 判断，纯框架套用
❌ "重点是估值"——估值是结果不是核心矛盾，应该是"驱动估值的本质因素"
❌ "中美博弈"——这不是核心矛盾本身，是核心矛盾的 derived 影响

✅ "本行业核心矛盾是 X，因为 Y"——句子清晰，原因可验证
