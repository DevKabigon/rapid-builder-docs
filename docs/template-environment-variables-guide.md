# 템플릿 환경 변수 및 플레이스홀더 자동 주입 가이드

이 가이드는 템플릿 제작자를 위한 환경 변수 및 플레이스홀더 자동 주입 기능에 대한 설명입니다.

## 개요

프로젝트 생성 시 다음이 자동으로 템플릿에 주입됩니다:
- 사용자가 설정한 서비스(Resend, Supabase)의 환경 변수
- 브랜드 이름 및 프로젝트 이름으로 플레이스홀더 자동 치환

사용자는 수동으로 환경 변수나 브랜드 이름을 설정할 필요가 없습니다.

## 자동 주입되는 환경 변수

### Resend (활성화 시)

프로젝트 생성 시 Resend가 활성화된 경우, 다음 환경 변수들이 자동으로 주입됩니다:

- `RESEND_API_KEY`: 사용자의 Resend API 키
- `RESEND_AUDIENCE_ID`: 자동 생성된 Audience ID

### Supabase (활성화 시)

프로젝트 생성 시 Supabase가 활성화된 경우, 다음 환경 변수들이 자동으로 주입됩니다:

- `NEXT_PUBLIC_SUPABASE_URL`: Supabase 프로젝트 URL
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`: Supabase Anon Key

## 플레이스홀더 자동 치환

프로젝트 생성 시 템플릿 파일 내의 플레이스홀더가 자동으로 치환됩니다.

### 지원되는 플레이스홀더

다음 플레이스홀더들이 자동으로 치환됩니다:

- `Your Brand` → 사용자가 입력한 브랜드 이름
- `{{BRAND_NAME}}` → 사용자가 입력한 브랜드 이름
- `{{PROJECT_NAME}}` → 자동 생성된 프로젝트 이름 (slug)
- `{{brandName}}` → 사용자가 입력한 브랜드 이름
- `{{projectName}}` → 자동 생성된 프로젝트 이름 (slug)

### 치환되는 파일

다음 파일들이 자동으로 스캔되어 플레이스홀더가 치환됩니다:

- `README.md`
- `package.json`
- `app/layout.tsx`
- `app/page.tsx`
- `components/header.tsx`
- `components/footer.tsx`

### 사용 예시

템플릿 파일에서 다음과 같이 사용하세요:

```tsx
// app/layout.tsx
export default function RootLayout() {
  return (
    <html>
      <head>
        <title>Your Brand</title>
      </head>
      <body>
        <h1>Welcome to {{BRAND_NAME}}</h1>
      </body>
    </html>
  );
}
```

프로젝트 생성 시 "Acme Corp"을 브랜드 이름으로 입력하면:

```tsx
// 생성된 파일
export default function RootLayout() {
  return (
    <html>
      <head>
        <title>Acme Corp</title>
      </head>
      <body>
        <h1>Welcome to Acme Corp</h1>
      </body>
    </html>
  );
}
```

## 템플릿에서 사용 방법

### 1. 환경 변수 사용

템플릿 코드에서 다음과 같이 환경 변수를 사용하세요:

```typescript
// Resend 사용 예시
const resendApiKey = process.env.RESEND_API_KEY;
const audienceId = process.env.RESEND_AUDIENCE_ID;

if (resendApiKey && audienceId) {
  // Resend 기능 사용
  const resend = new Resend(resendApiKey);
  // ...
}

// Supabase 사용 예시
const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL;
const supabaseAnonKey = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY;

if (supabaseUrl && supabaseAnonKey) {
  // Supabase 클라이언트 생성
  const supabase = createClient(supabaseUrl, supabaseAnonKey);
  // ...
}
```

### 2. 환경 변수 존재 여부 확인

환경 변수가 주입되었는지 확인하고, 없을 경우 적절한 처리를 하세요:

```typescript
// Resend 예시
if (!process.env.RESEND_API_KEY) {
  console.warn("RESEND_API_KEY is not set");
  // Fallback 처리 또는 에러 표시
}

