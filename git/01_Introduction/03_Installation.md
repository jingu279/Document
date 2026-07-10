# Git 설치

지금까지 우리는 Git이 무엇이고 왜 사용해야 하는지에 대해 배웠습니다. 이제 본격적으로 Git을 사용해보기 위한 첫걸음을 떼어보겠습니다. 아무리 훌륭한 도구라도 컴퓨터에 설치되어 있지 않다면 사용할 수 없습니다. 이 장에서는 각 운영 체제별로 Git을 설치하는 방법과 Git을 처음 사용하기 전에 반드시 설정해야 할 기본 환경 구성에 대해 알아보겠습니다.

## 학습 목표

- Windows, macOS, Linux 환경에서 Git을 설치하는 방법을 이해하고 실습할 수 있다.
- Git 설치 후 최초 설정(사용자 이름, 이메일)을 올바르게 구성할 수 있다.
- Git의 유용한 추가 설정(기본 브랜치명, alias 등)을 적용할 수 있다.

Git을 사용하기 위해서는 먼저 컴퓨터에 Git을 설치해야 합니다. 운영 체제별 설치 방법을 설명합니다.

## Windows

Windows 환경에서 Git을 설치하는 방법부터 알아보겠습니다. Windows 사용자는 Git Bash라는 편리한 터미널을 함께 설치할 수 있어, 리눅스 환경과 유사한 명령어 경험을 할 수 있습니다.

1.  [Git 공식 웹사이트](https://git-scm.com/download/win)에 방문합니다. 자동으로 Windows용 설치 파일 다운로드가 시작됩니다.
2.  다운로드받은 `.exe` 파일을 실행합니다.
3.  설치 마법사의 안내에 따라 기본 설정을 그대로 유지한 채로 설치를 진행합니다.
    *   **Git Bash**와 **Git GUI**가 함께 설치됩니다.
    *   Git Bash는 리눅스/유닉스 스타일의 명령어를 Windows에서 사용할 수 있게 해주는 터미널입니다.
4.  설치가 완료되면 `Git Bash`를 실행하여 Git 명령어가 정상적으로 동작하는지 확인합니다.

```bash
git --version
# 예시 출력: git version 2.40.0.windows.1
```

## macOS

다음으로 macOS 환경에서의 설치 방법을 알아보겠습니다. macOS 사용자는 Homebrew를 사용하거나 Xcode Command Line Tools를 설치하는 두 가지 방법 중 하나를 선택할 수 있습니다.

1.  **Homebrew를 사용하는 방법 (추천):**
    ```bash
    brew install git
    ```
2.  **Xcode Command Line Tools를 설치하는 방법:**
    ```bash
    xcode-select --install
    ```
3.  설치가 완료되면 터미널을 실행하여 확인합니다.
    ```bash
    git --version
    ```

## Linux (Ubuntu/Debian 계열)

마지막으로 Linux 환경에서의 설치 방법입니다. Linux는 패키지 관리자를 통해 간단히 Git을 설치할 수 있습니다.

1.  터미널을 열고 패키지 목록을 업데이트한 후 Git을 설치합니다.
    ```bash
    sudo apt update
    sudo apt install git
    ```
2.  설치 확인:
    ```bash
    git --version
    ```

## 최초 설정 (Git 환경 설정)

지금까지 각 운영 체제별로 Git을 설치하는 방법에 대해 알아보았습니다. 설치가 완료되었다면 이제 Git을 사용하기 위한 기본 환경을 구성할 차례입니다. Git을 처음 설치한 후에는 반드시 해야 할 작업이 있습니다. 바로 **사용자 정보를 등록**하는 것입니다.

Git을 설치한 후에는 반드시 사용자 이름과 이메일을 설정해야 합니다. 이 정보는 커밋할 때 기록됩니다.

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

설정이 잘 되었는지 확인하려면 다음 명령어를 사용합니다.
```bash
git config --list
```

`--global` 옵션은 현재 사용자의 모든 Git 저장소에 대해 이 설정을 기본값으로 사용하겠다는 의미입니다. 프로젝트별로 다른 이름이나 이메일을 사용하고 싶다면 해당 저장소 디렉토리에서 `--global` 옵션 없이 `git config` 명령어를 다시 실행하면 됩니다.

## 유용한 추가 설정

기본 설정을 마친 후에는 개발 환경에 맞게 Git을 더욱 편리하게 사용할 수 있는 다양한 추가 설정을 적용할 수 있습니다.

**기본 브랜치 이름 변경 (main으로):**
```bash
git config --global init.defaultBranch main
```

**색상 출력 활성화:**
```bash
git config --global color.ui auto
```

**라인 엔딩 처리 (Windows vs Mac/Linux 협업 시):**
```bash
# Windows
git config --global core.autocrlf true

# macOS / Linux
git config --global core.autocrlf input
```

**커밋 메시지용 기본 에디터 설정:**
```bash
git config --global core.editor "code --wait"     # VS Code
git config --global core.editor "vim"             # Vim
git config --global core.editor "nano"            # Nano
```

**Git 명령어 단축어 (alias) 설정:**
```bash
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --all"

# 이제 아래처럼 짧게 사용 가능!
$ git st    # = git status
$ git ci    # = git commit
$ git lg    # = git log --oneline --graph --all
```

**설정 확인 예시:**
```bash
$ git config --list
user.name=홍길동
user.email=hong@example.com
init.defaultBranch=main
color.ui=auto
alias.st=status
alias.ci=commit

# 특정 설정만 확인
$ git config user.name
홍길동
```

## 한눈에 정리

| 구분 | 명령어 / 방법 | 설명 |
|------|--------------|------|
| **Windows 설치** | 공식 웹사이트에서 설치 파일 다운로드 | Git Bash, Git GUI 포함 |
| **macOS 설치** | `brew install git` 또는 `xcode-select --install` | Homebrew 또는 Xcode CLI 도구 |
| **Linux 설치** | `sudo apt install git` | 패키지 매니저 사용 |
| **최초 설정** | `git config --global user.name` / `user.email` | 커밋 작성자 정보 등록 |
| **추가 설정** | `init.defaultBranch`, `color.ui`, `core.autocrlf`, `alias.*` | 브랜치명, 색상, 줄바꿈, 단축키 등 |

## 연습 문제

1. 자신의 운영 체제에 맞는 Git 설치 방법을 순서대로 서술해보세요.
2. Git 설치 후 반드시 설정해야 하는 최초 설정 두 가지는 무엇이며, 왜 중요한지 설명해보세요.
3. `git config --global alias.lg "log --oneline --graph --all"` 명령어의 의미를 설명하고, 이 단축어(alias)를 사용하면 어떤 이점이 있는지 서술해보세요.
