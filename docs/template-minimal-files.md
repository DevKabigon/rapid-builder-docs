# 템플릿 리포지토리 최소 파일 구조

템플릿 리포지토리(`gyorutan/landing-waitlist`)에 추가해야 하는 **최소 필수 파일들**입니다.

## 📁 필수 파일 목록

### 1. 루트 파일들

#### `package.json` (필수)

```json
{
  "name": "landing-waitlist",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "next": "16.1.1",
    "react": "19.2.3",
    "react-dom": "19.2.3",
    "shadcn": "^3.6.3",
    "clsx": "^2.1.1",
    "tailwind-merge": "^3.4.0",
    "class-variance-authority": "^0.7.1",
    "@base-ui/react": "^1.0.0"
  },
  "devDependencies": {
    "@types/node": "^20",
    "@types/react": "^19",
    "@types/react-dom": "^19",
    "typescript": "^5",
    "tailwindcss": "^4",
    "@tailwindcss/postcss": "^4"
  }
}
```

#### `tsconfig.json` (필수)

```json
{
  "compilerOptions": {
    "target": "ES2017",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "react-jsx",
    "incremental": true,
    "plugins": [
      {
        "name": "next"
      }
    ],
    "paths": {
      "@/*": ["./*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
```

#### `next.config.ts` (필수)

```typescript
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
  /* config options here */
};

export default nextConfig;
```

#### `.gitignore` (필수)

⚠️ **중요**: 템플릿 리포지토리에 `.gitignore` 파일이 반드시 있어야 합니다. 이 파일이 없으면 `node_modules`, 빌드 산출물 등이 포함되어 프로젝트 크기가 비정상적으로 커집니다.

```
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
```

#### `.env.example` (권장)

```env
RESEND_API_KEY=your_resend_api_key_here
NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

### 2. Next.js App Router 구조

#### `app/layout.tsx` 또는 `src/app/layout.tsx` (필수)

**옵션 1: 루트에 app 폴더**

```typescript
import type { Metadata } from "next";
import "./globals.css";

export const metadata: Metadata = {
  title: "Landing Page - Waitlist",
  description: "A beautiful landing page with waitlist functionality",
};

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en">
      <body className="antialiased">{children}</body>
    </html>
  );
}
```

#### `app/page.tsx` 또는 `src/app/page.tsx` (필수 - 메인 페이지)

**옵션 1: 루트에 app 폴더**

```typescript
export default function HomePage() {
  return (
    <div className="min-h-screen flex items-center justify-center bg-gradient-to-br from-blue-50 to-indigo-100">
      <div className="text-center space-y-8 p-8">
        <h1 className="text-5xl font-bold text-gray-900">
          Welcome to Your Landing Page
        </h1>
        <p className="text-xl text-gray-600">
          This is a minimal Next.js template
        </p>
        <button className="px-6 py-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition">
          Get Started
        </button>
      </div>
    </div>
  );
}
```

#### `app/globals.css` 또는 `src/app/globals.css` (필수 - Tailwind CSS + shadcn/ui)

**옵션 1: 루트에 app 폴더**

```css
@import "tailwindcss";
@import "shadcn/tailwind.css";

@theme inline {
  /* Tailwind CSS v4에서는 여기서 직접 테마 설정 */
}

:root {
  --foreground: #0a0a0a;
  --background: #ffffff;
}

@media (prefers-color-scheme: dark) {
  :root {
    --foreground: #ededed;
    --background: #0a0a0a;
  }
}

body {
  color: var(--foreground);
  background: var(--background);
}
```

**참고:** Tailwind CSS v4부터는 `tailwind.config.ts` 파일이 필요 없고, CSS 파일에서 `@theme` 블록을 사용해 설정합니다.

### 3. 설정 파일들

#### `postcss.config.mjs` (Tailwind CSS 사용 시 필수)

```javascript
/** @type {import('postcss-load-config').Config} */
const config = {
  plugins: {
    "@tailwindcss/postcss": {},
  },
};

