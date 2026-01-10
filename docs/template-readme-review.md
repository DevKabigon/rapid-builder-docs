# 템플릿 README 검토 가이드

템플릿 제작자가 작성한 README를 검토할 때 확인해야 할 사항들입니다.

## ✅ 잘 작성된 README의 특징

### 1. 구조와 내용

- ✅ 명확한 섹션 구분
- ✅ 상세한 설명
- ✅ 코드 예시 포함
- ✅ 설치 및 실행 가이드
- ✅ 배포 가이드

### 2. 기술적 정확성

- ✅ 정확한 버전 정보
- ✅ 올바른 기술 스택 설명
- ✅ 환경 변수 설명

## ⚠️ 필수 확인 사항

### 1. 브랜드 플레이스홀더 사용

**문제:** README에 브랜드 이름이 하드코딩되어 있으면 안 됩니다.

**❌ 잘못된 예:**

```markdown
# Premium Landing Page Template

Welcome to Your Product Name
```

**✅ 올바른 예:**

```markdown
# {{BRAND_NAME}}

Welcome to {{BRAND_NAME}} - A modern web application
```

**지원되는 플레이스홀더:**

- `{{BRAND_NAME}}` - 대문자 형식
- `{{brandName}}` - camelCase 형식
- `{{PROJECT_NAME}}` - 프로젝트 이름
- `{{projectName}}` - 프로젝트 이름 (camelCase)

### 2. CSS 하드코딩 경고

README의 Customization 섹션에 다음 내용이 포함되어야 합니다:

```markdown
### Colors & Theme

⚠️ **중요**: 이 템플릿은 CSS 변수를 사용합니다. 색상이나 radius 값을 하드코딩하지 마세요.

- 모든 색상은 `hsl(var(--primary))`, `hsl(var(--secondary))` 등 CSS 변수 사용
- Radius는 `var(--radius)` 사용
- 사용자가 선택한 프리셋 설정이 자동으로 적용됩니다
```

### 3. 환경 변수 설명

환경 변수 섹션에서 `BRAND_NAME`을 언급할 때:

```markdown
| Variable         | Description                                                                 | Required |
| ---------------- | --------------------------------------------------------------------------- | -------- |
| `RESEND_API_KEY` | Your Resend API key                                                         | ✅       |
| `BRAND_NAME`     | ⚠️ **자동 설정됨** - Rapid Builder에서 프로젝트 생성 시 자동으로 설정됩니다 | ❌       |
```

## 📋 README 검토 체크리스트

템플릿 제작자의 README를 검토할 때 다음을 확인하세요:

- [ ] 브랜드 이름이 플레이스홀더(`{{BRAND_NAME}}`)로 되어 있는가?
- [ ] CSS 하드코딩을 피해야 한다는 경고가 있는가?
- [ ] 프리셋 설정에 대한 설명이 있는가?
- [ ] 환경 변수 설명이 정확한가?
- [ ] 설치 및 실행 가이드가 명확한가?
- [ ] 배포 가이드가 포함되어 있는가?
- [ ] 프로젝트 구조 설명이 있는가?

## 💡 피드백 제공 예시

템플릿 제작자에게 제공할 수 있는 피드백:

### 긍정적인 피드백

- "README가 매우 상세하고 전문적으로 작성되었습니다!"
- "프리셋 설정에 대한 설명이 잘 되어 있습니다."
- "코드 예시가 명확하고 이해하기 쉽습니다."

### 개선 제안

- "브랜드 이름을 `{{BRAND_NAME}}` 플레이스홀더로 변경해주세요."
- "CSS 하드코딩을 피해야 한다는 경고를 추가해주세요."
- "환경 변수 섹션에서 `BRAND_NAME`이 자동 설정됨을 명시해주세요."

## 🔗 관련 문서

- [템플릿 생성 가이드](./template-creation-guide.md)
- [템플릿 프리셋 가이드](./template-preset-guide.md)
- [템플릿 예시 README](./template-examples/landing-waitlist-README.md)
