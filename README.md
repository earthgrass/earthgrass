# 你好，我是张家昊 👋

**Computer Science Undergraduate @ Beijing University of Technology (BJUT)**

关注 AI 优化算法、结构化稀疏、时空预测与多智能体系统。

我希望将数学推导、可复现实验和软件工程结合起来：不仅提出研究假设，也明确验证条件、实验边界和当前尚未解决的问题。

[![GitHub](https://img.shields.io/badge/GitHub-earthgrass-181717?logo=github)](https://github.com/earthgrass)
[![Email](https://img.shields.io/badge/Email-champion041827%40163.com-blue?logo=maildotru)](mailto:champion041827@163.com)

---

## 👨‍💻 关于我 | About Me

目前就读于北京工业大学计算机科学与技术专业。我的主要工作方向包括：

- **AI 理论与优化**：Sharpness-Aware Minimization (SAM)、一般 N:M 结构化稀疏、Hessian 与曲率分析。
- **时空智能**：台风极端降水短临预测、多源气象数据融合、受控消融与事件级评估。
- **AI Agent**：多智能体金融研究、独立量化验证、证据追溯与工作流编排。
- **软件工程**：安全数据管线、图算法、后端服务、自动化测试与系统可靠性。

我重视可验证的结论，不将理论设想、实验计划或单次实验结果直接表述为已被充分证明的研究成果。

---

## 💼 实习经历 | Experience

### 金山云 · 网络安全开发实习生

**2026.07 – 2026.09**

参与企业网络安全数据处理与智能分析相关研发，工作涉及异构数据接入、数据标准化和安全事件分析。

- **数据接入与标准化**：参与设计 Syslog、API、Webhook 和文件等输入的数据处理流程，梳理 Parser、来源专属 Mapping 与统一数据结构之间的职责边界。
- **日志与告警处理**：围绕大规模安全数据开展字段清洗、时间窗口聚合、去重与结构化存储。
- **安全事件分析**：参与事件、证据与相关实体的关联分析，关注结果的可追溯性和结构化展示。
- **工程可靠性**：关注异常处理、数据一致性、字段缺失和离线验证。

**技术关键词：** `Python` `SQLite` `FastAPI` `REST API` `Data Pipelines` `Security Analytics`

> 企业项目涉及非公开业务数据，此处仅描述可公开的技术工作范围。

---

## 🔬 科研项目 | Research

### 01 · N:M + SAM：完整空间鲁棒目标下的结构化剪枝

**Post-Training N:M Structured Sparsity under Full-Space SAM Robust Geometry**

**研究状态：** 理论与算法研究进行中，核心评分方法尚待实验验证。

- [当前研究实现分支：research/rebuild-v1](https://github.com/earthgrass/N-M-SAM/tree/research/rebuild-v1)
- [历史实验归档分支](https://github.com/earthgrass/N-M-SAM/tree/%E5%88%9D%E7%89%88%E5%BE%85%E5%AE%8C%E5%96%84%E7%89%88%E6%9C%AC)

#### 研究问题

在稠密模型训练完成后，如何选择合法的一般 N:M 稀疏结构，使其尽可能保持完整参数空间 SAM 鲁棒目标下的低损失状态？

研究范围为一般 \(0<N<M\)，2:4 是初期实验实例，而不是理论适用范围的限制。

从完整空间 SAM 目标出发：

\[
F_\rho(W)=
\max_{\|\epsilon\|_2\leq\rho}L(W+\epsilon)
\]

给定稠密权重 \(W_0\)、合法 Mask \(m\) 和相应投影 \(P_m\)，研究目标为：

\[
m^*\in\arg\min_{m\in\mathcal M_{N:M}}
F_\rho(P_mW_0)
\]

#### 理论路线

1. **Global–Local–Cross 分解**

   将联合参数扰动引起的损失变化分解为组内局部增量和跨组交互项。

2. **匹配梯度探针**

   研究同一参考中心、匹配扰动下的 Global / Local 梯度差异，识别指定扰动方向上的跨组交互梯度。

3. **梯度与曲率联系**

   对可微损失，在固定状态下分析路径积分关系：

   \[
   g_2-g_1=
   \int_0^1 H(W+t\epsilon)\epsilon\,dt
   \]

4. **鲁棒代价代理**

   研究如何利用有限梯度与曲率观测估计候选 Mask 的鲁棒代价，并分析候选排序误差。

5. **两阶段实验**

   第一阶段进行不补偿的渐进式训练后剪枝；第二阶段固定最终 Mask，研究完整参数空间 SAM 目标下的鲁棒恢复。

这些数学关系为研究提供分析工具，但不意味着已恢复完整 Hessian、得到理论最优 Mask，或证明新方法优于现有基线。

#### 当前实现与实验状态

- 已有本地 Dense-SAM checkpoint：200 epochs，`global_step=78,200`。模型权重未随公开仓库归档。
- 新研究分支已实现 SAM 基础训练组件、N:M 布局、合法 Mask 检查、候选枚举和结构位移 \(q\) 等基础模块。
- 该分支的验证记录为 **57 项测试通过**，包含 CPU toy 实验；尚未完成 CUDA 验证、CIFAR 正式训练和完整的鲁棒评分算法。
- 旧分支归档了六组单随机种子的 200-epoch CIFAR-10 / ResNet18 实验。这些属于历史训练时稀疏实验，不能作为当前 V0.3 训练后剪枝方法有效性的证据。

#### 下一阶段实验计划

1. 从同一稠密 checkpoint 出发，比较一次性剪枝与按 `layer1–layer4` 分批执行的渐进式剪枝。
2. 对照 `Magnitude`、`Taylor-g1`、`Taylor-g2` 和梯度差相关评分。
3. 第一轮固定为不补偿的结构选择实验。
4. 第二轮固定最终 Mask，比较不补偿、最终阶段恢复和逐批恢复。
5. 统一评价准确率、鲁棒损失、Mask 合法性和计算成本。

以上为待执行与验证的实验方案，不代表新方法已获得性能提升。

---

### 02 · GeoAI：台风极端降水短临预测

**Tropical-Cyclone Precipitation Nowcasting via Controlled Ablation**

**研究状态：** 受控消融实验已冻结，后续以结果核验和论文分析为主。

[GeoAI Repository](https://github.com/earthgrass/Geo_AI)

研究面向台风降水的 30 分钟短临预测，采用固定的 Residual ConvLSTM 主干，研究输入信息与训练目标对预测结果的边际影响。

- **多源数据**：GPM IMERG 降水、CMA 台风路径与强度、ETOPO1 地形。
- **输入信息消融**：比较降水基线、气旋状态、静态地形及地形梯度等输入。
- **损失函数消融**：比较基础 MSE、平滑正则和极端降水加权等设置。
- **评估规范**：采用事件级划分、测试集隔离与事件级统计分析。

当前项目记录包括冻结的 TEST A/B 实验、各 3 个随机种子、主实验与敏感性设置，以及 2,000 次 bootstrap 分析。主实验与敏感性设置分别涉及 707 和 696 个测试窗口。

仓库 README 记录的验证测试为 69/69 通过。

**研究边界：** 项目的重点是可复现的受控实证分析，而不是提出全新的预测架构。平滑正则或极端降水加权不能直接等同于物理方程约束，也不据此宣称 SOTA。

---

### 03 · 动态多目标进化优化 | DMOEA

**Dynamic Multi-Objective Evolutionary Optimization**

**研究状态：** 算法原型与实验验证阶段。

[Repository: LSTM_DMOEA_earthgrass](https://github.com/earthgrass/LSTM_DMOEA_earthgrass)

项目围绕动态多目标优化中的历史状态利用、时序预测和搜索策略调整开展探索。

目前公开代码仍以早期时序建模、历史检索及相关原型为主。新版预测与自适应路由方案仍需进一步实现和验证。

在可复现的正式基准实验和结果归档完成之前，不宣称残差 LSTM、曲率驱动三态路由或 CEC / PlatEMO 指标已经取得优于现有方法的结果。

---

## 🤖 AI Agent 与软件系统 | Engineering

### 04 · FinAgent-X：多智能体金融研究系统

**Multi-Agent Financial Research and Verification System**

[Repository: AI-finance-agent](https://github.com/earthgrass/AI-finance-agent)

面向金融研究任务，构建研究、量化验证、观点质疑、证据仲裁和报告生成的协作工作流。

#### 核心模块

- `QueryInterpreter` / `Planner`：解析研究需求并规划执行路径。
- `Research` / `Quant`：整理研究证据，并使用 Python 和金融数据独立验证定量结论。
- `Critic` / `Committee`：检查结论、组织不同观点并进行证据仲裁。
- `Report` / `MemoryWriter`：生成结构化报告并管理研究上下文。

#### 工程进展

当前本地开发版本为 V2.0.1，已实现动态路由、迭代 Critic、Replanner、Stop、Committee、Memory 和 `as_of` 时间约束等功能。

**验证状态：** 当前开发快照的端到端测试为 12/12 通过；运行时回归测试为 12 项通过。回归测试使用模拟叶子 Agent，但保留真实工作流拓扑和 Supervisor 路由检查。

公开仓库主要展示系统架构和使用方法；本地开发版本的验证记录不应被误认为全部已同步至公开分支。

**技术关键词：** `Python` `LLM Agents` `FastAPI` `React` `Quantitative Analysis` `Evidence Traceability`

系统用于研究辅助，不提供收益保证，也不将模型生成结论视为未经核验的投资事实。

---

### 05 · LogiRoute：单车物流路径规划系统

**Handwritten Graph Algorithms and Logistics Simulation**

[Repository: Data-structure-project](https://github.com/earthgrass/Data-structure-project) · [Phase 2 PR #1](https://github.com/earthgrass/Data-structure-project/pull/1)

数据结构课程设计项目，按照课程要求采用**单车配送**约束，围绕有向带权图实现物流路径规划。

- 使用邻接表作为主要图存储结构，支持邻接矩阵导出。
- 手写 MinHeap 和 Dijkstra，避免调用第三方图算法库。
- 将场景和业务参数放在配置文件中，便于固定场景测试与后续扩展。
- 通过独立测试验证数据结构、路径计算与边界条件。

Phase 2 的实现和测试位于待合并的 PR 分支，当前 PR #1 仍为 Open。该分支此前的验证记录为 224/224 测试通过；不应将其表述为已经合并到主分支的功能。

---

### 06 · 棒球队管理系统

**Full-Stack Baseball Team Management System**

[Repository: bjut-baseball-system](https://github.com/earthgrass/bjut-baseball-system) · [Demo](https://bjut-baseball-system.onrender.com)

独立开发的棒球队数据管理系统，将实际训练与比赛管理需求转化为软件功能。

- 球员档案、比赛记录、对局查询与统计分析。
- 打击、投球等数据的汇总与可视化。
- 比赛 PDF 解析、数据导入与 CSV 导出。
- 基于 Flask、SQLAlchemy 与 SQLite 的后端实现，支持 Docker 部署。

**技术关键词：** `Flask` `SQLAlchemy` `SQLite` `REST API` `Data Visualization`

---

## 🛠 技术栈 | Tech Stack

| 方向 | 技术与方法 |
|---|---|
| 编程语言 | Python · C · Java · MATLAB · JavaScript / TypeScript · SQL |
| 深度学习 | PyTorch · CNN / ResNet · LSTM / ConvLSTM · SAM |
| 数学与优化 | N:M Sparsity · Hessian / Curvature Analysis · Robust Optimization · Evolutionary Optimization |
| 数据处理 | NumPy · Pandas · SQLite · Structured Data Pipelines |
| AI Agent | LLM APIs · Tool Calling · Multi-Agent Workflows · Evidence-Based Verification |
| 后端与前端 | FastAPI · Flask · React · REST API · WebSocket |
| 工程实践 | Git / GitHub · Linux · Docker · Pytest · Unittest · Automated Regression Testing |

---

## 🔭 近期研究与工程重点

- **N:M + SAM**：探索有限 Global–Local 梯度探测到结构代价代理的映射，并验证候选保序与固定结构鲁棒恢复。
- **GeoAI**：推进冻结实验的结果核验、事件级统计分析与论文整理。
- **DMOEA**：完善算法原型、正式基准对比与消融分析。
- **FinAgent-X**：强化独立量化验证、多智能体协作、异常处理与证据可追溯性。
- **系统工程**：持续改进数据管线、图算法、自动化测试与项目文档。

---

## 🏆 经历与荣誉 | Highlights

- 🥇 北京高校数学建模校际联赛一等奖。
- ⚾ 中国国家二级棒球运动员。
- 🏆 带领校队获得首都高校棒球锦标赛冠军。
- 📄 独立完成 MCM 全英文数学建模论文。
- 👥 担任行政班长，参与团队组织与项目统筹。

---

## 📊 GitHub Stats

<div align="center">

<img height="165" src="https://github-readme-stats.vercel.app/api?username=earthgrass&show_icons=true&hide_border=true&include_all_commits=true&theme=transparent&locale=cn" alt="GitHub Stats" />

<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=earthgrass&layout=compact&hide_border=true&theme=transparent&locale=cn" alt="Top Languages" />

</div>

---

## 📫 联系我 | Contact

- **GitHub：** [github.com/earthgrass](https://github.com/earthgrass)
- **Email：** [champion041827@163.com](mailto:champion041827@163.com)

> From mathematical ideas to reproducible experiments, and from prototypes to working systems.

*Project status snapshot: 2026-10-17. Completed implementation, historical experiments, and planned research are described separately.*
