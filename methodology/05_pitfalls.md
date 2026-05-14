# 8 条避坑铁律 · The Ironclad Rules

> 这是这个 Skill 最重要的文件。每次跑 pipeline 前必须重读。所有规则都来自真实研究项目的血泪教训。

---

## ⚠️ 1. 不要表面模仿参考报告

**反例**：用户给了一份"电池产业链分析"作为对标，于是把"上游矿物 / 中游材料 / 下游整车"硬套到具身智能上，强行写"基础原材料层（稀土/铜/PEEK）"作为核心章节。

**正解**：参考报告是"分析思维 reference"，不是"目录模板"。学的是 **怎么思考行业的核心矛盾**，不是抄章节标题。

**操作纪律**：
- Phase 1 诊断未完成前，禁止决定章节
- 看到"对标 XX 报告"指令时，先读那份报告的"为什么这样组织"，再问"我的行业是否有同样的矛盾"
- 如果矛盾不同，章节就不同

---

## ⚠️ 2. 先想行业本质，再想结构

**反例**：上来就写 5 个并行 agent 跑"上游 / 中游 / 下游 / 应用 / 政策"——但这是制造业思维，对 AI 软件 / 消费品 / 服务业 / 医药完全不适用。

**正解**：每个行业有 1-2 个"决定胜负的核心矛盾"，先抓住这个：

| 行业类型 | 真正的核心矛盾 |
|---|---|
| 早期硬科技 | 技术路线之争 + PMF 时间 + 玩家路径 |
| AI 软件 | 模型能力 + 分销渠道 + 单位经济 + 数据 moat |
| 制造业 / 工业品 | 供应链 + 成本 + 规模 + 政策 |
| 消费品 | 品牌 + 渠道 + 用户洞察 + 单店模型 + 海外扩张 |
| 服务业 / 平台 | 供需匹配 + 网络效应 + 单位经济 |
| 创新药 / 医疗器械 | 管线 + 临床数据 + 适应症 + 支付方 + 监管路径 |
| 能源 / 新能源 | 技术 + 规模 + 政策 + 单位经济 + 供应链 |
| Fintech | 监管 + 单位经济 + 风险模型 + 网络效应 |

Phase 1 诊断要明确写出本行业的核心矛盾。

---

## ⚠️ 3. 信息源 > 框架

**反例**：写"a16z 一定看好 humanoid"——这是凭训练记忆编造，没有可追溯的 URL。

**正解**：所有"顶尖人物 thesis"必须来自可追溯的公开来源（X / 播客 / 博客 / 官方访谈 / 机构 thesis post）。

**操作纪律**：
- 引用任何人物的观点 → 必须带 URL + 时间
- 抓不到原话 → 不写或标 `[INFERRED]`
- 优先搜的 5 类源：
  1. **创业者 X / 播客**：Brett Adcock / Eric Jang / 王兴兴 / Sam Altman 等
  2. **投资机构 thesis post**：a16z / Sequoia / Benchmark 的官方博客
  3. **学者访谈**：Lex Fridman / Dwarkesh / 20VC
  4. **行业批评者**：被忽略的反方声音（最珍贵）
  5. **官方文件**：FDA / SEC / 工信部 / BIS

---

## ⚠️ 4. PE 内部工具放附录，不污染行业研究

**反例**：在主报告里写"投委会必问 10 个问题 + 标准答案"、"IC Memo 模板"、"投资优先级 ★★★★★ 矩阵"、"组合配置建议（人民币 30% + 美元 15%）"、"决策树"。

**正解**：这些是 **deal-level 工具**，与"行业研究"是两个完全不同的产品。投委会 Q&A 不会出现在任何专业的行业研究报告里。

**操作纪律**：
- 主报告：行业现状、技术、玩家、商业化、政策、变量、争议
- 附录：仅在用户明确要求时才有 IC memo / 决策树 / 组合配置
- 默认：不放任何 PE deal-level 工具进主报告

