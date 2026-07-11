# AI 프로그래밍 완전 정복

**실전 AI 프로그래밍 가이드 — A to Z Guide for Beginner & Intermediate Software Engineers**

> **📝 안내:** 이 문서는 AI에 의해 작성되었습니다.
> **⚠️ 경고:** AI가 생성한 문서이므로 내용에 부정확하거나 잘못된 정보가 포함될 수 있습니다. 학습 시 공식 문서 및 학술 자료를 함께 참고하는 것을 권장합니다.
> **© License:** 교육 목적 자유 사용, 상업적 사용 및 무단 수정/배포 금지.

---

## 이 책이 필요한 사람

- AI 프로그래밍을 **처음 배우는** 소프트웨어 엔지니어
- **Python** 기본 문법을 알고 있지만 AI 프로그래밍 라이브러리(NumPy, PyTorch 등)는 처음인 개발자
- 머신러닝/딥러닝 **프로그래밍의 이론과 실무**를 함께 익히고 싶은 주니어 개발자
- "AI 시대에 개발자가 무엇을 공부해야 할지" 막막한 엔지니어

## 독자가 알고 있어야 할 것

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'primaryColor': '#e3f2fd', 'primaryTextColor': '#0d47a1', 'primaryBorderColor': '#1565c0', 'lineColor': '#1565c0', 'fontSize': '14px'}}}%%
flowchart LR
  subgraph Prerequisites[시작하기 전에 알면 좋은 것]
    direction LR
    Python["🐍 Python 기본 문법<br/>변수, 함수, 클래스"]
    Logic["🧩 기초 논리 & 알고리즘<br/>조건문, 반복문, 배열"]
    English["📖 영어 독해 능력<br/>공식 문서와 논문"]
  end
  Pre_Out["➡️"]
  Nice_In["⬅️"]
  subgraph NiceToHave[있으면 더 좋지만,<br/>책에서 다시 가르쳐줌]
    direction LR
    Math["📐 고등학교 수학<br/>행렬, 미분, 확률"]
    Git["🔀 Git 기초"]
    Linux["💻 터미널 사용 경험"]
  end

  Pre_Out --- Nice_In

  classDef blue fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#0d47a1
  classDef green fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  class Python,Logic,English blue
  class Math,Git,Linux green
```

> **걱정 마세요.** 선형대수, 미적분, 통계는 **필요한 만큼만** 책에서 다시 설명합니다. "수포자"도 따라올 수 있습니다.

---

## 학습 로드맵

전체 과정은 **4개 파트, 16개 장**으로 구성됩니다.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart TB
  subgraph Part1[PART 1: 기초 다지기]
    direction TB
    Ch01["01장: AI란 무엇인가?"]
    Ch02["02장: 개발 환경 설정"]
    Ch03["03장: 수학 기초"]
    Ch04["04장: Python 데이터 과학"]
  end
  P1_Out["→"]
  P2_In["←"]
  subgraph Part2[PART 2: 머신러닝]
    direction TB
    Ch05["05장: 머신러닝 개념"]
    Ch06["06장: 지도 학습"]
    Ch07["07장: 비지도 학습"]
    Ch08["08장: 모델 평가와 최적화"]
  end
  P2_Out["→"]
  P3_In["←"]
  subgraph Part3[PART 3: 딥러닝과 응용]
    direction TB
    Ch09["09장: 신경망 기초"]
    Ch10["10장: 컴퓨터 비전"]
    Ch11["11장: 자연어 처리"]
    Ch12["12장: 생성형 AI와 LLM"]
    Ch13["13장: AI Agent, MCP, Harness"]
  end
  P3_Out["→"]
  P4_In["←"]
  subgraph Part4[PART 4: 실무 프로젝트]
    direction TB
    Ch14["14장: AI 개발 워크플로우"]
    Ch15["15장: 실전 프로젝트"]
    Ch16["16장: AI 윤리와 미래"]
  end

  Ch01 --> Ch02 --> Ch03 --> Ch04 --> P1_Out
  P2_In --> Ch05 --> Ch06 --> Ch07 --> Ch08 --> P2_Out
  P3_In --> Ch09 --> Ch10
  Ch09 --> Ch11 --> Ch12 --> Ch13 --> P3_Out
  P4_In --> Ch14 --> Ch15 --> Ch16
  P1_Out --> P2_In
  P2_Out --> P3_In
  P3_Out --> P4_In

  classDef p1 fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#0d47a1
  classDef p2 fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef p3 fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  classDef p4 fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  class Ch01,Ch02,Ch03,Ch04 p1
  class Ch05,Ch06,Ch07,Ch08 p2
  class Ch09,Ch10,Ch11,Ch12,Ch13 p3
  class Ch14,Ch15,Ch16 p4
```

