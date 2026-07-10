# Cherry-Pick: 특정 커밋만 골라서 가져오기

Cherry-Pick은 다른 브랜치의 **특정 커밋 하나만** 골라서 현재 브랜치에 적용하는 기능입니다. 병합(merge)이나 리베이스(rebase)처럼 브랜치 전체를 가져오는 것이 아니라, 원하는 커밋만 선별적으로 가져올 때 사용합니다.

```mermaid
gitGraph
   commit id: "C1"
   commit id: "C2"
   branch feature/login
   checkout feature/login
   commit id: "C3: 로그인 폼"
   commit id: "C4: 유효성 검사"
   commit id: "C5: 스타일 적용"
   checkout main
   commit id: "C6"
   cherry-pick id: "C4"
```

## Cherry-Pick이 필요한 상황

| 상황 | 설명 |
|---|---|
| **버그 수치 (hotfix)** | 개발 중인 브랜치에서 버그 수정 커밋만 골라서 main에 적용 |
| **선별적 기능 백포트** | 최신 브랜치의 특정 기능만 예전 릴리스 브랜치에 적용 |
| **실수한 커밋 위치 수정** | 잘못된 브랜치에 한 커밋을 올바른 브랜치로 이동 |

## 기본 사용법

```bash
git cherry-pick <커밋해시>
```

### 예시: 버그 수정 커밋만 main에 적용하기

```bash
# 현재 브랜치 확인 (main)
$ git branch
* main
  feature/payment

# feature/payment 브랜치에서 버그 수정 커밋 확인
$ git log --oneline feature/payment
d4e5f6f 결제 API 연동
a1b2c3d 버그 수정: 가격 계산 오류   ← 이 커밋만 필요!
g7h8i9j 결제 모듈 초안

# main에서 특정 커밋만 cherry-pick
$ git cherry-pick a1b2c3d
[main 9i8h7g6] 버그 수정: 가격 계산 오류
 Date: Mon Jul 10 14:30:00 2026 +0900
 1 file changed, 2 insertions(+), 1 deletion(-)

# 결과: main에 버그 수정만 적용됨 (결제 모듈 전체는 아직)
$ git log --oneline -3
9i8h7g6 (HEAD -> main) 버그 수정: 가격 계산 오류
f4e5d6c README 업데이트
k1l2m3n 첫 번째 커밋
```

### 여러 커밋 한 번에 Cherry-Pick

```bash
# 연속된 커밋 범위 지정
$ git cherry-pick a1b2c3d..d4e5f6f

# 또는 하나씩 나열
$ git cherry-pick a1b2c3d d4e5f6f g7h8i9j
```

## Cherry-Pick 주의사항

### 1. 충돌이 발생할 수 있음

Cherry-Pick도 병합이므로 충돌이 발생할 수 있습니다. 해결 방법은 일반 병합 충돌과 동일합니다.

```bash
# 충돌 발생 시
$ git cherry-pick a1b2c3d
error: could not apply a1b2c3d... 버그 수정: 가격 계산 오류
hint: resolve the conflicts and run "git cherry-pick --continue"

# 충돌 해결 후 계속
$ git add .
$ git cherry-pick --continue

# 또는 cherry-pick 취소
$ git cherry-pick --abort
```

### 2. 커밋 해시가 달라짐

Cherry-Pick으로 가져온 커밋은 원본과 **다른 해시**를 갖습니다. 내용은 같지만 새로운 커밋으로 간주됩니다.

```bash
# 원본 커밋
a1b2c3d 버그 수정: 가격 계산 오류   (feature/payment)

# Cherry-Pick된 커밋 (내용은 같지만 해시가 다름)
9i8h7g6 버그 수정: 가격 계산 오류   (main)
```

### 3. 의존성이 있는 커밋은 함께 가져오기

커밋 A가 커밋 B에 의존한다면, A만 cherry-pick하면 문제가 생길 수 있습니다. 이런 경우 연관된 커밋들을 함께 가져오는 것이 좋습니다.

## Cherry-Pick 활용: 잘못된 브랜치에 한 커밋 수정

```bash
# 실수: main에서 직접 수정해버림
$ git switch main
$ echo "hotfix" > urgent.txt
$ git add . && git commit -m "긴급 수정"

# 😱 알고 보니 feature 브랜치에서 작업해야 했음!

# 방법 1: Cherry-Pick + Reset (추천)
$ git switch feature/hotfix
$ git cherry-pick main       # main의 마지막 커밋을 feature에 적용
$ git switch main
$ git reset --hard HEAD~1    # main에서 잘못된 커밋 제거

# 방법 2: 단순 복사
$ git switch feature/hotfix
$ git cherry-pick main       # main의 최신 커밋을 가져옴
```

## Cherry-Pick 옵션

| 옵션 | 설명 |
|---|---|
| `-e`, `--edit` | 커밋 메시지 편집 허용 (기본값) |
| `--no-commit` | 변경 사항만 적용하고 커밋은 직접 수행 |
| `-x` | 커밋 메시지에 원본 커밋 해시 추가 (이력 추적용) |
| `--signoff` | 커밋에 Signed-off-by 줄 추가 |

```bash
# 원본 추적 정보 포함
$ git cherry-pick -x a1b2c3d

# 커밋 없이 변경 사항만 적용
$ git cherry-pick --no-commit a1b2c3d
$ git add .
$ git commit -m "직접 작성한 커밋 메시지"
```

## 실습 시나리오

```bash
# 1. feature 브랜치에서 작업 중
$ git switch -c feature/dashboard

# 2. 긴급 버그 수정 커밋 생성
$ echo "fix" > bugfix.js
$ git add . && git commit -m "대시보드 버그 수정"

# 3. 그 외 기능 개발 계속...
$ echo "feature" > chart.js
$ git add . && git commit -m "차트 기능 추가"

# 4. 갑자기! 운영 서버에 버그 수정이 필요함
$ git switch main

# 5. 버그 수정 커밋만 골라서 적용
$ git cherry-pick abc1234   # feature/dashboard의 버그 수정 커밋

# 6. 배포 준비 완료! feature 브랜치의 나머지 기능은 아직 개발 중
```