---

## ⚠️ 5. 每个数字必须可追溯

**反例**：写"中国稀土永磁市占 92%"但没有引用源；写"2030 全球出货 150-300 万台"没区分"年度新增"vs"累计保有量"。

**正解**：
- 每个数字 ≥ 1 个 URL 引用
- 核心论点的数字 ≥ 2 个独立源交叉验证
- 不可追溯时明确标：
  - `[UNSOURCED]` — 无来源，需 reviewer 补
  - `[INFERRED]` — 基于其他数据推算
  - `[UNDISCLOSED]` — 公司未披露
- 单位 / 口径 / 时间标清楚（年度 vs 累计、出货 vs 装机 vs 交付、USD vs RMB）

---

## ⚠️ 6. 基础数学必须两次验证

**反例**：写"Figure RaaS = $25/hr × 8h × 250d = $360K/年"——实际是 $50K（差 7×）；写"Figure 2030 收入 $25B"但全球 TAM 仅 $15B——单家公司不可能占 167%。

**正解**：
- 定价公式（× 小时 × 天）当场算两次
- 收入预测对比 TAM——单家公司不能占 > 60-70%
- DCF 输入（出货量 × ASP × 毛利率 × 折现因子）每一步验算
- 占比数字（GDP / 市场份额）算两次

**操作纪律**：写完每个含乘除的公式后，重新算一遍。

---

## ⚠️ 7. 软化强判断

**反例**："必然洗牌"、"稳态格局"、"全链垄断"、"世代级机会"、"绝对主导"。

**正解**：
- 必然 → 大概率 / 有较高概率
- 稳态格局 → 当前格局
- 全链垄断 → 主导 / 高份额
- 世代级机会 → 历史级量级机会（前提：…）
- 绝对主导 → 主导
- 概率给定（"40%"）→ 区间（"30-50%"）+ 触发条件

**操作纪律**：写完每个段落后扫描强词，软化。

---

## ⚠️ 8. v1 完成后必须跑对抗性评审

**反例**：v1 完成就交付，自己没找到 3 处致命错（口径错位 / 数学错 / 概率拍脑袋）。

**正解**：
- v1 完成后强制跑 `debate-critic` agent（参考 `07_critic_protocol.md`）
- Critic 找出 fatal / severe / improvement / gap 4 类问题
- Fatal & severe **inline 修复**，不在报告里写"自审与勘误"章节
- 自审是内部 ERRATA 文档（`WORKING/ERRATA.md`），不出现在交付报告里

---

## 元规则

**怀疑你自己**：v1 报告的 80% 内容大概率是对的；20% 隐藏致命错。这 20% 一定要 critic 帮你找出来。

**怀疑训练记忆**：训练数据截止在过去某个点；行业每周都在变。任何"我记得 XX 公司估值 XX 亿"都要 WebSearch 验证。

**怀疑表面共识**：媒体说"行业一片大好"时，最重要的信息往往在反方声音里（a16z 内部 Casado vs Hsu 的张力比 a16z 的官方 thesis 更值钱）。

---

## ⚠️ 9. PE 报告是"投资逻辑驱动"，不是"产业链全景图"

来自 embodied_ai_2026 第三方评审的尖锐教训：

**反例**：花一整章写"基础原材料层"（稀土永磁 / 铜 / 镁 / 特种钢 / PEEK / 碳纤维 / 铍铜），含储量-开采-加工三段式 + 多个饼图 + 战略地缘叙事。结果第三方反馈："**一般分析具身智能，谁会拿完整的一页专门分析上游原材料呢？**"

**为什么错**：
- PE 关心的是：这个标的能不能在 3-5 年内退出、估值能涨多少、护城河在哪
- 上游材料对一个具身智能整机厂（或 Tier 1）的投资逻辑影响**有限**——它影响 BOM 成本和毛利，但**不影响这家公司能不能赢**
- 除非你投的就是上游材料公司本身

