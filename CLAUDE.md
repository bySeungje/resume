# Resume Project — Harness Engineering

> 이 파일은 Claude Code 에이전트의 행동 제약과 피드백 루프를 정의하는 **하네스(Harness)** 입니다.
> 에이전트가 실수할 때마다 이 파일을 업데이트하여 동일 실수를 영구 방지합니다.

## Architecture Invariants (절대 규칙)

### Single Source of Truth
- **`resume.json`이 유일한 데이터 원본**. 경력, 기술스택, 자격, 프로젝트의 모든 사실 데이터는 여기서 시작
- 파생 파일(README.md, RESUME.html, applications/**)에 직접 데이터를 수정하지 않음
- resume.json을 변경하면 **반드시 파생 파일 목록을 사용자에게 안내**

### Derived Files (파생 파일 의존 관계)
```
resume.json (SSOT)
  ├── README.md              ← Career Highlights, Tech Stack, AI Tools
  ├── RESUME.html            ← 범용 이력서 HTML (gitignored, 로컬 전용)
  └── applications/{company}/
       ├── RESUME_{CO}.md    ← 기업 맞춤 이력서
       ├── COVER_LETTER.md   ← 기업 맞춤 커버레터
       └── {CO}_APPLICATION.html ← 합본 HTML (gitignored, 로컬 전용)
```

### 금지 사항
- resume.json을 거치지 않고 파생 파일의 경력 데이터를 직접 수정하는 것
- 회사명, 날짜, 수치를 파일마다 다르게 기재하는 것
- 삭제된 경력(서한통산, 정우정보통신)을 다시 추가하는 것
- `*.html`과 `applications/`는 .gitignore 대상 — git add 시 확인 필요

## Data Constraints (데이터 규칙)

### 경력 년차 계산
- 경력 시작: **2017-03** (홍카)
- 계산법: `현재년월 - 2017-03` → 한국식 N년차 (만 9년 = 10년차)
- **resume.json의 summary에서 "N년차" 수정 시 README.md도 동기화**

### 회사명 매핑 (과거 실수 방지)
| resume.json 표기 | 절대 사용하지 않는 이름 |
|------------------|----------------------|
| 코엑시스 | ~~널코드~~ (구 상호) |
| Claude Code | ~~Claude CLI~~ (구 명칭, meta.note 이력 제외) |

### 리더십 카운트
- CTO 2회: 코엑시스, 그리너랩
- PM 3회: 앤솔루션, KISA, 우체국쇼핑 WBS
- PL 1회: 한전KDN 영배 4.0

## Quality Gates (변경 전 체크리스트)

### resume.json 변경 시
1. 년차 수치가 경력 시작일(2017-03) 기준과 일치하는가?
2. 회사명이 매핑 테이블과 일치하는가?
3. 파생 파일(README.md, RESUME.html) 동기화가 필요한가?
4. highlights의 수치/성과가 면접 근거(memory/MEMORY.md AML 사실 확인)와 일치하는가?

### 기업 맞춤 이력서 생성 시
1. resume.json에서 데이터를 가져왔는가? (직접 작성 금지)
2. 공고 요건과의 매칭 분석을 먼저 수행했는가?
3. WHY→WHAT→RESULT 3단 구조를 적용했는가?
4. 콜센터 명예사원상, 지명실적은 제외했는가? (사용자 판단: "짜고 치는 느낌")

## Workflows (표준 워크플로우)

### WF-1: 기업 맞춤 지원서류 생성
```
1. 공고 분석 → 요건 추출
2. resume.json과 매칭 분석 (강점/갭 식별)
3. applications/{company}/ 디렉토리 생성
4. COVER_LETTER.md 작성 (지원동기 + 요건매칭 + 핵심역량)
5. RESUME_{CO}.md 작성 (경력 순서 = 공고 관련도순, 데이터 = resume.json)
6. {CO}_APPLICATION.html 작성 (합본, Print CSS, A4 2-3페이지)
7. 사용자 리뷰 → 피드백 반영
```

### WF-2: resume.json 업데이트
```
1. 변경 내용 확인 (사실 데이터 검증)
2. resume.json 수정
3. 영향받는 파생 파일 목록 제시
4. 파생 파일 동기화 (사용자 승인 후)
5. meta.lastModified, meta.note 업데이트
```

### WF-3: 리서치 → 전략 수립
```
1. /sc:research로 기업·시장 조사
2. 조사 결과를 memory에 저장 (MCP search)
3. resume.json 강점과 매칭 분석
4. 전략 문서 작성 → 사용자 리뷰
5. 승인 시 WF-1로 이행
```

## File Purposes (이 리포지토리에 없는 것)

- 이 리포에는 **실행 코드가 없음** — 순수 문서/데이터 프로젝트
- `node_modules/`, `package.json`은 resume-cli 도구용 (gitignored)
- `private/`은 전략 문서 (gitignored, 로컬 전용)
- 블로그 초안(`posts/`)은 Velog 수동 발행용 — 자동 배포 없음

## AI Positioning (이력서 내 AI 표현 규칙)

- "도구 사용자"가 아닌 **"프로세스 설계자"**로 프레이밍
- 구체적 도구명 사용: Claude Code (~~Claude CLI~~)
- AGENTS.md 컨텍스트 설계, 워크플로우 확립 등 **설계 행위** 강조
- "AI가 코드를 써줬다"가 아닌 "AI 에이전트의 제약 환경을 설계했다"
- Harness Engineering 용어는 금융/엔터프라이즈 면접에서는 풀어서 설명

## Learned Failures (에이전트 실수 이력)

| 날짜 | 실수 | 방지 규칙 |
|------|------|-----------|
| 2026-02-27 | 널코드→코엑시스 변경 시 일부 파일 누락 | 회사명 변경 시 `grep -r` 으로 전체 파일 검색 필수 |
| 2026-02-27 | RESUME.html을 git add 시도 → gitignore 충돌 | html, applications/ 는 gitignored 확인 후 커밋 |
| 2026-02-27 | 이력서를 보고서 스타일로 생성 | 이력서는 깔끔한 표+불릿 형식, 분석 보고서 요소 금지 |
| 2026-02-27 | 11년차로 잘못 기재 | 경력 시작일(2017-03) 기준으로 계산, 서한통산/정우정보 제외 |
