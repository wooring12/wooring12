<p align="left">
  <a href="README.md"><img src="https://img.shields.io/badge/English-selected-1f5fa8?style=flat-square" alt="English"></a>
  <a href="README.ko.md"><img src="https://img.shields.io/badge/%ED%95%9C%EA%B5%AD%EC%96%B4-view-555?style=flat-square" alt="한국어"></a>
  <a href="README.zh.md"><img src="https://img.shields.io/badge/%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-view-555?style=flat-square" alt="简体中文"></a>
</p>

### Yurim Oh [@wooring12]

<p align="left">
  <img src="https://komarev.com/ghpvc/?username=wooring12" alt="wooring12" />
</p>

---

## 🏗️ AI Platform Engineer

I build the **platform layer that lets an organization actually use LLMs**: knowledge pipelines, closed-network model serving, deployment infrastructure, and agent tooling.

Since early 2026 I have been working on an **AI Transformation (AX) program at a financial institution**, involved from planning through environment build-out. Most of that work happens in an **air-gapped, security-regulated environment**, which shapes how I design systems:

- every model, image, and dependency has to be brought in, scanned, and patched deliberately
- serving has to be reproducible and operable by a small team
- knowledge and agents have to stay grounded in internal data, with auditable behavior

What I care about:

- **Grounded knowledge** — turning internal documents and regulations into graphs and retrieval systems an LLM can reason over
- **Operable model serving** — open-weight models running reliably on in-house GPUs
- **Platform, not demos** — CI/CD, registries, gateways, observability, and access control around the models
- **Agentic engineering** — coding agents and agent CLIs used as real development tools, with shared rules, skills, and a common model gateway

---

## 🔭 Experience

**AI Platform Engineer · Financial sector** — 2026 – Present
AX program: planning and building the in-house LLM environment end to end (knowledge, serving, platform, agents).

**Research Intern · Dareesoft** — WEMEET program
**Research Intern · Rural Development Administration** — WEMEET program
**Certificate program · University of Toronto C-MORE Lab**

---

## 🧭 What I Have Built (2026)

The year followed one direction: from *making internal knowledge usable by LLMs*, to *running models in a closed network*, to *building the platform and agent tooling on top*.

### 1. Knowledge Infrastructure for LLMs

- Built a **GraphRAG pipeline over legal and regulatory documents** using Neo4j's LLM graph builder
- Iterated the **graph schema** through several versions (flat → typed schema → hierarchy-aware) and multi-source document ingestion
- Set up **graph quality evaluation** with LLM-based judges and pre-release smoke tests
- Built **RAG operations for financial documents** (ingestion, retrieval, evaluation loop)
- Studied **ontology modeling** and **code call-graph analysis** as knowledge sources for agents

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

### 2. Closed-Network LLM Serving

- **Scouted open-weight models** and ran the **air-gapped import** process (weights, tokenizers, serving images)
- Built and **patched serving-engine container images** for vulnerabilities before import
- Generated **SBOM / AI-BOM** inventories for imported software and models
- Served models with **vLLM and SGLang**, including long-context configuration and quantized variants
- Prepared **offline GPU Operator** installs on enterprise Linux for Kubernetes GPU nodes

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

### 3. Platform & Delivery

- **Kubernetes**-based exploration of model serving and agent platforms
- **CI/CD for model and app delivery** (Jenkins Configuration-as-Code, Argo CD readiness)
- Self-hosted **Git and container registry** (GitLab, Harbor) for closed-network development
- Shared **PostgreSQL / Redis** services and a **GPU server operations portal** (usage, monitoring, docs)
- **Speech-to-knowledge pipeline**: speech recognition and speaker diarization feeding a knowledge base

### 4. Agent Platform & Agentic Engineering

- Evaluated **agent platforms** and the LLM capabilities they depend on (tool calling, long context, structured output)
- Adopted **agent CLIs** (Claude Code, Codex CLI, Antigravity CLI, OpenCode) as daily development tools, with a **shared harness**: common rules, reusable skills, session hand-off, and cross-agent memory
- Built **MCP servers** (e.g. vector database access) and agent skill libraries
- Built an **LLM Gateway**: one endpoint and per-user keys for every agent CLI, routing across cloud APIs and in-house GPU models, tiered model access, complexity-based auto routing, fallback, and usage logging in a database
- Developing (in progress) an **SR-to-deployment coding agent** on Codex CLI: it takes service requests (SRs) for a banking app, implements the code changes automatically, and carries them through CI/CD

