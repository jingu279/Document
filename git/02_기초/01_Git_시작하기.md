# Git 시작하기: 초기화 및 클론

버전 관리를 시작하려면 먼저 Git 저장소를 만들어야 합니다. 이 장은 Git을 사용하는 모든 작업의 출발점이 되는 핵심 과정입니다. 우리는 이 장에서 Git 저장소를 시작하는 두 가지 방법을 배웁니다: 처음부터 새로 시작하는 **초기화 (init)**와 기존 저장소를 복사해 오는 **클론 (clone)**입니다.


## 학습 목표

- Git 저장소를 새로 생성하는 `git init` 명령어의 사용법을 이해합니다
- 원격 저장소를 로컬로 복사하는 `git clone` 명령어의 사용법을 이해합니다
- `git init`과 `git clone`의 차이점과 각각의 적절한 사용 상황을 구분할 수 있습니다
- `.git` 디렉토리의 구조와 역할을 설명할 수 있습니다

**Init vs Clone 개념도:**

```mermaid
flowchart TB
  subgraph Init[git init - 처음부터 시작]
    I1["내 컴퓨터<br/>my-project/ (빈 폴더)"] --> I2["내 컴퓨터<br/>.git/ 폴더 생성"]
    I2 --> I3["💡 내가 처음부터 만들래!"]
  end

  subgraph Clone[git clone - 기존 저장소 복사]
    C1["GitHub<br/>원격 저장소<br/>C1-C2-C3"] -->|"git clone URL"| C2["내 컴퓨터<br/>my-project/<br/>C1-C2-C3 + .git/ 자동 설정"]
    C2 --> C3["💡 다른 사람이 만든 걸 가져올래!"]
  end
```

## 1. `git init` — 새로운 Git 저장소 만들기

로컬 컴퓨터에서 새로운 프로젝트를 시작할 때 `git init`을 사용합니다. 이 명령어는 프로젝트 디렉토리를 Git 저장소로 초기화하는 역할을 합니다.

**사용 방법:**

```bash
# 새 프로젝트 디렉토리를 만들고 이동합니다.
mkdir my-first-project
cd my-first-project

# 현재 디렉토리를 Git 저장소로 초기화합니다.
git init
```

`git init` 명령어를 실행하면 해당 디렉토리에 `.git`이라는 숨김 폴더가 생성됩니다. 이 폴더에는 버전 관리에 필요한 모든 메타데이터와 데이터가 저장됩니다. 우리는 이 `.git` 폴더 덕분에 이후 모든 Git 명령어를 사용할 수 있게 됩니다.

**출력 예시:**
```
Initialized empty Git repository in /Users/username/my-first-project/.git/
```

**`.git` 디렉토리 구조:**
```bash
$ ls -la my-first-project/.git/
drwxr-xr-x    HEAD                    # 현재 HEAD가 가리키는 브랜치
drwxr-xr-x    config                  # 저장소 설정 파일
drwxr-xr-x    description             # 저장소 설명
drwxr-xr-x    hooks/                  # Git 훅 스크립트
drwxr-xr-x    info/                   # 추가 정보
drwxr-xr-x    objects/                # 모든 데이터 (커밋, 파일 등)
drwxr-xr-x    refs/                   # 브랜치, 태그 참조

$ cat my-first-project/.git/HEAD
ref: refs/heads/main
```

**`git init`의 다양한 옵션:**

```bash
# 기본 브랜치 이름을 main으로 초기화 (기본값과 동일)
git init --initial-branch=main

# 빈 디렉토리만 생성 (작업 트리 없음, 서버용)
git init --bare

# 기존 디렉토리를 Git 저장소로 만들기
$ cd /home/user/existing-project
$ git init
$ git add .
$ git commit -m "기존 프로젝트 Git 초기화"
```

지금까지 `git init`을 사용하여 로컬에서 새로운 저장소를 만드는 방법에 대해 배웠습니다. 다음으로는 원격에 존재하는 저장소를 내 컴퓨터로 가져오는 `git clone`에 대해 알아보겠습니다.

## 2. `git clone` — 기존 저장소 복사하기

GitHub, GitLab, Bitbucket 등 원격 저장소에 있는 프로젝트를 내 컴퓨터로 복사할 때 `git clone`을 사용합니다. 원격 저장소의 전체 이력과 모든 파일을 가져오기 때문에, 우리는 즉시 그 프로젝트의 모든 버전을 열람하고 작업할 수 있습니다.

