<p align="left">
  <a href="README.md"><img src="https://img.shields.io/badge/English-view-555?style=flat-square" alt="English"></a>
  <a href="README.ko.md"><img src="https://img.shields.io/badge/%ED%95%9C%EA%B5%AD%EC%96%B4-view-555?style=flat-square" alt="한국어"></a>
  <a href="README.zh.md"><img src="https://img.shields.io/badge/%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-selected-1f5fa8?style=flat-square" alt="简体中文"></a>
</p>

### Yurim Oh [@wooring12]

<p align="left">
  <img src="https://komarev.com/ghpvc/?username=wooring12" alt="wooring12" />
</p>

---

## 🏗️ AI 平台工程师

我负责构建**让组织真正用好 LLM 的平台层**：知识管道、封闭网络模型服务、部署基础设施以及 Agent 工具链。

自 2026 年初起，我参与**某金融机构的 AI 转型（AX）项目**，从规划阶段一直到环境搭建全程参与。其中大部分工作在**物理隔离（air-gapped）且受安全监管的环境**中进行，这也决定了我的系统设计方式：

- 每个模型、镜像和依赖都必须经过审慎的引入、扫描与补丁修复
- 模型服务必须可复现，并能由小规模团队运维
- 知识与 Agent 必须基于内部数据，且行为可审计

我关注的方向：

- **有据可依的知识** — 将内部文档与规章制度转化为 LLM 可进行推理的图谱与检索系统
- **可运维的模型服务** — 让开源权重模型在自有 GPU 上稳定运行
- **平台而非演示** — 围绕模型构建 CI/CD、镜像仓库、网关、可观测性与访问控制
- **Agentic 工程** — 将编码 Agent 与 Agent CLI 作为真正的开发工具使用，配套共享规则、技能（skills）与统一模型网关

---

## 🔭 工作经历

**AI 平台工程师 · 金融行业** — 2026 年至今
AX 项目：端到端规划并搭建内部 LLM 环境（知识、服务、平台、Agent）。

**研究实习生 · Dareesoft** — WEMEET 项目
**研究实习生 · Rural Development Administration（韩国农村振兴厅）** — WEMEET 项目
**证书项目 · University of Toronto C-MORE Lab（多伦多大学 C-MORE 实验室）**

---

## 🧭 主要成果（2026）

这一年沿着一条主线推进：从*让内部知识可被 LLM 使用*，到*在封闭网络中运行模型*，再到*在其之上构建平台与 Agent 工具链*。

### 1. 面向 LLM 的知识基础设施

- 基于 Neo4j 的 LLM graph builder，构建了**面向法律与监管文档的 GraphRAG 管道**
- 对**图谱 Schema** 进行了多轮迭代（扁平结构 → 类型化 Schema → 层级感知），并实现多来源文档导入
- 搭建了基于 LLM 评审器与发布前冒烟测试的**图谱质量评估**机制
- 构建了**面向金融文档的 RAG 运维体系**（导入、检索、评估闭环）
- 研究了**本体建模**与**代码调用图分析**，作为 Agent 的知识来源

```text
Internal Documents / Regulations
    ↓
Parsing · Chunking · Entity/Relation Extraction
    ↓
Knowledge Graph (Neo4j) + Vector Index
    ↓
Graph + Vector Hybrid Retrieval
    ↓
LLM Answering · Evaluation · Feedback
```

### 2. 封闭网络 LLM 服务

- **调研开源权重模型**，并执行**物理隔离环境的引入**流程（权重、分词器、服务镜像）
- 在引入前构建服务引擎容器镜像并**修补安全漏洞**
- 为引入的软件与模型生成 **SBOM / AI-BOM** 清单
- 使用 **vLLM 与 SGLang** 提供模型服务，包括长上下文配置与量化版本
- 在企业级 Linux 上为 Kubernetes GPU 节点准备**离线 GPU Operator** 安装

