# 로컬에서 템플릿 프로젝트 완성하기

로컬에서 완전히 완성한 후 깨끗하게 GitHub에 업로드하는 방법입니다.

## 🎯 올바른 순서

1. ✅ 로컬에서 프로젝트 완성
2. ✅ `.gitignore` 먼저 설정
3. ✅ 필수 파일만 커밋
4. ✅ GitHub에 푸시
5. ✅ 템플릿으로 설정

## 📋 단계별 가이드

### 1단계: 로컬 프로젝트 생성

```bash
# 새 디렉토리 생성
mkdir landing-waitlist-template
cd landing-waitlist-template

# Git 초기화
git init
git branch -M main
```

### 2단계: `.gitignore` 먼저 추가 (가장 중요!)

**⚠️ 반드시 가장 먼저 `.gitignore`를 추가하세요!**

```bash
# .gitignore 파일 생성
cat > .gitignore << 'EOF'
# dependencies
/node_modules
/.pnp
.pnp.*
.yarn/*
!.yarn/patches
!.yarn/plugins
!.yarn/releases
!.yarn/versions

# testing
/coverage

# next.js
/.next/
/out/

# production
/build

# misc
.DS_Store
*.pem

# debug
npm-debug.log*
yarn-debug.log*
yarn-error.log*
.pnpm-debug.log*

# env files
.env*
.env.local
.env.development.local
.env.test.local
.env.production.local

# vercel
.vercel

# typescript
*.tsbuildinfo
next-env.d.ts
EOF

# .gitignore 커밋 (첫 번째 커밋!)
git add .gitignore
git commit -m "Add .gitignore"
```

### 3단계: 필수 파일들 추가

`docs/template-minimal-files.md`를 참고하여 필수 파일들을 순서대로 추가:

#### 3-1. `package.json` 추가

```bash
# package.json 생성 (docs/template-minimal-files.md 참고)
# 파일 생성 후:
git add package.json
git commit -m "Add package.json"
```

#### 3-2. 설정 파일들 추가

```bash
# tsconfig.json, next.config.ts, postcss.config.mjs, components.json 등
# 각 파일 생성 후 개별적으로 커밋하거나:
git add tsconfig.json next.config.ts postcss.config.mjs components.json
git commit -m "Add configuration files"
```

#### 3-3. 소스 코드 추가

```bash
# app/, lib/, components/ 등 소스 코드 추가
git add app/ lib/ components/
git commit -m "Add source code"
```

#### 3-4. README 추가

```bash
# README.md 추가 (docs/template-examples/ 참고)
git add README.md
git commit -m "Add README"
```

### 4단계: 의존성 설치 (`.gitignore`가 있으므로 안전)

```bash
# 이제 안전하게 설치 가능 (node_modules는 .gitignore에 의해 무시됨)
npm install
# 또는
pnpm install
```

### 5단계: 테스트

```bash
# 로컬에서 테스트
npm run dev

# 빌드 테스트
npm run build
```

**⚠️ 중요**: `npm install`이나 `npm run build`를 실행해도 `.gitignore`가 있으므로 불필요한 파일이 Git에 추가되지 않습니다.

### 6단계: GitHub에 푸시

```bash
# GitHub 리포지토리 생성 (웹사이트에서 또는 GitHub CLI)
# 웹사이트에서: https://github.com/new
#   - Public으로 설정
#   - README 추가하지 않기 (이미 로컬에 있음)
#   - .gitignore 추가하지 않기 (이미 로컬에 있음)

# 리모트 추가 및 푸시
git remote add origin https://github.com/gyorutan/landing-waitlist.git
git push -u origin main
```

### 7단계: 템플릿으로 설정

1. GitHub 리포지토리 페이지로 이동
2. **Settings** → **General**
3. 아래로 스크롤하여 **Template repository** 체크박스 활성화
4. 저장

## ✅ 확인 사항

푸시 후 확인:

1. **GitHub 리포지토리 페이지에서:**

   - "Languages" 섹션 확인
   - CSS 비율이 10% 이하여야 함
   - TypeScript/JavaScript가 대부분

2. **파일 구조 확인:**

   - `node_modules` 폴더가 보이지 않아야 함
   - `.next` 폴더가 보이지 않아야 함
   - `.gitignore` 파일이 있어야 함

3. **템플릿 테스트:**
   - Rapid Builder에서 프로젝트 생성
   - 생성된 리포지토리에 불필요한 파일이 없는지 확인

## 💡 팁

### 작은 단위로 커밋

```bash
# 한 번에 다 커밋하지 말고:
git add .
git commit -m "Initial commit"

# 이렇게 작은 단위로:
git add .gitignore
git commit -m "Add .gitignore"

git add package.json
git commit -m "Add package.json"

git add tsconfig.json next.config.ts
git commit -m "Add config files"
```

### 커밋 전 확인

```bash
# 커밋 전에 어떤 파일이 추가되는지 확인
git status

# .gitignore가 제대로 작동하는지 확인
git status --ignored
```

### 실수로 잘못된 파일 추가한 경우

```bash
# Git 캐시에서 제거 (파일은 유지)
git rm --cached node_modules -r
git rm --cached .next -r

# .gitignore 확인 후 다시 커밋
git commit -m "Remove accidentally added files"
```

## 🚫 하지 말아야 할 것

❌ **`node_modules` 설치 후에 `.gitignore` 추가**

- 이미 `node_modules`가 Git에 추가된 상태

❌ **빌드 후에 `.gitignore` 추가**

- 이미 `.next`가 Git에 추가된 상태

❌ **한 번에 모든 파일 추가**

- 실수로 불필요한 파일 포함 가능

✅ **`.gitignore`를 가장 먼저 추가**

- 이후 모든 작업이 안전

## 📁 권장 파일 추가 순서

1. `.gitignore` ⭐ (가장 먼저!)
2. `package.json`
3. `tsconfig.json`
4. `next.config.ts`
5. `postcss.config.mjs`
6. `components.json` (shadcn/ui 사용 시)
7. `lib/utils.ts` (shadcn/ui 사용 시)
8. `app/globals.css`
9. `app/layout.tsx`
10. `app/page.tsx`
11. 기타 컴포넌트 및 소스 코드
12. `README.md` (마지막)

## 🔗 관련 문서

- [템플릿 최소 파일 구조](./template-minimal-files.md)
- [템플릿 생성 가이드](./template-creation-guide.md)