---

## 전체 목차

### PART 1: 기초 다지기

#### 01장: AI 프로그래밍 개요
- AI 프로그래밍이란? (전통적 프로그래밍 vs AI 프로그래밍)
- AI 프로그래밍의 전체 생명주기: 데이터 → 모델 → 배포
- AI 프로그래밍 접근법: 규칙 기반, 머신러닝 기반, LLM 기반
- AI 프로그래밍 도구와 기술 스택
- 이 책에서 배울 전체 로드맵

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart LR
  AI["🤖 인공지능 (AI)<br/>지능을 가진 시스템"]
  ML["📊 머신러닝 (ML)<br/>데이터로부터 학습"]
  DL["🧠 딥러닝 (DL)<br/>인공 신경망 학습"]
  GenAI["✨ 생성형 AI<br/>새로운 콘텐츠 생성"]

  AI --> ML --> DL --> GenAI

  classDef ai fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  classDef ml fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#0d47a1
  classDef dl fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef gen fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  class AI ai
  class ML ml
  class DL dl
  class GenAI gen
```

#### 02장: AI 프로그래밍을 위한 개발 환경 설정
- Python과 Anaconda 설치 (AI 개발 환경 구축)
- 가상 환경 (venv, conda)을 활용한 프로젝트 격리
- Jupyter Notebook: AI 실험/분석 환경 vs Python 스크립트: 프로덕션 코드
- 주요 AI 라이브러리 설치 (NumPy, Pandas, Scikit-learn, PyTorch, TensorFlow)
- AI 개발을 위한 GPU 설정 (CUDA, cuDNN)
- AI 프로그래밍에 최적화된 코드 에디터 추천 (VS Code, PyCharm)
- Google Colab을 활용한 클라우드 AI 개발 환경

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart TB
  Setup["⚙️ AI 개발 환경"]
  Python["🐍 Python 3.10+"]
  Env["📦 가상 환경<br/>conda / venv"]
  Libs["📚 핵심 라이브러리"]
  Editor["🛠️ 개발 도구"]

  Setup --> Python & Env & Libs & Editor

  NP["🔢 NumPy<br/>수치 계산"]
  PD["🗂️ Pandas<br/>데이터 분석"]
  SK["🤖 Scikit-learn<br/>머신러닝"]
  PT["🔥 PyTorch<br/>딥러닝"]

  Libs --> NP & PD & SK & PT

  JN["📓 Jupyter<br/>실험/분석"]
  VS["💻 VS Code<br/>개발"]
  GC["☁️ Google Colab<br/>클라우드 GPU"]

  Editor --> JN & VS & GC

  classDef root fill:#e3f2fd,stroke:#1565c0,stroke-width:3px,color:#0d47a1
  classDef cat fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  classDef lib fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef tool fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  class Setup root
  class Python,Env cat
  class NP,PD,SK,PT lib
  class JN,VS,GC tool
```

