# 프로젝트 생성 테스트 가이드

## 테스트 전 확인사항

### 1. 마이그레이션 실행 확인
다음 마이그레이션들이 실행되어야 합니다:
- ✅ `004_template_enhancements.sql` (템플릿 확장)
- ✅ `005_job_logs.sql` (Job 로그 테이블)
- ✅ `006_job_step_state.sql` (Job 단계 상태)

**확인 방법:**
- Supabase Dashboard → Database → Migrations에서 확인
- 또는 SQL Editor에서 다음 쿼리 실행:
```sql
SELECT column_name 
FROM information_schema.columns 
WHERE table_name = 'project_jobs' 
AND column_name IN ('completed_steps', 'step_results');

SELECT EXISTS (
  SELECT FROM information_schema.tables 
  WHERE table_schema = 'public' 
  AND table_name = 'job_logs'
);
```

### 2. 필수 설정 확인
- ✅ GitHub 토큰 설정됨
- ✅ 템플릿 데이터베이스에 존재 (`landing-waitlist` 템플릿)
- ✅ 로그인 상태

## 기대 동작

### 정상 케이스 (마이그레이션 완료 시)

#### 1. 프로젝트 생성 시작
- "Create Project" 버튼 클릭
- Job이 생성되고 `pending` 상태로 시작

#### 2. 병렬 실행 (GitHub + Supabase)
- **GitHub 레포지토리 생성** (병렬)
  - 로그: "Creating GitHub repository..."
  - 완료 시: `completed_steps`에 "github" 추가
  - `step_results.github`에 `{repoUrl: "...", completed: true}` 저장
  
- **Supabase 프로젝트 생성** (병렬, 활성화된 경우)
  - 로그: "Creating Supabase project..."
  - 완료 시: `completed_steps`에 "supabase" 추가
  - `step_results.supabase`에 프로젝트 정보 저장

#### 3. Vercel 배포 (GitHub 완료 후)
- GitHub 레포지토리가 생성된 후에만 실행
- 로그: "Deploying to Vercel..."
- 완료 시: `completed_steps`에 "vercel" 추가

#### 4. 완료
- `status`: "completed"
- `progress`: 100%
- `projects` 테이블에 최종 프로젝트 레코드 생성

### 로그 기록
모든 단계에서 `job_logs` 테이블에 로그가 기록됩니다:
- `step`: "github", "supabase", "vercel", "start", "complete", "error"
- `level`: "info", "warning", "error"
- `message`: 상세 메시지
- `details`: JSONB 형태의 추가 정보

### 멱등성 테스트
1. 프로젝트 생성 시작
2. 중간에 실패하거나 중단
3. 같은 Job ID로 다시 시작
4. **기대 결과**: 완료된 단계는 스킵되고, 실패한 단계부터 재시작

## 예상 에러 케이스

### 마이그레이션 미실행 시
```
Error: column "completed_steps" does not exist
또는
Error: relation "job_logs" does not exist
```

**해결 방법**: 마이그레이션 실행 필요

### GitHub 토큰 없음
```
Error: GitHub token not found
```

**해결 방법**: GitHub 토큰 설정 필요

### 템플릿 레포지토리 없음
```
Error: Repository not found
```

**해결 방법**: 템플릿 레포지토리가 존재하는지 확인

## 현재 UI 상태

**Progress Tracker**는 아직 기본 버전입니다:
- ✅ 프로그레스 바 표시
- ✅ 상태 메시지 표시
- ❌ 로그 스트리밍 미구현 (Phase 3에서 구현 예정)
- ❌ 터미널 스타일 UI 미구현 (Phase 3에서 구현 예정)

## 테스트 체크리스트

- [ ] 마이그레이션 실행 확인
- [ ] GitHub 토큰 설정 확인
- [ ] 템플릿 존재 확인
- [ ] 프로젝트 생성 시작
- [ ] 병렬 실행 확인 (GitHub + Supabase 동시 진행)
- [ ] 로그가 `job_logs` 테이블에 기록되는지 확인
- [ ] `completed_steps`와 `step_results`가 업데이트되는지 확인
- [ ] 완료 후 `projects` 테이블에 레코드 생성 확인

## 다음 단계 (Phase 3)

테스트가 성공하면:
1. 로그 스트리밍 API 구현
2. 터미널 스타일 Progress Tracker
3. 실시간 로그 표시
4. 성공 애니메이션 및 바로가기 버튼
