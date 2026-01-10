# 템플릿 리포지토리 정리 가이드

템플릿 리포지토리에 불필요한 파일(`node_modules`, 빌드 산출물 등)이 포함되어 있어 CSS 비율이 높게 나타나는 문제를 해결하는 방법입니다.

## 🎯 문제 상황

GitHub 리포지토리의 "Languages" 섹션에서 CSS가 50% 이상을 차지하는 경우:

- `node_modules` 폴더가 커밋되어 있음
- `.next`, `out` 등 빌드 산출물이 포함되어 있음
- `.gitignore` 파일이 없거나 제대로 설정되지 않음

## ✅ 해결 방법

### 방법 1: 자동화 스크립트 사용 (가장 쉬움)

```bash
# 스크립트에 실행 권한 부여 (Mac/Linux)
chmod +x scripts/clean-template-repo.sh

# 템플릿 리포지토리 정리
./scripts/clean-template-repo.sh gyorutan/landing-waitlist
```

스크립트가 자동으로:

1. 리포지토리를 클론
2. `.gitignore` 파일 확인/생성
3. 불필요한 파일들을 Git 캐시에서 제거
4. 변경사항 커밋 및 푸시 (선택)

### 방법 2: 수동으로 정리

```bash
# 1. 리포지토리 클론
git clone https://github.com/gyorutan/landing-waitlist.git
cd landing-waitlist

# 2. .gitignore 확인/생성
# .gitignore 파일이 없으면 docs/template-minimal-files.md 참고하여 생성

# 3. Git 캐시에서 불필요한 파일 제거
git rm -r --cached node_modules .next .vercel out coverage 2>/dev/null || true
git rm --cached .env.local .env *.tsbuildinfo 2>/dev/null || true

# 4. 커밋
git commit -m "chore: remove build artifacts and dependencies"

# 5. 푸시
git push origin main
```

### 방법 3: 새로 깨끗한 리포지토리 만들기 (가장 확실함)

이미 많은 불필요한 파일이 커밋되어 있다면, 새로 만드는 것이 더 쉬울 수 있습니다:

1. **새 리포지토리 생성**

   ```bash
   gh repo create gyorutan/landing-waitlist-v2 --public --description "Clean template repository"
   ```

2. **필수 파일만 추가**

   - `docs/template-minimal-files.md` 참고하여 필수 파일만 추가
   - `.gitignore` 파일을 **먼저** 추가

3. **템플릿으로 설정**

   - GitHub 웹사이트에서 Settings → General → Template repository 활성화

4. **기존 리포지토리 업데이트**
   - 데이터베이스의 템플릿 리포지토리 경로를 새 리포지토리로 변경

## 📋 체크리스트

정리 후 확인사항:

- [ ] `.gitignore` 파일이 루트에 있음
- [ ] GitHub 리포지토리 "Languages"에서 CSS 비율이 10% 이하
- [ ] TypeScript/JavaScript가 대부분을 차지
- [ ] 새로 생성된 프로젝트에 불필요한 파일이 없음

## 💡 예방 방법

앞으로 템플릿 리포지토리를 만들 때:

1. **`.gitignore`를 먼저 추가**

   ```bash
   # 리포지토리 생성 후 첫 번째 커밋
   git add .gitignore
   git commit -m "Add .gitignore"
   ```

2. **`node_modules` 설치 전에 `.gitignore` 확인**

   ```bash
   # .gitignore 확인 후
   npm install  # 또는 pnpm install
   ```

3. **빌드 전에 `.gitignore` 확인**
   ```bash
   # .gitignore 확인 후
   npm run build
   ```

## 📝 README를 지워버렸을 때

템플릿 리포지토리에서 README.md를 실수로 삭제한 경우:

### 문제 상황

- 템플릿 상세 페이지에서 "Documentation" 섹션이 비어있음
- "README file not found" 에러 메시지 표시
- 사용자가 템플릿 정보를 확인할 수 없음

### 해결 방법

**README.md를 다시 추가하세요:**

```bash
# 1. 리포지토리 클론 (또는 이미 클론되어 있다면)
git clone https://github.com/[owner]/[repo].git
cd [repo]

# 2. README.md 파일 생성
# docs/template-examples/ 폴더의 예시를 참고하여 작성
# 또는 이전 버전을 Git 히스토리에서 복구

# 3. Git 히스토리에서 이전 README 복구 (가능한 경우)
git log --all --full-history -- README.md
git checkout [commit-hash] -- README.md

# 4. 또는 새로 작성
# docs/template-examples/landing-waitlist-README.md 참고

# 5. 커밋 및 푸시
git add README.md
git commit -m "Add README.md"
git push origin main
```

### README가 없을 때 사용자에게 표시되는 내용

시스템은 자동으로 다음 메시지를 표시합니다:

> "The repository exists but doesn't contain a README file yet. Documentation will be available once the README is added."

이 메시지는 사용자에게 템플릿이 아직 문서화되지 않았음을 알려줍니다.

### 권장사항

- **README는 필수입니다**: 템플릿의 기능, 사용법, 설정 방법을 설명하는 문서입니다
- **최소한의 내용이라도 포함**: 템플릿 이름, 간단한 설명, 시작 방법 정도는 포함하세요
- **예시 참고**: `docs/template-examples/` 폴더의 예시를 참고하여 작성하세요

## ⚠️ 주의사항

- `node_modules`가 이미 커밋되어 있다면, 리포지토리 크기가 매우 커질 수 있습니다
- 이 경우 새 리포지토리를 만드는 것을 권장합니다
- Git 히스토리에서 완전히 제거하려면 `git filter-branch` 또는 BFG Repo-Cleaner를 사용해야 합니다 (고급)
- **README.md는 절대 삭제하지 마세요**: 템플릿 사용자가 정보를 확인할 수 있는 유일한 방법입니다

## 🔗 관련 문서

- [템플릿 최소 파일 구조](./template-minimal-files.md)
- [템플릿 생성 가이드](./template-creation-guide.md)
- [수동 설정 가이드](./manual-setup-steps.md)
