# Git 설치

지금까지 우리는 Git이 무엇이고 왜 사용해야 하는지에 대해 배웠습니다. 이제 본격적으로 Git을 사용해보기 위한 첫걸음을 떼어보겠습니다. 아무리 훌륭한 도구라도 컴퓨터에 설치되어 있지 않다면 사용할 수 없습니다. 이 장에서는 각 운영 체제별로 Git을 설치하는 방법과 Git을 처음 사용하기 전에 반드시 설정해야 할 기본 환경 구성에 대해 알아보겠습니다.

👨‍💻 **실전 프로젝트: Git 설치 확인하기**

이론적인 설치 방법을 배우는 것도 중요하지만, 실제로 Git이 여러분의 컴퓨터에 제대로 설치되어 있는지 확인하는 것이 첫 번째 실습입니다. 지금부터 터미널(또는 명령 프롬프트)을 열고 다음과 같이 입력해 보시기 바랍니다. Git이 이미 설치되어 있다면 버전 정보가 출력될 것이고, 설치되어 있지 않다면 바로 설치 방법을 따라 하면 됩니다.

```bash
# 1. Git이 이미 설치되어 있는지 확인합니다
$ git --version

# 만약 설치되어 있지 않다면, 아래 메시지와 유사한 오류가 출력됩니다
# 'git'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는
# 배치 파일이 아닙니다.

# 2. Git 설치가 확인되면, 사용자 정보를 등록합니다
#    (이 정보는 모든 커밋에 기록되므로 반드시 정확하게 입력해야 합니다)
$ git config --global user.name "홍길동"
$ git config --global user.email "hong@example.com"

# 3. 설정이 올바르게 저장되었는지 확인합니다
$ git config --list
user.name=홍길동
user.email=hong@example.com

# 4. Git이 정상 동작하는지 테스트해 봅니다
$ mkdir test-repo && cd test-repo
$ git init
$ echo "Git 설치 완료!" > README.md
$ git add README.md
$ git commit -m "Git 설치 확인 커밋"
$ git log --oneline
```

이제 Git이 정상적으로 설치되었고 기본 설정도 완료되었습니다. 축하합니다! 여러분은 이제 Git을 사용할 준비를 마쳤습니다. 이어서 각 운영 체제별로 Git을 설치하는 구체적인 방법을 알아보겠습니다.

## 학습 목표

- Windows, macOS, Linux 환경에서 Git을 설치하는 방법을 이해하고 실습할 수 있다.
- Git 설치 후 최초 설정(사용자 이름, 이메일)을 올바르게 구성할 수 있다.
- Git의 유용한 추가 설정(기본 브랜치명, alias 등)을 적용할 수 있다.

Git을 사용하기 위해서는 먼저 컴퓨터에 Git을 설치해야 합니다. 운영 체제별 설치 방법을 설명합니다.

각 운영 체제마다 설치 방법은 다르지만, 한 가지 공통점이 있습니다. 모든 방법은 Git 공식 웹사이트나 해당 OS의 패키지 관리자를 통해 이루어집니다. 자신의 운영 체제에 맞는 방법을 선택하여 진행하면 됩니다. 만약 여러 운영 체제를 함께 사용한다면(예를 들어, 회사에서는 Windows, 집에서는 macOS), 각 환경에 맞는 설치 방법을 모두 알아 두는 것이 좋습니다.

## Windows

Windows 환경에서 Git을 설치하는 방법부터 알아보겠습니다. Windows 사용자는 Git Bash라는 편리한 터미널을 함께 설치할 수 있어, 리눅스 환경과 유사한 명령어 경험을 할 수 있습니다.

Windows에서 Git을 설치하는 가장 간단한 방법은 공식 웹사이트에서 설치 파일을 다운로드하는 것입니다. 설치 과정에서 다양한 옵션을 선택할 수 있지만, 초보자라면 기본 설정을 그대로 사용하는 것을 권장합니다. 특히 주목할 점은 Git Bash의 포함 여부입니다. Git Bash는 Windows에서 리눅스 스타일의 명령어(예: `ls`, `grep`, `sed` 등)를 사용할 수 있게 해 주는 에뮬레이터로, Git을 훨씬 편리하게 다룰 수 있도록 도와줍니다. 또한 Git 설치 과정에서 줄 바꿈(Line Ending) 처리 방식에 대한 옵션이 나타나는데, 이는 Windows와 macOS/Linux 간의 협업 시 매우 중요한 설정입니다.