#### 03장: AI 프로그래밍에 필요한 수학 기초
- **선형대수:** AI에서 벡터/행렬이 데이터를 표현하고 변환하는 방식
- **미적분:** AI 모델 학습의 핵심 — 미분, 체인 룰, 그래디언트
- **확률과 통계:** AI 모델의 불확실성 처리와 데이터 특성 분석
- **최적화:** 경사하강법을 통한 AI 모델 파라미터 학습

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart LR
  subgraph LA[🔷 선형대수]
    V["📐 벡터<br/>데이터 표현"]
    M["🔲 행렬<br/>변환과 연산"]
  end
  LA_Out["→"]
  CAL_In["←"]
  subgraph CAL[📈 미적분]
    D["📉 미분<br/>변화율"]
    GD["⬇️ 경사하강법<br/>최적화"]
  end
  subgraph STAT[🎲 확률통계]
    P["❓ 확률<br/>불확실성"]
    S["📊 통계<br/>데이터 특성"]
  end

  V --> M --> LA_Out
  D --> GD
  LA_Out --> CAL_In
  CAL_In --> GD
  P --> S
  GD --> ML["🤖 머신러닝 학습"]

  classDef la fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#0d47a1
  classDef cal fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  classDef stat fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef ml fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  class V,M la
  class D,GD cal
  class P,S stat
  class ML ml
```

#### 04장: AI 프로그래밍을 위한 Python 데이터 과학
- NumPy: AI 데이터의 배열 연산과 선형대수 프로그래밍
- Pandas: AI 학습용 데이터 불러오기, 정제, 변환 프로그래밍
- Matplotlib & Seaborn: AI 데이터 분석 결과 시각화 프로그래밍
- Scikit-learn: AI 모델 학습 파이프라인 프로그래밍

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart LR
  subgraph EDA[📊 데이터 분석 과정]
    direction LR
    Load["📂 데이터 불러오기<br/>Pandas read_csv"]
    Explore["🔍 데이터 탐색<br/>info, describe, head"]
    Clean["🧹 데이터 정제<br/>결측치 처리, 중복 제거"]
    Viz["📈 데이터 시각화<br/>Matplotlib, Seaborn"]
    MLReady["✅ ML 학습 준비 완료"]
  end

  Load --> Explore --> Clean --> Viz --> MLReady

  classDef step fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#0d47a1
  classDef done fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  class Load,Explore,Clean,Viz step
  class MLReady done
```

### PART 2: 머신러닝

#### 05장: AI 모델 프로그래밍의 시작 — 머신러닝 개념
- 지도학습 vs 비지도학습 vs 강화학습: 프로그래밍 패러다임 비교
- AI 모델 프로그래밍의 구성 요소: 특징(Feature), 레이블(Label), 모델(Model)
- 학습/검증/테스트 데이터 분할 프로그래밍
- 과대적합(Overfitting)과 과소적합(Underfitting) 디버깅
- 편향-분산 트레이드오프(Bias-Variance Tradeoff) 이해

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart TB
  ML["🤖 머신러닝"]
  Supervised["📋 지도 학습<br/>정답이 있는 데이터"]
  Unsupervised["🔓 비지도 학습<br/>정답이 없는 데이터"]
  RL["🏆 강화 학습<br/>보상을 통한 학습"]

  ML --> Supervised & Unsupervised & RL

  Class["📂 분류 (Classification)<br/>스팸 메일 탐지"]
  Reg["📈 회귀 (Regression)<br/>주택 가격 예측"]

  Supervised --> Class & Reg

  Clus["👥 군집화 (Clustering)<br/>고객 세분화"]
  Dim["📏 차원 축소<br/>특성 압축"]

  Unsupervised --> Clus & Dim

  classDef ml fill:#e8f5e9,stroke:#2e7d32,stroke-width:3px,color:#1b5e20
  classDef sup fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef unsup fill:#fff9c4,stroke:#f9a825,stroke-width:2px,color:#e65100
  classDef rl fill:#ffcdd2,stroke:#c62828,stroke-width:2px,color:#b71c1c
  classDef task fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#1b5e20
  class ML ml
  class Supervised,Class,Reg sup
  class Unsupervised,Clus,Dim unsup
  class RL rl
