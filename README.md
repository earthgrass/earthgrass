
<div align="center">

# 你好，我是张家昊 👋

### Computer Science Undergraduate @ Beijing University of Technology (BJUT)

**Robust Optimization · GeoAI · Multi-Agent Systems · Security Engineering**

以数学推导探索智能优化算法，也致力于将 AI 系统真正构建、验证并部署出来。

[![GitHub](https://img.shields.io/badge/GitHub-earthgrass-181717?logo=github)](https://github.com/earthgrass)
[![Email](https://img.shields.io/badge/Email-champion041827%40163.com-blue?logo=maildotru)](mailto:champion041827@163.com)
[![Research](https://img.shields.io/badge/Focus-AI%20Research%20%26%20Engineering-4C6EF5)](https://github.com/earthgrass?tab=repositories)

</div>

---

## 👨‍💻 关于我 | About Me

我就读于 **北京工业大学计算机科学与技术专业**。目前的学习与项目围绕三条主线展开：

- **AI 理论与优化**：Sharpness-Aware Minimization（SAM）、一般 N:M 结构化稀疏、Hessian / 曲率几何、动态多目标进化优化。
- **时空智能与 AI for Science**：台风极端降水短临预测、ConvLSTM、气象与地形多源数据融合、可复现的受控消融实验。
- **AI Agent 与系统工程**：多智能体金融研究、企业安全数据管线、证据关联分析、后端服务与复杂系统可靠性。

我的目标是把 **可解释的数学研究、可复现的实验，以及可交付的软件工程** 连接起来。

---

## 💼 实习经历 | Experience

### 金山云 · 网络安全开发实习生

**Beijing Kingsoft Cloud Network Technology Co., Ltd. | 2026.07 – 2026.09**

参与企业安全数据处理与智能分析相关研发，工作覆盖异构数据接入、资产状态建模和安全事件分析平台。

- **多来源数据处理**：围绕 Syslog、API、Webhook 和文件输入设计接入与标准化流程，将原始数据留存、Parser 解析、来源专属 Mapping 和统一结构输出分层解耦。
- **资产去重与状态建模**：针对大规模主机资产上报数据，区分完全重复记录、资产状态变化和当前快照，构建内容去重与版本化处理逻辑。
- **安全事件证据关联**：参与安全事件事实层和多维关联分析系统，围绕事件、证据、实体、主机、行为及攻击模式建立可追溯的结构化展示与关联视图。
- **可靠性与可验证性**：关注异常隔离、字段缺失的如实呈现、数据一致性与离线测试，支持分析结果的结构化导出。

`Python` `FastAPI` `SQLite` `Data Pipelines` `Syslog` `REST API` `Security Analytics` `React`

> 企业实习项目涉及非公开业务数据与代码，这里仅展示可公开的技术工作概述。

---

## 🔬 科研项目 | Research

### 01 · 一般 N:M 结构化稀疏中的 SAM 鲁棒几何保持

**Post-Training N:M Structured Sparsity through Global–Local SAM Robust Geometry**  
**独立理论推导与算法研究 · 进行中**

[![Repository](https://img.shields.io/badge/Repository-N--M--SAM-181717?logo=github)](https://github.com/earthgrass/N-M-SAM)
[![Status](https://img.shields.io/badge/Status-Research%20in%20Progress-orange)](https://github.com/earthgrass/N-M-SAM)

研究的问题是：**在完成稠密模型训练后，如何选择合法的 N:M 稀疏结构，并尽可能保留完整参数空间 SAM 目标下的低鲁棒损失状态？**

与仅依据参数幅值选取 Mask 的方法不同，我正在研究**全局扰动、组内局部响应与跨组曲率耦合**如何共同影响结构选择。理论不预先固定为 2:4；2:4 是可执行的实验实例。

**理论路线**

1. **完整空间 SAM 参考目标**：从 $F_\rho(W)=\max_{\|\epsilon\|_2\leq\rho}L(W+\epsilon)$ 出发，定义低鲁棒损失的连续 Ideal，而不是直接用权重欧氏距离或剪枝后的 Hessian 相似度作为终极目标。
2. **Global = Local + Cross**：将一次联合参数扰动引起的全网络损失变化，精确分解为组内损失增量与跨组交互项；所有组共享同一个全局扰动预算。
3. **梯度响应与曲率联系**：由 $g_2-g_1=\int_0^1 H(W+t\epsilon)\epsilon\,dt$ 分析沿扰动方向的 Hessian 响应；进一步通过**匹配的** Global / Local 探针，识别跨组交互对各组扰动的梯度。
4. **鲁棒几何匹配与保序结构选择**：研究从有限梯度与曲率观测构造候选 Mask 代价代理，在可控误差条件下尽可能保持候选结构对完整 SAM 鲁棒目标的排序。
5. **两阶段实施**：**Part 1** 在不补偿保留权重的前提下，渐进式选择一般 N:M Mask；**Part 2** 固定最终 Mask，只更新保留权重，进行完整空间 SAM 目标下的有限步鲁棒恢复。

<details>
<summary><b>核心数学关系（点击展开）</b></summary>

给定稠密 checkpoint $W_0$、合法结构集合 $\mathcal M_{N:M}$ 和相应投影 $P_m$：

$$
F_\rho(W)=\max_{\|\epsilon\|_2\le\rho}L(W+\epsilon),\qquad
m^*\in\arg\min_{m\in\mathcal M_{N:M}}F_\rho(P_mW_0).
$$

定义每组的局部损失增量 $\phi_b(W,\epsilon_b)=L(W+E_b\epsilon_b)-L(W)$，则跨组交互为：

$$
I_{\mathrm{cross}}(W,\epsilon)
=L(W+\epsilon)-L(W)-\sum_b\phi_b(W,\epsilon_b).
$$

当 Global 与 Local 在**同一参考中心、同一组内扰动分量**下进行匹配探测时，有严格恒等式：

$$
C_b(W,\epsilon)
=\nabla_b L(W+\epsilon)-\nabla_b L(W+E_b\epsilon_b)
=\nabla_{\epsilon_b}I_{\mathrm{cross}}(W,\epsilon).
$$

该恒等式识别的是指定扰动方向上的交互梯度，**并不意味着单次探测已恢复完整 Hessian，也不直接给出最优 Mask 分数**。

结构选择后的恢复仍以同一个完整参数空间 $F_\rho$ 为目标，SAM 的虚拟扰动不因永久稀疏 Mask 而自动限制到保留支撑。

</details>

**当前进展与边界**：

已经整理 Global–Local 交互的数学恒等关系、路径积分表达、局部二阶近似与条件性保序分析；已有 CIFAR-10 / ResNet18 / 2:4 稀疏的 200-epoch GPU 基线实验。

**如何以有限、低成本的探测构造足够准确的结构评分，仍是研究中的核心问题，尚未宣称获得理论最优剪枝算法。**

**关键词**：`SAM` `N:M Sparsity` `Hessian` `Cross-Group Interaction` `Robust Optimization` `Post-Training Pruning`

[查看研究代码与实验归档 →](https://github.com/earthgrass/N-M-SAM)

---

### 02 · GeoAI：台风极端降水短临预测与受控消融

**Tropical-Cyclone Precipitation Nowcasting · Spatiotemporal Modeling**  
**北京高校数学建模校际联赛一等奖相关项目 · 持续研究**

[![Repository](https://img.shields.io/badge/Repository-Geo__AI-181717?logo=github)](https://github.com/earthgrass/Geo_AI)

面向台风极端降水的 **30 分钟短临预测**，研究气旋状态、地形信息和训练目标设计对时空模型表现的实际贡献。

- **多源气象数据处理**：整合 GPM IMERG 降水、CMA 台风路径与强度、ETOPO1 地形数据，构建时间与空间对齐的数据管线。
- **时空预测模型**：以 ConvLSTM / Residual ConvLSTM 为模型基础，研究降水场演化与多源输入建模。
- **双轴受控消融**：分别检验气旋状态、静态地形、地形梯度等输入信息，以及平滑约束、极端降水加权损失的边际作用。
- **实验可信度**：强调事件级划分、训练集统计量归一化、测试集隔离、验证集选择以及事件级统计分析，避免数据泄漏与过度结论。

**研究定位**：当前重点是提供可复现的实证分析，**不把平滑损失直接表述为物理方程约束，也不提前宣称新网络架构或 SOTA 结果**。

**关键词**：`GeoAI` `ConvLSTM` `Spatiotemporal Forecasting` `GPM IMERG` `CMA` `Ablation Study`

[查看代码、实验协议与研究进展 →](https://github.com/earthgrass/Geo_AI)

---

### 03 · 动态多目标进化优化：残差 LSTM 与自适应搜索

**Dynamic Multi-Objective Evolutionary Optimization**  
**核心算法设计与实验研究**

- 针对非平稳环境中的预测失效与搜索方向偏移，设计基于**线性外推残差的 LSTM 预测机制**。
- 探索**曲率驱动的三态自适应路由**，在不同环境状态下调整搜索与种群初始化策略。
- 引入连续预测误差监测与熔断逻辑，降低错误外推对后续进化过程的干扰。
- 基于 CEC 动态多目标基准与 PlatEMO，围绕 MIGD、MHV 等指标开展对比和消融实验。

`LSTM` `DMOEA` `Evolutionary Computation` `PlatEMO` `Pareto Optimization`

[查看项目仓库 →](https://github.com/earthgrass/LSTM_DMOEA_earthgrass)

---

## 🤖 AI Agent 与软件系统 | Engineering

### 04 · 金融 AI：证据驱动的多智能体投研委员会

**Multi-Agent Financial Research System · 北大金融 AI 训练营延伸项目**

[![Repository](https://img.shields.io/badge/Repository-AI--finance--agent-181717?logo=github)](https://github.com/earthgrass/AI-finance-agent)

面向金融研究任务，设计由多个专职智能体协作的分析系统，重点解决**研究结论能否被验证、质疑与追溯**的问题。

- **监督与编排**：Supervisor 分解研究问题，组织 Research、Quant、Committee 和 Report 等模块的依赖与执行。
- **独立量化验证**：对研究假设引入 Python 与真实金融数据计算，而不是仅依赖 LLM 自述。
- **双视角辩论与证据仲裁**：积极与谨慎观点共享事实底座，在风险、估值和不确定性层面进行对照，由仲裁模块形成综合研判。
- **可追溯报告**：输出结构化研报，关联假设、定量分析、证据来源与时间信息；支持 A 股公司研究、公司比较和已配置主题研究。
- **系统工程**：构建 Web 前端、API、流程编排、运行状态管理与持久化层，并使用离线回归测试强化异常路径。

`Python` `LLM Agents` `Multi-Agent Orchestration` `Quantitative Analysis` `FastAPI` `React` `Evidence Traceability`

[查看多智能体架构与源代码 →](https://github.com/earthgrass/AI-finance-agent)

---

### 05 · 北京工业大学棒球队管理系统

**Full-Stack Development · Containerized Deployment**

[![Repository](https://img.shields.io/badge/Repository-bjut--baseball--system-181717?logo=github)](https://github.com/earthgrass/bjut-baseball-system)
[![Demo](https://img.shields.io/badge/Online%20Demo-Visit-2F9E44)](https://bjut-baseball-system.onrender.com)

独立开发面向高校棒球队的数据管理系统，将自己的运动需求转化为实际软件项目。

- 实现球员档案、比赛记录、打击与投球统计、对局查询和数据可视化。
- 构建 Flask / SQLAlchemy / SQLite 后端及 RESTful API，支持比赛 PDF 解析、数据导入与 CSV 导出。
- 完成 Docker 容器化与公网部署，并持续优化移动端交互、数据一致性和工程文档。

`Flask` `SQLAlchemy` `SQLite` `Docker` `REST API` `Data Visualization`

🌐 [在线体验](https://bjut-baseball-system.onrender.com) · [源代码](https://github.com/earthgrass/bjut-baseball-system)

---

### 06 · 多模态数字人系统：流式通信与异常链路优化

**LLM + TTS + Real-Time Interaction · 研发实践**

参与流式数字人交互系统的稳定性优化，排查外部语音 API 异常、线程退出、前端状态机阻塞和 WebSocket 连接故障；通过异常捕获、兜底策略和状态清理改进故障场景下的系统表现。

`WebSocket` `Concurrency` `State Machine` `Error Handling` `Real-Time Systems`

---

## 🛠 技术栈 | Tech Stack

| 方向 | 技术与方法 |
| --- | --- |
| **语言** | Python · MATLAB · C · Java · JavaScript / TypeScript · SQL |
| **深度学习与数学优化** | PyTorch · LSTM · ConvLSTM · SAM · Hessian / Curvature Analysis · N:M Sparsity · Evolutionary Optimization |
| **科研与数据分析** | NumPy · Pandas · scikit-learn · SHAP · PlatEMO · Experimental Design · Statistical Evaluation |
| **AI Agent** | LLM API · Multi-Agent Workflows · Tool Calling · MCP · Evidence-Based Reasoning |
| **后端与前端** | Flask · FastAPI · SQLite · RESTful API · WebSocket · React |
| **工程实践** | Git / GitHub · Linux · Docker · Pytest · CI/CD · Automated Testing · Claude Code · Codex |

---

## 🔭 近期研究与工程重点

- **N:M + SAM**：探索有限 Global–Local 梯度探测到结构代价代理的映射，并验证候选保序与固定结构鲁棒恢复。
- **GeoAI**：推进双轴受控消融、事件级统计分析和完整实验复现。
- **动态优化**：完善 DMOEA 算法的稳定性测试、对比基线与消融分析。
- **金融 Agent**：强化独立量化验证、多智能体协作、异常处理与证据可追溯性。

---

## 🏆 经历与荣誉

- 🥇 **2026 年北京高校数学建模校际联赛一等奖**
- ⚾ **带领校队获得首都高校棒球锦标赛冠军**
- 📄 独立完成 MCM 全英文数学建模论文
- 👥 担任行政班长，参与团队组织与项目统筹

---

## 📊 GitHub 数据

<div align="center">

<img height="165" src="https://github-readme-stats.vercel.app/api?username=earthgrass&show_icons=true&hide_border=true&include_all_commits=true&theme=transparent&locale=cn" alt="GitHub Stats" />
<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=earthgrass&layout=compact&hide_border=true&theme=transparent&locale=cn" alt="Top Languages" />

</div>

---

## 📫 联系我 | Contact

**GitHub**：[github.com/earthgrass](https://github.com/earthgrass) · **Email**：[champion041827@163.com](mailto:champion041827@163.com)

> From mathematical ideas to reproducible experiments, and from prototypes to working systems.