**普适原则**：
- **不要把"产业链全景图"塞进 PE 报告核心章节**——产业链分析是 sell-side / 政府咨询的产物，不是 buy-side 的核心
- **每个章节都要回答"对投资决策有什么影响"**——如果答案是"基本无影响"，就该压缩成一张表或一个段落，不该是独立章节
- **"概念材料 / 概念股"在二级市场叙事很热，但一级市场 PE 尽调要冷处理**——A 股一堆"机器人材料概念股"涨得很凶，但实际单机价值量、渗透节奏、能否锁定份额都不确定

**操作纪律**：
- Phase 2 章节装配时问自己："这一章不存在，投资决策会变吗？"
  - 答案"会"→ 核心章节
  - 答案"几乎不会"→ 压缩成一张表 + 一句战略提示，放进 BOM 拆解 / 投资优先级矩阵
- 上游材料的位置：
  - "成本结构 / BOM 拆解"那一节里**用一张表带过**（材料占 BOM 多少 / 关键材料价格敏感性 / 是否存在供应集中度风险，比如稀土的中国集中度其实是个值得提的地缘点）
  - "产业链投资机会图谱"里**作为优先级最低的一档**，明确标注"受益逻辑成立但弹性有限、确定性低、建议作为主题观察而非核心配置"

---

## ⚠️ 10. 排版纪律：CSS 统管，禁 inline style

来自 embodied_ai_2026 v4 → v5 layout 迭代教训：

**反例**：
- 部分 `<h2>` / `<h3>` 加了 `style="margin-top:0;"` 覆盖 CSS
- 卡片内 / 卡片外标题间距不一致
- TOC 用 3 列但章节顺序不连贯，导致左右列上下错位
- 同一个 `data-card` 内有的标题贴边、有的有间距

**正解**：
- **所有间距由 `<style>` 块统一管理**——CSS 是 single source of truth
- 标题间距标准化：
  - `h2`: `margin-top: 48px; margin-bottom: 20px;`
  - `h3`: `margin-top: 36px; margin-bottom: 14px;`
  - `:first-child` / `:first-of-type` 重置为 0（避免容器顶部空白）
  - `h2 + p` / `h3 + p` 重置 `margin-top: 0`（避免双重间距）
- **禁止 inline `style="margin-top:0"`**——用 utility class 如 `.!mt-0 { margin-top: 0 !important; }`
- **TOC 按阅读顺序排列**——不要 3 列把章节散开导致视觉错位；2 列分"核心 vs 补充"或单列展开更清晰
- **章节间距统一**：`section.section-anchor { padding-top: 64px; padding-bottom: 64px; }`

**操作纪律**：HTML 生成完后跑一次"排版自检"：
- grep `style="margin` 应该是 0 个 inline
- 看预览：每个 chapter header 高度一致，每个 h2/h3 前面间距一致
- TOC 行视觉对齐，左右列上下不错位

---

## ⚠️ 12. 数字一致性审计：TAM / CAGR / PSR / DCF 必须互相咬合

来自 embodied_ai_2026 v5→v6 数字审计教训（第三方反馈："现在不要再加内容了，先做一轮数字审计"）：

**反例**（v5 真实出错）：
- TAM 写"$120-150 亿（中位）"，但同时给"出货 25-80 万 × ASP $12-18K"——按这个区间中位应是 50万 × $15K = $75 亿，不是 $150 亿（差 2×）
- CAGR 写"35-45%"，但同时给"2025 1.8 万 → 2030 25-80 万"——按这个区间应是 69-113%（差 2-3×）
- PSR 写"智元 280×"，但同时给"¥200亿/¥10亿"——这是 20×，不是 280×（差 14×）
- DCF 写"三家 2030 收入 $8.5B 占 TAM $15B = 57%"，但 TAM 中位实际是 $7.5B——三家占 113%，超过全市场