export default config;
```

#### `components.json` (shadcn/ui 사용 시 필수)

```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "base-lyra",
  "rsc": true,
  "tsx": true,
  "tailwind": {
    "config": "",
    "css": "app/globals.css",
    "baseColor": "neutral",
    "cssVariables": true,
    "prefix": ""
  },
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils",
    "ui": "@/components/ui",
    "lib": "@/lib"
  }
}
```

#### `lib/utils.ts` 또는 `src/lib/utils.ts` (shadcn/ui 사용 시 필수)

**옵션 1: 루트에 lib 폴더**

```typescript
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

**옵션 2: src 폴더 안에 lib 폴더**

- `src/lib/utils.ts`에 동일한 내용을 넣으면 됩니다.

#### `tailwind.config.ts` (❌ 필요 없음!)

Tailwind CSS v4부터는 설정 파일이 필요 없습니다. CSS 파일(`globals.css`)에서 직접 설정합니다.

## 📂 최종 디렉토리 구조

Next.js는 두 가지 구조를 지원합니다:

### 옵션 1: 루트에 app 폴더 (권장)

```
landing-waitlist/
├── README.md              # 이미 있음
├── package.json           # 추가 필요
├── tsconfig.json          # 추가 필요
├── next.config.ts         # 추가 필요
├── .gitignore            # 추가 필요
├── .env.example          # 추가 필요 (선택)
├── postcss.config.mjs    # 추가 필요 (Tailwind 사용 시)
├── components.json       # 추가 필요 (shadcn/ui 사용 시)
├── app/
│   ├── layout.tsx        # 추가 필요
│   ├── page.tsx          # 추가 필요
│   └── globals.css       # 추가 필요
└── lib/
    └── utils.ts          # 추가 필요 (shadcn/ui 사용 시)
```

### 옵션 2: src 폴더 안에 app 폴더

```
landing-waitlist/
├── README.md              # 이미 있음
├── package.json           # 추가 필요
├── tsconfig.json          # 추가 필요
├── next.config.ts         # 추가 필요
├── .gitignore            # 추가 필요
├── .env.example          # 추가 필요 (선택)
├── postcss.config.mjs    # 추가 필요 (Tailwind 사용 시)
├── components.json       # 추가 필요 (shadcn/ui 사용 시)
├── src/
│   ├── app/
│   │   ├── layout.tsx    # 추가 필요
│   │   ├── page.tsx      # 추가 필요
│   │   └── globals.css   # 추가 필요
│   └── lib/
│       └── utils.ts      # 추가 필요 (shadcn/ui 사용 시)
```

**참고:** 두 구조 모두 Next.js에서 완전히 지원됩니다. `create-next-app` 실행 시 `--src-dir` 플래그를 사용하면 `src/` 폴더 구조로 생성됩니다.

## 🚀 빠른 시작 가이드

### 방법 1: 로컬에서 생성 후 푸시

1. **로컬에 새 Next.js 프로젝트 생성:**

**옵션 1: 루트에 app 폴더 (기본)**

```bash
npx create-next-app@latest landing-waitlist-template --typescript --tailwind --app
cd landing-waitlist-template
```

**옵션 2: src 폴더 안에 app 폴더**

```bash
npx create-next-app@latest landing-waitlist-template --typescript --tailwind --app --src-dir
cd landing-waitlist-template
```

**참고:**

- `create-next-app`으로 생성하면 Tailwind CSS v4가 설치되며, `tailwind.config.ts` 파일은 생성되지 않습니다. CSS 파일에서 직접 설정하세요.
- `--src-dir` 플래그를 사용하면 `src/app/` 구조로 생성됩니다.

2. **위의 파일들로 교체/추가**

3. **GitHub 리포지토리에 푸시:**

```bash
git remote add origin https://github.com/gyorutan/landing-waitlist.git
git branch -M main

# 리모트에 이미 파일이 있는 경우 (README.md 등)
git pull origin main --allow-unrelated-histories
# 또는 리베이스 방식:
# git pull origin main --rebase

# 충돌이 있다면 해결 후:
git push -u origin main
```

