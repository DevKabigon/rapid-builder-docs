# 템플릿 프리셋 설정 가이드

템플릿 제작 시 사용자가 선택한 UI 프리셋 설정이 자동으로 적용되는 방식과 템플릿에서 고려해야 할 사항들을 설명합니다.

## 개요

사용자가 프로젝트를 생성할 때 선택한 프리셋 설정(Radius, Theme, Icon Library, Font)은 자동으로 `components.json` 파일에 저장됩니다. 템플릿 제작자는 이 설정을 활용하여 일관된 UI를 제공할 수 있습니다.

## 프로젝트 생성 시 일어나는 일

### 1. GitHub 레포지토리 생성

- 템플릿 레포지토리에서 새 레포지토리 생성
- 템플릿의 모든 파일이 복사됨

### 2. `components.json` 자동 생성/업데이트

- 사용자가 선택한 프리셋 설정이 `components.json`에 저장됨
- 기존 `components.json`이 있으면 병합됨 (사용자 설정이 우선)

### 3. 패키지 자동 설치: 없음

- **중요**: 아이콘 라이브러리나 폰트는 자동으로 설치되지 않습니다
- 템플릿의 `package.json`에 필요한 패키지를 미리 포함해야 합니다

## 프리셋 옵션 설명

### 1. Radius (Style)

사용자가 선택하는 옵션: **Default** 또는 **Box**

- **Default (vega)**: `0.5rem` (8px) - 클래식하고 깔끔한 둥근 모서리
- **Box (lyra)**: `0.1rem` (~1.6px) - 날카롭고 박스 형태의 최소한의 둥근 모서리

**템플릿에서 활용:**

```tsx
// CSS 변수로 자동 적용됨
<div style={{ borderRadius: "var(--radius)" }}>{/* 컴포넌트 */}</div>
```

### 2. Theme

사용자가 선택하는 옵션: **Neutral**, **Amber**, **Blue**, **Cyan**, **Emerald**, **Fuchsia**, **Green**, **Indigo**, **Lime**, **Orange**, **Pink**, **Purple**, **Red**, **Rose**, **Sky**, **Teal**, **Violet**, **Yellow**

- Primary, Secondary, Accent 색상에 적용됨
- 배경색은 항상 Neutral로 고정됨 (실제 작업 환경과 동일)

**템플릿에서 활용:**

```tsx
// CSS 변수로 자동 적용됨
<button
  style={{
    backgroundColor: "hsl(var(--primary))",
    color: "hsl(var(--primary-foreground))",
  }}
>
  Primary Button
</button>
```

### 3. Icon Library

사용자가 선택하는 옵션: **Lucide**, **Tabler Icons**, **HugeIcons**, **Phosphor Icons**

**중요**: 템플릿의 `package.json`에 선택 가능한 모든 아이콘 라이브러리를 포함해야 합니다.

**권장 package.json 설정:**

```json
{
  "dependencies": {
    "lucide-react": "^0.562.0",
    "@tabler/icons-react": "^3.36.1",
    "@hugeicons/react": "^1.1.4",
    "@hugeicons/core-free-icons": "^3.1.1",
    "phosphor-react": "^1.4.1"
  }
}
```

**템플릿에서 활용:**

```tsx
// components.json의 iconLibrary 값을 확인하여 사용
// 예시: 동적으로 아이콘 라이브러리 선택
import { Star } from "lucide-react";
import { IconStar } from "@tabler/icons-react";
import { HugeiconsIcon } from "@hugeicons/react";
import { Star as PhosphorStar } from "phosphor-react";
import { StarIcon } from "@hugeicons/core-free-icons";

// 또는 템플릿에서 하나의 라이브러리만 사용하고
// 사용자가 나중에 변경할 수 있도록 안내
```

### 4. Font

사용자가 선택하는 옵션: **Inter**, **Noto Sans**, **Nunito Sans**, **Figtree**

**템플릿에서 활용:**

- Google Fonts를 통해 자동으로 로드됨
- CSS 변수 `--font-family`로 적용됨

```tsx
// globals.css 또는 layout.tsx에서
import { Inter } from "next/font/google";

const inter = Inter({ subsets: ["latin"] });

export default function RootLayout({ children }) {
  return (
    <html lang="en" className={inter.className}>
      {children}
    </html>
  );
}
```

