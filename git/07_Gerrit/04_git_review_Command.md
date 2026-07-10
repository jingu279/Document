# git review 명령어 사용법

지금까지 우리는 Gerrit에 변경 사항을 push하기 위해 `git push origin HEAD:refs/for/main`과 같은 긴 명령어를 사용해왔습니다. 이 장에서는 이러한 복잡한 명령어를 대신하여 Gerrit 작업을 더욱 편리하게 만들어주는 **git review** 도구에 대해 알아보겠습니다. git review를 사용하면 간단한 명령어만으로 Gerrit과 상호작용할 수 있어 개발 생산성을 크게 향상시킬 수 있습니다.

> **⚠️ 경고:** AI가 생성한 문서입니다. 내용에 부정확한 정보가 포함될 수 있으므로, 학습 시 공식 문서를 함께 참고하세요.

## 학습 목표

- git review 도구의 설치 및 설정 방법을 이해한다
- git review의 기본 명령어와 고급 사용법을 익힌다
- git review를 활용한 일일 개발 워크플로우를 설명할 수 있다
- git review 설정 파일(.gitreview)의 역할을 이해한다

## git review 설치

git review를 사용하기 위해서는 먼저 설치가 필요합니다. 운영체제에 따라 아래 방법 중 하나를 선택하여 설치할 수 있습니다.

```bash
# pip로 설치
$ pip install git-review

# macOS (Homebrew)
$ brew install git-review

# 설치 확인
$ git review --version
git-review 2.4.0
```

## git review 설정

설치가 완료되었다면, 저장소에서 git review를 사용할 수 있도록 초기화해야 합니다. 이 과정은 저장소마다 한 번만 수행하면 됩니다.

```bash
# 저장소 클론 후 한 번만 설정
$ git clone ssh://username@gerrit.example.com:29418/my-project
$ cd my-project

# git review 초기화 (Gerrit 원격 저장소 자동 설정)
$ git review -s

# 설정 확인
$ git remote -v
gerrit   ssh://username@gerrit.example.com:29418/my-project (fetch)
gerrit   ssh://username@gerrit.example.com:29418/my-project (push)
origin   ssh://username@gerrit.example.com:29418/my-project (fetch)
origin   ssh://username@gerrit.example.com:29418/my-project (push)
```

## git review 기본 명령어

이제 git review가 설치되고 설정되었습니다. 기본 명령어를 하나씩 살펴보겠습니다.

### 리뷰 요청 (Push)

가장 많이 사용하는 명령어는 `git review`입니다. 전통적인 방식과 비교하면 훨씬 간결합니다.

```bash
# 전통적인 방식
$ git push origin HEAD:refs/for/main

# git review 방식 (더 간단!)
$ git review
```

**내부 동작:**
- 현재 브랜치의 커밋을 Gerrit에 push
- `refs/for/main`으로 자동 변환
- Commit-msg hook으로 Change-ID 자동 생성

### 특정 브랜치로 리뷰 요청

기본적으로 git review는 main 브랜치를 대상으로 합니다. 다른 브랜치로 리뷰를 요청하려면 브랜치 이름을 인자로 전달하면 됩니다.

```bash
# main 브랜치로 리뷰 요청
$ git review main

# develop 브랜치로 리뷰 요청
$ git review develop

# feature 브랜치로 리뷰 요청
$ git review feature/new-feature
```

### 리뷰 다운로드

`git review -d` 명령어를 사용하면 Gerrit의 특정 Change를 로컬로 다운로드할 수 있습니다. 이는 다른 사람의 변경 사항을 로컬에서 테스트해볼 때 유용합니다.

```bash
# Change 123의 최신 Patch Set 다운로드
$ git review -d 123

# 특정 Patch Set 다운로드 (PS2)
$ git review -d 123,2

# 다운로드 결과
$ git branch
* review/alice/123   # 자동 생성된 리뷰 브랜치
  main
  feature/login
```

### 완료된 리뷰 브랜치 정리

리뷰가 완료된 후에는 불필요한 로컬 브랜치를 정리하는 것이 좋습니다.

```bash
# 리뷰 완료 후 로컬 리뷰 브랜치 삭제
$ git review -x

# 또는
$ git branch -D review/alice/123
```

## git review 고급 사용법

지금까지 기본 명령어를 알아보았습니다. 다음으로 더 다양한 상황에서 활용할 수 있는 고급 사용법을 살펴보겠습니다.

### WIP (Work In Progress)

```bash
# 아직 작업 중인 변경
$ git review -D
# = git push origin HEAD:refs/for/main%wip
```

### 리뷰어 지정

```bash
# 리뷰어 직접 지정
$ git review -r "alice@example.com"
$ git review --reviewer "alice@example.com"

# 여러 리뷰어
$ git review -r "alice@example.com,bob@example.com"
```

### 특정 주제(topic) 설정

```bash
# topic을 login으로 설정
$ git review -t login
# = gerrit UI에서 같은 topic의 Change들이 그룹화됨
```

### 여러 커밋을 하나의 Change로 squash

