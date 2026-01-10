# 랜딩 페이지 템플릿 완벽 가이드

`create next-app` 대신 직접 설정하여 깨끗하고 완벽한 템플릿을 만드는 방법입니다.

## 🎯 왜 직접 설정해야 하나요?

1. **불필요한 파일 제거**: `create next-app`은 많은 예제 파일을 생성합니다
2. **최소한의 파일만**: 템플릿에는 필수 파일만 있어야 합니다
3. **완전한 제어**: 필요한 것만 정확히 포함할 수 있습니다
4. **깨끗한 구조**: CSS 비율 문제 없이 깨끗한 리포지토리 유지

## ⚡ 빠른 시작: shadcn create 사용 (권장!)

**더 나은 방법**: `shadcn create` 명령어를 사용하면 고품질 설정이 자동으로 적용됩니다!

```bash
npx shadcn@latest create --preset "https://ui.shadcn.com/init?base=radix&style=vega&baseColor=neutral&theme=neutral&iconLibrary=lucide&font=inter&menuAccent=subtle&menuColor=default&radius=default&template=next" --template next
```

이 명령어는:

- ✅ 최신 shadcn/ui 설정 자동 적용
- ✅ 고품질 기본 구조 생성
- ✅ 필요한 파일만 생성
- ✅ 템플릿에 적합한 구조

**주의**: `.gitignore`를 먼저 추가한 후 실행해야 안전합니다!

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

```bash
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

git add .gitignore
git commit -m "Add .gitignore"
```

### 2-1단계: shadcn create 실행 (권장!)

`.gitignore`를 추가한 후, shadcn create를 실행합니다:

```bash
# shadcn create 실행 (고품질 설정 자동 적용)
npx shadcn@latest create --preset "https://ui.shadcn.com/init?base=radix&style=vega&baseColor=neutral&theme=neutral&iconLibrary=lucide&font=inter&menuAccent=subtle&menuColor=default&radius=default&template=next" --template next

# 생성된 파일 확인
git status

# 생성된 파일들 커밋 (node_modules는 .gitignore에 의해 자동 제외됨)
git add .
git commit -m "Initialize project with shadcn create"
```

**이 명령어가 생성하는 파일들:**

- ✅ `package.json` (의존성 포함)
- ✅ `tsconfig.json`
- ✅ `next.config.ts`
- ✅ `postcss.config.mjs`
- ✅ `components.json`
- ✅ `app/globals.css` (Tailwind + shadcn 설정)
- ✅ `app/layout.tsx`
- ✅ `app/page.tsx` (기본 페이지)
- ✅ `lib/utils.ts`
- ✅ 기타 필요한 설정 파일들

**주의사항:**

- `.gitignore`가 먼저 있어야 `node_modules`가 커밋되지 않습니다
- 생성된 파일 중 불필요한 예제 파일이 있다면 제거하세요
- `app/page.tsx`는 랜딩 페이지로 교체해야 합니다

### 3단계: 수동 설정 (shadcn create 사용 안 하는 경우)

**shadcn create를 사용했다면 이 단계는 건너뛰세요!**

필수 설정 파일들을 수동으로 추가합니다:

#### `package.json`

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

#### `tsconfig.json`

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

#### `next.config.ts`

```typescript
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
  /* config options here */
};

export default nextConfig;
```

#### `postcss.config.mjs`

```javascript
/** @type {import('postcss-load-config').Config} */
const config = {
  plugins: {
    "@tailwindcss/postcss": {},
  },
};

export default config;
```

#### `components.json`

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

각 파일을 추가한 후 커밋:

```bash
git add package.json tsconfig.json next.config.ts postcss.config.mjs components.json
git commit -m "Add configuration files"
```

### 4단계: 유틸리티 파일 추가

#### `lib/utils.ts`

```typescript
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

```bash
mkdir -p lib
# lib/utils.ts 생성 후
git add lib/utils.ts
git commit -m "Add lib/utils.ts"
```

### 5단계: 스타일 파일 추가

#### `app/globals.css`

```css
@import "tailwindcss";
@import "shadcn/tailwind.css";

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

```bash
mkdir -p app
# app/globals.css 생성 후
git add app/globals.css
git commit -m "Add app/globals.css"
```

### 6단계: 기본 레이아웃 및 페이지

#### `app/layout.tsx`

```typescript
import type { Metadata } from "next";
import "./globals.css";

export const metadata: Metadata = {
  title: "Landing Page - Waitlist",
  description: "Beautiful landing page with waitlist functionality",
};

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

#### `app/page.tsx` (랜딩 페이지)

```typescript
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Card, CardContent } from "@/components/ui/card";

