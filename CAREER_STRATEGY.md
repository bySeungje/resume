# Developer Career Strategy 2026

> 작성일: 2026-02-18
> 목표: 체계적인 개인 브랜딩과 커리어 성장을 위한 전략 문서

---

## 핵심 원칙

**"한 곳에 쓰고, 여러 곳에 퍼뜨린다" (Write Once, Publish Everywhere)**

이 레포가 커리어 관리의 Single Source of Truth 역할을 한다.

```
resume/
├── CAREER_STRATEGY.md      ← 이 문서 (전략 + 로드맵)
├── resume.json              ← JSON Resume 표준 스키마 (이력서 원본)
├── README.md                ← GitHub 프로필 README 템플릿
├── posts/                   ← 블로그 글 마크다운 원본
├── projects/                ← 프로젝트별 포트폴리오 설명
└── .github/workflows/       ← 자동화 파이프라인
```

---

## 플랫폼 전략

### 운영할 플랫폼 (3개만)

| 플랫폼 | 역할 | 우선순위 |
|--------|------|----------|
| **Velog** | 국내 개발자 도달, 한글 기술 블로그 | 주력 |
| **dev.to** | 글로벌 노출, API 자동화 가능, 영문 크로스포스팅 | 보조 |
| **LinkedIn** | 헤드헌터/채용담당자 접점, 프로페셔널 브랜딩 | 보조 |

### 보조 인프라

| 인프라 | 역할 |
|--------|------|
| **GitHub Profile** | 기술력 증명의 허브, README 자동 갱신 |
| **resume.json** | 이력서 버전 관리, 테마 교체로 PDF/웹 자동 생성 |
| **GitHub Actions** | Velog RSS → README 갱신, 크로스포스팅 자동화 |

---

## 커리어 자산: MeowRo 프로젝트

### 임팩트 있는 1줄 소개
> 길고양이 돌보미 커뮤니티를 위한 크로스플랫폼 앱을 기획부터 App Store 심사 통과까지 1인 풀스택으로 완성

### 기술 스택 어필 포인트
- **프론트엔드**: Flutter 3.41 + Riverpod + Clean Architecture
- **백엔드**: Supabase (Auth, PostgreSQL, Storage, Edge Functions, Realtime)
- **인프라**: FCM 푸시 알림, iOS WidgetKit, Fastlane CI/CD
- **배포**: App Store + Google Play 양대 마켓 자동 배포

### 차별화 스토리텔링 5원칙
1. **문제 먼저**: "왜 만들었나"가 "무엇을 만들었나"보다 앞에 온다
2. **숫자로 구체화**: 사용자 수, 기록 건수, 빌드 시간 단축 등
3. **기술 결정의 이유**: "OpenStreetMap을 선택한 이유", "Supabase를 선택한 이유"
4. **실패와 해결**: APNs 토큰 3중 실패 → 해결, iOS 하얀 화면 → Flutter 업그레이드
5. **사회적 의미**: 시민 기술(Civic Tech), 동물 복지

---

## 콘텐츠 전략

### 블로그 글 우선순위 (MeowRo 기반)

| # | 제목 (안) | 타입 | 검색 수요 | 작성 난이도 |
|---|-----------|------|-----------|------------|
| 1 | Flutter iOS 하얀 화면 해결기 (3.32→3.41) | 전투 기록 | 높음 | 하 |
| 2 | iOS APNs 토큰 발급 실패의 숨겨진 원인 3가지 | 전투 기록 | 높음 | 중 |
| 3 | Fastlane + iTMSTransporter: 2026년 iOS 자동 배포 | 실전 가이드 | 높음 | 중 |
| 4 | Flutter 앱을 혼자 출시하기까지 전체 여정 | 빌드 로그 | 높음 | 하 |
| 5 | Supabase RLS로 급식 데이터 공개/비공개 제어 | 튜토리얼 | 중 | 하 |

### 콘텐츠 리듬
- **Velog**: 격주 1편 (한글, 기술 깊이 중심)
- **LinkedIn**: 주 1회 짧은 포스트 (인사이트, 마일스톤 공유)
- **dev.to**: 월 1편 (Velog 베스트 글 영문 번역)

---

## 비대칭 레버리지 활동

### S급: 컨퍼런스 발표 (3-6개월 목표)
- **GDG DevFest Korea**: Flutter 세션 수요 높음
- **Flutter Korea Meetup**: 커뮤니티 앱 사례 발표
- **주제 안**: "Flutter로 시민 기술 앱 App Store까지 1인 출시한 경험"

### A급: 오픈소스 기여
- `home_widget` 패키지 버그 리포트/PR
- `flutter_map` 한국어 문서 기여
- MeowRo에서 만든 유틸리티 → pub.dev 패키지 배포

### A급: 기술 블로그
- 위 콘텐츠 전략 실행
- 검색 트래픽이 복리로 쌓이는 구조

### B급: LinkedIn 프레즌스
- 프로필 최적화 (Flutter Developer 포지셔닝)
- 기술 글 요약본 크로스포스팅

---

## 실행 로드맵

### Phase 1: 기반 구축 (이번 주)
- [x] 전략 문서 작성
- [x] resume.json 생성
- [x] GitHub 프로필 README 템플릿
- [ ] LinkedIn 프로필 업데이트
- [ ] rxresu.me에서 PDF 이력서 출력

### Phase 2: 콘텐츠 시작 (2주 이내)
- [ ] Velog 첫 글 발행: "Flutter iOS 하얀 화면 해결기"
- [ ] 같은 글 영문 번역 → dev.to 크로스포스팅
- [ ] GitHub Actions Blog Post Workflow 설정

### Phase 3: 확장 (1-3개월)
- [ ] 기술 글 총 3편 발행
- [ ] GDG/Flutter Korea Meetup CFP 확인 및 제출
- [ ] pub.dev 패키지 1개 배포
- [ ] LinkedIn 콘텐츠 리듬 시작 (주 1회)

### Phase 4: 가속 (3-6개월)
- [ ] 컨퍼런스 발표 1회 완료
- [ ] 영문 블로그 누적 3편
- [ ] 오픈소스 PR 1건 이상
- [ ] 포트폴리오 사이트 구축 (Astro/Next.js)

---

## 도구 체크리스트

| 도구 | URL | 용도 | 설정 완료 |
|------|-----|------|-----------|
| JSON Resume | jsonresume.org | 이력서 코드 관리 | [ ] |
| Reactive Resume | rxresu.me | PDF 이력서 생성 | [ ] |
| Blog Post Workflow | github.com/gautamkrishnar/blog-post-workflow | README 자동 갱신 | [ ] |
| Crier | metafunctor.com/projects/crier | 크로스포스팅 CLI | [ ] |
| readme-ai | github.com/eli64s/readme-ai | 프로젝트 README 자동 생성 | [ ] |

---

## 참고 자료
- [JSON Resume 표준](https://jsonresume.org)
- [Reactive Resume](https://rxresu.me)
- [Blog Post Workflow](https://github.com/gautamkrishnar/blog-post-workflow)
- [Crier 크로스포스팅](https://metafunctor.com/projects/crier/)
- [Stack Overflow Developer Survey 2024](https://survey.stackoverflow.co/2024/)
- [F-Lab 면접관 관점 블로그 팁](https://f-lab.ai/en/blog/developer-blog-tips)