```

#### 06장: 지도 학습 알고리즘 프로그래밍
- 선형 회귀 (Linear Regression) 구현과 해석
- 로지스틱 회귀 (Logistic Regression) 구현과 활용
- 결정 트리 & 랜덤 포레스트 프로그래밍
- 서포트 벡터 머신 (SVM) 실전 구현
- K-최근접 이웃 (K-NN) 프로그래밍
- 각 알고리즘의 장단점과 실전 선택 기준

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart TB
  Problem["🤔 어떤 문제인가?"]
  Regression{"📊 예측값이<br/>연속적인가?"}
  Linear["📈 선형 회귀<br/>단순하고 빠름"]
  Classify{"🔍 데이터가<br/>선형 분리되는가?"}

  Problem --> Regression
  Regression -->|Yes| Linear
  Regression -->|No| Classify

  SVM2["⚡ SVM<br/>고성능"]
  Tree["🌲 랜덤 포레스트<br/>대부분 잘 작동"]

  Classify -->|Yes| SVM2
  Classify -->|No| Tree

  DeepCheck{"📏 데이터가<br/>매우 많은가?"}
  XGB["🚀 XGBoost<br/>캐글 대회 왕"]
  RF["🌲 랜덤 포레스트<br/>충분히 좋음"]

  Tree --> DeepCheck
  DeepCheck -->|Yes| XGB
  DeepCheck -->|No| RF

  classDef start fill:#e8f5e9,stroke:#2e7d32,stroke-width:3px,color:#1b5e20
  classDef decision fill:#fff9c4,stroke:#f9a825,stroke-width:2px,color:#e65100
  classDef model fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  class Problem start
  class Regression,Classify,DeepCheck decision
  class Linear,SVM2,Tree,XGB,RF model
```

#### 07장: 비지도 학습 프로그래밍
- K-Means 군집화 알고리즘 구현
- 계층적 군집화 프로그래밍
- DBSCAN을 활용한 이상 탐지 프로그래밍
- 주성분 분석 (PCA)을 통한 차원 축소 구현
- t-SNE를 활용한 고차원 데이터 시각화 프로그래밍

#### 08장: 모델 평가와 최적화 프로그래밍
- 분류 모델 평가 프로그래밍: 정확도, 정밀도, 재현율, F1-score, ROC-AUC
- 회귀 모델 평가 프로그래밍: MSE, MAE, R²
- 교차 검증 (Cross Validation) 구현
- 하이퍼파라미터 튜닝 프로그래밍: Grid Search, Random Search
- 특성 공학 (Feature Engineering) 실전 기법
- 앙상블 기법 프로그래밍

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart LR
  Train["📦 데이터"]
  Split["✂️ Train / Test 분할"]
  CV["🔄 교차 검증"]
  TrainModel["⚙️ 모델 학습"]
  Tune{"🔧 하이퍼파라미터<br/>튜닝"}
  Eval["✅ 최종 평가"]
  Report["📋 성능 리포트<br/>Accuracy: 0.95<br/>F1: 0.92<br/>AUC: 0.97"]

  Train --> Split --> CV --> TrainModel --> Tune
  Tune -->|반복| CV
  Tune -->|완료| Eval --> Report

  classDef data fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef process fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  classDef decision fill:#fff9c4,stroke:#f9a825,stroke-width:2px,color:#e65100
  classDef result fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  class Train,Split data
  class CV,TrainModel process
  class Tune decision
  class Eval,Report result