**为什么致命**：PE 投委会会盯着分母（TAM）和分子（收入 / 估值）的咬合度。任何一组数字内部不自洽，**整份报告的信誉就崩了**。第三方反馈原话："报告越专业，投委会越会盯着这些分母打"。

**正解 · 数字一致性审计纪律**：

报告 v1 完成 → **立刻跑数字一致性审计**，至少校 4 组：

| 维度 | 检查方法 | 一致性公式 |
|---|---|---|
| **TAM** | 出货 × ASP = TAM | 低端低端 / 中位×中位 / 高端×高端 三组都验算 |
| **CAGR** | (终值/起值)^(1/n) - 1 | 出货 CAGR ≠ 市场规模 CAGR（口径不同要明示） |
| **PSR** | 估值 / 营收 | 货币口径统一（USD or RMB），不混用 |
| **DCF / Sanity check** | 三家合计收入 / TAM | 不能超过 60-70% 集中度上限 |
| **市占率** | 公司份额 % 总和 ≤ 100% | 全行业各家份额和 |
| **百分比** | 必有分母明示 | 占 GDP %、占总收入 %、占 TAM % 不能混 |

**做法**：
- v1 完成后写一个 Python 脚本，把所有"X 元 / X% / X 亿"提取出来交叉验算
- 或人工把每组数字列在 Excel / Markdown table 里逐行检查
- 用"高低区间端点"对照公式，验证"中位"是否真在中间

**额外纪律**：
- **CAGR 必须标基期与口径**：是出货 CAGR 还是市场规模 CAGR？基期是 2024 还是 2025？
- **PSR 必须标 LTM / NTM**：LTM (last 12 months) 用历史营收；NTM (next 12) 用预测营收。混用是常见错
- **DCF 名称要诚实**：不含 capex / NWC / 税 / 逐年现金流的不能叫"完整 DCF"，应叫"EBIT terminal-value sanity check"或"简化估值锚"
- **占 GDP 等百分比**：算两次。如 "550 亿 / 130 万亿 GDP = 0.04%" 不是 "0.07%"

**操作前先回答**："如果一个投委会成员拿计算器复算每组数字，会发现哪里不咬合？" — 如果答不上，就还没做完审计。

---

## ⚠️ 13. 引语 attribution 必须 web-verify · Critic 也会犯错

来自 R1 F4 + R3 F2 双向教训（critic 自己一次错一次对）：

**R1 F4** · Critic 说 "Oliver Hsu" 是虚构的（a16z 找不到此人）→ **Critic 错了**，Oliver Hsu 是真实 a16z partner，文章在 a16z.news/p/the-physical-ai-deployment-gap

**R3 F2** · Critic 说 "Humanoids are most hyped" 这句话不是 Casado 说的，是 Polovets 说的 → **Critic 对了**，web 验证确认 Polovets 是嘉宾，Casado 是主持人

**操作纪律**：
- 每个引语 attribution 必须 web verify 一次（不是只验证 quote 内容，还要验证 speaker）
- Critic 找到的 attribution 错误也要 web verify（critic 可能错也可能对）
- 引语模板：`<speaker, role, affiliation> 在 <publication, date> 说："<quote>"` + URL
- Multi-speaker 场景（播客 / 圆桌 / 对谈）必须明确"是谁在那一句话上说的"

**典型错误**：把 podcast guest 的发言归于 podcast host，把官方机构博客的 author 名字搞错——这些是引语 attribution 的 P0 bug。

---

## ⚠️ 14. Critic 循环的"修订效率衰减"

来自 embodied_ai_2026 三轮 critic 实测：

| Round | 找到 issues | 一轮内 resolved | Resolved 率 |
|---|---|---|---|
| R1 | 14 (4F+10S) | 12 fully + 2 partial | 86% |
| R2 | 11 (3F+8S) | 7 fully + 4 partial | 64% |
| R3 | 5 (2F+3S) | 5 inline (no critic verify) | n/a |
| **3 轮累计** | **30 issues** | **~24 resolved** | **~80%** |

