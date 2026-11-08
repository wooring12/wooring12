<p align="left">
  <a href="README.md"><img src="https://img.shields.io/badge/English-view-555?style=flat-square" alt="English"></a>
  <a href="README.ko.md"><img src="https://img.shields.io/badge/%ED%95%9C%EA%B5%AD%EC%96%B4-selected-1f5fa8?style=flat-square" alt="한국어"></a>
  <a href="README.zh.md"><img src="https://img.shields.io/badge/%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-view-555?style=flat-square" alt="简体中文"></a>
</p>

### Yurim Oh [@wooring12]

<p align="left">
  <img src="https://komarev.com/ghpvc/?username=wooring12" alt="wooring12" />
</p>

---

## 🏗️ AI Platform Engineer

조직이 LLM을 실제로 활용할 수 있도록 하는 **플랫폼 계층**을 구축합니다. 지식 파이프라인, 폐쇄망 모델 서빙, 배포 인프라, 에이전트 도구가 그 범위입니다.

2026년 초부터 **금융권 기관의 AI 전환(AX) 프로그램**에 참여해 기획부터 환경 구축까지 담당하고 있습니다. 대부분의 작업이 **망분리된 보안 규제 환경**에서 이루어지며, 이는 시스템 설계 방식에 다음과 같은 영향을 줍니다.

- 모든 모델·이미지·의존성의 계획적인 반입, 점검, 패치
- 소규모 팀으로도 재현·운영 가능한 서빙
- 내부 데이터에 근거하고 동작을 감사할 수 있는 지식 체계와 에이전트

중점을 두는 영역:

- **근거 기반 지식** — 내부 문서와 규정을 LLM이 추론할 수 있는 그래프 및 검색 시스템으로 전환
- **운영 가능한 모델 서빙** — 사내 GPU에서 안정적으로 동작하는 open-weight 모델
- **데모가 아닌 플랫폼** — 모델을 둘러싼 CI/CD, 레지스트리, 게이트웨이, 관측성(observability), 접근 제어
- **Agentic engineering** — 공통 규칙, 스킬, 공용 모델 게이트웨이를 갖춘 실제 개발 도구로서의 코딩 에이전트와 에이전트 CLI 활용

---

## 🔭 경력

**AI Platform Engineer · 금융권** — 2026 – 현재
AX 프로그램: 사내 LLM 환경 전반(지식, 서빙, 플랫폼, 에이전트)의 기획 및 구축.

**연구 인턴 · Dareesoft** — WEMEET 프로그램
**연구 인턴 · 농촌진흥청** — WEMEET 프로그램
**수료 과정 · University of Toronto C-MORE Lab**

---

## 🧭 구축 성과 (2026)

한 해 동안 하나의 방향으로 작업했습니다. *내부 지식을 LLM이 활용할 수 있게 만드는 것*에서 출발해 *폐쇄망에서 모델을 운영하는 것*, 그리고 *그 위에 플랫폼과 에이전트 도구를 구축하는 것*으로 이어졌습니다.

### 1. LLM을 위한 지식 인프라

- Neo4j LLM graph builder를 활용한 **법령·규정 문서 기반 GraphRAG 파이프라인** 구축
- 여러 버전에 걸친 **그래프 스키마** 개선(flat → typed schema → hierarchy-aware) 및 다중 출처 문서 적재
- LLM 기반 평가자(judge)와 배포 전 smoke test를 활용한 **그래프 품질 평가** 체계 구축
- **금융 문서 RAG 운영** 체계 구축(적재, 검색, 평가 루프)
- 에이전트의 지식 원천으로서 **온톨로지 모델링**과 **코드 call-graph 분석** 연구

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

### 2. 폐쇄망 LLM 서빙

- **open-weight 모델 검토·선정** 및 **망분리 환경 반입** 절차 수행(가중치, 토크나이저, 서빙 이미지)
- 반입 전 **서빙 엔진 컨테이너 이미지** 빌드 및 취약점 **패치**
- 반입 소프트웨어와 모델에 대한 **SBOM / AI-BOM** 목록 생성
- **vLLM 및 SGLang** 기반 모델 서빙(long-context 설정 및 양자화 모델 포함)
- Kubernetes GPU 노드용 엔터프라이즈 Linux 환경의 **오프라인 GPU Operator** 설치 준비

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

