# 第三章 中游：AI 模型、仿真平台、数据采集、训练算力

> 数据截止 2026-05-12。本章聚焦具身智能产业链"大脑"层级——VLA / 世界模型 / 仿真 / 数据 / 算力。这是参考报告（弘毅 2023.9《全球电池与电动车产业链格局分析》）所没有的层级，也是 PE 判断技术代差与投资窗口的核心。

---

## 0. 章节摘要（Executive Summary）

具身智能中游正在经历从"小模型 + 特定任务"到"端到端 VLA + 大规模预训练"的范式迁移。我们将中游拆为四层：

1. **模型层（VLA & 世界模型）**：2023 年 RT-2 首次把互联网级 VLM 引入机器人；2024 年 OpenVLA (7B)、π0、Octo 把开源水位拉到接近 SOTA；2025 年进入"双系统架构"主流时代——Figure Helix（S2 7B VLM + S1 80M 视觉运动策略）、NVIDIA GR00T N1（2B）、智元 GO-1（ViLLA）三足鼎立；2026 年 π0.5、GR-3、GR-RL、SmolVLA (450M) 把"小模型 + 强后训练"推到新高度。LIBERO 4 个 task suite 平均成功率从 2024 年 76%（OpenVLA）→ 2025 年 97.1%（OpenVLA-OFT），数据飞轮已经启动。

2. **仿真层**：NVIDIA Isaac Lab + Cosmos 世界基础模型构成西方阵营；Genesis（MIT 牵头 20 个实验室）以 430,000× 实时倍速开源、ManiSkill3（SAPIEN/Hillbot）以 4M+ 演示数据成为开源黑马。国内字节、华为、商汤主要采购或基于 Isaac 二次开发，Sim-to-Real Gap 仍是核心瓶颈。

3. **数据层（最核心瓶颈）**：三条路径并行——(a) 真机遥操作（ALOHA $32k / UMI $2-3k / DexCap）；(b) 大规模人类视频（Ego4D 3,670 小时 + EgoVLA）；(c) 仿真合成（银河通用 GraspVLA 十亿帧）。开源数据集进入"百万轨迹"时代：Open X-Embodiment 100 万 + 轨迹 / 22 embodiment；DROID 76k trajectories / 564 scenes；智元 AgiBot World 100 万 + 真机轨迹 / 217 任务（号称比 OXE 长程数据规模高 10×）。数据 Scaling Law 已被实证（Stanford 2024）：环境与物体多样性 > 单环境演示数。

4. **算力层**：训练 OpenVLA = 64×A100 × 15 天 ≈ 23k GPU-hour；π0 / Helix / GR00T 量级未公开但估算在 1k–10k H100 量级。中美算力差距是中国具身智能最大的"卡脖子"——2025.12 美国虽然部分放开 H200 对华出口（加 25% 关税），B100/B200/Blackwell 全系仍受限。中国具身智能公司不得不走"仿真大数据 + 小模型"路线（银河通用、智元）以及"国产芯片"路线（华为昇腾、寒武纪）。

**底层判断**：(1) VLA 模型层正以 6 个月一代的速度迭代，参数规模与训练数据相比 LLM 仍小 100–1000×，"GPT-3 时刻"尚未到来，但临近；(2) 数据是结构性壁垒，谁掌握遥操作工厂 + 仿真管线 + 真机部署回流，谁就掌握具身智能的"Data Engine"；(3) 仿真 + 世界模型将吃掉相当一部分真机数据需求，对资本密集型玩家不利。

---

## 1. 技术路线全景

### 1.1 端到端 VLA（Vision-Language-Action）：主流路线

VLA = 把 Vision-Language Model（VLM）当 backbone，对机器人动作做联合建模。一句话：让 GPT-4V 不光能"看图说话"，还能"看图动手"。

#### 主要 VLA 模型对比表