**发现**：
- R1 resolved 率最高（修主战场效果好）
- R2 大量 partial：作者修了主要文本，但**联动数字 / 图表 JS / 不同章节引用未同步**
- R3 又找到 R1+R2 漏过的 fresh-eye issue（如 attribution 错）

**纪律**：
- 不要假设"一轮修干净"——partial 修复是常态
- 修订必须**逐行联动**：修一个数字，grep 所有同名 / 同义引用一起改
- 关键数字（TAM / PSR / DCF / 概率）建立"single source of truth"变量，正文统一引用
- R1 → R2 之间应该跑"数字咬合自检"（pitfall #12），不要直接进 R2
- Max rounds 3 协议下，R3 末 critic 仍可能找到 fatal——这是常态，可以承认 known limitations 交付，不必无限循环

**对 industry-report skill 的隐含改进**：
- 在 Phase 5 Adversarial review 后加 **Phase 5.5 · Number reconciliation**：跑 grep 把 critic 找到的数字在全报告所有引用位置找出来，一并修
- 避免"修了主表没修解读 / 修了文字没修 chart JS / 修了主报告没修 IC Memo 残留"

---

## ⚠️ 11. 章节编号必须前后一致

来自 v3 → v4 重排教训：

**反例**：新增第一-四章后，旧"第一章/第二章/第三章"内的小标题仍是 1.0 / 1.1 / 2.x / 3.x。读者看到"第五章 产业链与硬件"下面的小标题是 1.0、1.1、1.2 会立刻觉得是"拼接稿"。

**正解**：
- 任何章节级别的重排，必须连带 sub-section 编号一起改
- 编号规则要明示：
  - 核心章节用阿拉伯数字 1-N
  - 补充章节延续编号（如 5-6）或用罗马数字
  - 附录用字母 A / B / C
- 不要混用：不能"第五章"配 "1.0 / 1.1"，要么改成"5.0 / 5.1"，要么把"第五章"改成"第一章"

**操作纪律**：重排后 grep `<h2>` 看所有标题编号是否连贯；TOC 锚点是否还对得上。

---

## ⚠️ 15. HTML 结构完整性：禁用正则破坏性改写，div balance 必跑

来自 embodied_ai_2026 v6 layout-bug 教训（用户反馈："你现在已经把格式跑乱了"，配截图：summary 区出现 0.2 / 0.3 单字换行）：

**反例**（真实事故）：
- v6 自动审计脚本里写了 `html = re.sub(r'  +', ' ', html)`，意图压缩多余空白，但 **HTML 里的多空格在 `<pre>` / 属性串 / inline-block 排版中是有意义的**
- 同一次改写漏掉一个 `</div>`（line 332 kpi-label 未闭合），并多写一个 `</div>` （line 303 TOC 区），结果整个文档 grid 容器闭合错位
- 浏览器没报错，但 grid 退化导致 `grid-cols-2` 变成超窄列，文字逐字换行 → 用户截图里看到的 "0./.2/./3/x" 单字流

**为什么致命**：
- HTML 静默崩塌——浏览器不会抛错，靠肉眼很难发现
- 单字换行的视觉信号 = grid / flex 容器宽度异常 = 99% 是上游 `<div>` 未闭合或多闭合
- 用户在大屏看效果，单字换行立刻被注意到，但模型本地的 markdown / 文本预览看不出

**正解 · 结构性改 HTML 的纪律**：
1. **永远不要用 `re.sub` 改 HTML 结构**——空白压缩、属性重写、标签替换都禁用正则
   - 要改用 BeautifulSoup / lxml / html5lib 解析后操作 DOM
   - 唯一可以用正则的：注释 (`<!-- ... -->`) 或注释里的纯文本片段