```

### PART 3: 딥러닝과 응용

#### 09장: 신경망 프로그래밍 기초
- 퍼셉트론 (Perceptron) 구현부터 시작하는 신경망 프로그래밍
- 활성화 함수 프로그래밍: Sigmoid, Tanh, ReLU, Softmax
- 다층 퍼셉트론 (MLP) 구현
- 순전파 (Forward Propagation) 프로그래밍
- 역전파 (Backpropagation) 구현 원리
- 손실 함수 프로그래밍: MSE, Cross-Entropy
- 옵티마이저 프로그래밍: SGD, Adam
- PyTorch/TensorFlow를 활용한 딥러닝 프로그래밍

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart LR
  subgraph NN[🧠 신경망 구조]
    direction LR
    I["📥 Input Layer<br/>데이터 입력"]
    H1["⚡ Hidden Layer 1<br/>64 nodes, ReLU"]
    H2["⚡ Hidden Layer 2<br/>32 nodes, ReLU"]
    O["📤 Output Layer<br/>10 nodes, Softmax"]
  end

  I --> H1 --> H2 --> O
  
  subgraph Process[🔄 학습 과정]
    direction LR
    FP["➡️ 순전파<br/>예측값 계산"]
    Loss["📉 손실 계산<br/>예측 vs 정답"]
    BP["⬅️ 역전파<br/>그래디언트 계산"]
    Update["🔄 가중치 갱신<br/>Adam 옵티마이저"]
  end

  FP --> Loss --> BP --> Update
  Update -.->|반복 (Epoch)| FP

  classDef layer fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  classDef process fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  class I,H1,H2,O layer
  class FP,Loss,BP,Update process
```

#### 10장: 컴퓨터 비전 프로그래밍 (CNN)
- 합성곱 신경망 (CNN) 프로그래밍 개념
- 합성곱(Convolution)과 풀링(Pooling) 계층 구현
- 주요 CNN 아키텍처 구현: VGG, ResNet
- 이미지 분류 모델 프로그래밍 실습 (CIFAR-10)
- 데이터 증강 (Data Augmentation) 프로그래밍
- 전이 학습 (Transfer Learning) 구현
- 객체 탐지 (YOLO) 프로그래밍 개요

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart LR
  Input["🖼️ 입력 이미지<br/>224x224x3"]
  Conv1["🔲 Conv + ReLU<br/>64 filters"]
  Pool1["📉 Max Pooling<br/>2x2"]
  Conv2["🔲 Conv + ReLU<br/>128 filters"]
  Pool2["📉 Max Pooling"]
  FC["🔗 Fully Connected<br/>4096 nodes"]
  Output["🎯 출력<br/>클래스 확률"]

  Input --> Conv1 --> Pool1 --> Conv2 --> Pool2 --> FC --> Output

  subgraph Kernel[🔍 합성곱 연산]
    direction LR
    K["🧩 입력 이미지"]
    Filter["🎛️ 필터 (Kernel)<br/>3x3"]
    Result["🗺️ 특징 맵<br/>(Feature Map)"]
  end

  K --> Filter --> Result

  classDef input fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  classDef conv fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef pool fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  classDef fc fill:#ffcdd2,stroke:#c62828,stroke-width:2px,color:#b71c1c
  classDef out fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  class Input input
  class Conv1,Conv2 conv
  class Pool1,Pool2 pool
  class FC fc
  class Output out
  class K,Filter,Result conv
