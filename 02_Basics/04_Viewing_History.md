# 커밋 기록 확인

Git의 강력한 기능 중 하나는 프로젝트의 변경 이력을 자유롭게 살펴볼 수 있다는 것입니다. `git log` 명령어를 사용하여 커밋 기록을 확인하는 방법을 알아봅니다.

## 1. 기본 로그 확인: `git log`

```bash
git log
```

**출력 예시:**
```
commit 7a3fb42e8d9c1f5b2a4c6d8e0f1a2b3c4d5e6f7a (HEAD -> main)
Author: Your Name <your.email@example.com>
Date:   Mon Jul 10 14:30:00 2026 +0900

    index.html 스타일 업데이트 및 new-style.css 추가

commit 1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b
Author: Your Name <your.email@example.com>
Date:   Mon Jul 10 12:00:00 2026 +0900

    첫 번째 커밋: 프로젝트 초기화
```

각 커밋은 다음 정보를 포함합니다.
*   **커밋 해시 (Commit Hash):** `7a3fb42...`와 같은 고유한 40자리 16진수 식별자
*   **Author:** 커밋을 작성한 사람
*   **Date:** 커밋이 생성된 날짜와 시간
*   **Commit Message:** 커밋할 때 작성한 메시지

**커밋 해시의 의미:**

커밋 해시는 SHA-1 알고리즘으로 생성된 고유 식별자입니다. 다음 정보를 기반으로 만들어집니다:
- 파일 스냅샷의 내용
- 부모 커밋의 해시
- 커밋 시간
- 작성자 정보

그래서 **같은 내용이라도 다른 시간에 커밋하면 다른 해시**가 생성됩니다.

```bash
$ git rev-parse HEAD
7a3fb42e8d9c1f5b2a4c6d8e0f1a2b3c4d5e6f7a

# 앞 7자리만 사용해도 충분히 고유함
$ git show 7a3fb42  # 가능!
```

## 2. 다양한 로그 옵션

`git log`는 다양한 옵션을 제공하여 원하는 형태로 이력을 조회할 수 있습니다.

### 한 줄로 간략하게 보기
```bash
git log --oneline
```
```
7a3fb42 (HEAD -> main) index.html 스타일 업데이트 및 new-style.css 추가
1a2b3c4 첫 번째 커밋: 프로젝트 초기화
```

### 그래프 형태로 보기 (브랜치 구조 확인)
```bash
git log --oneline --graph --all
```
```
* 7a3fb42 (HEAD -> main) index.html 스타일 업데이트 및 new-style.css 추가
* 1a2b3c4 첫 번째 커밋: 프로젝트 초기화
```

### 최근 N개의 커밋만 보기
```bash
git log -3          # 최근 3개의 커밋만 표시
git log -n 5        # 최근 5개의 커밋만 표시
```

### 특정 작성자의 커밋만 보기
```bash
git log --author="홍길동"
```

### 날짜/시간 범위로 검색
```bash
git log --since="2025-01-01" --until="2025-12-31"
git log --after="2 weeks ago"   # 2주 전 이후 커밋
git log --before="yesterday"    # 어제 이전 커밋
```

### 특정 문자열이 포함된 커밋 찾기
```bash
git log --grep="버그"           # 메시지에 "버그"가 포함된 커밋
git log --grep="fix" -i         # 대소문자 무시하고 "fix" 검색
git log -S "console.log"        # 코드에 "console.log"가 추가/제거된 커밋
```

### 로그 출력 형식 커스터마이징
```bash
git log --pretty=format:"%h - %an, %ar : %s"
# a1b2c3d - 홍길동, 2 days ago : README 업데이트
# d4e5f6f - 김철수, 5 days ago : 로그인 버그 수정

# %h : 짧은 해시
# %an : 작성자 이름
# %ar : 상대적 시간 (2 days ago)
# %s : 커밋 메시지 제목
# %d : ref 이름 (브랜치, 태그)
```

### 특정 파일의 변경 이력만 보기
```bash
git log -- index.html
```

### 변경된 파일 목록만 확인
```bash
git log --name-only
git log --name-status    # 변경 유형까지 표시
```

## 3. 변경 사항 비교하기: `git diff`

### 스테이징되지 않은 변경 사항 확인 (Working Directory vs Staging Area)
```bash
git diff
```

### 스테이징된 변경 사항 확인 (Staging Area vs Repository)
```bash
git diff --staged
```

### 두 커밋 간의 차이 확인
```bash
git diff <커밋해시1> <커밋해시2>
```

### 실제 diff 출력 예시 (커밋 간 비교)
```bash
$ git diff a1b2c3d..d4e5f6f
diff --git a/README.md b/README.md
index e69de29..d95f3ad 100644
--- a/README.md
+++ b/README.md
@@ -0,0 +1,3 @@
+# My Project
+
+This is a sample project for learning Git.
```

**diff 출력 읽는 법:**
- `--- a/file` : 원본 파일 (a)
- `+++ b/file` : 비교 대상 파일 (b)
- `@@ -시작줄,줄수 +시작줄,줄수 @@` : 변경 위치
- `-` 로 시작하는 줄: 삭제된 내용
- `+` 로 시작하는 줄: 추가된 내용

### 특정 파일의 변경 이력만 diff
```bash
git diff a1b2c3d..d4e5f6f -- README.md
```

### 단어 단위로 diff 보기
```bash
git diff --word-diff
```

## 4. 특정 커밋의 상세 내용 확인: `git show`

```bash
git show 7a3fb42
```

이 명령어는 특정 커밋의 변경 사항과 메타데이터를 자세히 보여줍니다.

**출력 예시:**
```bash
$ git show d4e5f6f
commit d4e5f6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2d
Author: 홍길동 <hong@example.com>
Date:   Tue Jul 11 10:30:00 2026 +0900

    README에 설치 방법 추가

diff --git a/README.md b/README.md
index d95f3ad..b1c2d3e 100644
--- a/README.md
+++ b/README.md
@@ -1,3 +1,8 @@
 # My Project

 This is a sample project for learning Git.
+
+## Installation
+
+```bash
+npm install my-project
+```
```

## 5. git log와 git diff 종합 예제

```bash
# 1. 최근 5개 커밋을 한 줄로 확인
$ git log --oneline -5
a1b2c3d README에 설치 방법 추가
d4e5f6f 로그인 페이지 구현
g7h8i9j 메인 페이지 레이아웃 수정
k1l2m3n 첫 번째 커밋: 프로젝트 초기화

# 2. 특정 범위의 변경 사항 확인
$ git diff g7h8i9j..a1b2c3d

# 3. 특정 파일이 어떤 커밋에서 변경되었는지
$ git log --oneline -- README.md
a1b2c3d README에 설치 방법 추가
k1l2m3n 첫 번째 커밋: 프로젝트 초기화

# 4. 각 커밋별로 변경된 파일 목록
$ git log --oneline --stat
a1b2c3d README에 설치 방법 추가
 README.md | 5 +++++
 1 file changed, 5 insertions(+)

d4e5f6f 로그인 페이지 구현
 login.html | 20 ++++++++++++++++++++
 style.css  | 10 ++++++++++
 2 files changed, 30 insertions(+)
```

이러한 명령어들을 활용하면 프로젝트의 이력을 쉽게 추적하고, 어떤 변경이 언제, 왜 발생했는지 명확하게 파악할 수 있습니다.