2. **每次保存 HTML 后强制跑 div balance check**：
   ```python
   from html.parser import HTMLParser
   class Counter(HTMLParser):
       def __init__(self): super().__init__(); self.opens=0; self.closes=0
       def handle_starttag(self, tag, _): 
           if tag=='div': self.opens+=1
       def handle_endtag(self, tag):
           if tag=='div': self.closes+=1
   c = Counter(); c.feed(open('report.html').read())
   assert c.opens == c.closes, f"DIV MISMATCH: {c.opens} open vs {c.closes} close"
   ```
3. **section 级别 balance**：把每个 `<section>` 单独喂进 parser，验证每段内部 self-contained
4. **修复后用 Playwright 取多个 section 截图**，肉眼对比 grid 列宽是否正常

**用户信号识别**（critical）：
- 截图里看到 "0./.2/./3" 单字独占一行 → grid 容器破损，**最优先排查 `</div>` 平衡**
- 不要去调 CSS / 字号 / flex-wrap——那是症状，根因 99% 在 HTML 闭合

---

## ⚠️ 16. 用户重金投入的 HTML 资产不要轻易转 PPT

来自 embodied_ai_2026 PPT 实验教训（用户反馈三连："图太少了"→"和 html 完全不一样"→"不希望你做 ppt 了"）：

**反例**：用户在 HTML 报告里投入 25+ Chart.js 图表 + Mermaid 流程图 + 多列 grid 排版。我接到"做 PPT"指令后另起炉灶用 python-pptx 写了 76 页稀疏 PPT（一页内容拆成几页讲），完全丢掉 HTML 的视觉资产。

**为什么错**：
- 用户的"做 PPT" ≠ "从零开始写 PPT"
- 默认意图是："把 HTML 报告的信息密度和图表带到 PPT 里"
- 重做 PPT 等于把几个小时的 HTML 设计劳动全部作废

**正解 · PPT 转换决策树**：

接到"做 PPT"指令时，先问三个问题：

| 问题 | 答案 → 路径 |
|---|---|
| 已经有 HTML 报告吗？ | 有 → 走"HTML 转 PPT"路径，不要重做 |
| HTML 里有图表 / mermaid / 排版资产吗？ | 有 → 必须保留，最低限度截图嵌入 PPT |
| 用户给了页数限制吗？ | 没说 → 默认 25-40 页（不是 70+ 页稀疏稿） |

**HTML → PPT 的两种正解**：

1. **截图嵌入路线**（保真度高，编辑性低）
   - Playwright 把每个 section 渲染为 PNG → 整页或多张拼贴塞 PPT
   - 适合：用户只看不改，重视视觉一致性
   - 缺点：PPT 里图不能再编辑，文本不可选

2. **重建路线**（编辑性高，工作量大）
   - HTML 里的 Chart.js 数据 → 提取为 pptx native chart
   - HTML 里的表格 → pptx table
   - 配色 / 字体 / 间距严格沿用 HTML 的设计语言
   - 适合：用户要在 PPT 里改数字 / 配合内部模板
   - 必须：每页信息密度 ≥ HTML 同等 section，不允许"一页拆成几页"

**PPT 密度规则**（来自用户反馈"图太少 / 一页拆几页"）：
- 每页 ≥ 1 个可视元素（图 / 表 / 图标矩阵），纯文字页禁出
- 标题 + 3-5 个支撑论点 / 数据点 + 1 个图——这是"密"的基线
- 把 HTML 一个 section 的全部信息塞 1-2 页 PPT，不是 5-8 页

---

## ⚠️ 17. Playwright 渲染 CDN-heavy HTML：用 `load` 不用 `networkidle`

来自 embodied_ai_2026 截图验证教训：

**反例**：写截图脚本默认 `await page.goto(url, wait_until="networkidle")`——但 HTML 用 Chart.js / Mermaid / Tailwind 全走 CDN，CDN heartbeat + 字体加载让 network 永远不 idle，60s 后 timeout。