### 3. 플랫폼 및 배포

- **Kubernetes** 기반 모델 서빙 및 에이전트 플랫폼 검토
- **모델·애플리케이션 배포용 CI/CD**(Jenkins Configuration-as-Code, Argo CD 도입 준비)
- 폐쇄망 개발을 위한 자체 호스팅 **Git 및 컨테이너 레지스트리**(GitLab, Harbor)
- 공용 **PostgreSQL / Redis** 서비스 및 **GPU 서버 운영 포털**(사용 현황, 모니터링, 문서)
- **음성-지식 변환 파이프라인**: 음성 인식과 화자 분리(speaker diarization) 결과의 지식 베이스 연계

### 4. 에이전트 플랫폼 및 Agentic Engineering

- **에이전트 플랫폼**과 그 기반이 되는 LLM 역량(tool calling, long context, structured output) 평가
- **에이전트 CLI**(Claude Code, Codex CLI, Antigravity CLI, OpenCode)를 일상 개발 도구로 도입하고 **공용 harness** 구성: 공통 규칙, 재사용 스킬, 세션 인계(hand-off), 에이전트 간 공유 메모리
- **MCP 서버**(예: 벡터 데이터베이스 접근) 및 에이전트 스킬 라이브러리 구축
- **LLM Gateway** 구축: 모든 에이전트 CLI를 위한 단일 엔드포인트와 사용자별 키, 클라우드 API와 사내 GPU 모델 간 라우팅, 등급별 모델 접근, 복잡도 기반 자동 라우팅, fallback, 데이터베이스 사용 로그 기록
- 뱅킹 앱 업무 SR(서비스 요청)을 받아 코드를 자동으로 작성하고 CI/CD 배포까지 수행하는 Codex CLI 기반 **SR 자동 개발 에이전트** 개발 중

```text
Claude Code · Codex CLI · OpenCode · Antigravity CLI
    ↓  (one endpoint, per-user virtual keys)
LLM Gateway  —  auth · tiers · auto-routing · fallback · usage logs
    ↓
Cloud APIs  +  In-house GPU models (SGLang / vLLM)
```

---

## 🧩 주요 저장소

| 저장소 | 설명 |
|---|---|
| dotfiles | 에이전트 CLI용 공용 harness: 공통 규칙, 스킬, hooks, 세션 인계 |
| llm-gateway | 에이전트 CLI용 단일 엔드포인트 LLM 게이트웨이(LiteLLM + nginx + PostgreSQL, 클라이언트 설치 도구) |
| a100-portal | GPU 서버 운영 포털 |

---

## 🔬 연구 (석사 과정 및 개인 연구)

플랫폼 업무 이전부터 병행해 온 대학원 및 개인 연구는 지식 증강 LLM, 효율적인 모델, 사후 학습(post-training)에 초점을 두었습니다.


### 1. 그래프 기반 AI 및 지식 통합 LLM

특히 **구조화된 지식**과 언어 모델을 연결하는 데 관심이 있습니다.

주요 주제:

- Knowledge Graph Embedding: `TransE`, `RotatE`, `DistMult`, `ComplEx`
- Graph Neural Networks 및 Graph Transformers
- GraphRAG 및 그래프 기반 검색
- 구조화된 지식에 대한 multi-hop 추론
- 법률 지식 그래프 구축 및 법률 QA
- KG-to-LLM 표현 주입

현재 방향:

> 그래프 조각을 텍스트로 검색하는 데 그치지 않고, **KG 임베딩을 LLM 임베딩 공간으로 투영**해 추론을 위한 추가 그래프 토큰으로 활용하는 방법을 연구합니다.

구조 예시:

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

연구 질문:

- KG 임베딩이 검색 전용 GraphRAG보다 그래프 전역 구조를 더 잘 보존할 수 있는가?
- LLM 추론에 유용한 그래프 토큰의 수는 몇 개인가?
- 그래프 토큰은 전역 triple, head-relation 관점, relation-tail 관점 중 무엇을 표현해야 하는가?
- frozen LLM이 전체 fine-tuning 없이 투영된 그래프 표현을 활용할 수 있는가?
- KG-LLM 시스템을 multi-hop QA에서 어떻게 평가해야 하는가?

---

### 2. GraphRAG, 법률 QA, Multi-Hop 평가

