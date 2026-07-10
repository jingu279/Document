# 용어 설명

Git을 처음 배울 때 가장 큰 장벽 중 하나는 생소한 용어들입니다. 이 장에서는 Git을 사용하면서 자주 접하게 되는 주요 용어들을 한글 자모순으로 정리하여, 필요할 때마다 빠르게 의미를 확인할 수 있도록 구성하였습니다. 각 용어는 실제 사용 예시와 함께 설명되어 있으므로, 단순 암기보다는 문맥 속에서 이해하는 데 도움이 될 것입니다.

> **⚠️ 경고:** AI가 생성한 문서입니다. 내용에 부정확한 정보가 포함될 수 있으므로, 학습 시 공식 문서를 함께 참고하세요.

## 학습 목표

- Git의 핵심 용어와 개념을 이해하고 설명할 수 있다
- 각 용어에 대응하는 실제 Git 명령어를 익힌다
- 용어 간의 관계(예: 스테이징 → 커밋 → 푸시)를 이해한다

## ㄱ

- **Git (깃):** 분산형 버전 관리 시스템. 파일의 변경 이력을 추적하고 여러 개발자 간의 협업을 돕는 도구입니다.
  ```bash
  $ git --version
  git version 2.40.0
  ```
- **GitHub (깃허브):** Git 저장소를 호스팅하는 웹 서비스. 협업, 코드 리뷰, 이슈 트래킹 등의 기능을 제공합니다.
  ```
  https://github.com/username/project
  ```

## ㄸ

- **Detached HEAD:** HEAD가 특정 브랜치가 아닌, 과거의 특정 커밋을 직접 가리키고 있는 상태.
  ```bash
  $ git checkout a1b2c3d  # Detached HEAD 상태 진입
  $ git log --oneline -1
  a1b2c3d (HEAD) 과거 커밋  # (main)이 없음!
  ```

## ㅂ

- **브랜치 (Branch):** 코드의 독립적인 작업 흐름을 나타내는 포인터.
  ```bash
  $ git branch feature/login   # 새 브랜치 생성
  $ git switch feature/login   # 브랜치 전환
  ```
- **병합 (Merge):** 두 브랜치의 변경 사항을 하나로 합치는 작업.
  ```bash
  $ git switch main && git merge feature/login
  ```

## ㅅ

- **스테이징 영역 (Staging Area / Index):** 커밋을 준비하는 중간 영역.
  ```bash
  $ git add index.html   # 스테이징 영역에 추가
  $ git status           # 'Changes to be committed' 확인
  ```

## ㅇ

- **원격 저장소 (Remote Repository):** 인터넷이나 네트워크 상에 있는 Git 저장소.
  ```bash
  $ git remote -v
  origin  https://github.com/me/repo.git (fetch)
  ```
- **워킹 디렉토리 (Working Directory):** 현재 작업 중인 실제 파일들이 있는 디렉토리.
  ```bash
  $ ls -la   # 현재 작업 중인 파일들
  ```

## ㅋ

- **커밋 (Commit):** Git 저장소에 변경 사항을 기록하는 행위.
  ```bash
  $ git commit -m "로그인 버그 수정"
  ```
- **커밋 메시지 (Commit Message):** 커밋할 때 변경 사항에 대한 설명.
  ```bash
  $ git log --oneline
  a1b2c3d 로그인 버그 수정   # ← 이 부분이 커밋 메시지
  ```
- **클론 (Clone):** 원격 저장소를 로컬 컴퓨터로 복사.
  ```bash
  $ git clone https://github.com/facebook/react.git
  # react/ 디렉토리가 생성됨
  ```

## ㅌ

- **태그 (Tag):** 특정 커밋에 이름표를 붙이는 기능. 주로 버전 릴리스에 사용.
  ```bash
  $ git tag v1.0.0          # 현재 커밋에 v1.0.0 태그
  $ git tag -a v2.0.0 -m "릴리스 v2.0.0"  # 주석 태그
  $ git push origin --tags  # 태그를 원격에 푸시
  ```

## ㅍ

- **푸시 (Push):** 로컬 저장소 → 원격 저장소로 업로드.
  ```bash
  $ git push origin main
  ```
