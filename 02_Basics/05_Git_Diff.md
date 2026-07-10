# 변경 사항 확인: git diff

`git diff`는 파일의 변경 사항을 **줄 단위**로 비교하여 보여주는 명령어입니다. 커밋하기 전에 무엇이 바뀌었는지 확인할 때 유용합니다.

## 1. 작업 디렉토리 vs Staging Area: `git diff`

아직 `git add`하지 않은 변경 사항을 확인합니다.

```bash
# 모든 파일의 변경 사항 확인
$ git diff

# 특정 파일만 확인
$ git diff index.html
```

**출력 예시:**

```diff
$ git diff
diff --git a/index.html b/index.html
index a1b2c3d..d4e5f6g 100644
--- a/index.html
+++ b/index.html
@@ -10,6 +10,7 @@
     <title>내 웹사이트</title>
   </head>
   <body>
+    <h1>환영합니다!</h1>      ← 초록색: 추가된 줄
     <p>내용입니다.</p>
-    <p>이전 텍스트</p>        ← 빨간색: 삭제된 줄
+    <p>새로운 텍스트</p>      ← 수정됨 (삭제 + 추가)
   </body>
 </html>
```

**diff 출력 구조:**

```
@@ -10,6 +10,7 @@
```

- `-10,6`: 원본 파일의 10번째 줄부터 6줄
- `+10,7`: 변경 후 파일의 10번째 줄부터 7줄
- `-`: 삭제된 줄 (빨간색)
- `+`: 추가된 줄 (초록색)

## 2. Staging Area vs 저장소: `git diff --staged`

`git add`로 스테이징된 변경 사항을 확인합니다.

```bash
git diff --staged
# 또는
git diff --cached
```

```bash
$ echo "<footer>ⓒ 2024</footer>" >> index.html
$ git add index.html

$ git diff                    # 출력 없음 (이미 Staging에 있음)
$ git diff --staged           # 변경 사항 출력!
diff --git a/index.html b/index.html
+    <footer>ⓒ 2024</footer>
```

## 3. 커밋 간 비교

```bash
# 현재 HEAD와 비교
$ git diff HEAD

# 특정 커밋과 비교
$ git diff a1b2c3d

# 두 커밋 사이의 변경 사항
$ git diff a1b2c3d..d4e5f6f

# 두 브랜치 비교
$ git diff main..feature/login
```

**커밋 비교 예시:**

```bash
$ git log --oneline
d4e5f6f (HEAD) 푸터 추가
a1b2c3d 첫 번째 커밋

# 첫 번째 커밋과 두 번째 커밋의 차이
$ git diff a1b2c3d..d4e5f6f
diff --git a/index.html b/index.html
+    <footer>ⓒ 2024</footer>
```

## 4. 요약 보기: `git diff --stat`

변경된 파일과 줄 수만 간략히 표시합니다.

```bash
$ git diff --stat
 index.html | 3 ++-
 style.css  | 5 +++++
 README.md  | 1 +
 3 files changed, 8 insertions(+), 1 deletion(-)
```

## 5. diff 도구 사용하기

복잡한 diff는 터미널 대신 GUI 도구로 보는 것이 편리합니다.

```bash
git difftool
```

설정에 따라 VS Code, Beyond Compare 등 외부 도구가 실행됩니다.

## 실습 시나리오

```bash
# 1. 파일 수정
$ echo "새로운 내용" > hello.txt

# 2. 변경 사항 확인 (Unstaged)
$ git diff
diff --git a/hello.txt b/hello.txt
+새로운 내용

# 3. 스테이징
$ git add hello.txt
$ git diff              # 출력 없음

# 4. 스테이징된 변경 사항 확인
$ git diff --staged
diff --git a/hello.txt b/hello.txt
+새로운 내용

# 5. 커밋
$ git commit -m "hello.txt 추가"

# 6. 커밋 후에는 diff 출력 없음
$ git diff              # 출력 없음
$ git diff --staged     # 출력 없음

# 7. 이전 커밋과 비교하려면
$ git diff HEAD~1 HEAD
```