export default function Home() {
  return (
    <main className="flex min-h-screen flex-col">
      {/* Hero Section */}
      <section className="flex flex-col items-center justify-center px-4 py-24 text-center">
        <h1 className="text-5xl font-bold tracking-tight lg:text-6xl mb-6">
          Welcome to Our Product
        </h1>
        <p className="text-xl text-muted-foreground mb-8 max-w-2xl">
          Join thousands of users who are already using our amazing product.
        </p>

        {/* Waitlist Form */}
        <Card className="w-full max-w-md">
          <CardContent className="pt-6">
            <form className="space-y-4">
              <Input
                type="email"
                placeholder="Enter your email"
                className="w-full"
              />
              <Button type="submit" className="w-full">
                Join Waitlist
              </Button>
            </form>
          </CardContent>
        </Card>
      </section>

      {/* Features Section */}
      <section className="container mx-auto px-4 py-24">
        <h2 className="text-3xl font-bold text-center mb-12">Features</h2>
        <div className="grid gap-6 md:grid-cols-3">
          <Card>
            <CardContent className="pt-6">
              <h3 className="text-xl font-semibold mb-2">Feature 1</h3>
              <p className="text-muted-foreground">Description of feature 1</p>
            </CardContent>
          </Card>
          <Card>
            <CardContent className="pt-6">
              <h3 className="text-xl font-semibold mb-2">Feature 2</h3>
              <p className="text-muted-foreground">Description of feature 2</p>
            </CardContent>
          </Card>
          <Card>
            <CardContent className="pt-6">
              <h3 className="text-xl font-semibold mb-2">Feature 3</h3>
              <p className="text-muted-foreground">Description of feature 3</p>
            </CardContent>
          </Card>
        </div>
      </section>
    </main>
  );
}
```

```bash
git add app/layout.tsx app/page.tsx
git commit -m "Add layout and landing page"
```

### 7단계: 필요한 shadcn/ui 컴포넌트 추가

```bash
# 의존성 설치 (안전 - .gitignore가 있음)
npm install

# 필요한 컴포넌트만 추가
npx shadcn@latest add button
npx shadcn@latest add input
npx shadcn@latest add card

# 컴포넌트 커밋
git add components/
git commit -m "Add shadcn/ui components"
```

### 8단계: README 추가

`docs/template-examples/landing-waitlist-README.md` 내용을 참고하여 README.md 생성:

```bash
# README.md 생성 후
git add README.md
git commit -m "Add README"
```

### 9단계: 테스트 및 확인

```bash
# 로컬에서 테스트
npm run dev

# 빌드 테스트
npm run build
```

**확인 사항:**

- ✅ `node_modules`가 Git에 포함되지 않았는지 확인
- ✅ `.next` 폴더가 Git에 포함되지 않았는지 확인
- ✅ 모든 파일이 정상적으로 작동하는지 확인

### 10단계: GitHub에 푸시

```bash
# GitHub 리포지토리 생성 (웹사이트에서)
# Public으로 설정, README 추가하지 않기

# 리모트 추가 및 푸시
git remote add origin https://github.com/YOUR_USERNAME/landing-waitlist.git
git push -u origin main
```

### 11단계: 템플릿으로 설정

1. GitHub 리포지토리 페이지로 이동
2. **Settings** → **General**
3. **Template repository** 체크박스 활성화
4. 저장

## ✅ 최종 확인

푸시 후 확인:

1. **GitHub 리포지토리 "Languages" 섹션**

   - CSS 비율이 10% 이하여야 함
   - TypeScript/JavaScript가 대부분

2. **파일 구조**

   - `node_modules` 폴더가 보이지 않아야 함
   - `.next` 폴더가 보이지 않아야 함
   - `.gitignore` 파일이 있어야 함

3. **템플릿 테스트**
   - Rapid Builder에서 프로젝트 생성
   - 생성된 리포지토리에 불필요한 파일이 없는지 확인
   - Vercel 배포 후 정상 작동 확인

## 📁 최종 파일 구조

```
landing-waitlist/
├── .gitignore          ✅
├── package.json        ✅
├── tsconfig.json       ✅
├── next.config.ts      ✅
├── postcss.config.mjs  ✅
├── components.json     ✅
├── README.md           ✅
├── lib/
│   └── utils.ts        ✅
└── app/
    ├── layout.tsx      ✅
    ├── page.tsx        ✅
    └── globals.css     ✅
```

## 💡 팁

- **작은 단위로 커밋**: 한 번에 다 커밋하지 말고 단계별로
- **테스트 먼저**: 각 단계마다 로컬에서 테스트
- **불필요한 파일 제거**: `create next-app`을 사용했다면 예제 파일들 제거
- **README 작성**: 사용자가 쉽게 이해할 수 있도록 상세히 작성

## 🚫 하지 말아야 할 것

- ❌ `create next-app` 사용 후 그대로 푸시
- ❌ `node_modules` 설치 전에 `.gitignore` 추가 안 함
- ❌ 예제 파일들 그대로 두기
- ❌ 불필요한 설정 파일 포함

## 🔗 관련 문서

- [템플릿 최소 파일 구조](./template-minimal-files.md)
- [로컬에서 템플릿 설정](./template-local-setup.md)
- [템플릿 예제 README](../template-examples/landing-waitlist-README.md)