법률 문서와 구조화된 triple을 활용한 그래프 기반 검색 시스템을 구축했습니다.

주요 관심사:

- 법률 문서 파싱
- 개체 및 관계 추출
- SPO triple 구성
- Neo4j 기반 그래프 저장
- OpenSearch 기반 벡터 검색
- 그래프 + 벡터 하이브리드 검색
- Multi-hop QA 데이터셋 구축
- 검색 결과 평가

시스템 방향:

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

다음과 같이 문서 경계를 넘나들어야 하는 질문에 집중합니다.

- 0-hop: 직접적인 사실 조회
- 1-hop: 개체-법령 또는 개체-사건 관계
- 2-hop: 사건 → 쟁점 → 법령 / 판례 → 법률 개념

---

### 3. 소형 언어 모델 최적화

제한된 자원에서도 LLM 기반 시스템을 실용적으로 만드는 데 관심이 있습니다.

주요 주제:

- 소형 언어 모델(Small Language Models)
- Parameter-Efficient Fine-Tuning
- LoRA / PEFT
- 메모리 효율적 추론
- 양자화를 고려한 배포
- vLLM 기반 서빙
- 경량 모델을 위한 RAG 최적화
- 경량 agentic 워크플로

핵심 동기:

> 많은 기업 및 폐쇄망 환경에서는 단순히 가장 큰 모델을 쓰는 것보다 비용, 지연 시간, 배포 제약, 유지보수성이 더 중요한 경우가 많습니다.

---

### 4. LLM 에이전트 및 Agentic 워크플로 시스템

LLM 에이전트를 단순한 프롬프트 체인이 아닌 **상태를 가지고 도구를 사용하며 워크플로로 제어되는 시스템**으로 연구합니다.

주요 주제:

- LangGraph 기반 에이전트 오케스트레이션
- Agent-to-Agent 워크플로 설계
- MCP 방식 도구 연동
- A2A 방식 에이전트 상호운용성
- Human-in-the-loop 제어
- 에이전트 메모리 및 상태 관리
- Tool calling 및 structured output
- 기업 업무 워크플로 자동화

시스템 패턴 예시:

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

특히 기업 환경에서 동작할 수 있는 에이전트 시스템 구축에 관심이 있습니다.

- 내부 문서 검색
- 그래프/데이터베이스 질의
- 보고서 생성
- 모니터링 및 알림
- 실험 자동화
- 재현 가능한 AI 파이프라인

---

### 5. LLM 사후 학습을 위한 강화학습

수학적 추론 과제를 대상으로 GRPO 방식의 사후 학습 실험을 수행했습니다.

주요 주제:

- GRPO
- 보상 설계
- 그룹 단위 최적화
- 적응형 임계값(adaptive thresholding)
- 그룹 구성 인식 학습
- 평가 harness 구축
- 보상 / 손실 / 생성 결과 로깅

현재 연구 아이디어:

> 정답과 오답 샘플이 섞인 그룹은 모든 샘플이 정답이거나 모두 오답인 그룹보다 더 유용한 학습 신호를 담고 있을 수 있습니다.

방향 예시:

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

평가 관심 지표:

- 정확도
- 샘플 활용도
- 보상 분포
- 그룹 정답 비율
- 토큰 효율
- 학습 안정성
- vanilla GRPO와의 비교

---

### 6. 컴퓨터 비전 및 의료 AI

경량 의료 영상 분할, 특히 뇌종양 분할 연구를 수행했습니다.

주요 주제:

- U-Net 변형 모델
- Depthwise convolution
- 경량 분할(segmentation)
- 의료 영상 분석
- MRI 뇌종양 분할
- 자원 제약 임상 환경을 위한 AI

대표 연구:

- **LAG-UNet: Optimized Brain Tumor Segmentation for Resource-Constrained Clinical Environments via Adaptive Gating**

핵심 아이디어:

> 연산 자원이 제한된 임상 환경을 위해 분할 품질을 유지하거나 개선하면서 모델 크기와 메모리 사용량을 줄입니다.

---

### 7. 생성형 AI 및 콘텐츠 자동화

AI 에이전트를 활용한 콘텐츠 자동 생성 파이프라인에도 관심이 있습니다.

주요 주제:

- 시나리오 생성
- 캐릭터 데이터베이스
- 스토리보드 생성
- text-to-image 프롬프팅
- text-to-video 프롬프팅
- 음성 생성
- 후처리
- 게시 자동화
- 콘텐츠 모니터링

구조 예시:

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

이 방향은 생성형 AI를 agentic 자동화 및 프로덕션 파이프라인과 연결합니다.

---

---

### 연구 프로젝트

#### KG-LLM Token Injection

지식 그래프 표현을 LLM에 주입하는 연구 방향입니다.

핵심 아이디어:

- KG 임베딩 학습 또는 로드
- 그래프 벡터의 LLM 임베딩 공간 투영
- 그래프 토큰과 질문 토큰 결합
- LLM은 frozen 상태 유지 또는 LoRA 적용
- GraphRAG 및 프롬프트 전용 baseline과 비교

---

#### 법률 GraphRAG 시스템

구조화된 법률 데이터를 활용한 그래프 기반 법률 QA 시스템입니다.

구성 요소:

- 법률 문서 파서
- SPO triple 추출
- Neo4j 그래프 데이터베이스
- OpenSearch 벡터 인덱스
- 그래프/벡터 하이브리드 검색기
- Multi-hop 법률 QA 벤치마크
- 평가 harness

---

#### GRPO 개선 실험

LLM 추론 능력 향상을 위한 사후 학습 실험 파이프라인입니다.

중점:

- vanilla GRPO baseline
- 적응형 임계값 GRPO
- 그룹 구성 인식 업데이트 가중치
- 보상, 손실, 생성 결과, 정답 여부의 상세 로깅
- 재현 가능한 실험 보고서 및 표

---

#### 기업용 AI 에이전트 MVP

공공 정보 검색과 기관 안내를 위한 LangGraph 기반 AI 에이전트 시스템입니다.

기능:

- 공지사항 검색
- 학사 일정 안내
- 공공 서비스 정보
- 부서/담당자 연결
- React 스타일 UI
- OpenWebUI 유사 인터랙션 설계
- 역할 기반 모의 로그인
- LangGraph 워크플로 백엔드

---

#### LAG-UNet 뇌종양 분할

뇌종양 MRI 분석을 위한 경량 분할 모델입니다.

중점:

- 파라미터 감소
- 메모리 효율
- Adaptive gating
- vanilla U-Net과의 비교
- 자원 제약 임상 환경 배포

---

---

## 🎓 학력

- 전주대학교 Agro AI 석사 — 2027년 2월 졸업 예정
- 전주대학교 인공지능학 학사, 2025

---

## 📜 자격 및 수료

- NVIDIA — Fundamentals of Deep Learning
- NVIDIA — Transformer Based Natural Language Processing Models
- Microsoft Certified — Azure AI Fundamentals
- Microsoft Certified — Azure Data Fundamentals

---

## 🧰 언어 및 도구

### 프로그래밍

- Python
- Bash
- SQL
- TypeScript

### LLM 서빙 및 게이트웨이

- vLLM
- SGLang
- LiteLLM
- OpenAI 호환 API
- 양자화 모델 배포

### 에이전트

- Claude Code / Codex CLI / Antigravity CLI / OpenCode
- Model Context Protocol (MCP)
- LangGraph
- LangChain
- Tool Calling / Structured Output

### 지식 및 검색

- Neo4j / LLM Graph Builder
- GraphRAG
- OpenSearch
- Milvus
- 벡터 검색 / 하이브리드 검색
- Knowledge Graph Embedding

### 플랫폼 / DevOps

- Docker / Docker Compose
- Kubernetes / GPU Operator
- Jenkins / Argo CD
- GitLab / Harbor
- Nginx
- PostgreSQL / Redis
- SBOM (CycloneDX)
- 망분리 환경 배포

### 딥러닝

- PyTorch
- Hugging Face Transformers
- PEFT / LoRA
- TensorFlow / Keras

### 컴퓨터 비전

- OpenCV
- Ultralytics
- U-Net
- 의료 영상 분할

---

## 📫 연락처

- LinkedIn: [Yurim Oh](https://www.linkedin.com/in/yurim-oh-225001285/)

---

<p>
  <img align="center" src="https://github-readme-stats.vercel.app/api?username=wooring12&show_icons=true" alt="wooring12" />
</p>
