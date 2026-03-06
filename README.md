# Hi there, I'm 张家昊 (earthgrass) 👋

🎓 **Computer Science & Technology | Algorithm & Backend Optimization**

目前就读于北京工业大学计算机科学与技术专业，具备“深度学习+运筹优化”的复合视野。热衷于解决不可导排序优化与多目标平衡问题，并兼具全栈工程落地与底层系统排障能力。同时，我也在积极备战蓝桥杯（Python 组）并筹备前往香港科技大学深造。

## 🛠 Tech Stack

* **Languages:** Python, MATLAB, C, Java
* **AI & Algorithms:** Evolution Strategy (ES), Multi-Objective Optimization, LSTM, Pipeline Architecture
* **Data & Tools:** Data Cleaning, Pandas, Git, LaTeX, WebSocket

## 🚀 Featured Projects & Research

### 1. 基于进化策略的推荐系统多目标重排与偏差消除框架
* **Role:** 核心算法设计 (2026.01 - 2026.02)
* **Key Contributions:**
    * **偏差消除：** 针对流行度偏差，利用 Pandas 完成数据清洗，设计 Deep Rank-Inverse 网络解耦用户偏好与内容质量。
    * **排序优化 (NES)：** 针对 Top-K 截断不可导难题，摒弃 Point-wise 回归，自主实现自然进化策略 (NES) 替代梯度下降，直接在离散排序空间寻优。
    * **多目标决策：** 利用 DMOEA 求解帕累托前沿，确定最优干预阈值 (k=0.85)，在仅牺牲 2% 头部收益的情况下，提升了 32% 的长尾优质内容生存率。

### 2. 基于 LSTM 的动态多目标进化算法研究
* **Role:** 项目负责人 (2025.09 - 至今)
* **Key Contributions:**
    * 构建基于 LSTM 的时间序列预测模块以预测帕累托最优集的变化趋势。
    * 设计预测引导的种群初始化策略显著减少搜索盲区。
    * 在 Python/MATLAB 仿真环境中验证了该算法在响应突变环境时收敛代数明显缩短。

### 3. 多模态数字人智能体系统 (OpenAvatar Chat)
* **Role:** 研发实习生 (2025.09 - 至今)
* **Description:** 参与构建基于大语言模型(LLM)、文本转语音(TTS)与视觉动作驱动(Vision)的流式并发数字人交互系统。
* **Key Contributions:**
    * **通信死锁排查：** 剖析并解决因外部语音 API 严格风控引发的底层子线程静默崩溃，修复前端状态机死锁与收音阻塞等级联故障。
    * **防御性编程：** 针对不稳定网络，设计异常捕获、兜底空帧注入及 WebSocket 跌落休眠机制，在极端异常下强制释放前端系统锁，大幅提升流式特征传输鲁棒性。

## 🏅 Beyond Coding

* 习惯高强度竞技环境，曾带领校队斩获首都高校棒球锦标赛冠军。这种在压力下的决策能力与团队协作精神，同样被我应用在复杂系统的底层排障与硬核科研开发中。
* 具备优秀的英文文献阅读与学术写作能力，曾独立完成 MCM 全英论文。

## 📊 GitHub Stats

<div align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=earthgrass&show_icons=true&theme=transparent&hide_border=true&title_color=black&text_color=333" alt="earthgrass's GitHub Stats" />
  <br/>
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=earthgrass&layout=compact&theme=transparent&hide_border=true&title_color=black&text_color=333" alt="Top Languages" />
</div>

📫 **Reach out to me:** 041827@163.com
