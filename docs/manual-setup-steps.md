# 템플릿 레포지토리 수동 생성 가이드

## 방법 1: GitHub 웹사이트에서 직접 생성 (가장 간단)

### 단계별 가이드

#### 1단계: GitHub 레포지토리 생성 페이지 열기

- https://github.com/new 접속
- 또는 GitHub 메인 페이지에서 "+" 버튼 → "New repository" 클릭

#### 2단계: 레포지토리 정보 입력

- **Owner**: `rapid-builder-templates` (조직) 또는 본인의 GitHub 사용자명
- **Repository name**: `landing-waitlist` (또는 `ai-chatbot`, `nextjs-saas-starter`)
- **Description**: (선택사항) "Landing page template with waitlist"
- **Public** 선택 ⚠️ 필수! (Private이면 README를 가져올 수 없음)
- **Add a README file** 체크 ✅
- **Add .gitignore**: None (나중에 추가 가능)
- **Choose a license**: None (나중에 추가 가능)

#### 3단계: Create repository 클릭

#### 4단계: README.md 편집

- 생성된 레포지토리 페이지에서 README.md 파일 클릭
- 연필 아이콘(✏️) 클릭하여 편집 모드로 전환
- 아래 내용 중 하나를 복사해서 붙여넣기:
  - Landing Page: `docs/template-examples/landing-waitlist-README.md` 내용
  - AI Chatbot: `docs/template-examples/ai-chatbot-README.md` 내용

#### 5단계: 커밋

- 페이지 하단의 "Commit changes" 클릭
- 커밋 메시지: "Add README"
- "Commit changes" 버튼 클릭

#### 완료! 🎉

이제 우리 앱에서 템플릿 상세 페이지를 열어보세요:

- `http://localhost:3000/templates/landing-waitlist`

---

## 방법 2: GitHub CLI 사용 (자동화)

### 전제 조건

- GitHub CLI 설치: https://cli.github.com
- GitHub CLI 인증: `gh auth login`

### 실행

```bash
# 스크립트에 실행 권한 부여 (Mac/Linux)
chmod +x scripts/setup-template-repo.sh

# 레포지토리 생성
./scripts/setup-template-repo.sh landing-waitlist
```

### 또는 직접 명령어 사용

```bash
gh repo create rapid-builder-templates/landing-waitlist \
  --public \
  --description "Landing page template with waitlist" \
  --add-readme
```

---

## 방법 3: 로컬에서 Git으로 생성

### 1. 로컬 디렉토리 생성

```bash
mkdir landing-waitlist
cd landing-waitlist
```

### 2. README.md 생성

```bash
# 예시 README 복사
cp ../docs/template-examples/landing-waitlist-README.md ./README.md
```

### 3. Git 초기화 및 커밋

```bash
git init
git add README.md
git commit -m "Add README"
```

### 4. GitHub에 레포지토리 생성 및 푸시

```bash
# GitHub CLI 사용
gh repo create rapid-builder-templates/landing-waitlist --public --source=. --push

# 또는 GitHub 웹사이트에서 레포지토리 생성 후:
git remote add origin https://github.com/rapid-builder-templates/landing-waitlist.git
git branch -M main
git push -u origin main
```

---

## 템플릿 리포지토리로 설정하기 (중요!)

레포지토리를 생성한 후, **반드시 템플릿 리포지토리로 설정**해야 합니다:

### 방법 1: GitHub 웹사이트에서 설정 (권장)

1. 레포지토리 페이지로 이동: `https://github.com/[owner]/[repo]`
2. **Settings** 탭 클릭
3. 왼쪽 사이드바에서 **General** 선택
4. 페이지를 아래로 스크롤하여 **Template repository** 섹션 찾기
5. **Template repository** 체크박스 활성화 ✅
6. 변경사항 저장

### 방법 2: GitHub API 사용 (고급)

리포지토리 소유자인 경우, API를 통해 자동으로 설정할 수 있습니다:

```bash
# GitHub CLI 사용
gh api repos/[owner]/[repo] -X PATCH -f is_template=true

# 또는 curl 사용
curl -X PATCH \
  -H "Authorization: token YOUR_GITHUB_TOKEN" \
  -H "Accept: application/vnd.github+json" \
  https://api.github.com/repos/[owner]/[repo] \
  -d '{"is_template":true}'
```

### 확인 방법

템플릿 리포지토리로 설정되면:

- 레포지토리 페이지에 **"Use this template"** 버튼이 표시됩니다
- 레포지토리 설명 아래에 **"Template"** 배지가 표시됩니다

## 체크리스트

레포지토리 생성 후 확인사항:

- [ ] 레포지토리가 Public으로 설정되어 있음
- [ ] README.md 파일이 main 브랜치에 있음
- [ ] README.md에 내용이 있음 (빈 파일이 아님)
- [ ] 레포지토리 이름이 정확함 (`owner/repo` 형식)
- [ ] **템플릿 리포지토리로 설정됨** ⚠️ 필수!

## 문제 해결

### "Repository not found" 에러

- 레포지토리 이름 확인: `rapid-builder-templates/landing-waitlist`
- 레포지토리가 실제로 존재하는지 확인
- Public으로 설정되어 있는지 확인

### "Repository exists but is not marked as a template repository" 에러

이 에러는 레포지토리가 존재하지만 템플릿으로 설정되지 않았을 때 발생합니다.

**해결 방법:**

1. 레포지토리 Settings → General로 이동
2. "Template repository" 옵션 활성화
3. 또는 위의 "템플릿 리포지토리로 설정하기" 섹션 참조

**자동 설정 (리포지토리 소유자인 경우):**

- 코드에서 `autoEnableTemplate: true` 옵션을 사용하면 자동으로 템플릿으로 설정을 시도합니다
- 하지만 기본적으로는 수동 설정을 권장합니다

### "README not found" 에러

- main 브랜치에 README.md가 있는지 확인
- 파일 이름이 정확한지 확인 (대소문자 구분)

### README가 표시되지 않음

- 브라우저 콘솔에서 에러 확인
- 서버 로그 확인
- 레포지토리 URL이 정확한지 확인

---

## 다음 단계

README가 정상적으로 표시되면:

1. 실제 코드 추가 (package.json, Next.js 구조 등)
2. 기능 구현
3. 테스트