```text
Model / Image Selection
    ↓
Offline Packaging · SBOM · Vulnerability Patch
    ↓
Air-gapped Transfer · Internal Registry
    ↓
Serving Engine (vLLM / SGLang) on GPU nodes
    ↓
OpenAI-compatible Endpoint
```

### 3. 平台与交付

- 基于 **Kubernetes** 探索模型服务与 Agent 平台
- **面向模型与应用交付的 CI/CD**（Jenkins Configuration-as-Code，Argo CD 就绪）
- 为封闭网络开发自建 **Git 与容器镜像仓库**（GitLab、Harbor）
- 共享 **PostgreSQL / Redis** 服务，以及 **GPU 服务器运维门户**（用量、监控、文档）
- **语音到知识管道**：通过语音识别与说话人分离为知识库提供数据

### 4. Agent 平台与 Agentic 工程

- 评估了 **Agent 平台**及其依赖的 LLM 能力（工具调用、长上下文、结构化输出）
- 将 **Agent CLI**（Claude Code、Codex CLI、Antigravity CLI、OpenCode）作为日常开发工具，并配套**共享 harness**：通用规则、可复用技能、会话交接与跨 Agent 记忆
- 构建了 **MCP 服务器**（如向量数据库访问）与 Agent 技能库
- 构建了 **LLM Gateway**：为所有 Agent CLI 提供统一端点与按用户分配的密钥，在云端 API 与自有 GPU 模型之间路由，支持分级模型访问、基于复杂度的自动路由、故障回退，并将用量日志记录到数据库
- 正在基于 Codex CLI 开发**SR 自动开发 Agent**：接收银行 App 的业务 SR（服务请求），自动完成代码编写，并贯通 CI/CD 交付

```text
Claude Code · Codex CLI · OpenCode · Antigravity CLI
    ↓  (one endpoint, per-user virtual keys)
LLM Gateway  —  auth · tiers · auto-routing · fallback · usage logs
    ↓
Cloud APIs  +  In-house GPU models (SGLang / vLLM)
```

---

## 🔬 研究（硕士阶段与独立研究）

在从事平台工作之前及同期，我的研究生阶段与独立研究主要聚焦于知识增强 LLM、高效模型与后训练。


### 1. 基于图的 AI 与知识融合 LLM

我尤其关注将**结构化知识**与语言模型相结合。

主要方向：

- 知识图谱嵌入：`TransE`、`RotatE`、`DistMult`、`ComplEx`
- 图神经网络与 Graph Transformer
- GraphRAG 与基于图的检索
- 基于结构化知识的多跳推理
- 法律知识图谱构建与法律问答
- KG 到 LLM 的表示注入

当前方向：

> 不仅仅是将图谱片段以文本形式检索出来，我还在探索如何**将 KG 嵌入投影到 LLM 嵌入空间**，并作为额外的图 token 用于推理。

示例架构：

```text
Knowledge Graph
    ↓
KGE Model: TransE / RotatE / DistMult
    ↓
Graph Vector s
    ↓
Projection Layer: g = W s + b
    ↓
[Graph Tokens] + [Question Tokens]
    ↓
Frozen LLM / LoRA-adapted LLM
    ↓
Answer Generation
```

研究问题：

- 与仅依赖检索的 GraphRAG 相比，KG 嵌入能否更好地保留全局图结构？
- 多少个图 token 对 LLM 推理有帮助？
- 图 token 应表示全局三元组、头实体-关系视角，还是关系-尾实体视角？
- 冻结的 LLM 能否在不进行全量微调的情况下利用投影后的图表示？
- 应如何在多跳问答上评估 KG-LLM 系统？

---

### 2. GraphRAG、法律问答与多跳评估

我曾基于法律文档与结构化三元组构建基于图的检索系统。

主要兴趣：

- 法律文档解析
- 实体与关系抽取
- SPO 三元组构建
- 基于 Neo4j 的图存储
- 基于 OpenSearch 的向量检索
- 图 + 向量混合检索
- 多跳问答数据集构建
- 检索结果评估