| 模型 | 团队 | 时间 | 参数量 | 训练数据 | 关键贡献 | 代表 Benchmark | 是否开源 |
|------|------|------|--------|---------|----------|---------------|---------|
| **RT-1** | Google | 2022.12 | 35M (EfficientNet+Transformer) | 130k episodes / 13 robots / 17 月 | 首个 Transformer 化端到端机器人策略 | 真机 700+ 任务 | 部分 |
| **RT-2** | Google DeepMind | 2023.7 | 55B (PaLI-X) | OXE + web 数据 co-finetune | 首次把互联网 VLM 用作机器人 backbone；emergent semantic reasoning | RT-2 emergent eval | 闭源 |
| **RT-X / RT-2-X** | Google DeepMind + 21 实验室 | 2023.10 | 55B | OXE 100 万 + 轨迹 / 22 embodiment | 首个跨 embodiment 大模型 | 9 个真机 lab | 闭源 |
| **Octo** | UC Berkeley | 2024.5 | 27M / 93M | OXE 800k episodes | Transformer + Diffusion Policy；模块化 | LIBERO / 真机 | 开源 |
| **OpenVLA** | Stanford+Berkeley | 2024.6 (arXiv 2406.09246) | 7B (Llama-2 + SigLIP+DINOv2) | OXE 970k episodes | 7B 在 BridgeV2 上超过 RT-2-X (55B)；64×A100×15 天 | LIBERO 4 套件 76.5% (orig); OFT 版 **97.1%** | 完全开源 |
| **π0** | Physical Intelligence | 2024.10 (arXiv 2410.24164) | 3B (PaliGemma+ Flow-matching) | 10k+ 小时多机器人数据 | Flow-matching 替代离散动作 token；50Hz 高频控制 | 真机 SOTA | 开源 (openpi) |
| **π0-FAST** | Physical Intelligence | 2025.1 | 3B | 同上 | DCT 频域 action tokenizer，训练加速 5× | 真机 SOTA | 开源 |
| **π0.5** | Physical Intelligence | 2025.4 (arXiv 2504.16054) | 3B+ | 多机器人 + web + 高层语义 | "Knowledge Insulation"；open-world 泛化 | 真新家庭场景 | PyTorch 开源 (2025.9) |
| **Helix** | Figure AI | 2025.2 | S2: 7B VLM + S1: 80M policy | ~500 小时多机器人多操作员数据 | S1/S2 双系统；35-DoF / 200Hz；首个双机器人共享任务 VLA | 真机零样本上千物体 | 闭源 |
| **Helix 02** | Figure AI | 2025.11 | 同上扩展全身 | + 全身行走数据 | 走路 + 操作 + 平衡，单网络 | 长 horizon 整屋自主 | 闭源 |
| **GR00T N1** | NVIDIA | 2025.3 (arXiv 2503.14734) | 2B | Ego human video + sim + 真机 + 合成 | 首个"全开源"通用人形 foundation model；S1/S2 双系统 | 真机泛化 | HF 开源 (`nvidia/GR00T-N1-2B`) |
| **GR00T N1.5 / Newton** | NVIDIA + Disney + DeepMind | 2025.6+ | 持续迭代 | + Newton 物理引擎合成数据 | 物理引擎共建生态 | — | 部分开源 |
| **GR-1** | 字节 Seed | 2023.12 | ~270M | 大规模视频生成预训练 + 机器人微调 | 用视频生成模型预训练 | CALVIN SOTA | 开源 |
| **GR-2** | 字节 Seed | 2024.10 | — | 真机 + 网络视频 | 世界建模 + 动作生成统一 | 真机长 horizon | 闭源 |
| **GR-3 + ByteMini** | 字节 Seed | 2025.7 | — | 真机 + 仿真 | 形变物（衣物折叠/挂衣 70-80%） | 真机 | 闭源 |
| **GR-RL** | 字节 Seed | 2025.12 | — | 真实 RL 微调 GR-3 | 系鞋带成功率 45.7% → 83.3%；首次 real-world RL for VLA | 真机长 horizon | 闭源 |
| **GO-1 (ViLLA)** | 智元 (AgiBot) | 2025.3，2025.9 开源 | 多模态 | AgiBot World 100 万 + 轨迹 | "ViLLA"潜动作 token；通用基座 | 真机 5 大场景 | 全面开源 |
| **GraspVLA** | 银河通用 | 2025.1 | — | **10 亿帧** 全仿真合成 V-L-A 对 | 全球首个全仿真预训练抓取基础模型；CES NV 黄仁勋演讲 | 真机抓取超 OpenVLA/π0/RT-2/RDT | 即将开源 |
| **CogACT** | Microsoft | 2024.11 (arXiv 2411.19650) | 7B + diffusion action transformer | OXE | 解耦 VLM 与动作模块，diffusion 动作头 | 仿真 +35% over OpenVLA，真机 +55% | 开源 |
| **RDT-1B** | 清华 TSAIL | 2024.10 | 1B (Diffusion Transformer) | OXE + 自采 6k+ episodes | 双臂 diffusion 策略 | 真机双臂 | 开源 |
| **SmolVLA** | HuggingFace LeRobot | 2025.5 | **450M** | 仅 LeRobot 社区开源数据 | 消费级 GPU 可跑；在 LIBERO/Meta-World 超 ACT | LIBERO/Meta-World/SO-100 | 完全开源 |
| **OpenVLA-OFT** | Stanford | 2025.2 | 7B + OFT | LIBERO 4 任务 LoRA r=32 | 微调加速 + 推理加速；LIBERO 平均 97.1% | LIBERO SOTA | 开源 |
| **Spirit v1** | LeRobot/Pollen Robotics | 2024 | — | 社区数据 | 开源 humanoid demo | — | 开源 |

#### 几个关键技术 takeaway

