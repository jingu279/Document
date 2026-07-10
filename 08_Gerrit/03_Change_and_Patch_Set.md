# Change와 Patch Set 이해하기

Gerrit의 Change와 Patch Set은 코드 리뷰의 핵심 단위입니다. 이 개념을 이해하면 Gerrit 워크플로우를 효과적으로 활용할 수 있습니다.

**Change와 Patch Set의 관계:**

```
Patch Set 생명주기:

  하나의 Change 안에서 여러 버전(Patch Set)이 관리됨

                  같은 Change-ID 유지
  ┌──────────────────────────────────────────────────┐
  │  Change 123: "로그인 페이지 추가"                 │
  │                                                  │
  │  시간 ───────────────────────────────────────►   │
  │                                                  │
  │  Patch Set 1   Patch Set 2   Patch Set 3        │
  │  (최초 제출)    (스타일 추가)   (리뷰 반영)       │
  │       │             │             │              │
  │       ▼             ▼             ▼              │
  │  ┌────────┐  ┌────────┐  ┌──────────────────┐   │
  │  │login   │  │login   │  │login.html (38줄) │   │
  │  │.html   │  │.html   │  │style.css (25줄)  │   │
  │  │(30줄)  │  │(35줄)  │  │README.md (5줄)   │   │
  │  └────────┘  │style   │  └──────────────────┘   │
  │              │.css    │                          │
  │              │(20줄)  │                          │
  │              └────────┘                          │
  │                                                  │
  │  Status:         Open    Open    Merged          │
  │  Reviews:        0/2     +1/2    +2/2  ✅       │
  └──────────────────────────────────────────────────┘

  💡 PS1 → PS2: "스타일이 없습니다" 리뷰 반영
  💡 PS2 → PS3: "README도 업데이트해주세요" 리뷰 반영
  💡 각 PS 간의 차이(diff)를 Gerrit UI에서 볼 수 있음
```

## Change (변경)

Change는 하나의 논리적인 작업 단위입니다. GitHub의 Pull Request와 유사하지만, Gerrit에서는 하나의 **커밋**이 하나의 Change가 됩니다.

### Change의 구성 요소

```
Change 12345
├── Subject: "로그인 페이지 추가"
├── Owner: 홍길동 <hong@example.com>
├── Project: my-project
├── Branch: main
├── Status: Open / Merged / Abandoned
├── Created: 2026-07-10 14:30
├── Patch Sets:
│   ├── Patch Set 1 (최초 업로드)
│   ├── Patch Set 2 (스타일 추가)
│   └── Patch Set 3 (리뷰 반영) ← 현재
├── Reviewers:
│   ├── alice@example.com (+2 Code-Review)
│   └── bob@example.com (+1 Verified)
└── Comments: 12
```

### Change-ID

Change-ID는 Change를 식별하는 고유 값입니다. 커밋 메시지에 포함되며, `git commit --amend`로 수정해도 같은 Change-ID를 유지하면 동일한 Change의 새 Patch Set이 됩니다.

```bash
# Change-ID의 형식
Change-Id: I47c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5

# commit-msg hook이 자동 생성
$ git commit -m "내용"
# → 자동으로 Change-Id 추가됨
```

### Change 상태

| 상태 | 설명 |
|---|---|
| **New** | 새로 생성됨, 아직 리뷰 전 |
| **Open** | 리뷰 진행 중 |
| **Merged** | 리뷰 완료, main에 병합됨 |
| **Abandoned** | 포기됨 (더 이상 진행하지 않음) |
| **Draft** | 비공개 초안 (초대된 사람만 볼 수 있음) |

## Patch Set (패치 세트)

Patch Set은 Change의 버전입니다. 첫 push는 PS1, 수정 후 다시 push하면 PS2가 됩니다.

### Patch Set 생명주기

