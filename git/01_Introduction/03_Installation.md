# Git 설치

Git을 사용하기 위해서는 먼저 컴퓨터에 Git을 설치해야 합니다. 운영 체제별 설치 방법을 설명합니다.

## Windows

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