**正解**：
```python
await page.goto(f"file://{path}", wait_until="load", timeout=60000)
await page.wait_for_timeout(3000)  # 给 Chart.js / Mermaid 一点渲染时间
# 如果有 chart.js，可以等具体的 canvas 元素：
await page.wait_for_selector("canvas", state="attached", timeout=10000)
```

**优先级**：
- `load` — DOM + 图片 + 字体加载完即 OK（推荐 default）
- `domcontentloaded` — 只等 DOM，最快但 chart 可能未渲染
- `networkidle` — 用于 SPA 已知 network 会 idle 的场景，CDN-heavy 报告不要用

---

## ⚠️ 18. 仓库卫生：实验产物不入主仓库，保留入口文件

来自 embodied_ai_2026 → xiongjjlj/embodied-ai-report 推送教训：

**反例**：开发过程产出 7-8 个 PPT 实验文件（`generate_deck.py` v1 / v2、`html_to_pptx.py`、`embodied_ai_deck.pptx`、`section_pngs/` 几百张 PNG、`report_v2_backup.html`、`deck_outline.md`），若直接 `git add .` 全推上去——主仓库被实验垃圾污染。

**正解 · 推送前 checklist**：

1. **明确"交付物" vs "工作产物"**：
   - 交付物：`report.html` / `FULL_REPORT.md` / `sections/` / `data/` → 推
   - 工作产物：`generate_*.py` / `*.pptx` / `section_pngs/` / `*_backup.*` / `deck_outline.md` / `.DS_Store` → 不推
   - 中间审计：`ADVERSARIAL_REVIEW.md` / `PIPELINE.md` / `SKILL_EVALUATION.md` → 看情况，作为"研究过程留痕"可以放，作为"内部 ERRATA"不放

2. **保留远端入口**：远端可能已有 `index.html`（GitHub Pages redirect）/ README 等入口文件——`git clone` 后**先 inspect 远端有什么**，不要本地直接覆盖
   ```bash
   git clone <remote> /tmp/remote-check
   ls /tmp/remote-check/   # 看远端有什么必须保留
   # 然后选择性 cp，不要 rsync --delete
   ```

3. **commit 前 dry-run**：
   ```bash
   git status --short | head -30   # 看新增 / 修改 / 删除
   git diff --stat <changed_file>  # 看每个文件改了多少行
   # 异常大的 diff（如 report.html 改了 3000 行）要警觉是不是误格式化
   ```

4. **commit message 写"为什么"**：
   - ❌ "Update report.html"
   - ✅ "Fix HTML layout bug: missing </div> at line 332 caused grid collapse and single-char wrapping in summary sections"

---

## ⚠️ 19. 用户截图反馈的"症状 → 根因"映射表

来自三轮用户视觉反馈累积：

| 症状（用户截图） | 99% 是这个根因 | 排查命令 |
|---|---|---|
| 文字 0./.2/./3 单字换行 | grid / flex 容器破损（div 不闭合） | HTMLParser div balance |
| 整页空白只有一行字 | section padding 或 height: 100vh 错误 | grep `100vh\|padding-top` |
| 图表显示"Loading..."不出来 | Chart.js / Mermaid CDN 没加载 | 看 console，等 `wait_for_selector("canvas")` |
| TOC 链接跳不到 | anchor id 和 href 不匹配 | grep `id="ch` vs `href="#ch` |
| 不同 section 同字号但视觉大小不一 | container width 不同导致响应字号 | 看 `clamp() / vw` 单位 |
| 一列变两列错位 | grid-cols-2 容器破损（同 #1） | 同 #1 |
| 字看不清（低对比度） | 配色冲突，深底深字或浅底浅字 | 改 CSS variables，重审色板 |
| 文字溢出卡片边缘 | 卡片 overflow 没设 / 字号过大 | `overflow: hidden` + 缩字号 |

**操作纪律**：用户发截图 + 一句话反馈时，先对照这张表，不要直接动手——猜错根因等于二次破坏。
