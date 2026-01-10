# 문서 공개 전략 가이드

SaaS 프로젝트 코드는 비공개로 유지하면서, README와 문서는 공개하는 방법들입니다.

## 🎯 목표

- ✅ README와 문서는 공개하여 프로젝트를 홍보하고 사용자가 이해할 수 있게
- ✅ 소스 코드는 비공개로 유지하여 비즈니스 로직 보호
- ✅ SEO 최적화로 검색 엔진에서 발견 가능

---

## 방법 1: 별도 퍼블릭 문서 레포지토리 (추천 ⭐)

### 장점
- ✅ 구현이 간단함
- ✅ GitHub에서 직접 문서 확인 가능
- ✅ GitHub Stars로 프로젝트 인기도 측정 가능
- ✅ 이슈/PR로 문서 피드백 받기 가능

### 단계별 가이드

#### 1. 퍼블릭 레포지토리 생성

```bash
# GitHub에서 새 레포지토리 생성
# 이름: rapid-builder-docs (또는 rapid-builder)
# Public으로 설정
```

#### 2. 문서 동기화

```bash
# 프로젝트 루트에서 실행
pnpm sync:docs

# 또는 수동 실행
bash scripts/sync-docs.sh ../rapid-builder-docs
```

#### 3. README 수정 (필요시)

퍼블릭 레포지토리의 README 상단에 다음을 추가:

```markdown
> **Note**: This is the documentation repository. The main source code is private.

# 🚀 Rapid Builder Documentation

[원본 README 내용...]
```

#### 4. 자동화 (선택사항)

GitHub Actions로 자동 동기화 설정:

```yaml
# .github/workflows/sync-docs.yml
name: Sync Documentation

on:
  push:
    paths:
      - 'README.md'
      - 'docs/**'
    branches:
      - main

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Sync to public repo
        run: |
          git clone https://github.com/YOUR_USERNAME/rapid-builder-docs.git public-docs
          cp README.md public-docs/
          cp -r docs public-docs/
          cd public-docs
          git config user.name "GitHub Actions"
          git config user.email "actions@github.com"
          git add .
          git commit -m "Update documentation" || exit 0
          git push https://${{ secrets.PUBLIC_REPO_TOKEN }}@github.com/YOUR_USERNAME/rapid-builder-docs.git
```

---

## 방법 2: 문서 전용 웹사이트 (고급)

### 장점
- ✅ 더 나은 SEO
- ✅ 커스터마이징 가능한 디자인
- ✅ 검색 기능, 다크모드 등 추가 기능
- ✅ 프로페셔널한 느낌

### 옵션 A: Next.js 정적 사이트

```bash
# 문서 전용 Next.js 프로젝트 생성
npx create-next-app@latest rapid-builder-docs-site

# README와 docs를 마크다운으로 렌더링
# next-mdx-remote 또는 remark 사용
```

### 옵션 B: Docusaurus

```bash
npx create-docusaurus@latest rapid-builder-docs classic

# README와 docs 폴더를 복사
# 자동으로 마크다운을 웹페이지로 변환
```

### 옵션 C: Vercel Documentation

Vercel의 문서 템플릿 사용:
- 자동 SEO 최적화
- 검색 기능 내장
- 빠른 로딩 속도

---

## 방법 3: 하이브리드 접근법

### 퍼블릭 레포 + 문서 사이트

1. **퍼블릭 레포지토리**: GitHub에서 문서 확인
2. **문서 웹사이트**: SEO 최적화된 공식 문서
3. **메인 앱**: 문서 링크 제공

```
rapid-builder.com/docs → 문서 웹사이트
rapid-builder.com → 메인 SaaS 앱
github.com/username/rapid-builder-docs → GitHub 문서
```

---

## 🔒 보안 고려사항

### 공개하지 말아야 할 것

- ❌ `.env` 파일이나 실제 환경 변수
- ❌ API 키나 토큰
- ❌ 데이터베이스 스키마 (민감한 정보 포함 시)
- ❌ 내부 비즈니스 로직
- ❌ 사용자 데이터나 통계

### 공개해도 괜찮은 것

- ✅ README와 문서
- ✅ 예제 코드 (민감한 정보 없이)
- ✅ API 사용 예시
- ✅ 아키텍처 다이어그램
- ✅ 템플릿 예시

---

## 📊 추천 전략

### 시작 단계
1. **퍼블릭 문서 레포지토리 생성** (방법 1)
2. README와 docs 폴더 복사
3. 수동 또는 스크립트로 동기화

### 성장 단계
1. **문서 웹사이트 추가** (방법 2)
2. SEO 최적화
3. 검색 기능 추가

### 성숙 단계
1. **자동 동기화** (GitHub Actions)
2. 문서 버전 관리
3. 다국어 지원 (필요시)

---

## 💡 추가 팁

### README 최적화

퍼블릭 문서 레포지토리의 README에 추가할 내용:

```markdown
## 📦 Repository Structure

- **Main Repository**: Private (source code)
- **Documentation Repository**: This repository (public)
- **Live Application**: [rapid-builder.com](https://rapid-builder.com)

## 🔗 Links

- 🌐 [Official Website](https://rapid-builder.com)
- 📚 [Documentation](https://rapid-builder.com/docs)
- 🐛 [Report Issues](https://rapid-builder.com/support)
- 💬 [Discord Community](https://discord.gg/rapid-builder)
```

### SEO 최적화

- GitHub 레포지토리 설명에 키워드 포함
- Topics 추가: `saas`, `nextjs`, `automation`, `developer-tools`
- README에 적절한 헤딩 구조 사용
- 이미지 alt 텍스트 추가

---

## 🚀 빠른 시작

가장 빠르게 시작하려면:

```bash
# 1. 퍼블릭 레포지토리 생성 (GitHub 웹사이트에서)
# 2. 문서 동기화
pnpm sync:docs

# 3. 퍼블릭 레포에서 커밋
cd ../rapid-builder-docs
git add .
git commit -m "Initial documentation"
git push origin main
```

완료! 🎉