- **参数规模**：当前主流 VLA 在 0.45B–7B 之间，远小于 LLM 的 70B–700B；瓶颈是 (a) 高频实时控制约束模型 ≤7B；(b) 机器人数据量远不够撑 100B+ 模型。
- **动作表达三大路线**：① 离散 token（RT-2, OpenVLA）；② Diffusion 连续（Octo, RDT, CogACT, Diffusion Policy）；③ Flow-matching（π0、π0.5）。Flow-matching 在 2025 年成为高频控制（50–200Hz）的事实标准。
- **双系统架构 (S1/S2)** 在 2025 年成为人形机器人主流：System 2 (慢思考 VLM, 7-9Hz) + System 1 (快反应 policy, 200Hz)。Figure Helix / NVIDIA GR00T / Helix 02 / 智元 GO-1 全部采用。

### 1.2 分层架构 vs 端到端：路线之争

| 路线 | 代表 | 优点 | 缺点 |
|------|------|------|------|
| 完全端到端（pixel-to-action） | Helix 02、π0、OpenVLA | 减少误差累积、scaling 友好 | 训练数据要求极大 |
| 双系统（VLM 规划 + 控制策略） | Helix v1、GR00T N1、GO-1 | 平衡推理与高频；可解释 | 接口设计是 hack |
| 三层（任务规划 + 技能 + 控制） | 早期 SayCan、ALFRED、Figure 01 | 模块化、可调试 | 误差累积、僵化 |

2026 年趋势：**端到端（含双系统）是主流**，"三层"逐步被淘汰，但在工业场景仍有市场。

### 1.3 Diffusion Policy：上一代基础

- **论文**：Chi et al. 2023, RSS Best Paper Nominee（Columbia + TRI + MIT）
- **核心**：把动作建模为条件扩散过程，处理多模态分布
- **影响**：在 12 个任务上平均比 SOTA 高 46.9%；成为 Octo、CogACT、RDT 的"事实基础组件"
- **TRI Large Behavior Model (LBM)** 是基于 Diffusion Policy 的工业化版本，2024 年成果

### 1.4 世界模型（World Model）：第二条战线

世界模型 = 让 AI"在脑子里模拟物理世界"，可作为：
- 仿真器（生成训练数据）
- Planner（在脑内 rollout 多个未来）
- 通用表征学习（学到的隐空间作为机器人 backbone）

| 模型 | 团队 | 时间 | 训练数据 | 关键能力 |
|------|------|------|---------|----------|
| **Genie 2** | DeepMind | 2024.12 | 大规模视频 | 文本→可玩 3D 环境；360p / 1 分钟一致性 |
| **Genie 3** | DeepMind | 2025.8 | 视频 + RL | 720p / 24fps 实时交互；记忆 1 分钟；2026.1 商业化（$250/月 AI Ultra） |
| **V-JEPA 2** | Meta | 2025.6 (arXiv 2506.09985) | **100 万小时**互联网视频 + 62 小时 DROID 机器人数据 | 自监督视频世界模型；Franka 零样本 pick&place 65-80% |
| **Cosmos WFM** | NVIDIA | 2025.1 (CES) / 2025.3 GTC / 2025.12 v2.5 | 200M curated 视频片段 | Text2World/Image2World/Video2World 统一；2B/14B 双尺度 |
| **Cosmos-Predict 2.5** | NVIDIA | 2025.12 | 同上 + Image2Image/ImagePrompt | 物理感知预测；为 GR00T 提供合成数据 |
| **Newton** | NVIDIA + DeepMind + Disney | 2025.3 announced | — | 开源物理引擎，差异化点 GPU 化的可微物理 |

**Cosmos 的合作生态**：1X、Agile Robots、Agility、Figure AI、Fourier、Galbot（银河通用海外名）、Hillbot、NEURA、Skild AI、小鹏 XPENG、Uber 等。

### 1.5 基础大模型作为 backbone

主流 VLA 的 VLM backbone 选型：

| Backbone | 厂商 | 被谁用 |
|----------|------|--------|
| PaLI-X (55B) | Google | RT-2, RT-2-X |
| Llama-2 7B + SigLIP/DINOv2 | Meta / Google | OpenVLA |
| PaliGemma (3B) | Google | π0, π0.5 |
| Qwen2-VL | Alibaba | 多个国内 VLA |
| SmolVLM (450M) | HF | SmolVLA |
| Eagle / NVLM | NVIDIA | GR00T N1 |
| GPT-4o / Claude / Gemini | OpenAI / Anthropic / Google | 高层规划 prompting |
| Florence-2 / LLaVA | Microsoft | 学术原型 |

---

## 2. 仿真平台

### 2.1 主流仿真器对比