**참고:** 리모트 리포지토리에 이미 README.md가 있는 경우, `--allow-unrelated-histories` 플래그를 사용해야 합니다.

### 방법 2: GitHub에서 직접 파일 추가

1. 템플릿 리포지토리(`gyorutan/landing-waitlist`)로 이동
2. "Add file" → "Create new file" 클릭
3. 위의 각 파일을 하나씩 생성:
   - `package.json`
   - `tsconfig.json`
   - `next.config.ts`
   - `.gitignore`
   - `postcss.config.mjs`
   - `components.json` (shadcn/ui용)
   - `app/layout.tsx`
   - `app/page.tsx`
   - `app/globals.css`
   - `lib/utils.ts` (shadcn/ui용)
4. 커밋 & 푸시

## 🎨 shadcn/ui 컴포넌트 추가하기 (선택)

템플릿에 기본 UI 컴포넌트를 추가하려면:

```bash
# 템플릿 리포지토리에서
npx shadcn@latest add button
npx shadcn@latest add card
npx shadcn@latest add input
# 등등...
```

또는 GitHub에서 직접 `components/ui/` 폴더를 만들고 컴포넌트 파일들을 추가할 수 있습니다.

## ⚠️ 중요: 불필요한 파일 제거

템플릿 리포지토리에 **절대 포함하면 안 되는 파일들**:

- ❌ `node_modules/` - 의존성은 `package.json`만 있으면 됩니다
- ❌ `.next/` - 빌드 산출물입니다
- ❌ `out/` - 빌드 산출물입니다
- ❌ `.vercel/` - Vercel 설정 파일입니다
- ❌ `.env.local`, `.env` - 환경 변수 파일입니다
- ❌ `*.tsbuildinfo` - TypeScript 빌드 정보입니다
- ❌ `coverage/` - 테스트 커버리지 리포트입니다

### 이미 커밋된 불필요한 파일 제거하기

만약 템플릿 리포지토리에 이미 위의 파일들이 커밋되어 있다면:

```bash
# 템플릿 리포지토리 클론
git clone https://github.com/[owner]/[repo].git
cd [repo]

# .gitignore에 추가 (이미 있다면 스킵)
# 위의 .gitignore 내용 확인

# Git 캐시에서 제거 (파일은 삭제하지만 Git 히스토리에는 남음)
git rm -r --cached node_modules .next .vercel out coverage 2>/dev/null || true
git rm --cached .env.local .env *.tsbuildinfo 2>/dev/null || true

# 커밋
git commit -m "Remove build artifacts and dependencies"

# 푸시
git push origin main
```

**주의**: `node_modules`가 이미 커밋되어 있다면, GitHub에서 리포지토리 크기가 매우 커질 수 있습니다. 이 경우 리포지토리를 새로 만드는 것을 권장합니다.

## ✅ 확인 사항

템플릿 리포지토리에 파일을 추가한 후:

1. **리포지토리 구조 확인:**

   - `package.json`이 있는지 확인
   - `app/` 폴더가 있는지 확인
   - `app/page.tsx`가 있는지 확인
   - `components.json`이 있는지 확인 (shadcn/ui 사용 시)
   - `lib/utils.ts`가 있는지 확인 (shadcn/ui 사용 시)
   - `.gitignore`가 있는지 확인 ⚠️ 필수!

2. **불필요한 파일 확인:**

   - GitHub 리포지토리 페이지에서 "Languages" 섹션 확인
   - CSS가 50% 이상이면 `node_modules`나 빌드 산출물이 포함된 것입니다
   - TypeScript/JavaScript가 대부분이어야 정상입니다

3. **프로젝트 생성 테스트:**
   - Rapid Builder에서 프로젝트 생성
   - 생성된 리포지토리에 파일들이 복사되었는지 확인
   - Vercel 배포 후 404가 아닌 실제 페이지가 보이는지 확인

## 💡 팁

- **최소한으로 시작:** 위의 필수 파일들만 먼저 추가하고 테스트
- **점진적 추가:** 기본 구조가 작동하면 기능을 하나씩 추가
- **README 업데이트:** 코드를 추가할 때마다 README도 업데이트
