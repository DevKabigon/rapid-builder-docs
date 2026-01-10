# 템플릿 레포지토리 생성 가이드

## 단계별 접근 방법

### 1단계: 최소 템플릿 (빠른 테스트용)

- README.md만 있는 최소 템플릿 생성
- README 로드가 정상 작동하는지 확인
- 이후 점진적으로 기능 추가

### 2단계: 기본 구조 템플릿

- Next.js 기본 구조 추가
- package.json, tsconfig.json 등 필수 파일
- 간단한 페이지 1-2개

### 3단계: 완성된 템플릿

- 모든 기능 구현
- 환경 변수 설정
- 배포 가이드

## 템플릿 우선순위

### 추천 순서:

1. **Landing Page + Waitlist** (가장 간단)

   - 정적 페이지 위주
   - 이메일 수집 기능만
   - Supabase/Vercel 선택적

2. **AI Chatbot Template** (중간 난이도)

   - OpenAI API 통합
   - 채팅 UI
   - Supabase 필수

3. **Next.js SaaS Starter** (가장 복잡)
   - 인증, 결제, 대시보드
   - 모든 통합 필요

## 템플릿 레포지토리 구조

### 필수 파일:

```
template-name/
├── README.md              # 필수! (우리가 렌더링할 문서)
├── package.json           # 의존성 관리
├── tsconfig.json          # TypeScript 설정
├── next.config.ts         # Next.js 설정
├── tailwind.config.ts     # Tailwind 설정 (필요시)
├── .env.example           # 환경 변수 예시
├── .gitignore            # Git 무시 파일
└── app/                   # Next.js App Router
    ├── layout.tsx
    ├── page.tsx
    └── ...
```

### README.md 필수 섹션:

```markdown
# Template Name

## Overview

템플릿 설명

## Features

- Feature 1
- Feature 2

## Tech Stack

- Next.js 16.1.1
- React 19.2.3
- TypeScript 5.0.0

## Getting Started

설치 및 실행 방법

## Environment Variables

필요한 환경 변수 설명

## Deployment

배포 가이드
```

## GitHub Template Repository 설정

1. **레포지토리 생성**

   - GitHub에서 새 레포지토리 생성
   - 이름: `rapid-builder-templates/[template-name]`
   - Public으로 설정 (README 로드를 위해 필수)

2. **Template Repository로 설정** ⚠️ 필수!

   - 레포지토리 페이지에서 **Settings** 탭 클릭
   - 왼쪽 사이드바에서 **General** 선택
   - 페이지를 아래로 스크롤하여 **Template repository** 섹션 찾기
   - **Template repository** 체크박스 활성화 ✅
   - 변경사항 저장
   - 이렇게 하면 "Use this template" 버튼이 생기고, GitHub API를 통해 템플릿에서 리포지토리를 생성할 수 있습니다

   **참고:** 템플릿 리포지토리로 설정하지 않으면 프로젝트 생성 시 에러가 발생합니다!

3. **README.md 작성**

   - 상대 경로 이미지는 `./assets/image.png` 형식 사용
   - 우리 시스템이 자동으로 GitHub raw URL로 변환

4. **초기 커밋**
   - 최소한 README.md만이라도 커밋
   - main 브랜치에 푸시

## 브랜드 정보 전달하기

템플릿에서 사용자 브랜드 정보를 받아서 사용하려면 **플레이스홀더(Placeholder)**를 사용하세요.

### 지원되는 플레이스홀더

템플릿 파일에서 다음 플레이스홀더를 사용하면 프로젝트 생성 시 자동으로 실제 값으로 교체됩니다:

#### 브랜드 이름 (Brand Name)

- `Your Brand` - 일반적인 브랜드 이름 플레이스홀더
- `{{BRAND_NAME}}` - 대문자 형식
- `{{brandName}}` - camelCase 형식

#### 프로젝트 이름 (Project Name)

- `{{PROJECT_NAME}}` - 대문자 형식
- `{{projectName}}` - camelCase 형식

### 사용 예시

#### 1. README.md에서 사용

```markdown
# {{BRAND_NAME}}

Welcome to {{BRAND_NAME}} - A modern web application built with Next.js.

## Getting Started

This project is named `{{projectName}}` and uses the latest technologies.
```

#### 2. package.json에서 사용

```json
{
  "name": "{{projectName}}",
  "description": "{{BRAND_NAME}} - A modern web application",
  "version": "1.0.0"
}
```

#### 3. React 컴포넌트에서 사용

```tsx
// app/layout.tsx
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html>
      <head>
        <title>{{ BRAND_NAME }}</title>
      </head>
      <body>
        <header>
          <h1>{{ BRAND_NAME }}</h1>
        </header>
        {children}
      </body>
    </html>
  );
}
```

```tsx
// app/page.tsx
export default function HomePage() {
  return (
    <div>
      <h1>Welcome to {{ BRAND_NAME }}</h1>
      <p>This is the homepage of {{ projectName }}.</p>
    </div>
  );
}
```

#### 4. 컴포넌트에서 사용

```tsx
// components/header.tsx
export function Header() {
  return (
    <header>
      <nav>
        <a href="/">{{ BRAND_NAME }}</a>
      </nav>
    </header>
  );
}
```

### 자동 교체되는 파일 목록

다음 파일들에서 플레이스홀더가 자동으로 교체됩니다:

- `README.md`
- `package.json`
- `app/layout.tsx`
- `app/page.tsx`
- `components/header.tsx`
- `components/footer.tsx`

**참고:** 파일이 존재하지 않으면 자동으로 건너뜁니다. 템플릿에 필요한 파일만 포함하면 됩니다.

### 주의사항

1. **정확한 플레이스홀더 사용**: 위에 나열된 플레이스홀더만 지원됩니다. 다른 형식은 교체되지 않습니다.

2. **대소문자 구분**: `{{BRAND_NAME}}`과 `{{brandName}}`은 다릅니다. 일관되게 사용하세요.

3. **전역 교체**: 파일 내의 모든 플레이스홀더가 교체됩니다. 예를 들어 `{{BRAND_NAME}}`이 10번 나오면 모두 교체됩니다.

4. **정규식 이스케이프**: 특수 문자(`.*+?^${}()|[]\`)는 자동으로 이스케이프되므로 안전하게 사용할 수 있습니다.

### 예시: 완전한 템플릿 파일

```tsx
// app/layout.tsx
import type { Metadata } from "next";

export const metadata: Metadata = {
  title: "{{BRAND_NAME}}",
  description: "Welcome to {{BRAND_NAME}}",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>
        <header>
          <h1>{{ BRAND_NAME }}</h1>
        </header>
        <main>{children}</main>
        <footer>
          <p>&copy; 2024 {{ BRAND_NAME }}. All rights reserved.</p>
        </footer>
      </body>
    </html>
  );
}
```

## 빠른 시작: Landing Page 템플릿

가장 간단한 템플릿부터 시작하세요:

1. GitHub에 `rapid-builder-templates/landing-waitlist` 생성
2. README.md만 작성 (아래 예시 참고)
3. 커밋 & 푸시
4. 우리 앱에서 확인

이렇게 하면 README 로드가 작동하는지 바로 확인할 수 있습니다!