| 仿真器 | 开发者 | 物理引擎 | GPU 并行 | 速度（vs real-time） | 强项 | 弱项 | 许可 |
|--------|--------|---------|---------|--------------------|------|------|------|
| **Isaac Sim** | NVIDIA | PhysX | 是 | 数千×并行 | 工业级、Omniverse 生态 | 闭源；GPU only | 商业免费 |
| **Isaac Lab**（继任 Isaac Gym） | NVIDIA | PhysX + Warp | 是 | 数千×并行 | 强化学习、人形支持齐 | 依赖闭源 Isaac Sim | Apache 2.0 框架 |
| **Genesis** | MIT + 19 实验室 | 自研 unified | 是 | **430,000×**（RTX 4090 单臂 43M FPS）；总体快 Isaac 10–80× | 多物理（刚体/软体/流体/布料）；4D 生成 | 生态较新 | 开源 Apache 2.0 |
| **MuJoCo / MJX** | DeepMind | MuJoCo | 是（MJX） | 数千×并行 | 接触建模精确；学术黄金标准 | MJX 仍在追赶 | Apache 2.0 |
| **PyBullet** | Erwin Coumans | Bullet | 否 | 实时 | 易上手 | 速度慢，物理粗糙 | Zlib |
| **Drake** | TRI / MIT | 自研 | 否 | 实时 | 控制理论严谨 | 学习曲线高 | BSD |
| **SAPIEN** | UCSD / Hillbot | PhysX (旧) | 是 | 数千× | ManiSkill 基座 | 渲染较弱 | MIT |
| **CoppeliaSim** | Coppelia Robotics | 多种 | 否 | 实时 | 工业 | 商业受限 | 商业 + 教育免费 |
| **Webots** | Cyberbotics | ODE | 否 | 实时 | ROS 友好 | 速度慢 | Apache 2.0 |
| **Gazebo** | OSRF | ODE/Bullet/DART | 否 | 实时 | ROS 默认 | 速度慢 | Apache 2.0 |
| **Newton** | NVIDIA+DeepMind+Disney | 可微 GPU 物理 | 是 | — | 开源、可微 | 2025.3 announce，未成熟 | Apache 2.0 |

### 2.2 benchmark 仿真任务套件

| Benchmark | 团队 | 任务数 | 数据规模 | 用途 |
|-----------|------|--------|---------|------|
| **CALVIN** | 弗莱堡大学 | 34 long-horizon | 24 小时演示 | 长 horizon 语言条件 |
| **LIBERO** | UT Austin | 130（4 套件 ×30 任务 + LIBERO-90/LIBERO-Long） | 大量演示 | VLA 标准评估 |
| **SimplerEnv** | Google + UCSD | 模拟 Google Robot + WidowX | — | 接近真机分布的仿真评估 |
| **RoboCasa** | UT Austin + NVIDIA | 365 任务，2,500+ 厨房场景，3,200+ 3D 物体 | 600+ 小时人类 + 1,600+ 小时机器人演示 | 大规模厨房日常任务 |
| **RoboCasa-GR1** | 同上 + GR1 humanoid | — | — | 人形版本 |
| **ManiSkill3** | UCSD / Hillbot | 20 任务族 | 4M+ 演示帧，2000+ 物体 | GPU 并行 RL/IL |
| **BEHAVIOR-1K** | Stanford | 1000 长 horizon 家庭任务 | — | 全场景 home robot |
| **RoboTwin 2.0** | 国内联合 | — | — | 国内双臂 benchmark |
| **VLABench** | 国内 ICCV 2025 | 长 horizon 语言条件 | 大规模 | 国内主推 |

### 2.3 Sim-to-Real Gap 现状

2026 年 sim-to-real 进展：
- **运动控制（locomotion）**：已基本解决——宇树 G1、特斯拉 Optimus、Boston Dynamics Atlas 都在 Isaac Lab/MuJoCo 训练后零样本部署
- **灵巧操作（manipulation）**：仍有显著 gap——主要痛点是接触动力学、可形变物体、视觉真实感
- **三种弥合手段**：(a) 域随机化（gold standard）；(b) Cosmos / Genie 类生成模型增强视觉真实感；(c) 仿真 + 少量真机 fine-tune（fewshot 50–500 demo）
- **银河通用 GraspVLA 案例**：纯仿真预训练（10 亿帧）+ 0 真机数据，在真机抓取上号称已经超过 π0、RT-2、OpenVLA、RDT——若属实，意味着仿真路线在抓取场景已经突破

---

## 3. 数据采集（核心瓶颈）

### 3.1 三种范式总结

| 范式 | 单条成本 | 数据质量 | 规模 | 代表 |
|------|---------|---------|------|------|
| 真机遥操作 | 高 ($5-50 / 条) | 高 (匹配本体) | 难突破百万 | ALOHA、Mobile ALOHA、AgiBot 数据工厂 |
| 人类视频 | 极低 (~$0.1/h) | 中 (有 embodiment gap) | 已达千万小时 | Ego4D, EgoVLA, Vid2Robot |
| 仿真合成 | 极低 (~$0.001/条) | 中-低 (sim-real gap) | 千亿+ 帧理论无上限 | GraspVLA, GR00T blueprint, Cosmos |

### 3.2 遥操作硬件