1.  [Git 공식 웹사이트](https://git-scm.com/download/win)에 방문합니다. 자동으로 Windows용 설치 파일 다운로드가 시작됩니다.
2.  다운로드받은 `.exe` 파일을 실행합니다.
3.  설치 마법사의 안내에 따라 기본 설정을 그대로 유지한 채로 설치를 진행합니다.
    *   **Git Bash**와 **Git GUI**가 함께 설치됩니다.
    *   Git Bash는 리눅스/유닉스 스타일의 명령어를 Windows에서 사용할 수 있게 해주는 터미널입니다.
4.  설치가 완료되면 `Git Bash`를 실행하여 Git 명령어가 정상적으로 동작하는지 확인합니다.

설치 과정 중간에 "Choosing the default editor" 화면이 나타나면, 기본 에디터로 VS Code나 Nano 등을 선택할 수 있습니다. 이후 "Adjusting your PATH environment" 화면에서는 "Git from the command line and also from 3rd-party software" 옵션을 선택하면 일반 명령 프롬프트(cmd)에서도 git 명령어를 사용할 수 있게 됩니다.

```bash
git --version
# 예시 출력: git version 2.40.0.windows.1
```

## macOS

다음으로 macOS 환경에서의 설치 방법을 알아보겠습니다. macOS 사용자는 Homebrew를 사용하거나 Xcode Command Line Tools를 설치하는 두 가지 방법 중 하나를 선택할 수 있습니다.

macOS는 유닉스 기반의 운영 체제이므로, Windows보다 Git과의 호환성이 더 좋습니다. Homebrew는 macOS에서 가장 널리 사용되는 패키지 관리자로, 터미널 한 줄이면 Git 설치가 완료됩니다. Xcode Command Line Tools를 설치하는 방법은 Apple이 공식적으로 제공하는 도구들을 함께 설치할 수 있다는 장점이 있습니다. 두 방법 모두 장단점이 있으므로, 자신의 환경에 맞는 방법을 선택하면 됩니다.

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

Homebrew를 사용할 때는 먼저 Homebrew 자체가 설치되어 있어야 합니다. Homebrew가 설치되어 있지 않다면, [brew.sh](https://brew.sh)에 방문하여 설치 명령어를 확인한 후 먼저 Homebrew를 설치하시기 바랍니다.

## Linux (Ubuntu/Debian 계열)

마지막으로 Linux 환경에서의 설치 방법입니다. Linux는 패키지 관리자를 통해 간단히 Git을 설치할 수 있습니다.

Linux는 다양한 배포판이 있지만, 가장 널리 사용되는 Ubuntu/Debian 계열을 기준으로 설명합니다. Linux 사용자에게는 터미널과 패키지 관리자가 이미 익숙할 것이므로, 설치 과정이 가장 간단합니다. 패키지 관리자를 사용하면 Git의 최신 안정 버전이 자동으로 설치되며, 보안 업데이트도 시스템 업데이트와 함께 자동으로 관리됩니다.

1.  터미널을 열고 패키지 목록을 업데이트한 후 Git을 설치합니다.
    ```bash
    sudo apt update
    sudo apt install git
    ```
2.  설치 확인:
    ```bash
    git --version
    ```

`sudo apt update` 명령어는 패키지 목록을 최신 상태로 갱신하는 역할을 합니다. 이 단계를 건너뛰면 이전 버전의 Git이 설치되거나 설치 자체가 실패할 수 있으므로, 반드시 먼저 실행해야 합니다. Fedora나 CentOS와 같은 Red Hat 계열 배포판을 사용한다면, `sudo dnf install git`(Fedora) 또는 `sudo yum install git`(CentOS) 명령어를 사용하면 됩니다.

## 최초 설정 (Git 환경 설정)

지금까지 각 운영 체제별로 Git을 설치하는 방법에 대해 알아보았습니다. 설치가 완료되었다면 이제 Git을 사용하기 위한 기본 환경을 구성할 차례입니다. Git을 처음 설치한 후에는 반드시 해야 할 작업이 있습니다. 바로 **사용자 정보를 등록**하는 것입니다.

Git을 설치한 후에는 반드시 사용자 이름과 이메일을 설정해야 합니다. 이 정보는 커밋할 때 기록됩니다.

이 설정이 중요한 이유는 Git의 모든 커밋에 작성자 정보가 포함되기 때문입니다. 만약 이 설정을 건너뛰면 Git은 커밋을 허용하지 않거나, 시스템의 기본 사용자 정보를 사용하게 되어 나중에 누가 어떤 작업을 했는지 추적하기 어려워집니다. 특히 팀 프로젝트에서 이메일 주소는 GitHub와 같은 원격 저장소에서 기여자(Contributor)를 식별하는 중요한 기준이 됩니다. 잘못된 이메일을 등록하면 여러분의 커밋이 프로필에 연결되지 않을 수 있으므로 주의해야 합니다.

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

설정이 잘 되었는지 확인하려면 다음 명령어를 사용합니다.
```bash
git config --list
```

`--global` 옵션은 현재 사용자의 모든 Git 저장소에 대해 이 설정을 기본값으로 사용하겠다는 의미입니다. 프로젝트별로 다른 이름이나 이메일을 사용하고 싶다면 해당 저장소 디렉토리에서 `--global` 옵션 없이 `git config` 명령어를 다시 실행하면 됩니다.

예를 들어, 회사 프로젝트에서는 회사 이메일을 사용하고, 개인 프로젝트에서는 개인 이메일을 사용하고 싶다면 해당 프로젝트 디렉토리에서 `--global` 옵션 없이 `git config user.name`과 `git config user.email`을 다시 설정하면 됩니다. 이렇게 하면 글로벌 설정보다 로컬 설정이 우선 적용됩니다. Git의 설정은 `--local`(기본값, 프로젝트 단위), `--global`(사용자 단위), `--system`(시스템 전체)의 세 가지 범위(Scope)로 나뉘며, 좁은 범위의 설정이 넓은 범위의 설정보다 우선합니다.

## 유용한 추가 설정

기본 설정을 마친 후에는 개발 환경에 맞게 Git을 더욱 편리하게 사용할 수 있는 다양한 추가 설정을 적용할 수 있습니다.

이러한 추가 설정들은 필수 사항은 아니지만, 한 번 설정해 두면 Git 사용 경험이 크게 개선됩니다. 특히 alias(단축어) 설정은 Git을 매일 사용하는 개발자에게 거의 필수적인 설정입니다. 아래 설정들을 하나씩 적용하면서 자신의 개발 환경을 최적화해 보시기 바랍니다.

**기본 브랜치 이름 변경 (main으로):**
```bash
git config --global init.defaultBranch main
```

과거 Git의 기본 브랜치 이름은 `master`였습니다. 그러나 2020년 이후 GitHub를 비롯한 많은 플랫폼과 커뮤니티에서 `main`으로 변경하는 추세입니다. 이 설정을 적용하면 `git init`으로 저장소를 생성할 때 기본 브랜치 이름이 `main`이 됩니다.

**색상 출력 활성화:**
```bash
git config --global color.ui auto
```

이 설정을 활성화하면 `git status`, `git diff`, `git log` 등의 출력에 색상이 적용됩니다. 예를 들어, 수정된 파일은 빨간색, 추가된 파일은 초록색으로 표시되어 가독성이 크게 향상됩니다.

**라인 엔딩 처리 (Windows vs Mac/Linux 협업 시):**
```bash
# Windows
git config --global core.autocrlf true

# macOS / Linux
git config --global core.autocrlf input
```

운영 체제마다 줄 바꿈 문자(Line Ending)가 다릅니다. Windows는 `CRLF`(\\r\\n)를, macOS와 Linux는 `LF`(\\n)를 사용합니다. 이 차이로 인해 크로스 플랫폼 협업 시 불필요한 변경 사항이 발생할 수 있습니다. `core.autocrlf` 설정은 Git이 자동으로 줄 바꿈 문자를 변환하여 이러한 문제를 방지합니다.

**커밋 메시지용 기본 에디터 설정:**
```bash
git config --global core.editor "code --wait"     # VS Code
git config --global core.editor "vim"             # Vim
git config --global core.editor "nano"            # Nano
```

`git commit` 명령어를 -m 옵션 없이 실행하면 에디터가 열려 커밋 메시지를 작성하게 됩니다. 이때 사용할 기본 에디터를 지정할 수 있습니다. VS Code를 사용한다면 `code --wait` 옵션을 주어 VS Code가 커밋 메시지 작성을 마칠 때까지 터미널이 대기하도록 설정해야 합니다.

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

Alias 설정은 Git을 사용하는 효율성을 극적으로 향상시킵니다. 매일 수십 번씩 입력하는 명령어를 2~3글자로 줄임으로써 타이핑 시간을 절약하고 작업 흐름을 끊김 없이 유지할 수 있습니다. 위 예시 외에도 자신이 자주 사용하는 명령어를 자유롭게 alias로 등록할 수 있습니다.

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

이제 Git 설치와 기본 설정이 모두 완료되었습니다. 아래의 한눈에 정리 표를 통해 지금까지 배운 내용을 최종적으로 정리해 보겠습니다.

## 한눈에 정리

| 구분 | 명령어 / 방법 | 설명 |
|------|--------------|------|
| **Windows 설치** | 공식 웹사이트에서 설치 파일 다운로드 | Git Bash, Git GUI 포함 |
| **macOS 설치** | `brew install git` 또는 `xcode-select --install` | Homebrew 또는 Xcode CLI 도구 |
| **Linux 설치** | `sudo apt install git` | 패키지 매니저 사용 |
| **최초 설정** | `git config --global user.name` / `user.email` | 커밋 작성자 정보 등록 |
| **추가 설정** | `init.defaultBranch`, `color.ui`, `core.autocrlf`, `alias.*` | 브랜치명, 색상, 줄바꿈, 단축키 등 |

## 연습 문제

배운 내용을 바탕으로 직접 실습해 보면서 Git 설치와 설정 과정을 완벽히 이해해 보시기 바랍니다. 실제로 터미널에 명령어를 입력하며 진행하는 것이 가장 효과적입니다.

1. 자신의 운영 체제에 맞는 Git 설치 방법을 순서대로 서술해보세요.
2. Git 설치 후 반드시 설정해야 하는 최초 설정 두 가지는 무엇이며, 왜 중요한지 설명해보세요.
3. `git config --global alias.lg "log --oneline --graph --all"` 명령어의 의미를 설명하고, 이 단축어(alias)를 사용하면 어떤 이점이 있는지 서술해보세요.
