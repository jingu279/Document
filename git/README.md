> **📝 안내:** 이 문서는 AI에 의해 작성되었습니다.
> **⚠️ 경고:** AI가 생성한 문서이므로 내용에 부정확하거나 잘못된 정보가 포함될 수 있습니다. 학습 시 공식 문서(Pro Git, Git 공식 문서 등)를 함께 참고하는 것을 권장합니다.

# 모두를 위한 Git 초보자 가이드

Git은 소프트웨어 개발 프로젝트에서 필수적인 버전 관리 시스템입니다. 개인 프로젝트는 물론, 여러 사람과 협업할 때 코드 변경 이력을 효율적으로 관리하고 팀원들과 원활하게 협업할 수 있도록 돕습니다.

## Topics Covered / 다루는 내용

이 가이드는 Git을 처음 접하는 분들을 위해 **기초부터 실무까지** 단계별로 설명합니다.

| Topic | 설명 |
|---|---|
| **Git 기초** | 저장소 생성, 변경 사항 추가/커밋, 작업 복귀 |
| **브랜치와 병합** | 브랜치 생성/전환, 병합(merge), 충돌 해결, cherry-pick |
| **원격 저장소** | push/pull/fetch, 원격 협업, patch 작업 |
| **GitHub** | PR, GitHub Flow, Fork, Actions, Issues/Projects |
| **Gerrit** | 코드 리뷰 시스템, Patch Set 관리 |
| **실무 워크플로우** | reset/revert, GitHub Flow vs Git Flow |
| **FAQ** | 70개 이상의 실전 Q&A |

모든 파일은 Markdown 형식으로 작성되었으며, Mermaid 다이어그램을 포함하여 시각적으로 이해하기 쉽게 구성되었습니다.

---

## 목차 (Table of Contents)

### 01. 서론 (Introduction)
*   [Git이란 무엇인가요?](01_서론/01_Git이란.md)
*   [왜 Git을 사용해야 하나요?](01_서론/02_왜_Git을_사용하는가.md)
*   [Git 설치](01_서론/03_Git_설치.md)

### 02. 기초 (Basics)
*   [Git 시작하기: 초기화 및 클론](02_기초/01_Git_시작하기.md)
*   [Git 워크플로우 이해](02_기초/02_Git_워크플로우.md)
*   [변경 사항 추가 및 커밋](02_기초/03_추가와_커밋.md)
*   [커밋 기록 확인](02_기초/04_커밋_기록_확인.md)
*   [변경 사항 확인: git diff](02_기초/05_변경_사항_확인.md)

### 03. 변경 되돌리기 (Undoing Changes)
*   [Reset과 Revert](03_변경_되돌리기/01_Reset과_Revert.md)
*   [Checkout 사용하기](03_변경_되돌리기/02_Checkout_사용하기.md)

### 04. 브랜치와 병합 (Branching and Merging)
*   [브랜치란 무엇인가요?](04_브랜치와_병합/01_브랜치란.md)
*   [브랜치 생성, 전환 및 삭제](04_브랜치와_병합/02_브랜치_생성_전환_삭제.md)
*   [브랜치 병합](04_브랜치와_병합/03_브랜치_병합.md)
*   [병합 충돌 해결](04_브랜치와_병합/04_충돌_해결.md)
*   [Cherry-Pick: 특정 커밋만 가져오기](04_브랜치와_병합/05_Cherry_Pick.md)

### 05. 원격 저장소 (Remote Repositories)
*   [원격 저장소 이해](05_원격_저장소/01_원격_저장소_이해.md)
*   [푸시, 풀, 페치](05_원격_저장소/02_Push_Pull_Fetch.md)
*   [Patch: 코드를 파일로 주고받기](05_원격_저장소/03_Patch_작업.md)

### 06. GitHub 활용
*   [GitHub 소개](06_GitHub/01_GitHub_소개.md)
*   [Pull Request 이해하기](06_GitHub/02_Pull_Request.md)
*   [GitHub Flow 워크플로우](06_GitHub/03_GitHub_Flow.md)
*   [Fork와 오픈소스 기여](06_GitHub/04_Fork와_기여.md)
*   [GitHub Actions 기초](06_GitHub/05_GitHub_Actions.md)
*   [Issues와 Projects 관리](06_GitHub/06_Issues와_Projects.md)

### 07. Gerrit
*   [Gerrit 소개](07_Gerrit/01_Gerrit_소개.md)
*   [코드 리뷰 프로세스](07_Gerrit/02_코드_리뷰_프로세스.md)
*   [Change와 Patch Set 이해](07_Gerrit/03_Change와_Patch_Set.md)
*   [git review 명령어 사용법](07_Gerrit/04_git_review_명령어.md)

### 08. 자주 묻는 질문 (FAQ)
*   [Git FAQ](08_FAQ.md) — 70개 이상의 Q&A

### 09. 용어 설명 (Glossary)
*   [용어 설명](09_용어_설명.md)