| 系统 | 团队 | 硬件成本 | 特点 |
|------|------|---------|------|
| **ALOHA** | Stanford (Tony Zhao) | ~$20k | 双臂主从遥操作 |
| **ALOHA 2** | Stanford / Google | 同级 | 改进版 |
| **Mobile ALOHA** | Stanford | **$32k** | 双臂 + 移动底盘 + 全身遥操作 |
| **UMI (Universal Manipulation Interface)** | Columbia (Cheng Chi) | **$2-3k** | 手持夹爪 + GoPro，无需机器人即可采数据 |
| **DexCap** | Stanford | ~$5k | 灵巧手 + 动捕 |
| **AnyTeleop** | NVIDIA | 软件方案 | 跨硬件遥操作 |
| **HumanPlus** | Stanford | — | 人形全身遥操作 |
| **AgileX Cobot Magic** | AgileX | ~$15k 商业版 | 商用 ALOHA 替代品 |
| **AgiBot Genie / 数据工厂** | 智元 | 工厂模式 | 4,000+㎡ 工厂，3,000+ 物品，5 大场景 |

**洞察**：ALOHA → UMI 数据采集成本下降 10×；2025 年开始进入"数据工厂"模式——智元自建 4,000 ㎡ 工厂、Tesla 投资遥操作工厂、特斯拉 / Figure 推出训练员制度。

### 3.3 人类视频学习

| 数据集 | 团队 | 规模 | 用途 |
|--------|------|------|------|
| **Ego4D** | Meta + 13 大学 | 3,670 小时 / 923 人 / 9 国 | 第一视角通用 |
| **Ego-Exo4D** | Meta | 1,422 小时 双视角同步 | 技能学习 |
| **Epic-Kitchens** | Bristol | 100 小时厨房 | 动作识别 |
| **EgoVLA** | NVIDIA + UT 等 | 500k image-action pairs | 人类视频 → 机器人转移 |
| **Vid2Robot** | Google | — | 视频条件机器人策略 |

**π0 团队论文 (2025-2026)**：随 VLA 模型规模增大，人类视频数据带来的提升越大——"Emergence of Human to Robot Transfer"。

### 3.4 大规模开源数据集

| 数据集 | 团队 | 规模 | 关键特征 |
|--------|------|------|----------|
| **Open X-Embodiment (OXE)** | DeepMind + 34 实验室 | 100 万 + 轨迹，22 embodiment，500 技能，150,000 任务 | 跨本体黄金数据集；60 个子数据集合并 |
| **DROID** | Stanford + Berkeley | 76k trajectories / 350 小时 / 564 场景 / 86 任务 / 52 建筑 | 多样性最强 |
| **AgiBot World (Alpha / Beta)** | 智元 | **100 万 +** 真机轨迹 / 217 任务 / 5 场景 / 100 机器人 | 国内最大；长程数据规模号称 10× OXE |
| **RH20T** | 上交 | 20+ TB / 110k+ 轨迹 / 147 任务 | 灵巧多任务 |
| **Bridge V2 / BridgeData** | Berkeley | 60k trajectories | OpenVLA 主力训练数据 |
| **RoboMIND** | 北大 + 国地中心 | 60k+ 轨迹 / 4 embodiment | 国内开源 |
| **AgileX 公开数据** | AgileX | 1万+ | 商业开源 |
| **LeRobot Community Datasets** | HF | 数百个社区数据集 | SmolVLA 训练源 |

### 3.5 数据 Scaling Law 现状

**Stanford 2024.10 (arXiv 2410.18647) "Data Scaling Laws in Imitation Learning for Robotic Manipulation"** 重要发现：

1. 真机演示策略的泛化性能与 **(环境数 × 物体数)** 呈幂律关系
2. **多样性 > 单环境演示数**：32 个环境 × 50 演示 → 90% 新物体新环境成功率
3. 单环境演示超过阈值后回报递减

**Physical Intelligence 2025.4 (π0.5 paper)** 进一步发现：随 VLA 模型规模增大，从人类视频与跨域数据中迁移的能力会"涌现"——这是 LLM 涌现规律在机器人上的初步验证。

**判断**：机器人领域"GPT-3 时刻"（即明确的 scaling law + emergent capability）已经初现端倪，但 100 万轨迹 ≪ 互联网级 token，预计 2027–2028 真正到来。

---

## 4. 训练算力

### 4.1 主流 VLA 训练成本估算

| 模型 | GPU | 时长 | 总 GPU-hour | 估算成本 (按 $2/H100-h) |
|------|-----|------|-------------|------------------------|
| OpenVLA 7B | 64 × A100 | 15 天 | ~23k | ~$50k |
| π0 3B | 未公开（估 ~256 × H100） | 数周 | ~50–200k | $100k–$400k |
| Helix (S2 7B + S1 80M) | 未公开 | — | 估 ~100k | ~$200k |
| GR00T N1 2B | 未公开（NVIDIA 内部 DGX cluster） | — | 估 ~50–200k | — |
| RT-2 55B | TPUv4 大规模 | — | >1M TPU-h | >$1M |
| Cosmos 14B | 10,000 + NVIDIA H100 | 数月 | >5M | >$10M |
| Genie 3 | 未公开 / DeepMind 规模 | — | 估 >10M | >$20M |

