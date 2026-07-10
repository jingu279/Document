# GitHub Actions 기초

GitHub Actions는 CI/CD(지속적 통합/지속적 배포)를 자동화하는 GitHub의 내장 도구입니다. 코드 푸시, PR 생성 등 특정 이벤트가 발생하면 자동으로 워크플로우를 실행합니다.

## GitHub Actions 개념

**워크플로우 실행 흐름:**

```mermaid
flowchart TB
  Dev["🧑 개발자 코드 푸시"] --> Event["⚡ Event 발생!<br/>(push / PR 생성 등)"]
  Event --> Trigger["🚀 Workflow 트리거<br/>(ci.yml 파일 실행)"]
  Trigger --> Runner["🖥️ Runner 서버<br/>ubuntu-latest"]

  subgraph Job[Job: test]
    direction TB
    S1["① actions/checkout@v4<br/>→ 내 코드를 Runner로 가져오기"]
    S2["② actions/setup-node@v4<br/>→ Node.js 20 설치"]
    S3["③ npm ci<br/>→ 의존성 설치"]
    S4["④ npm test<br/>→ ✅ 테스트 실행"]

    S1 --> S2 --> S3 --> S4
  end

  Runner --> Job
  Job --> Result["📊 GitHub Actions 탭<br/>✅ CI / test (ubuntu-latest)<br/>✓ actions/checkout@v4<br/>✓ actions/setup-node@v4<br/>✓ npm ci<br/>✓ npm test"]
```
| **Workflow** | 자동화 프로세스 전체 (`.github/workflows/`에 YAML 파일) |
| **Job** | 워크플로우 내의 작업 단위 (예: "test", "build", "deploy") |
| **Step** | Job 내의 개별 명령어 또는 액션 실행 |
| **Action** | 재사용 가능한 자동화 단위 (GitHub Marketplace에서 공유) |
| **Runner** | 워크플로우를 실행하는 서버 (GitHub 호스팅 or 자체 호스팅) |
| **Event** | 워크플로우를 트리거하는 이벤트 (`push`, `pull_request` 등) |

## 첫 번째 워크플로우 만들기

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npm test
```

**실행 결과 화면:**
```
GitHub 저장소 → Actions 탭 → CI 워크플로우
  ✓ test (ubuntu-latest)
    ✓ actions/checkout@v4
    ✓ actions/setup-node@v4
    ✓ npm ci
    ✓ npm test    ← 모두 통과!
```

## 다양한 워크플로우 예시

### Node.js 프로젝트 테스트

```yaml
# .github/workflows/node-test.yml
name: Node.js Test

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [18, 20, 22]

    steps:
      - uses: actions/checkout@v4
      - name: Node.js ${{ matrix.node-version }} 설정
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'npm'
      - run: npm ci
      - run: npm run lint
      - run: npm test
      - name: 테스트 결과 업로드
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: test-results-${{ matrix.node-version }}
          path: test-results/
```

### PR에 자동 라벨 추가

```yaml
# .github/workflows/pr-label.yml
name: PR Labeler

on:
  pull_request:
    types: [opened]

jobs:
  label:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/labeler@v5
        with:
          repo-token: ${{ secrets.GITHUB_TOKEN }}
```

### 배포 자동화

```yaml
# .github/workflows/deploy.yml
name: Deploy to Production

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npm run build
      - name: Deploy to S3
        uses: jakejarvis/s3-sync-action@v0.5.1
        with:
          args: --delete
        env:
          AWS_S3_BUCKET: ${{ secrets.AWS_BUCKET_NAME }}
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          SOURCE_DIR: 'build'
```

## GitHub Actions Marketplace

Actions Marketplace에서 수천 개의 사전 제작 액션을 사용할 수 있습니다.

```yaml
# 인기 있는 액션 예시
- uses: actions/checkout@v4              # 저장소 체크아웃
- uses: actions/setup-node@v4            # Node.js 설정
- uses: actions/setup-python@v5          # Python 설정
- uses: docker/build-push-action@v5      # Docker 이미지 빌드/푸시
- uses: actions/cache@v4                  # 의존성 캐싱 (빌드 속도 향상)
- uses: github/codeql-action@v3           # 코드 보안 취약점 분석
```

## 워크플로우 실행 확인

```bash
# GitHub CLI로 Actions 상태 확인
$ gh run list
STATUS  NAME        WORKFLOW  BRANCH  COMMIT  AGE
✓       CI          main      a1b2c3  2m ago
✗       Deploy      develop   d4e5f6  1h ago
✓       Node Test   feat/x    g7h8i9  3h ago

# 특정 실행 상세 보기
$ gh run view 123456789
✓ CI · main · a1b2c3d
Jobs:
  ✓ test (18)   12s
  ✓ test (20)   11s
  ✓ test (22)   14s

# 로그 확인
$ gh run view 123456789 --log
```

## Secrets와 환경 변수

비밀 키나 API 토큰은 저장소 설정의 **Secrets and variables**에 저장합니다.

```bash
# GitHub CLI로 Secrets 설정
$ gh secret set AWS_ACCESS_KEY_ID
✓ Set Actions secret AWS_ACCESS_KEY_ID for username/repo

$ gh secret set DEPLOY_KEY --body "ssh-rsa AAAA..."
✓ Set Actions secret DEPLOY_KEY for username/repo
```

```yaml
# 워크플로우에서 Secrets 사용
jobs:
  deploy:
    steps:
      - run: deploy.sh
        env:
          AWS_KEY: ${{ secrets.AWS_ACCESS_KEY_ID }}
          NODE_ENV: production   # 일반 환경 변수
```

## CI/CD 파이프라인 전체 예시

```yaml
# .github/workflows/main.yml
name: CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci && npm run lint

  test:
    needs: lint
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node: [18, 20]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node }}
      - run: npm ci
      - run: npm test -- --coverage
      - uses: actions/upload-artifact@v4
        with:
          name: coverage-${{ matrix.node }}
          path: coverage/

  deploy:
    needs: test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci && npm run build
      - run: ./deploy.sh
        env:
          DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
```