```

#### 11장: 자연어 처리 프로그래밍 (NLP)
- 텍스트 전처리 프로그래밍: 토큰화, 정제, 형태소 분석
- 단어 임베딩 구현: Word2Vec, GloVe
- 순환 신경망 (RNN)과 LSTM 프로그래밍
- 트랜스포머 (Transformer) 아키텍처 구현
- BERT를 활용한 문맥 이해 프로그래밍
- 감성 분석, 텍스트 분류 모델 구현 실습

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart TB
  subgraph NLP_Pipeline[📝 NLP 파이프라인]
    direction TB
    Raw["📄 원본 텍스트<br/>'나는 오늘 기분이 좋다'"]
    Token["✂️ 토큰화<br/>['나', '는', '오늘', '기분', '좋다']"]
    Embed["🔢 임베딩<br/>단어 → 벡터"]
    Model["🧠 NLP 모델<br/>BERT, GPT 등"]
    Result["🎯 결과<br/>긍정/부정, 요약, 번역"]
  end

  Raw --> Token --> Embed --> Model --> Result

  classDef raw fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  classDef proc fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  classDef model fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef result fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  class Raw raw
  class Token,Embed proc
  class Model model
  class Result result
```

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart LR
  subgraph Transformer[🏗️ 트랜스포머 아키텍처]
    direction LR
    Input2["📥 입력 문장"]
    Pos["📍 위치 인코딩"]
    MH["👁️ Multi-Head<br/>Attention"]
    Add1["➕ Add & Norm"]
    FF["⚡ Feed Forward"]
    Add2["➕ Add & Norm"]
    Output2["📤 출력"]
  end

  Input2 --> Pos --> MH --> Add1 --> FF --> Add2 --> Output2

  subgraph Attention[🎯 어텐션 메커니즘]
    direction LR
    Q["❓ Query"]
    K["🔑 Key"]
    V["💎 Value"]
    Score["📊 점수 계산"]
    Soft["🌀 Softmax"]
    Weight["⚖️ 가중합"]
  end

  Q --> Score
  K --> Score
  Score --> Soft
  V --> Weight
  Soft --> Weight

  classDef input fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  classDef proc fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  classDef att fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef out fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  class Input2,Output2 input
  class Pos,MH,Add1,FF,Add2 proc
  class Q,K,V,Score,Soft,Weight att
```

#### 12장: 생성형 AI와 LLM 프로그래밍
- 생성형 AI 프로그래밍 개념
- GPT 아키텍처 이해와 활용 프로그래밍
- 프롬프트 엔지니어링 (Prompt Engineering) 프로그래밍
- RAG (Retrieval Augmented Generation) 시스템 구현
- LangChain 프레임워크를 활용한 AI 애플리케이션 개발
- LLM Fine-tuning 프로그래밍 기초
- Vector Database와 임베딩 검색 프로그래밍

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart TB
  subgraph RAG[🔗 RAG 시스템]
    direction TB
    Q2["💬 사용자 질문"]
    EmbedQ["🔢 질문 임베딩"]
    Search
    Context["📄 검색된 문서 + 질문"]
    LLM["🧠 LLM (GPT-4, Claude)"]
    Answer["✅ 최종 답변 생성"]
  end

  Q2 --> EmbedQ --> Search --> Context --> LLM --> Answer

  Search["🔍 Vector DB 검색<br/>관련 문서 찾기"]
  Store["💾 Vector Store<br/>Pinecone / Chroma"]

  subgraph VectorDB[🗄️ Vector Database 구축]
    direction TB
    Docs["📚 문서들"]
    Chunk["✂️ 문서 분할"]
    EmbedD["🔢 청크 임베딩"]
    Store
  end

  Docs --> Chunk --> EmbedD --> Store
  Store --> Search

  classDef user fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  classDef proc fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  classDef db fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef answer fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  class Q2 user
  class EmbedQ,Search,Context proc
  class LLM answer
  class Docs,Chunk,EmbedD,Store db
```

#### 13장: AI Agent, MCP, Harness 프로그래밍
- AI Agent 개념과 ReAct 패턴 구현
- Function Calling / Tool Use 프로그래밍
- Multi-Agent 시스템과 Skills 개발
- MCP (Model Context Protocol) 서버/클라이언트 프로그래밍
- AI Harness를 활용한 LLM/Agent 평가 프로그래밍
- API 제공자 연동과 토큰 관리 프로그래밍

---

### PART 4: 실무 프로젝트