**结论**：VLA 训练成本目前仍比 LLM 低 10–100×。**真正贵的是世界模型 + 仿真预训练**。

### 4.2 中美算力差距对具身智能的影响

| 维度 | 美国 | 中国 |
|------|------|------|
| 可用最强 GPU | B200 / GB200 (Blackwell) | H20（推理优化弱化版）、H200（2025.12 部分放开，25% 关税） |
| 头部公司算力规模 | xAI 200k H100、OpenAI 数 10 万、Tesla Dojo + H100 数 10 万 | 字节、阿里、华为各 1-3 万张高端 GPU |
| 国产替代 | — | 华为昇腾 910B/910C、寒武纪 MLU、燧原 |
| 对具身智能影响 | 充足 | 中度受限：训练 7B–10B VLA 仍可，训练 100B+ 困难 |

**实际影响判断**：
1. **训练**：当前 VLA 主流 ≤7B，1024 张 H100 即可完成一轮训练，**短期国产具身公司算力够用**。
2. **世界模型 / 大规模仿真**：需要 1 万 + GPU，国内仅字节、华为、阿里、智元 + 大金主可承担——**这是结构性差距**。
3. **推理**：边缘端 GPU（NVIDIA Jetson Thor、Orin、华为昇腾 Atlas）已成关键，Jetson Thor 2026 出货是行业事件。
4. **应对策略**：中国具身公司高度依赖（a）仿真合成数据；（b）小模型 + 后训练（SmolVLA 思路）；（c）国产芯片适配。

### 4.3 出口管制时间线

- 2022.10：A100/H100 对华禁运
- 2023.10：H800/A800 也被禁，NVIDIA 推出"特供" H20
- 2024.4：H20 也面临限制讨论
- 2025.4：美国进一步限制
- **2025.12**：Trump 政府宣布允许 H200 对华出口，加 25% 关税；B100/B200/Blackwell 仍全面受限
- 2026.1：业内传闻 Rubin 系列将设阉割版

---

## 5. 关键论文里程碑年表（2022–2026）

| 时间 | 论文 / 模型 | 团队 | 关键贡献 | arXiv |
|------|-----------|------|----------|-------|
| 2022.4 | SayCan | Google | LLM + 机器人技能 grounding | 2204.01691 |
| 2022.12 | RT-1 | Google | 端到端 Transformer 操作 | 2212.06817 |
| 2023.3 | Diffusion Policy | Columbia/TRI/MIT | 扩散动作建模；+46.9% 平均 | 2303.04137 |
| 2023.5 | PaLM-E | Google | 562B 多模态具身模型 | 2303.03378 |
| 2023.7 | RT-2 | Google DeepMind | 互联网 VLM 直接做机器人策略 | 2307.15818 |
| 2023.10 | Open X-Embodiment / RT-X | 21 lab 联盟 | 跨 embodiment 大数据集 | 2310.08864 |
| 2023.10 | ALOHA / ACT | Stanford | 低成本双臂遥操作 | 2304.13705 |
| 2023.12 | Eureka (LLM-Reward) | NVIDIA | LLM 自动写 RL reward | 2310.12931 |
| 2024.1 | Mobile ALOHA | Stanford | 移动 + 双臂遥操作 | 2401.02117 |
| 2024.2 | UMI | Columbia | $2-3k 通用数据采集 | 2402.10329 |
| 2024.3 | DROID | Berkeley + 13 lab | 76k 多样性数据集 | 2403.12945 |
| 2024.5 | Octo | Berkeley | 开源通用机器人策略 | 2405.12213 |
| 2024.6 | OpenVLA | Stanford/Berkeley | 7B 开源 VLA | 2406.09246 |
| 2024.7 | GR-1 | 字节 | 视频生成预训练 → 机器人 | 2312.13139 |
| 2024.7 | RoboCasa | UT Austin / NVIDIA | 大规模厨房任务 sim | 2406.02523 |
| 2024.10 | π0 | Physical Intelligence | Flow-matching 通用机器人 | 2410.24164 |
| 2024.10 | ManiSkill3 | UCSD | GPU 并行 sim benchmark | 2410.00425 |
| 2024.10 | Data Scaling Laws | Stanford | 多样性 > 数量 | 2410.18647 |
| 2024.10 | RDT-1B | 清华 TSAIL | 1B Diffusion Transformer 双臂 | 2410.07864 |
| 2024.11 | CogACT | Microsoft | 解耦 VLM + Diffusion 动作 | 2411.19650 |
| 2024.12 | Genie 2 | DeepMind | 文本→可玩 3D 环境 | (blog) |
| 2024.12 | Genesis | MIT + 19 lab | 430,000× 实时仿真 | (blog) |
| 2025.1 | NVIDIA Cosmos WFM | NVIDIA | 物理世界基础模型 | 2501.03575 |
| 2025.1 | GraspVLA | 银河通用 Galbot | 10 亿帧合成预训练 | (blog) |
| 2025.2 | Helix | Figure AI | S1/S2 双系统人形 VLA | (blog) |
| 2025.2 | OpenVLA-OFT | Stanford | LIBERO 97.1% SOTA | 2502.19645 |
| 2025.3 | GR00T N1 | NVIDIA | 开源人形 foundation model | 2503.14734 |
| 2025.3 | 智元 AgiBot World + GO-1 | 智元 | 100 万真机 + ViLLA | (blog) |
| 2025.4 | π0.5 | Physical Intelligence | Open-world 泛化 | 2504.16054 |
| 2025.5 | SmolVLA | HF LeRobot | 450M 消费级 VLA | 2505.xxxxx |
| 2025.6 | V-JEPA 2 | Meta | 100 万小时视频世界模型 | 2506.09985 |
| 2025.7 | GR-3 + ByteMini | 字节 Seed | 形变物操作 70-80% | (blog) |
| 2025.7 | EgoVLA | NVIDIA + UT 等 | 人类视频 → 机器人 VLA | 2507.12440 |
| 2025.8 | Genie 3 | DeepMind | 实时交互世界 720p/24fps | (blog) |
| 2025.9 | Isaac Lab paper | NVIDIA | 多模态机器人学习框架 | 2511.04831 |
| 2025.11 | Helix 02 | Figure AI | 全身自主 | (blog) |
| 2025.11 | Cosmos 视频基础模型 | NVIDIA | 物理 AI 世界模拟 | 2511.00062 |
| 2025.12 | GR-RL | 字节 Seed | 首次 real-world RL for VLA | (blog) |
| 2025.12 | Cosmos-Predict 2.5 | NVIDIA | 2B/14B 统一世界模型 | (blog) |
| 2026.1 | Project Genie 商业化 | DeepMind | $250/月 AI Ultra | (blog) |
| 2026.4 | GEN-1 | Generalist AI | 99%+ 任务成功率，3× 加速 | (blog) |

