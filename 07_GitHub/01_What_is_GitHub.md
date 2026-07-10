# GitHub 소개

GitHub는 Git 저장소를 호스팅하는 가장 인기 있는 웹 서비스입니다. 단순한 저장소 호스팅을 넘어 협업, 코드 리뷰, CI/CD, 프로젝트 관리 등 개발 생산성을 높이는 다양한 기능을 제공합니다.

## GitHub 계정 만들기

1. [github.com](https://github.com)에 방문하여 **Sign up** 클릭
2. 이메일 주소, 비밀번호, 사용자명 입력
3. 이메일 인증 완료 후 계정 활성화

## GitHub 주요 기능

| 기능 | 설명 |
|---|---|
| **저장소 (Repository)** | Git 저장소를 웹에서 호스팅 |
| **Pull Request** | 코드 변경 요청 및 리뷰 시스템 |
| **Issues** | 버그, 기능 요청, 할 일 추적 |
| **Projects** | 칸반 보드 형태의 프로젝트 관리 |
| **Actions** | CI/CD 자동화 (빌드, 테스트, 배포) |
| **Wiki** | 프로젝트 문서화 |
| **GitHub Pages** | 정적 웹사이트 호스팅 |
| **Discussions** | 팀 커뮤니케이션 포럼 |

## GitHub 저장소 만들기

```bash
# 방법 1: GitHub에서 새 저장소 생성 후 로컬에 clone
# 1) github.com에서 "New repository" 버튼 클릭
# 2) 저장소 이름 입력 (예: my-project)
# 3) "Create repository" 클릭
# 4) 로컬에서 clone

$ git clone https://github.com/username/my-project.git
$ cd my-project
$ echo "# My Project" > README.md
$ git add . && git commit -m "첫 커밋"
$ git push origin main
```

```bash
# 방법 2: 로컬 저장소를 GitHub에 연결
$ mkdir my-project && cd my-project && git init
$ echo "# My Project" > README.md
$ git add . && git commit -m "첫 커밋"

# GitHub에서 빈 저장소 생성 후:
$ git remote add origin https://github.com/username/my-project.git
$ git push -u origin main
```

## 저장소 설정 화면 둘러보기

GitHub 저장소 페이지의 주요 탭:

```
Code        → 저장소 파일 브라우저
Issues      → 버그 및 기능 요청 관리
Pull requests → 코드 리뷰 관리
Actions     → CI/CD 워크플로우
Projects    → 칸반 보드
Wiki        → 문서
Security    → 보안 취약점 점검
Insights    → 저장소 통계 (컨트리뷰터, 트래픽 등)
Settings    → 저장소 설정 (브랜치 보호, 협업자 등)
```

## 저장소 가시성 (Visibility)

| 설정 | 설명 |
|---|---|
| **Public** | 누구나 저장소를 볼 수 있음 (오픈소스) |
| **Private** | 초대된 사람만 볼 수 있음 |
| **Internal** (Enterprise) | 조직 내 모든 구성원이 볼 수 있음 |

## README와 .gitignore

GitHub는 저장소 생성 시 README와 .gitignore 파일을 자동으로 생성할 수 있습니다.

**README.md:** 프로젝트 소개, 설치 방법, 사용법 등을 Markdown으로 작성
** .gitignore:** Git이 추적하지 않을 파일 패턴을 정의

```bash
# .gitignore 예시
node_modules/      # Node.js 의존성
.env               # 환경 변수 (비밀 키)
*.log              # 로그 파일
dist/              # 빌드 결과물
.DS_Store          # macOS 시스템 파일
```