#### 14장: AI 개발 워크플로우 프로그래밍
- AI 프로젝트 구조와 파일 관리
- 데이터 수집 및 라벨링 파이프라인 구축
- 실험 관리 프로그래밍 (MLflow, Weights & Biases)
- 모델 저장 및 버전 관리 프로그래밍
- 모델 배포: Flask/FastAPI API 서버 구현
- Docker를 이용한 AI 애플리케이션 컨테이너화
- 클라우드 배포 프로그래밍 (AWS, GCP, Hugging Face)

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart LR
  subgraph MLOps[🔄 ML 개발 → 배포 파이프라인]
    direction LR
    Data["📦 데이터 수집"]
    Prep["🧹 데이터 전처리"]
    Train2["⚙️ 모델 학습"]
    Eval2["📊 모델 평가"]
    Register["📋 모델 등록"]
    Deploy["🚀 모델 배포<br/>FastAPI + Docker"]
    Monitor["📈 성능 모니터링"]
    Retrain["🔄 재학습"]
  end

  Data --> Prep --> Train2 --> Eval2
  Eval2 -->|통과| Register --> Deploy --> Monitor
  Eval2 -->|실패| Train2
  Monitor -->|데이터 드리프트| Retrain --> Train2

  classDef data fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  classDef train fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  classDef eval fill:#fff9c4,stroke:#f9a825,stroke-width:2px,color:#e65100
  classDef deploy fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  class Data,Prep data
  class Train2,Retrain train
  class Eval2 eval
  class Register,Deploy,Monitor deploy
```

#### 15장: 실전 AI 프로그래밍 프로젝트
- **프로젝트 1:** 이미지 분류기 프로그래밍 (개 vs 고양이)
- **프로젝트 2:** 영화 리뷰 감성 분석기 프로그래밍
- **프로젝트 3:** RAG 기반 문서 Q&A 챗봇 프로그래밍
- **프로젝트 4:** 실시간 객체 탐지 앱 프로그래밍

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart TB
  subgraph Proj1[📱 프로젝트 1: 이미지 분류]
    direction TB
    P1Data["🐱 고양이/개 사진"]
    P1Train["🧠 CNN or 전이 학습"]
    P1Result["📷 웹캠으로 실시간 분류"]
  end

  subgraph Proj2[🎬 프로젝트 2: 감성 분석]
    direction TB
    P2Data["🎥 영화 리뷰 데이터"]
    P2Train["🔤 BERT Fine-tuning"]
    P2Result["😊 리뷰 긍정/부정 판단"]
  end

  subgraph Proj3[🤖 프로젝트 3: RAG 챗봇]
    direction TB
    P3Data["📄 회사 문서 PDF"]
    P3Embed["🔢 임베딩 + Vector DB"]
    P3RAG["🔗 RAG 파이프라인"]
    P3Result["💬 문서 기반 질의응답"]
  end

  subgraph Proj4[🎯 프로젝트 4: 객체 탐지]
    direction TB
    P4Data["📹 실시간 영상"]
    P4Model["👁️ YOLOv8"]
    P4Result["📦 객체 탐지 + 바운딩 박스"]
  end

  P1Data --> P1Train --> P1Result
  P2Data --> P2Train --> P2Result
  P3Data --> P3Embed --> P3RAG --> P3Result
  P4Data --> P4Model --> P4Result

  classDef p1 fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#0d47a1
  classDef p2 fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef p3 fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  classDef p4 fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  class P1Data,P1Train,P1Result p1
  class P2Data,P2Train,P2Result p2
  class P3Data,P3Embed,P3RAG,P3Result p3
  class P4Data,P4Model,P4Result p4
```

#### 16장: AI 프로그래밍 윤리와 미래
- AI 프로그래밍에서의 편향 (Bias) 사례와 대처
- 공정성 (Fairness) 평가 프로그래밍
- 설명 가능한 AI (XAI) 구현 기법
- 프라이버시와 데이터 보호 프로그래밍 원칙
- AI 개발자의 미래와 역할

---

## 각 장의 구성

각 장은 다음과 같은 형식으로 구성됩니다:

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart LR
  subgraph Chapter[📋 각 장의 구성]
    direction LR
    Goals["🎯 학습 목표<br/>이 장에서 배울 것"]
    Theory["📖 이론 설명<br/>개념 + Mermaid 다이어그램"]
    Code["💻 코드 예제<br/>실행 가능한 Python 코드"]
    Practice["✏️ 실습 문제<br/>직접 해보는 문제"]
    Summary["📋 한눈에 정리<br/>핵심 요약 표"]
  end

  Goals --> Theory --> Code --> Practice --> Summary

  classDef goal fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  classDef theory fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#0d47a1
  classDef code fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef practice fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  classDef summary fill:#ffcdd2,stroke:#c62828,stroke-width:2px,color:#b71c1c
  class Goals goal
  class Theory theory
  class Code code
  class Practice practice
  class Summary summary