// Supabase 예시
if (!process.env.NEXT_PUBLIC_SUPABASE_URL) {
  console.warn("Supabase environment variables are not set");
  // Fallback 처리 또는 에러 표시
}
```

### 3. 타입 안전성 (TypeScript)

TypeScript를 사용하는 경우, 환경 변수 타입을 정의하세요:

```typescript
// types/env.d.ts 또는 env.ts
declare namespace NodeJS {
  interface ProcessEnv {
    RESEND_API_KEY?: string;
    RESEND_AUDIENCE_ID?: string;
    NEXT_PUBLIC_SUPABASE_URL?: string;
    NEXT_PUBLIC_SUPABASE_ANON_KEY?: string;
  }
}
```

## 파일 구조

### .env.local 파일

- 프로젝트 생성 시 `.env.local` 파일이 자동으로 생성됩니다
- 이 파일에는 주입된 환경 변수들이 포함됩니다
- **중요**: `.env.local` 파일은 Git에 커밋되지 않도록 `.gitignore`에 포함되어 있어야 합니다

### .env.example 파일 (권장)

템플릿에 `.env.example` 파일을 포함하여 필요한 환경 변수를 문서화하세요:

```env
# Resend Configuration
# These will be automatically set when Resend is enabled during project creation
RESEND_API_KEY=your_resend_api_key
RESEND_AUDIENCE_ID=your_audience_id

# Supabase Configuration
# These will be automatically set when Supabase is enabled during project creation
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

## 템플릿 체크리스트

템플릿을 제작할 때 다음 사항을 확인하세요:

- [ ] `.gitignore`에 `.env.local`이 포함되어 있는지 확인
- [ ] `.env.example` 파일을 포함하여 환경 변수를 문서화
- [ ] 환경 변수가 없을 경우 적절한 에러 처리 또는 Fallback 구현
- [ ] README.md에 환경 변수에 대한 설명 추가 (선택사항)
- [ ] 브랜드 이름이 필요한 곳에 플레이스홀더 사용 (`Your Brand`, `{{BRAND_NAME}}` 등)
- [ ] 프로젝트 이름이 필요한 곳에 플레이스홀더 사용 (`{{PROJECT_NAME}}`, `{{projectName}}` 등)

## 예시: .gitignore 설정

템플릿의 `.gitignore` 파일에 다음을 포함하세요:

```gitignore
# local env files
.env.local
.env*.local

# 환경 변수 파일 (일반적으로)
.env
```

## 예시: README.md 섹션

템플릿의 README.md에 다음과 같은 섹션을 추가할 수 있습니다:

```markdown
## Environment Variables

This template uses the following environment variables:

### Resend (Optional)

- `RESEND_API_KEY`: Your Resend API key
- `RESEND_AUDIENCE_ID`: Your Resend Audience ID

These are automatically set when you enable Resend during project creation.

### Supabase (Optional)

- `NEXT_PUBLIC_SUPABASE_URL`: Your Supabase project URL
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`: Your Supabase anonymous key

These are automatically set when you enable Supabase during project creation.

> **Note**: Environment variables are automatically injected during project creation. You don't need to set them manually.
```

## 주의사항

1. **환경 변수는 선택사항입니다**: 사용자가 Resend나 Supabase를 활성화하지 않으면 해당 환경 변수는 주입되지 않습니다.

2. **로컬 개발**: `.env.local` 파일은 로컬 개발 환경에서 사용됩니다. 프로덕션 배포 시에는 Vercel 환경 변수로 설정됩니다.

3. **보안**: 환경 변수는 민감한 정보를 포함할 수 있으므로, 절대 Git에 커밋하지 마세요.

4. **타입 체크**: TypeScript를 사용하는 경우, 환경 변수가 `undefined`일 수 있으므로 적절한 타입 가드를 사용하세요.

## 문제 해결

### 환경 변수가 주입되지 않는 경우

- 사용자가 해당 서비스를 활성화하지 않았을 수 있습니다
- 프로젝트 생성 과정에서 오류가 발생했을 수 있습니다
- 환경 변수 이름이 정확한지 확인하세요

### .env.local 파일이 Git에 커밋되는 경우

- `.gitignore`에 `.env.local`이 포함되어 있는지 확인하세요
- 이미 커밋된 경우, Git 히스토리에서 제거해야 합니다

## 추가 리소스

- [Next.js Environment Variables](https://nextjs.org/docs/app/building-your-application/configuring/environment-variables)
- [Resend Documentation](https://resend.com/docs)
- [Supabase Documentation](https://supabase.com/docs)