系统方向：

```text
Legal Documents
    ↓
Chunking / Parsing
    ↓
Entity-Relation Extraction
    ↓
Knowledge Graph Construction
    ↓
Neo4j + OpenSearch
    ↓
Graph Retrieval + Vector Retrieval
    ↓
LLM-based Legal QA
```

我重点关注需要跨越文档边界的问题，例如：

- 0 跳：直接事实查询
- 1 跳：实体与法律条文或实体与案例之间的关系
- 2 跳：案例 → 争议焦点 → 法律条文 / 判例 → 法律概念

---

### 3. 小语言模型优化

我关注如何在有限资源下让基于 LLM 的系统切实可用。

主要方向：

- 小语言模型
- 参数高效微调
- LoRA / PEFT
- 内存高效推理
- 量化感知部署
- 基于 vLLM 的模型服务
- 面向小型模型的 RAG 优化
- 轻量级 Agentic 工作流

核心动机：

> 在许多企业与封闭网络环境中，成本、延迟、部署限制与可维护性往往比单纯使用最大的模型更为重要。

---

### 4. LLM Agent 与 Agentic 工作流系统

我将 LLM Agent 视为**有状态、可调用工具、受工作流控制的系统**，而不仅仅是提示词链。

主要方向：

- 基于 LangGraph 的 Agent 编排
- Agent-to-Agent 工作流设计
- MCP 风格的工具集成
- A2A 风格的 Agent 互操作
- 人在回路（Human-in-the-loop）控制
- Agent 记忆与状态管理
- 工具调用与结构化输出
- 企业工作流自动化

示例系统模式：

```text
User Request
    ↓
Planner Agent
    ↓
Task-Specific Agents
    ├── Search Agent
    ├── DB Agent
    ├── Report Agent
    ├── Evaluation Agent
    └── Deployment Agent
    ↓
State Store / Version DB
    ↓
Final Output + Logs + Feedback Loop
```

我尤其关注构建能够在企业环境中运行的 Agent 系统：

- 内部文档检索
- 图谱/数据库查询
- 报告生成
- 监控与通知
- 实验自动化
- 可复现的 AI 管道

---

### 5. 面向 LLM 后训练的强化学习

我曾针对数学推理任务开展 GRPO 风格的后训练实验。

主要方向：

- GRPO
- 奖励设计
- 组级优化
- 自适应阈值
- 组构成感知学习
- 评估框架构建
- 奖励 / 损失 / 生成日志记录

当前研究思路：

> 同时包含正确与错误样本的组，可能比全部正确或全部错误的组蕴含更多有用的学习信号。

示例方向：

```text
Prompt
    ↓
Generate Group of Responses
    ↓
Reward Evaluation
    ↓
Analyze Group Composition
    ↓
Adjust Update Strength
    ↓
Policy Optimization
```

评估关注点：

- 准确率
- 样本利用率
- 奖励分布
- 组正确率
- token 效率
- 学习稳定性
- 与原始 GRPO 的对比

---

### 6. 计算机视觉与医疗 AI

我曾从事轻量级医学图像分割研究，尤其是脑肿瘤分割。

主要方向：

- U-Net 变体
- 深度可分离卷积
- 轻量级分割
- 医学图像分析
- MRI 脑肿瘤分割
- 资源受限的临床 AI

代表性工作：

- **LAG-UNet: Optimized Brain Tumor Segmentation for Resource-Constrained Clinical Environments via Adaptive Gating**

核心思路：

> 在计算资源有限的临床环境中，降低模型规模与内存占用，同时保持或提升分割质量。

---

### 7. 生成式 AI 与内容自动化

我也关注基于 AI Agent 的自动化内容生成管道。

主要方向：

- 剧本生成
- 角色数据库
- 分镜生成
- 文生图提示词设计
- 文生视频提示词设计
- 语音生成
- 后期处理
- 发布自动化
- 内容监控