```bash
# PS1: 첫 번째 시도 (스타일 없음)
login.html (30줄)
$ git push origin HEAD:refs/for/main
→ Change 123, Patch Set 1 생성

# PS2: 스타일 추가 (리뷰어 피드백 반영)
login.html (35줄) + style.css (20줄)
$ git add .
$ git commit --amend --no-edit
$ git push origin HEAD:refs/for/main
→ Change 123, Patch Set 2 자동 생성

# PS3: 추가 수정 (두 번째 리뷰 반영)
login.html (38줄) + style.css (25줄) + README.md (5줄)
$ git add .
$ git commit --amend -m "로그인 페이지 추가

스타일 및 문서 업데이트 포함

Change-Id: I47c7d8e9..."
$ git push origin HEAD:refs/for/main
→ Change 123, Patch Set 3 자동 생성
```

### Patch Set 간 차이 보기

Gerrit 웹 UI에서 각 Patch Set 간의 차이를 확인할 수 있습니다.

```
Gerrit UI:
  Change 123: 로그인 페이지 추가

  ▼ Patch Sets (3)
    ◉ Patch Set 1 (기본)
    ○ Patch Set 2 (+스타일)
    ○ Patch Set 3 (+문서)

  Diff against: [Patch Set 1 ▼]
  ┌─────────────────────────────────┐
  │ @@ -1,5 +1,8 @@                 │
  │  <h1>Login</h1>                 │
  │ +<link rel="stylesheet" ...>    │ ← PS2에서 추가
  │ +<style>...</style>             │
  │  <form>...</form>               │
  │ +<p>문서 링크: ...</p>          │ ← PS3에서 추가
  └─────────────────────────────────┘
```

## 여러 커밋 다루기

Gerrit은 기본적으로 **커밋 하나 = Change 하나**입니다. 여러 커밋을 푸시하면 각각 별도의 Change가 생성됩니다.

```bash
# 여러 커밋 푸시
$ git log --oneline -3
a1b2c3d 문서 업데이트
d4e5f6f 로그인 페이지 추가
g7h8i9j 설정 파일 수정

$ git push origin HEAD:refs/for/main
→ Change 124: 문서 업데이트 (a1b2c3d)
→ Change 125: 로그인 페이지 추가 (d4e5f6f)
→ Change 126: 설정 파일 수정 (g7h8i9j)
# 각각 독립적인 Change로 생성됨!
```

### 의존 관계 (Dependency)

순서대로 적용되어야 하는 변경은 의존 관계가 생깁니다.

```
Change 124: 문서 업데이트 (의존성 없음)
Change 125: 로그인 페이지 추가 (Change 124에 의존)
Change 126: 설정 파일 수정 (Change 125에 의존)
```

Gerrit UI에서:
```
Change 125
  Depends On: Change 124 (문서 업데이트)
  Needed By: Change 126 (설정 파일 수정)

→ Change 124가 먼저 승인되어야 Change 125 승인 가능
```

## Patch Set 관리 팁

### 1. 작은 단위로 유지

```bash
# ❌ 변경 하나에 모든 것을 넣기
$ git commit -m "로그인, 결제, 프로필 기능 구현"

# ✅ 각각 별도 Change로 분리
$ git commit -m "로그인 페이지 추가"
$ git commit -m "결제 모듈 구현"
$ git commit -m "프로필 페이지 추가"
```

### 2. 불필요한 Patch Set 방지

```bash
# 로컬에서 충분히 테스트한 후 push
$ git add .
$ git commit -m "완성된 기능"

# push 전에 최종 확인
$ git diff --cached
$ npm test

# 문제 없으면 push
$ git push origin HEAD:refs/for/main
```

### 3. Patch Set 히스토리 관리

```bash
# 이전 Patch Set의 코멘트를 확인
# PS1의 코멘트: "이 변수명이 이해하기 어렵습니다"
# PS2에서 반영했는지 확인

# 원한다면 PS1과 PS3의 차이만 볼 수도 있음
# Gerrit UI: "Diff against Patch Set 1" 선택
```

### 4. WIP (Work In Progress) 활용

```bash
# 아직 작업 중인 변경은 WIP으로 표시
$ git push origin HEAD:refs/for/main%wip

# Gerrit에서 "WIP" 표시, 리뷰어에게 알림 안 감
# 작업 완료 후 WIP 해제
# Gerrit UI → "Start Review" 버튼

# 또는 CLI로
$ git push origin HEAD:refs/for/main%ready
```