```bash
# 최근 3개의 커밋을 하나의 리뷰로 제출
$ git review --no-rebase
# 또는 squash 후
$ git reset --soft HEAD~3
$ git commit -m "하나의 변경으로 통합"
$ git review
```

## git review 실제 워크플로우

이제 실제 개발 현장에서 git review를 어떻게 활용하는지 전체 워크플로우를 살펴보겠습니다.

### 일일 개발 워크플로우

```bash
# 1. 최신 코드로 업데이트
$ git checkout main
$ git pull origin main

# 2. 기능 브랜치 생성
$ git checkout -b feature/search

# 3. 코드 작성 및 커밋 (여러 번)
$ echo "search input" > search.html
$ git add . && git commit -m "검색 입력 필드 추가"

$ echo "search function" > search.js
$ git add . && git commit -m "검색 기능 구현"

# 4. 리뷰 요청 (자동으로 refs/for/main 으로 push)
$ git review
Creating review for feature/search →
  https://gerrit.example.com/c/my-project/+/127
  https://gerrit.example.com/c/my-project/+/128
# 커밋 수만큼 Change 생성됨
```

### 리뷰 피드백 반영

```bash
# 리뷰어가 코멘트를 남김
# "검색어가 비었을 때 처리 필요"

# 1. 수정
$ vi search.js
# if (!query) return;  추가

# 2. 수정한 파일만 스테이징
$ git add search.js

# 3. 마지막 커밋 수정 (--amend)
$ git commit --amend --no-edit

# 4. 다시 리뷰 요청 (새 Patch Set 자동 생성)
$ git review
```

### 충돌 해결

```bash
# 리뷰 중에 main 브랜치가 업데이트되어 충돌 발생
$ git review
error: merge conflict in search.js

# 1. Rebase로 충돌 해결
$ git pull --rebase origin main
# 충돌 해결 후
$ git add search.js
$ git rebase --continue

# 2. 다시 리뷰 요청
$ git review
```

### 리뷰 완료 후 브랜치 정리

```bash
# 1. main으로 전환
$ git checkout main

# 2. 최신 코드 가져오기
$ git pull origin main

# 3. feature 브랜치 삭제
$ git branch -d feature/search

# 4. git review 임시 브랜치도 정리
$ git review -x
```

## git review 설정 파일

프로젝트별 설정을 `.gitreview` 파일에 저장할 수 있습니다. 이 파일이 있으면 매번 `git review -s`로 초기화할 필요가 없습니다.

```ini
# .gitreview
[gerrit]
host=gerrit.example.com
port=29418
project=my-project
defaultbranch=main
defaultrebase=0

# 설정 파일이 있으면 git review -s 없이 바로 사용 가능
$ git clone https://gerrit.example.com/my-project
$ cd my-project
$ git review  # .gitreview 설정 자동 로드!
```

## git review 팁과 트릭

### 자주 사용하는 옵션 모음

```bash
# 가장 간단하게
$ git review

# 리뷰어 지정
$ git review -r alice@example.com

# WIP
$ git review -D

# 특정 브랜치
$ git review develop

# 리베이스 후 리뷰
$ git review -R

# 도움말
$ git review --help
```

### 일반 git push vs git review 비교

```bash
# git push 방식
$ git push origin HEAD:refs/for/main%r=alice@example.com,topic=login

# git review 방식 (더 간결!)
$ git review -r alice@example.com -t login
```

### 여러 저장소에서 git review 사용

```bash
# 저장소마다 한 번씩만 설정
$ cd ~/projects/project-a
$ git review -s

$ cd ~/projects/project-b
$ git review -s

# 이후 모든 저장소에서 git review 사용 가능!
```

### 문제 해결

```bash
# "We don't know where your gerrit is" 오류
$ git remote add gerrit ssh://user@host:29418/project
$ git review -s

# "Change-ID missing" 오류
# commit-msg hook 누락
$ curl -Lo .git/hooks/commit-msg \
    http://gerrit.example.com/tools/hooks/commit-msg
$ chmod +x .git/hooks/commit-msg

# 이미 커밋한 경우 Change-ID 추가
$ git commit --amend
# :wq로 저장하면 hook이 자동으로 Change-ID 추가
```

## 한눈에 정리

| 개념 | 설명 |
|------|------|
| git review | Gerrit 작업을 간편하게 해주는 CLI 도구 |
| `git review` | 현재 브랜치의 커밋을 리뷰 요청 (refs/for/main) |
| `git review -s` | Gerrit 원격 저장소 초기화 |
| `git review -d <번호>` | 특정 Change 다운로드 |
| `git review -r <이메일>` | 리뷰어 지정 |
| `git review -t <주제>` | topic 설정 |
| `git review -D` | WIP 상태로 push |
| `.gitreview` | 프로젝트별 Gerrit 설정 파일 |

## 연습 문제

1. `git push origin HEAD:refs/for/main%r=alice@example.com,topic=login`과 동일한 동작을 하는 git review 명령어를 작성하시오.

2. git review를 사용하여 Change 456의 최신 Patch Set을 로컬로 다운로드하는 명령어를 작성하시오.

3. 리뷰 피드백을 반영한 후 `git review`를 실행하면 Gerrit에서 어떤 동작이 발생하는지 설명하시오.