**사용 방법:**

```bash
git clone <저장소_주소>
```

**출력 예시:**
```bash
$ git clone https://github.com/username/example-repo.git
```

```
Cloning into 'example-repo'...
remote: Enumerating objects: 45, done.
remote: Counting objects: 100% (45/45), done.
remote: Total 45 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (45/45), 12.34 KiB | 2.47 MiB/s, done.
Resolving deltas: 100% (5/5), done.
```

**`git clone`의 다양한 활용:**

```bash
# 1. 디렉토리 이름을 지정해서 클론
$ git clone https://github.com/username/example-repo.git my-folder
Cloning into 'my-folder'...

# 2. 특정 브랜치만 클론 (깊이 제한, 빠른 다운로드)
$ git clone --branch develop https://github.com/username/example-repo.git

# 3. 최근 1개의 커밋만 가져오기 (shallow clone, 대규모 프로젝트에 유용)
$ git clone --depth 1 https://github.com/username/large-project.git

# 4. SSH로 클론 (비밀번호 없이 push 가능)
$ git clone git@github.com:username/example-repo.git

# 5. 특정 태그 버전 클론
$ git clone --branch v2.0.0 https://github.com/username/example-repo.git
```

**클론 후 확인:**
```bash
$ cd example-repo
$ git remote -v
origin  https://github.com/username/example-repo.git (fetch)
origin  https://github.com/username/example-repo.git (push)

$ git branch -a
* main
  remotes/origin/main
  remotes/origin/develop

$ git log --oneline -3
a1b2c3d README 업데이트
d4e5f6f 첫 번째 릴리스 준비
g7h8i9j 프로젝트 초기화
```

## 3. 두 방법의 차이점

지금까지 `git init`과 `git clone`이라는 두 가지 저장소 생성 방법을 배웠습니다. 이 두 방법의 차이점을 한눈에 비교해보겠습니다.

```mermaid
flowchart LR
  Init["<b>git init</b><br/>새로운 프로젝트를 시작할 때 사용<br/>로컬에서 처음부터 모든 것을 만듦<br/>원격 저장소와 자동으로 연결되지 않음"]
  Clone["<b>git clone</b><br/>기존 프로젝트에 참여할 때 사용<br/>원격 저장소에서 코드를 가져옴<br/>원격 저장소와 자동으로 연결됨 (origin)"]
```

`git init`으로 생성한 저장소는 나중에 `git remote add` 명령어를 통해 원격 저장소와 연결할 수 있습니다.

## 4. 실습: 처음부터 끝까지 따라하기

이제 배운 내용을 실제로 실습해보겠습니다. 다음 명령어를 터미널에서 직접 따라 입력하면서 각 단계에서 어떤 일이 일어나는지 확인하시기 바랍니다.

```bash
# 1. 프로젝트 폴더 생성 및 초기화
$ mkdir my-awesome-app
$ cd my-awesome-app
$ git init
Initialized empty Git repository in /Users/me/my-awesome-app/.git/

# 2. 첫 파일 만들기
$ echo "# My Awesome App" > README.md
$ git status
On branch main
Untracked files:
    README.md

# 3. 첫 커밋
$ git add README.md
$ git commit -m "프로젝트 초기화: README 추가"
[main (root-commit) a1b2c3d] 프로젝트 초기화: README 추가
 1 file changed, 1 insertion(+)

# 4. GitHub에서 새 저장소를 만들고 연결
$ git remote add origin https://github.com/me/my-awesome-app.git

# 5. 원격에 푸시
$ git push -u origin main
```

## 한눈에 정리

| 명령어 | 사용 상황 | 원격 저장소 연결 | 저장소 이력 |
|--------|----------|-----------------|------------|
| `git init` | 새로운 프로젝트를 로컬에서 시작할 때 | 자동 연결되지 않음 (`git remote add` 필요) | 없음 (빈 저장소) |
| `git clone` | 기존 원격 저장소를 복사할 때 | 자동으로 `origin`으로 연결됨 | 원격 저장소의 전체 이력을 그대로 가져옴 |

## 연습 문제

1. `git init`과 `git clone`의 가장 큰 차이점은 무엇인지 서술하시오.
2. `git init` 명령어를 실행한 후 생성되는 `.git` 디렉토리의 역할은 무엇인지 설명하시오.
3. `git clone --depth 1` 옵션은 어떤 상황에서 유용하게 사용할 수 있는지 그 이유와 함께 서술하시오.