```text
Claude Code · Codex CLI · OpenCode · Antigravity CLI
    ↓  (one endpoint, per-user virtual keys)
LLM Gateway  —  auth · tiers · auto-routing · fallback · usage logs
    ↓
Cloud APIs  +  In-house GPU models (SGLang / vLLM)
```

---

## 🔬 Research (M.S. & Independent)

Before and alongside platform work, my graduate and independent research focused on knowledge-augmented LLMs, efficient models, and post-training.


### 1. Graph-based AI & Knowledge-Integrated LLMs

I am especially interested in connecting **structured knowledge** with language models.

Main topics:

- Knowledge Graph Embedding: `TransE`, `RotatE`, `DistMult`, `ComplEx`
- Graph Neural Networks and Graph Transformers
- GraphRAG and graph-based retrieval
- Multi-hop reasoning over structured knowledge
- Legal knowledge graph construction and legal QA
- KG-to-LLM representation injection

Current direction:

> Instead of only retrieving graph fragments as text, I explore how **KG embeddings can be projected into the LLM embedding space** and used as additional graph tokens for reasoning.

Example architecture:

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

Research questions:

- Can KG embeddings preserve global graph structure better than retrieval-only GraphRAG?
- How many graph tokens are useful for LLM reasoning?
- Should graph tokens represent global triples, head-relation views, or relation-tail views?
- Can frozen LLMs use projected graph representations without full fine-tuning?
- How should KG-LLM systems be evaluated on multi-hop QA?

---

### 2. GraphRAG, Legal QA, and Multi-Hop Evaluation

I have worked on building graph-based retrieval systems using legal documents and structured triples.

Main interests:

- Legal document parsing
- Entity and relation extraction
- SPO triple construction
- Neo4j-based graph storage
- OpenSearch-based vector retrieval
- Graph + vector hybrid retrieval
- Multi-hop QA dataset construction
- Retrieval result evaluation

System direction:

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

I focus on questions that require crossing document boundaries, such as:

- 0-hop: direct factual lookup
- 1-hop: entity-to-law or entity-to-case relation
- 2-hop: case → issue → law / precedent → legal concept

---

### 3. Small Language Model Optimization

I am interested in making LLM-based systems practical under limited resources.

Main topics:

- Small Language Models
- Parameter-Efficient Fine-Tuning
- LoRA / PEFT
- Memory-efficient inference
- Quantization-aware deployment
- vLLM-based serving
- RAG optimization for compact models
- Lightweight agentic workflows

Key motivation:

> In many enterprise and closed-network environments, cost, latency, deployment constraints, and maintainability are often more important than simply using the largest model.

---

### 4. LLM Agents and Agentic Workflow Systems

I explore LLM agents as **stateful, tool-using, workflow-controlled systems**, not just prompt chains.

Main topics:

- LangGraph-based agent orchestration
- Agent-to-Agent workflow design
- MCP-style tool integration
- A2A-style agent interoperability
- Human-in-the-loop control
- Agent memory and state management
- Tool calling and structured output
- Enterprise workflow automation

Example system pattern:

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

I am especially interested in building agent systems that can operate in enterprise environments:

- internal document search
- graph/database querying
- report generation
- monitoring and notification
- experiment automation
- reproducible AI pipelines

---

### 5. Reinforcement Learning for LLM Post-Training

I have explored GRPO-style post-training experiments for mathematical reasoning tasks.

Main topics:

- GRPO
- reward design
- group-level optimization
- adaptive thresholding
- group composition-aware learning
- evaluation harness construction
- reward / loss / generation logging

Current research idea:

> Groups with mixed correct and incorrect samples may contain more useful learning signal than groups where all samples are correct or all samples are wrong.

Example direction:

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

Evaluation interests:

- accuracy
- sample usage
- reward distribution
- group correctness ratio
- token efficiency
- learning stability
- comparison with vanilla GRPO

---

### 6. Computer Vision & Medical AI

