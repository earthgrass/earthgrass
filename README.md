<div align="center">

# 你好，我是张家昊 👋

### Computer Science Undergraduate @ BJUT

**AI Engineering · Intelligent Optimization · Backend Systems**

[![GitHub](https://img.shields.io/badge/GitHub-earthgrass-181717?logo=github)](https://github.com/earthgrass)
[![Email](https://img.shields.io/badge/Email-champion041827%40163.com-blue?logo=maildotru)](mailto:champion041827@163.com)

</div>

---

## 👨‍💻 关于我

我目前就读于 **北京工业大学计算机科学与技术专业**，主要关注：

- 动态多目标优化与进化计算
- LSTM、ConvLSTM 与时空序列建模
- 物理约束神经网络与多模态数据融合
- 大语言模型应用与 AI Agent 工程
- 后端系统、数据流水线与复杂系统排障

我希望将算法研究转化为能够实际运行的工程系统。目前正在持续完善智能优化算法、AI 应用系统和后端工程项目。

---

## 🛠 技术栈

### 编程语言

`Python` · `MATLAB` · `C` · `Java` · `HTML/CSS`

### AI 与算法

`LSTM` · `ConvLSTM` · `PINN` · `DMOEA` · `NES`  
`时间序列预测` · `多目标优化` · `SHAP` · `LLM 应用`

### 后端与数据

`Flask` · `SQLite` · `RESTful API` · `WebSocket`  
`Pandas` · `数据清洗` · `日志处理` · `自动化流水线`

### 工程工具

`Docker` · `Linux` · `Git/GitHub` · `Render` · `CI/CD`  
`Claude Code` · `Codex` · `DeepSeek API`

---

## 🚀 精选项目

### 1. 基于残差 LSTM 与三态自适应路由的动态多目标进化算法

**项目负责人 / 核心算法研发**

针对动态多目标优化环境中的非平稳变化、预测失效与断裂面陷阱问题，构建预测引导的动态进化优化框架。

- 使用增量训练的 LSTM 预测线性外推残差，提高环境变化趋势预测能力。
- 提出曲率驱动的三态自适应路由策略，在不同环境状态下动态切换搜索模式。
- 设计连续误差熔断机制，减少错误预测对种群初始化的干扰。
- 在 CEC 2015 动态多目标测试集和 PlatEMO 验证流程下，MIGD、MHV 指标优于多种对比算法。

**关键词：** `DMOEA` `LSTM` `PlatEMO` `Pareto Optimization` `Time-Series Prediction`

<!-- 整理仓库后将 YOUR_REPO_NAME 替换为真实仓库名 -->
[查看项目仓库](https://github.com/earthgrass/YOUR_REPO_NAME)

---

### 2. 数据与物理双驱动的台风极端降水 PINN-ConvLSTM 模型

**北京高校数学建模校际联赛一等奖｜全流程项目研发**

面向台风极端降水预测问题，构建融合气象数据、地形信息和物理先验的时空推演模型。

- 同化处理 CMA 台风数据、ERA5 再分析数据与高程数据。
- 使用随机森林与 SHAP 分析不同动力学参数对极端降水的非线性影响。
- 构建 Res-ConvLSTM 网络，提取降水场的时空演化特征。
- 引入高程生成的物理先验场，并通过残差学习缓解模型冷启动问题。
- 负责数据处理、模型设计、实验验证与工程流水线搭建。

**关键词：** `PINN` `ConvLSTM` `ERA5` `SHAP` `Spatiotemporal Forecasting`

<!-- 整理仓库后将 YOUR_REPO_NAME 替换为真实仓库名 -->
[查看项目仓库](https://github.com/earthgrass/YOUR_REPO_NAME)

---

### 3. 北工大棒球队管理系统

**全栈开发 / 独立部署**

面向高校棒球队日常管理、训练数据记录与比赛分析需求，独立开发并部署球队管理系统。

- 使用 Flask 与 SQLite 构建后端和数据持久化模块。
- 采用面向对象方法设计球员、训练、比赛与统计分析实体。
- 通过 Docker 与 Render 完成公网部署和持续交付。
- 接入 DeepSeek API，对非结构化训练记录进行语义解析。
- 使用 AI 编程工具辅助完成数据清洗、功能开发与测试流程。

**技术栈：** `Flask` `SQLite` `Docker` `Render` `DeepSeek API`

🌐 [访问在线系统](https://bjut-baseball-system.onrender.com)

<!-- 整理仓库后将 YOUR_REPO_NAME 替换为真实仓库名 -->
[查看项目仓库](https://github.com/earthgrass/YOUR_REPO_NAME)

---

### 4. 多模态数字人智能体系统架构优化

**研发实习经历**

参与基于 LLM、TTS 与视觉动作驱动的流式数字人交互系统开发，主要负责并发通信与异常链路排查。

- 定位外部语音 API 风控导致的底层子线程异常退出问题。
- 修复前端状态机死锁、收音阻塞和通信链路无法释放等故障。
- 增加异常捕获、空帧兜底和 WebSocket 跌落休眠机制。
- 提高网络异常和外部 API 不稳定场景下的系统鲁棒性。

**关键词：** `LLM` `WebSocket` `Concurrency` `State Machine` `Defensive Programming`

---

## 🔭 当前正在做

- 完善动态多目标进化算法的实验与消融分析。
- 优化大规模安全日志的标准化、去重和状态建模流程。
- 完善前后端项目的测试、部署、监控与工程文档。
- 探索 Codex、Claude Code 与 MCP 驱动的多 Agent 协作开发系统。

---

## 🏆 经历与荣誉

- 🥇 **2026 年北京高校数学建模校际联赛一等奖**
- ⚾ 带领校队获得 **首都高校棒球锦标赛冠军**
- 📄 独立完成 MCM 全英文建模论文
- 👥 担任行政班长，具有团队组织与多任务统筹经验

---

## 📊 GitHub 数据

<div align="center">

<img height="165" src="https://github-readme-stats.vercel.app/api?username=earthgrass&show_icons=true&hide_border=true&include_all_commits=true&theme=transparent&locale=cn" alt="GitHub Stats" />

<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=earthgrass&layout=compact&hide_border=true&theme=transparent&locale=cn" alt="Top Languages" />

</div>

---

## 📫 联系我

- **GitHub：** [github.com/earthgrass](https://github.com/earthgrass)
- **Email：** [champion041827@163.com](mailto:champion041827@163.com)

> 持续学习，持续构建，把算法真正变成能够解决问题的系统。