## 템플릿 제작 시 체크리스트

### 필수 사항

- [ ] **package.json에 아이콘 라이브러리 포함**

  - 모든 선택 가능한 아이콘 라이브러리를 dependencies에 추가
  - 사용자가 선택한 라이브러리를 바로 사용할 수 있도록 준비

- [ ] **components.json 파일 포함 여부 결정**

  - 포함하지 않으면: 시스템이 자동으로 생성
  - 포함하면: 사용자 설정과 병합됨 (사용자 설정이 우선)

- [ ] **CSS 변수 활용**
  - `hsl(var(--primary))`, `hsl(var(--radius))` 등 CSS 변수 사용
  - 하드코딩된 색상이나 radius 값 지양

### 권장 사항

- [ ] **아이콘 사용 예시 제공**

  - 템플릿에서 사용하는 아이콘 라이브러리 예시 코드 포함
  - README에 아이콘 라이브러리 변경 방법 안내

- [ ] **테마 색상 활용**

  - Primary, Secondary, Accent 색상을 적절히 활용
  - 배경색은 Neutral로 고정되어 있음을 고려

- [ ] **Radius 스타일 고려**
  - Default와 Box 스타일 모두에서 잘 보이도록 디자인
  - CSS 변수 `var(--radius)` 사용

## components.json 구조

자동 생성되는 `components.json` 예시:

```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "vega",
  "rsc": true,
  "tsx": true,
  "tailwind": {
    "config": "",
    "css": "app/globals.css",
    "baseColor": "neutral",
    "cssVariables": true,
    "prefix": ""
  },
  "iconLibrary": "lucide",
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils",
    "ui": "@/components/ui",
    "lib": "@/lib",
    "hooks": "@/hooks"
  },
  "menuColor": "default",
  "menuAccent": "subtle",
  "registries": {},
  "componentLibrary": "radix-ui",
  "font": "inter"
}
```

## 실제 예시

### 아이콘 라이브러리 사용 예시

```tsx
// components.json을 읽어서 동적으로 아이콘 사용
import { readFileSync } from "fs";
import { join } from "path";

const componentsJson = JSON.parse(
  readFileSync(join(process.cwd(), "components.json"), "utf-8")
);

const iconLibrary = componentsJson.iconLibrary;

// iconLibrary에 따라 다른 아이콘 사용
function Icon({ name }: { name: string }) {
  switch (iconLibrary) {
    case "lucide":
      return <LucideIcon name={name} />;
    case "tabler-icons":
      return <TablerIcon name={name} />;
    case "hugeicons":
      return <HugeiconsIcon icon={name} />;
    case "phosphor-icons":
      return <PhosphorIcon name={name} />;
    default:
      return <LucideIcon name={name} />;
  }
}
```

### CSS 변수 활용 예시

```tsx
// Button 컴포넌트 예시
export function Button({ children }: { children: React.ReactNode }) {
  return (
    <button
      className="px-4 py-2 rounded-md"
      style={{
        backgroundColor: "hsl(var(--primary))",
        color: "hsl(var(--primary-foreground))",
        borderRadius: "var(--radius)",
      }}
    >
      {children}
    </button>
  );
}
```

## FAQ

### Q: 템플릿에 components.json을 포함해야 하나요?

A: 선택사항입니다. 포함하지 않으면 시스템이 자동으로 생성하고, 포함하면 사용자 설정과 병합됩니다.

### Q: 아이콘 라이브러리를 자동으로 설치하나요?

A: 아니요. 템플릿의 `package.json`에 필요한 모든 아이콘 라이브러리를 포함해야 합니다.

### Q: 사용자가 선택한 테마가 모든 색상에 적용되나요?

A: 아니요. Primary, Secondary, Accent 색상만 테마에 따라 변경되고, 배경색은 항상 Neutral로 고정됩니다.

### Q: 폰트는 자동으로 로드되나요?

A: `components.json`에 폰트 정보는 저장되지만, 템플릿에서 직접 Google Fonts를 로드해야 합니다.

## 참고 자료

- [템플릿 생성 가이드](./template-creation-guide.md)
- [shadcn/ui 공식 문서](https://ui.shadcn.com)
- [components.json 스키마](https://ui.shadcn.com/schema.json)