I have worked on lightweight medical image segmentation, especially brain tumor segmentation.

Main topics:

- U-Net variants
- Depthwise convolution
- Lightweight segmentation
- Medical image analysis
- MRI brain tumor segmentation
- Resource-constrained clinical AI

Representative work:

- **LAG-UNet: Optimized Brain Tumor Segmentation for Resource-Constrained Clinical Environments via Adaptive Gating**

Key idea:

> Reduce model size and memory usage while preserving or improving segmentation quality for clinical environments with limited computational resources.

---

### 7. Generative AI and Content Automation

I am also interested in automated content generation pipelines using AI agents.

Main topics:

- scenario generation
- character database
- storyboard generation
- text-to-image prompting
- text-to-video prompting
- voice generation
- post-processing
- publishing automation
- content monitoring

Example architecture:

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

This direction connects generative AI with agentic automation and production pipelines.

---

---

### Research Projects

#### KG-LLM Token Injection

A research direction for injecting knowledge graph representations into LLMs.

Core idea:

- Train or load KG embeddings
- Project graph vectors into LLM embedding space
- Concatenate graph tokens with question tokens
- Keep the LLM frozen or LoRA-adapted
- Compare against GraphRAG and prompt-only baselines

---

#### Legal GraphRAG System

A graph-based legal QA system using structured legal data.

Components:

- legal document parser
- SPO triple extraction
- Neo4j graph database
- OpenSearch vector index
- hybrid graph/vector retriever
- multi-hop legal QA benchmark
- evaluation harness

---

#### GRPO Improvement Experiments

A post-training experiment pipeline for LLM reasoning.

Focus:

- vanilla GRPO baseline
- adaptive threshold GRPO
- group composition-aware update weighting
- detailed logging of rewards, losses, generations, and correctness
- reproducible experiment reports and tables

---

#### Enterprise AI Agent MVP

A LangGraph-based AI agent system for public information search and institutional guidance.

Features:

- notice search
- academic schedule guidance
- public service information
- department/contact routing
- React-style UI
- OpenWebUI-like interaction design
- role-based mock login
- LangGraph workflow backend

---

#### LAG-UNet Brain Tumor Segmentation

A lightweight segmentation model for brain tumor MRI analysis.

Focus:

- parameter reduction
- memory efficiency
- adaptive gating
- comparison with vanilla U-Net
- clinical resource-constrained deployment

---

---

## 🎓 Education

- M.S. in Agro AI, Jeonju University, Korea — expected Feb 2027
- B.S. in Artificial Intelligence, Jeonju University, Korea, 2025

---

## 📜 Qualifications

- NVIDIA — Fundamentals of Deep Learning
- NVIDIA — Transformer Based Natural Language Processing Models
- Microsoft Certified — Azure AI Fundamentals
- Microsoft Certified — Azure Data Fundamentals

---

## 🧰 Languages and Tools

### Programming

- Python
- Bash
- SQL
- TypeScript

### LLM Serving & Gateway

- vLLM
- SGLang
- LiteLLM
- OpenAI-compatible APIs
- Quantized model deployment

### Agents

- Claude Code / Codex CLI / Antigravity CLI / OpenCode
- Model Context Protocol (MCP)
- LangGraph
- LangChain
- Tool Calling / Structured Output

### Knowledge & Retrieval

- Neo4j / LLM Graph Builder
- GraphRAG
- OpenSearch
- Milvus
- Vector Search / Hybrid Retrieval
- Knowledge Graph Embedding

### Platform / DevOps

- Docker / Docker Compose
- Kubernetes / GPU Operator
- Jenkins / Argo CD
- GitLab / Harbor
- Nginx
- PostgreSQL / Redis
- SBOM (CycloneDX)
- Air-gapped deployment

### Deep Learning

- PyTorch
- Hugging Face Transformers
- PEFT / LoRA
- TensorFlow / Keras

### Computer Vision

- OpenCV
- Ultralytics
- U-Net
- Medical Image Segmentation

---

## 📫 Contact

- LinkedIn: [Yurim Oh](https://www.linkedin.com/in/yurim-oh-225001285/)

---

<p>
  <img align="center" src="https://github-readme-stats.vercel.app/api?username=wooring12&show_icons=true" alt="wooring12" />
</p>