---

## 6. 开源生态

### 6.1 LeRobot (HuggingFace)

- **GitHub Star**：23.9k+（2025.4），2026.5 估算 30k+
- **核心定位**：机器人的"Hugging Face Transformers"
- **核心资产**：(a) SmolVLA 450M；(b) 数百个社区数据集；(c) 与 Pollen Robotics 合作低成本硬件 SO-100/SO-101（<$500/臂）
- **重要事件**：2024.4 Hugging Face 收购 Pollen Robotics（推出 Reachy）

### 6.2 Open X-Embodiment 联盟

- 34 个全球研究机构、60 个数据集
- 主导方：Google DeepMind
- 影响：定义了"跨本体大数据集"标准，几乎所有开源 VLA 都基于此训练

### 6.3 Physical Intelligence π0 / openpi

- 2025.2 开源 π0 + π0-FAST 权重和代码
- 2025.4 发布 π0.5 论文
- 2025.9 PyTorch 支持上线 (openpi)
- 创始团队：Sergey Levine, Chelsea Finn, Karol Hausman 等 Stanford/Berkeley 大佬
- 估值：2024.11 完成 $400M B 轮，估值 $2.4B；传闻 2025 新一轮 $5–10B

### 6.4 中国开源力量

| 主体 | 开源资产 | 状态 |
|------|---------|------|
| **智元 (AgiBot)** | AgiBot World 100 万轨迹 + GO-1 模型（2025.9 全面开源） | 国内最完整开源 |
| **银河通用 (Galbot)** | GraspVLA（即将开源），仿真数据 pipeline | 仿真路线代表 |
| **字节 Seed** | GR-1 代码（GR-2/3/RL 闭源） | 部分开源 |
| **清华 TSAIL** | RDT-1B | 学术开源 |
| **北大 / 国地中心** | RoboMIND 数据集 | 数据开源 |
| **上交** | RH20T 数据集 | 数据开源 |
| **AgileX** | 部分数据集 + Cobot Magic 软件栈 | 商业开源 |

### 6.5 仿真器生态

| 项目 | 主导 | GitHub Star | 重要性 |
|------|------|------------|-------|
| Isaac Lab | NVIDIA | ~5k+ | 工业标准 |
| Genesis | 20 lab 联盟 | ~24k（首发即爆款） | 开源黑马 |
| ManiSkill | UCSD/Hillbot | 1.5k+ | 学术 RL 主力 |
| MuJoCo (MJX) | DeepMind | ~9k | 学术黄金 |
| Newton | NVIDIA+DM+Disney | TBD | 未来焦点 |

---

## 7. 关键洞察 10 条（PE 投资视角）

