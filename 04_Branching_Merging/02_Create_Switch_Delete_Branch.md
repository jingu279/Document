# 브랜치 생성, 전환 및 삭제

브랜치를 자유자재로 다루는 것은 Git 사용의 핵심입니다. 이 문서에서는 브랜치를 생성하고, 다른 브랜치로 전환하며, 불필요한 브랜치를 삭제하는 방법을 배웁니다.

## 1. 브랜치 목록 확인: `git branch`

현재 저장소에 있는 모든 브랜치의 목록을 확인합니다.

```bash
git branch
```

**출력 예시:**
```
* main
  feature/login
  feature/payment
```

`*` 표시가 된 브랜치가 현재 작업 중인 브랜치입니다.

**브랜치 목록 자세히 보기:**
```bash
$ git branch -v              # 브랜치 + 마지막 커밋 메시지
* main        a1b2c3d [최신] README 업데이트
  feature/x   d4e5f6f 로그인 기능 구현
  feature/y   g7h8i9j 결제 모듈 추가

$ git branch -vv             # 추적 브랜치 정보까지
* main        a1b2c3d [origin/main] README 업데이트
  feature/x   d4e5f6f [origin/feature/x: ahead 2] 로그인 기능 구현

$ git branch -r              # 원격 브랜치만
  origin/main
  origin/develop
  origin/feature/x

$ git branch -a              # 로컬 + 원격 모든 브랜치
* main
  feature/x
  remotes/origin/main
  remotes/origin/develop
```

## 2. 새 브랜치 생성: `git branch <이름>`

```bash
git branch feature/readme-update
```

이 명령어는 현재 커밋 위치를 기준으로 새 브랜치를 생성합니다. 브랜치를 생성만 할 뿐, 현재 작업 브랜치가 자동으로 전환되지는 않습니다.

## 3. 브랜치 전환: `git switch` (또는 `git checkout`)

다른 브랜치로 이동하여 작업하려면 브랜치를 전환합니다.

**`git switch` 사용 (Git 2.23+ 버전에서 권장):**
```bash
git switch feature/readme-update
```

**`git checkout` 사용 (전통적인 방법):**
```bash
git checkout feature/readme-update
```

## 4. 브랜치 생성과 동시에 전환

**`git switch -c` 사용 (권장):**
```bash
git switch -c feature/new-function
```

**`git checkout -b` 사용:**
```bash
git checkout -b feature/new-function
```

**브랜치 이름 짓는 규칙 예시:**
```bash
# 기능 개발
git switch -c feature/login-page         # 새로운 로그인 페이지
git switch -c feature/user-profile       # 사용자 프로필 기능

# 버그 수정
git switch -c hotfix/crash-on-login      # 로그인 시 크래시 버그
git switch -c hotfix/typo-in-readme      # README 오타 수정

# 실험/리팩토링
git switch -c refactor/database-layer    # DB 계층 리팩토링
git switch -c experiment/new-algorithm   # 새 알고리즘 실험
```

## 5. 브랜치 삭제: `git branch -d <이름>`

더 이상 필요하지 않은 브랜치는 삭제할 수 있습니다.

```bash
git branch -d feature/readme-update
```

**참고:** 현재 작업 중인 브랜치는 삭제할 수 없습니다. 다른 브랜치로 전환한 후 삭제해야 합니다.

**강제 삭제 (`-D`):** 병합되지 않은 브랜치라도 강제로 삭제하려면 대문자 `-D` 옵션을 사용합니다.

```bash
git branch -D feature/abandoned-work
```

## 6. 원격 브랜치 관련 명령어

로컬 브랜치 작업을 원격 저장소에 반영하려면 `git push`를 사용합니다.

```bash
# 로컬 브랜치를 원격에 푸시 (원격에 같은 이름의 브랜치 생성)
git push origin feature/login

# 로컬 브랜치를 삭제하고 원격 브랜치도 삭제하려면
git push origin --delete feature/login
```

## 실습 예제: 브랜치 만들고 전환하기

```bash
# 현재 브랜치 확인
git branch
* main

# 새 브랜치 생성
git branch experiment

# 브랜치 목록 확인 (experiment가 생성됨)
git branch
  experiment
* main

# experiment 브랜치로 전환
git switch experiment

# experiment 브랜치에서 파일 수정 후 커밋
echo "실험적인 코드" >> test.txt
git add test.txt
git commit -m "experiment 브랜치에서 작업"

# 다시 main 브랜치로 전환 (test.txt 파일이 사라진 것처럼 보임)
git switch main
```

이렇게 브랜치 전환 시 작업 디렉토리의 파일 내용이 해당 브랜치의 마지막 커밋 상태로 변경됩니다. 이것이 브랜치의 핵심 동작 방식입니다.

## 브랜치 전환 시 주의할 점

```bash
# ⚠️ 커밋하지 않은 변경 사항이 있으면 브랜치 전환이 거부될 수 있음
$ git switch feature/login
error: Your local changes to the following files would be overwritten by checkout:
    index.html
Please commit your changes or stash them before you switch branches.

# 해결 방법 1: 변경 사항 커밋
$ git add . && git commit -m "임시 저장"

# 해결 방법 2: stash (변경 사항을 임시 보관)
$ git stash
Saved working directory and index state WIP on main: a1b2c3d...

$ git switch feature/login  # 이제 가능!

# stash 복원
$ git stash pop
```

## 실습 예제: 로그인 기능 개발 시나리오

```bash
# 1. main 브랜치에서 시작
git switch main

# 2. 로그인 기능 개발 브랜치 생성
git switch -c feature/login
# (여기서 로그인 기능 구현...)
echo "<form>Login</form>" > login.html
git add . && git commit -m "로그인 폼 추가"

# 3. 긴급 버그 발견! main으로 돌아가기
git switch main
# (버그 수정 브랜치 생성)
git switch -c hotfix/critical-bug
echo "버그 수정" > fix.txt
git add . && git commit -m "긴급 버그 수정"

# 4. 버그 수정 완료, main에 병합
git switch main
git merge hotfix/critical-bug
git branch -d hotfix/critical-bug

# 5. 다시 로그인 기능 개발로 복귀
git switch feature/login
echo "<button>Submit</button>" >> login.html
git add . && git commit -m "로그인 버튼 추가"

# 6. 로그인 기능 완료, main에 병합
git switch main
git merge feature/login
git branch -d feature/login
```