- **풀 (Pull):** 원격 저장소 → 로컬 저장소로 가져오기 + 병합.
  ```bash
  $ git pull origin main   # = git fetch + git merge
  ```
- **페치 (Fetch):** 원격 저장소 → 로컬 저장소로 가져오기만.
  ```bash
  $ git fetch origin
  $ git diff main origin/main   # 변경 사항 확인 후
  $ git merge origin/main       # 수동 병합
  ```

## ㅎ

- **HEAD:** 현재 작업 중인 브랜치의 가장 최신 커밋을 가리키는 포인터.
  ```bash
  $ cat .git/HEAD
  ref: refs/heads/main     # 현재 main 브랜치에 있음
  ```
- **해시 (Hash):** Git에서 각 커밋을 식별하는 고유 40자리 16진수.
  ```bash
  $ git log --oneline
  a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0 로그인 버그 수정
  # 앞 7자리(a1b2c3d)만 사용해도 충분히 고유함
  ```

## ㅊ

- **체크아웃 (Checkout):** 브랜치 전환 또는 파일 복원.
  ```bash
  $ git checkout main          # 브랜치 전환
  $ git checkout -- app.js     # 파일 복원
  ```
  (Git 2.23+에서는 `git switch`와 `git restore`로 분리됨)

## 충돌 관련 용어

- **충돌 (Conflict):** 병합 시 같은 파일의 같은 부분이 다르게 수정된 상태.
  ```bash
  $ git merge feature/login
  CONFLICT in index.html   # 충돌 발생!
  # 수동으로 해결 후 git add + git commit
  ```
- **Fast-Forward 병합:** 브랜치 포인터만 앞으로 이동.
  ```mermaid
  gitGraph
     commit id: "D"
     commit id: "E"
     branch feature
     checkout feature
     commit id: "A"
     commit id: "B"
     checkout main
     merge feature
  ```
- **3-Way 병합:** 공통 조상을 기준으로 새 병합 커밋 생성.
  ```mermaid
  gitGraph
     commit id: "D"
     commit id: "E"
     commit id: "F"
     branch feature
     checkout feature
     commit id: "A"
     commit id: "B"
     checkout main
     merge feature id: "G"
  ```

## ㅅ (추가)

- **스태시 (Stash):** 작업 중인 변경 사항을 임시로 저장.
  ```bash
  $ git stash                # 현재 변경 사항 저장
  $ git switch other-branch  # 다른 브랜치로 이동
  $ git switch main
  $ git stash pop            # 저장한 변경 사항 복원
  ```

## 한눈에 정리

| 용어 | 영어 | 설명 | 주요 명령어 |
|------|------|------|------------|
| 깃 | Git | 분산형 버전 관리 시스템 | `git --version` |
| 깃허브 | GitHub | Git 저장소 호스팅 웹 서비스 | - |
| 브랜치 | Branch | 독립적인 작업 흐름 | `git branch`, `git switch` |
| 병합 | Merge | 두 브랜치 변경 사항 통합 | `git merge` |
| 스테이징 영역 | Staging Area | 커밋 준비 중간 영역 | `git add` |
| 원격 저장소 | Remote | 네트워크 상의 Git 저장소 | `git remote` |
| 커밋 | Commit | 변경 사항 기록 | `git commit` |
| 클론 | Clone | 원격 저장소 로컬 복사 | `git clone` |
| 태그 | Tag | 커밋에 이름표 부착 | `git tag` |
| 푸시 | Push | 로컬 → 원격 업로드 | `git push` |
| 풀 | Pull | 원격 → 로컬 가져오기 + 병합 | `git pull` |
| 페치 | Fetch | 원격 → 로컬 가져오기만 | `git fetch` |
| HEAD | - | 현재 작업 중인 브랜치 최신 커밋 | `cat .git/HEAD` |
| 해시 | Hash | 커밋 식별 40자리 16진수 | `git log` |
| 체크아웃 | Checkout | 브랜치 전환 / 파일 복원 | `git checkout` |
| 충돌 | Conflict | 병합 시 같은 부분 다르게 수정 | - |
| 스태시 | Stash | 변경 사항 임시 저장 | `git stash` |