示例架构：

```text
Trend Collector
    ↓
Scenario Agent
    ↓
Character / Relationship DB
    ↓
Storyboard Agent
    ↓
Image / Video / Voice Generation
    ↓
Post-processing Agent
    ↓
Publishing Agent
    ↓
Analytics Feedback
```

这一方向将生成式 AI 与 Agentic 自动化及生产管道相结合。

---

---

### 研究项目

#### KG-LLM Token 注入

一个将知识图谱表示注入 LLM 的研究方向。

核心思路：

- 训练或加载 KG 嵌入
- 将图向量投影到 LLM 嵌入空间
- 将图 token 与问题 token 拼接
- 保持 LLM 冻结或采用 LoRA 适配
- 与 GraphRAG 及仅提示词基线进行对比

---

#### 法律 GraphRAG 系统

一个使用结构化法律数据、基于图的法律问答系统。

组成部分：

- 法律文档解析器
- SPO 三元组抽取
- Neo4j 图数据库
- OpenSearch 向量索引
- 图/向量混合检索器
- 多跳法律问答基准
- 评估框架

---

#### GRPO 改进实验

一个面向 LLM 推理的后训练实验管道。

重点：

- 原始 GRPO 基线
- 自适应阈值 GRPO
- 组构成感知的更新加权
- 详细记录奖励、损失、生成结果与正确性
- 可复现的实验报告与表格

---

#### 企业 AI Agent MVP

一个基于 LangGraph、用于公共信息检索与机构指引的 AI Agent 系统。

功能：

- 公告检索
- 校历日程指引
- 公共服务信息
- 部门/联系人路由
- React 风格 UI
- 类 OpenWebUI 的交互设计
- 基于角色的模拟登录
- LangGraph 工作流后端

---

#### LAG-UNet 脑肿瘤分割

一个用于脑肿瘤 MRI 分析的轻量级分割模型。

重点：

- 参数量削减
- 内存效率
- 自适应门控
- 与原始 U-Net 的对比
- 面向资源受限临床环境的部署

---

---

## 🎓 教育背景

- 农业 AI 硕士，Jeonju University（全州大学），韩国 — 预计2027年2月毕业
- 人工智能学士，Jeonju University（全州大学），韩国，2025

---

## 📜 资格认证

- NVIDIA — Fundamentals of Deep Learning
- NVIDIA — Transformer Based Natural Language Processing Models
- Microsoft Certified — Azure AI Fundamentals
- Microsoft Certified — Azure Data Fundamentals

---

## 🧰 语言与工具

### 编程语言

- Python
- Bash
- SQL
- TypeScript

### LLM 服务与网关

- vLLM
- SGLang
- LiteLLM
- OpenAI 兼容 API
- 量化模型部署

### Agent

- Claude Code / Codex CLI / Antigravity CLI / OpenCode
- Model Context Protocol (MCP)
- LangGraph
- LangChain
- 工具调用 / 结构化输出

### 知识与检索

- Neo4j / LLM Graph Builder
- GraphRAG
- OpenSearch
- Milvus
- 向量检索 / 混合检索
- 知识图谱嵌入

### 平台 / DevOps

- Docker / Docker Compose
- Kubernetes / GPU Operator
- Jenkins / Argo CD
- GitLab / Harbor
- Nginx
- PostgreSQL / Redis
- SBOM (CycloneDX)
- 物理隔离部署

### 深度学习

- PyTorch
- Hugging Face Transformers
- PEFT / LoRA
- TensorFlow / Keras

### 计算机视觉

- OpenCV
- Ultralytics
- U-Net
- 医学图像分割

---

## 📫 联系方式

- LinkedIn: [Yurim Oh](https://www.linkedin.com/in/yurim-oh-225001285/)

---

<p>
  <img align="center" src="https://github-readme-stats.vercel.app/api?username=wooring12&show_icons=true" alt="wooring12" />
</p>