```

---

## 전체 학습 로드맵 요약

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
timeline
    title AI 프로그래밍 학습 로드맵
    Part 1 기초 다지기 : AI 개념 이해
            : 개발 환경 설정
            : 수학 기초 복습
            : Python 데이터 과학
    Part 2 머신러닝 : 머신러닝 개념
            : 지도 학습 알고리즘
            : 비지도 학습
            : 모델 평가와 최적화
    Part 3 딥러닝과 응용 : 신경망과 딥러닝
            : 컴퓨터 비전 (CNN)
            : 자연어 처리 (NLP)
            : 생성형 AI와 LLM
    Part 4 실무 프로젝트 : AI 개발 워크플로우
            : 실전 프로젝트 4개
            : AI 윤리와 미래
```

---

> **시작하려면:** `01_서론/01_AI란.md`에서부터 순서대로 읽으세요. 각 장은 이전 장의 내용을 기반으로 합니다.

---

## 수학이 두려우신가요?

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '13px'}}}%%
flowchart TB
  Question["😰 수학이 부족한데<br/>AI를 배울 수 있을까요?"]
  A1["✅ 네, 가능합니다!"]

  Question --> A1

  R1["📐 3장에서 필요한 수학만<br/>선별해서 가르쳐줍니다"]
  R2["🔢 NumPy가 행렬 연산을<br/>자동으로 처리합니다"]
  R3["🔥 PyTorch가 미분을<br/>자동으로 계산합니다"]
  R4["💡 공식 암기보다<br/>직관적 이해가 중요합니다"]

  A1 --> R1 & R2 & R3 & R4
  
  ExampleNode["💎 예: 행렬 곱셈<br/>수학: 직접 계산<br/>Python: @ 연산자 하나면 끝"]

  R2 --> ExampleNode

  classDef q fill:#ffcdd2,stroke:#c62828,stroke-width:3px,color:#b71c1c
  classDef yes fill:#c8e6c9,stroke:#2e7d32,stroke-width:3px,color:#1b5e20
  classDef reason fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#0d47a1
  classDef demo fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#bf360c
  class Question q
  class A1 yes
  class R1,R2,R3,R4 reason
  class ExampleNode demo
```

---

## 디렉토리 구조

```
ai-programming/
├── README.md                    # 이 파일 (전체 개요)
├── LICENSE.md                   # 라이선스
│
├── 01_서론/                     # Part 1: 기초
│   ├── 01_AI란.md
│   ├── 02_개발_환경.md
│   ├── 03_수학_기초.md
│   └── 04_Python_데이터과학.md
│
├── 02_머신러닝/                 # Part 2: 머신러닝
│   ├── 01_ML_개념.md
│   ├── 02_지도_학습.md
│   ├── 03_비지도_학습.md
│   └── 04_모델_평가.md
│
├── 03_딥러닝/                   # Part 3: 딥러닝
│   ├── 01_신경망_기초.md
│   ├── 02_컴퓨터_비전.md
│   ├── 03_자연어_처리.md
│   └── 04_생성형_AI.md
│
├── 04_실무/                     # Part 4: 실무
│   ├── 01_AI_워크플로우.md
│   ├── 02_실전_프로젝트.md
│   └── 03_AI_윤리.md
│
└── projects/                    # 실습 프로젝트 코드
    ├── image_classifier/
    ├── sentiment_analysis/
    ├── rag_chatbot/
    └── object_detection/
```

---

승인하시면 각 장을 하나씩 작성해 나가겠습니다. 먼저 어느 장부터 시작할까요?