1. **VLA 路线已确立为产业共识**：S1/S2 双系统 + Flow-matching 动作建模 + VLM backbone 是 2025–2026 主流模式；端到端 vs 分层之争基本结束（端到端胜出）。**但 VLA 远未达"GPT 时刻"**——参数 ≤7B、训练数据 ≪ 互联网级、跨场景 zero-shot 仍不可靠。

2. **数据是结构性壁垒，且分化为三条护城河**：(a) 工厂级遥操作（智元、Tesla、Figure 都在自建数据工厂）；(b) 仿真合成（银河通用 10 亿帧 + NVIDIA Cosmos）；(c) 全网视频（Meta V-JEPA、π0 的 human transfer）。**纯靠开源数据 (OXE) 的玩家会被甩开。**

3. **仿真层的赢家是 NVIDIA + 开源黑马**：Isaac Lab + Cosmos + Newton 三件套形成垂直整合；Genesis 用 430,000× 速度撕开了开源缺口。**Mujoco、PyBullet、Gazebo 走向边缘化。**

4. **中美差距集中在世界模型与超大规模仿真**：训练 7B VLA 国内算力够用，训练 14B+ 世界模型（Cosmos、Genie 3）严重受限。**国内的破局点是仿真数据 pipeline 而非更大模型。**

5. **银河通用的"全仿真 + 0 真机"路线值得高度关注**：若真能在抓取/灵巧操作上跑通，等于绕过中国真机数据稀缺与算力管制双重瓶颈，是"中国式具身智能"的可能解。

6. **智元 AgiBot World 是中国版 ImageNet 时刻**：100 万 + 真机轨迹 + 4000 ㎡ 数据工厂 + 全面开源 GO-1，建立了国内第一个"数据 + 模型 + 硬件"完整闭环。**但商业化路径（C 端家庭服务）仍未跑通。**

7. **Figure / 1X / Skild AI 估值飙升说明西方资本认定"通用大脑"赢家通吃**：Figure Helix 02 全身自主 + Skild Brain $14B 估值（2026.1）+ Physical Intelligence 估 $5–10B。**通用大脑是软件型公司价值最大的层级，超过本体。**

8. **小模型 + 后训练（SmolVLA / OpenVLA-OFT 路线）正在打破"模型越大越好"假设**：450M SmolVLA 在 LIBERO 超过 ACT；OpenVLA-OFT 在 LIBERO 达 97.1% SOTA。**对中国公司利好，因为更适合算力受限场景。**

9. **世界模型（Cosmos / Genie / V-JEPA）将吃掉相当一部分真机数据需求**：当 Genie 3 能生成 720p/24fps 一致世界、V-JEPA 用 1 万倍人类视频做预训练时，"真机数据飞轮"的护城河会被削弱。**长期看，数据工厂模式可能不如想象的有护城河。**

10. **真正的 "Scaling Law 时刻"还需 2–3 年**：当前 OXE (100 万轨迹) 相当于 LLM 的 GPT-1 时代；预计 2027–2028 在数据量级（1 亿 + 轨迹 / 10 万 + 小时人类视频）+ 模型规模（30B+）双双突破后，会出现明确 emergent 行为。**这是 PE 应该 bet on 的中期窗口。**

---

## 8. 参考资料（精选）

- arXiv: 2310.08864 (OXE), 2406.09246 (OpenVLA), 2410.24164 (π0), 2503.14734 (GR00T N1), 2504.16054 (π0.5), 2506.09985 (V-JEPA 2), 2511.04831 (Isaac Lab), 2403.12945 (DROID), 2410.18647 (Data Scaling Laws), 2411.19650 (CogACT), 2401.02117 (Mobile ALOHA), 2303.04137 (Diffusion Policy)
- Figure: figure.ai/news/helix, figure.ai/news/helix-02
- Physical Intelligence: pi.website, github.com/Physical-Intelligence/openpi
- NVIDIA: blogs.nvidia.com/blog/cosmos-world-foundation-models, developer.nvidia.com/isaac/lab, research.nvidia.com (GR00T N1)
- DeepMind: deepmind.google/blog/genie-2, deepmind.google/blog/genie-3
- Meta: ai.meta.com/blog/v-jepa-2-world-model-benchmarks
- 智元: agibot-world.cn, zhiyuan-robot.com
- 银河通用: 腾讯新闻 20250111A02ZHL00, 新浪科技 ineenpiz5566961
- 字节 Seed: seed.bytedance.com/en/blog/seed-research-gr-rl-released, jiqizhixin.com (GR-2)
- LeRobot: huggingface.co/blog/smolvla, github.com/huggingface/lerobot
- Genesis: genesis-embodied-ai.github.io, github.com/Genesis-Embodied-AI/genesis-world
- ManiSkill: github.com/haosulab/ManiSkill
- RoboCasa: robocasa.ai
- DROID: droid-dataset.github.io
- 算力管制：tomshardware.com (H200 export saga, 2025.12), cfr.org (China AI chip deficit)

