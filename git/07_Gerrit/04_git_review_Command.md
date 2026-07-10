# git review 명령어 사용법

`git review`는 Gerrit 작업을 더 편리하게 해주는 명령줄 도구입니다. 복잡한 `refs/for/main` 문법 대신 간단한 명령어로 Gerrit과 상호작용할 수 있습니다.

## git review 설치

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

### 리뷰 요청 (Push)

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

```bash
# main 브랜치로 리뷰 요청
$ git review main

# develop 브랜치로 리뷰 요청
$ git review develop

# feature 브랜치로 리뷰 요청
$ git review feature/new-feature
```

### 리뷰 다운로드

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

```bash
# 리뷰 완료 후 로컬 리뷰 브랜치 삭제
$ git review -x

# 또는
$ git branch -D review/alice/123
```

## git review 고급 사용법

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

프로젝트별 설정을 `.gitreview` 파일에 저장할 수 있습니다.

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
