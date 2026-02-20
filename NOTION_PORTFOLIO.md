# 지승제 (Seungje Ji)

## 금융 도메인 전문 백엔드 시니어

**AML** · **MyData** · **결제정산** · **Spring Batch**

> 11년차 | Java/Spring | CTO 2회 · PM 2회 · PL 1회 | 시장 희소성 1.5~3%

---

**Email** byseungje@gmail.com
**GitHub** [github.com/byseungje](https://github.com/byseungje)
**LinkedIn** [linkedin.com/in/seungje-ji](https://www.linkedin.com/in/seungje-ji/)
**Velog** [velog.io/@byseungje](https://velog.io/@seungje_labs/posts)

---

## 한 줄 소개 + 핵심 가치

> "11년간 금융·공공 도메인에서 **문제를 정의하고, 시스템으로 해결하는** 백엔드 개발자"

### 3가지 핵심 가치

| 가치 | 설명 |
|------|------|
| **문제 발견력** | 40년간 아무도 몰랐던 COBOL 이자계산 오류를 스스로 발견하고 증명. 코드를 넘어 **비즈니스 리스크를 감지하는 눈**. |
| **도메인 전문성** | AML 76개 STR 룰 DAG 분석, 마이데이터 5권역 API 설계, 일 2.6만 주문 결제·정산 운영 — **금융 규제와 시스템을 동시에 이해**하는 개발자. |
| **리더십** | CTO 2회, PM 2회, PL 1회. 주니어 교육·채용·팀 빌딩부터 고객사 직접 시연까지. **한전 3회 지명, 우체국금융 2회 직접 호출** — "지명받는 개발자". |

---

## 킬러 성과 TOP 3

---

### 성과 1. COBOL 40년 이자계산 오류 발견 — 70억원 소급 보정

#### Situation

한전KDN 영업배전 차세대 4.0 프로젝트에서 COBOL 기반 전기요금 정산 로직을 Spring Batch로 전환하는 작업을 수행. 40년간 운영되어 온 레거시 코드를 분석하는 과정에서 이자 계산 결과에 체계적인 편차가 있음을 발견.

#### 문제 정의

COBOL 내부 라운딩 로직이 **전기공급약관 규정과 불일치**하고 있었음. 단순 버그가 아니라 COBOL의 고유한 반올림 처리 방식이 약관에서 정한 이자 계산 기준을 위반하는 **구조적 오류(systematic bias)**. 건당 1원의 미세한 차이였지만, **10만+ 고객 x 40년**이 누적되면서 약 **70억원** 규모의 이자계산 오류가 발생.

#### 해결 과정

1. COBOL 소스의 라운딩 로직과 전기공급약관 이자 계산 기준을 1:1 대조 분석
2. 운영 데이터(실제 고객 정산 이력)를 기반으로 오류 규모 산출
3. 한전 + KDN 합동 시연회에서 운영 데이터로 직접 증명
4. Spring Batch 전환 시 약관 기준에 맞는 정확한 라운딩 로직으로 재구현

#### 정량적 결과

| 지표 | 수치 |
|------|------|
| 오류 누적 기간 | **40년** |
| 영향 규모 | 약 **70억원** 소급 보정 |
| 영향 고객 | **10만+** |
| 소급 보정 | 완료 |

#### 면접용 한마디

> "코드의 정합성을 넘어 **비즈니스 규정(약관)과의 정합성까지 검증**하는 습관이 40년간 묻혀있던 70억 규모 오류를 발견하게 했습니다."

---

### 성과 2. Spring Batch 마이그레이션 — 월 175만 건 처리 80%+ 단축

#### Situation

한전KDN 영업배전 차세대 4.0 프로젝트. COBOL 기반 전기요금 정산 배치를 Spring Batch로 전환해야 했으며, 월 **175만 건**(피크 일 20~30만 건) 처리를 안정적으로 수행해야 했음.

#### 문제 정의

기존 COBOL 배치는 순차 처리 구조로, 처리량 증가에 따라 3~4시간이 소요. 단순 언어 전환이 아닌 **아키텍처 수준의 성능 최적화**가 필요.

#### 해결 과정 — 3축 개선

| 축 | 적용 기술 | 효과 |
|----|-----------|------|
| **Chunk 최적화** | 1,000건 Chunk + 8스레드 병렬 처리 | 단위 처리량 극대화 |
| **파티셔닝** | 한전 6개 지역본부 기준 데이터 파티셔닝 | 데이터 분할 병렬 처리 |
| **Flow 병렬화** | Spring Batch Flow 기반 Step 병렬 실행 | 독립 Step 동시 수행 |

PL로서 5명(주니어 3명 + 6년차 2명) 대상 Spring Batch 기술 교육 및 코드 리뷰 진행. 카카오페이·네이버페이 PG 연동 및 농어촌융자금 연동 정산 배치까지 구현.

#### 정량적 결과

| 지표 | Before | After |
|------|--------|-------|
| 처리 시간 | 3~4시간 | **40~50분** |
| 단축률 | — | **80%+** |
| 월 처리량 | 175만 건 | 175만 건 (안정) |
| 피크 일 처리 | 20~30만 건 | 20~30만 건 (안정) |
| 외부 PG 연동 | — | **3개 채널** 통합 |

#### 면접용 한마디

> "Chunk/파티셔닝/Flow 3축 최적화로 **아키텍처 수준에서 성능을 설계**했고, PL로서 팀원 5명의 Spring Batch 역량까지 함께 끌어올렸습니다."

---

### 성과 3. 외부 마켓 3사 공통 아키텍처 — 연동 92% 단축

#### Situation

우체국 쇼핑몰에서 옥션·G마켓·11번가 외부 마켓과의 주문·클레임·정산 연동이 필요. 최초 eBay(옥션·G마켓) 연동에 **5개월**이 소요. 향후 추가 마켓 연동마다 동일한 개발 비용이 반복될 위기.

#### 문제 정의

마켓마다 API 규격, 데이터 모델, 에러 코드가 완전히 상이. 마켓별 개별 구현은 **유지보수 비용이 마켓 수에 비례하여 증가**하는 구조적 문제.

#### 해결 과정

**Anti-Corruption Layer + Adapter Pattern + Canonical Data Model** 3가지 아키텍처 패턴을 조합하여 공통 연동 아키텍처 설계.

```
┌─────────────┐     ┌──────────────────┐     ┌─────────────┐
│ 우체국 쇼핑몰  │ ←→ │  Canonical Model  │ ←→ │  ACL Layer   │
│ (내부 도메인)  │     │  (공통 데이터 모델)  │     │              │
└─────────────┘     └──────────────────┘     ├─────────────┤
                                              │ eBay Adapter │
                                              │ 11st Adapter │
                                              │ ... Adapter  │
                                              └─────────────┘
```

- 12명 프로젝트에서 WBS **25% 리드**
- 신규 마켓 온보딩 시 Adapter 구현만으로 연동 가능한 구조 확립

#### 정량적 결과

| 지표 | Before | After |
|------|--------|-------|
| 마켓 연동 기간 | 5개월 (eBay) | **2~3주** (11번가) |
| 단축률 | — | **92%** |
| 매출 증가 | — | **~20%** |
| CS 응대 | — | **30% 감소** |

#### 면접용 한마디

> "반복되는 비용을 **아키텍처로 해결**했습니다. 공통 구조 한 번 설계해서 신규 마켓 연동을 5개월에서 2~3주로 줄였습니다."

---

## 도메인 전문성 매트릭스

| 도메인 | 경험 상세 | 깊이 |
|--------|-----------|------|
| **AML (자금세탁방지)** | 76개 STR 룰 인벤토리 DAG 분석, 4층 중첩루프 진단, 양방향 시제(Bi-temporal) 데이터 관리, EDD/CDD 워크플로우 최적화, 룰 추출 모니터링 로그 시스템 구축 | Expert |
| **MyData (마이데이터)** | 5개 금융 권역(은행·카드·보험·대출·지원) API 설계·개발, DB 컬럼명 메타시스템 표준 등록·정비, 개인(신용)정보 제3자 제공 동의 API | Expert |
| **결제/정산** | 일 17K~26K 주문 2년 운영, PG/VAN 연동(카카오페이·네이버페이), 복합결제(신용카드·무통장·온누리상품권), 정산 대사 처리, 대량 주문 엑셀 업로드 | Expert |
| **레거시 전환** | COBOL → Spring Batch, 40년 운영 데이터 정합성 검증, 전기공급약관 기준 라운딩 로직 재설계, 월 175만 건 배치 최적화 | Expert |
| **보안/규제** | KISA 외부 보안 점검 300건+ 대응(XSS/SQL Injection), 금융 규제 감사 대응 이력 추적, RLS 기반 데이터 보안 | Advanced |

---

## 기술 스택

| Level | Category | Technologies |
|-------|----------|-------------|
| **Expert** | Backend Core | Java, Spring Boot, Spring Framework, Spring Batch, Spring Data JPA, MyBatis, RESTful API |
| **Expert** | Domain | AML, FDS, MyData API, Payment & Settlement, PG/VAN Integration, 정산 대사, Batch Processing, Legacy Modernization |
| **Advanced** | Database | Oracle, PostgreSQL, MariaDB, MySQL |
| **Intermediate** | Mobile & Frontend | Flutter, Dart, JavaScript, React, Vue.js |
| **Intermediate** | DevOps & Infra | Git, GitHub Actions, Fastlane CI/CD, Docker, Linux, AWS EC2 |
| **Intermediate** | Backend Infra | Supabase, Firebase (FCM), JWT Authentication |

---

## 경력 타임라인

> 역순 정렬 | 고객사 중심 5개 도메인으로 재편

---

### 한전KDN (전력/에너지 정산) — 3회 지명

> "정산 도메인의 깊이를 인정받아 한전에서 3차례 지명 요청"

#### [3차] 앤솔루션 — AMI 회선관리 시스템 PL (2025.03 ~ 현재)

| 항목 | 내용 |
|------|------|
| 역할 | 개발팀 팀장 / PL |
| 핵심 성과 | 한전 AMI 회선관리 시스템 PL — Spring Boot + JPA 기반 팀 리드. 프로젝트별 기술 스택 선정, 아키텍처 리뷰, 코드 품질 기준 수립 |
| 기술 스택 | Spring Boot, Spring Data JPA |

#### [2차] 영업배전 차세대 4.0 — PL (2023.02 ~ 2023.08)

| 항목 | 내용 |
|------|------|
| 역할 | PL / 과장 (파견: 라인정보통신) |
| 핵심 성과 | COBOL → Spring Batch 전환, 월 175만 건 **80%+ 단축**, COBOL 이자계산 오류 **70억원** 소급 보정, 카카오페이·네이버페이 PG 연동, PL로 5명 교육·리딩 |
| 기술 스택 | Spring Batch, Spring Boot, Oracle, COBOL |

#### [1차] 영업정보통합운영 (2021.01 ~ 2022.03)

| 항목 | 내용 |
|------|------|
| 역할 | 과장 (파견: 범우정보기술/테라에너지) |
| 핵심 성과 | COBOL+Servlet+JSP 3개 시스템 단독 운영, KISA 보안 점검 **300건+** 대응 및 양호 통과, 전기안전공사 데이터 연계 RESTful API + crontab 자동화 구축 |
| 기술 스택 | COBOL, Servlet, JSP, Java, Oracle |

---

### 우체국금융 (AML, 마이데이터) — 직접 호출 2회

> "금융 도메인 이해도를 인정받아 우체국금융에서 2차례 직접 호출"

#### [2차] AML 시스템 성능 최적화 (2025.01 ~ 2025.02)

| 항목 | 내용 |
|------|------|
| 역할 | 과장 / 백엔드 개발자 (파견: 인노앤엘테크) |
| 핵심 성과 | 76개 STR 룰 DAG 분석, 배치 처리 시간 **5시간 → 1시간 48분 (64% 단축)**, 4층 중첩루프 진단, Bi-temporal 데이터 관리 설계, 룰 추출 모니터링 로그 시스템 구축 |
| 기술 스택 | Java, Spring, Oracle, Batch Processing |

#### [1차] 마이데이터 차세대 시스템 (2023.11 ~ 2023.12)

| 항목 | 내용 |
|------|------|
| 역할 | 수석 개발자 (파견: 메타넷디지털) |
| 핵심 성과 | 마이데이터 2.0 신규 API 설계·개발 (은행·카드·보험·대출·지원 **5개 권역**), DB 메타시스템 표준 정비 (SR 건수 **20% 감소**), 개인정보 제3자 제공 동의 API 개발 |
| 기술 스택 | Java, Spring Boot, MyBatis, Oracle |

---

### 우체국 쇼핑몰 (이커머스 결제/정산)

> "일 2.6만 주문의 결제·정산을 2년간 안정 운영하며 아키텍처로 매출을 끌어올린 경험"

#### 이커머스 백엔드 2년 운영 (2018.11 ~ 2020.11)

| 항목 | 내용 |
|------|------|
| 역할 | 주임 (파견: 잡트러스트) |
| 핵심 성과 | 외부 마켓 3사 공통 아키텍처 설계 (ACL + Adapter + CDM) — 연동 **92% 단축**, 매출 **~20% 증가**, CS 응대 **30% 감소**. 12명 프로젝트 WBS 25% 리드. 결제·클레임·정산 대사 처리, 복합결제 기능 개발 |
| 기술 스택 | Java, Spring, MyBatis, Oracle, RESTful API |

---

### KISA 한국인터넷진흥원 (보안/공공)

> "PM으로서 채용부터 교육, 8개 사이트 운영까지 총괄한 리더십 경험"

#### 8개 사이트 운영 총괄 + 스팸 신고 앱 (2022.04 ~ 2023.01)

| 항목 | 내용 |
|------|------|
| 역할 | PM·팀장 / 과장 (파견: 아비도스/SDS) |
| 핵심 성과 | KISA 8개 사이트 4인 팀(신입 3명 직접 채용) 운영 총괄, 스팸 신고 앱 Flutter 단독 개발·출시, '털린 내정보 찾기' 서비스 개발, 블록체인 PMS 구축, 신입 매일 1~2시간 교육 |
| 기술 스택 | Spring Boot, Vue.js, Flutter, Oracle, Blockchain |

---

### 스타트업 (0→1 서비스, CTO 2회)

> "홍카에서 1인 서비스를 현대자동차에 납품하고, 이후 CTO로 제로부터 서비스를 설계하고 투자를 유치한 경험"

#### 널코드 — CTO (2024.01 ~ 2025.02)

| 항목 | 내용 |
|------|------|
| 역할 | CTO / 풀스택 개발자 |
| 핵심 성과 | Flutter + Spring Boot 기반 **3개 서비스 출시**, 창원시 동물 관리 시스템 수주·납품, MeowRo 앱 1인 출시 (10개 동물보호협회 도입 검토), GitHub Actions + Fastlane CI/CD 구축, OpenAI API 외주 개발 (긍정률 90%) |
| 기술 스택 | Flutter, Spring Boot, JPA, React.js, Supabase, GitHub Actions, Fastlane |

#### 그리너랩 (트리닥터) — CTO (2023.06 ~ 2023.12)

| 항목 | 내용 |
|------|------|
| 역할 | CTO (스타트업 첫 개발자) |
| 핵심 성과 | 나무의사 업무관리 플랫폼 전체 아키텍처 설계·구축, 사용자 인터뷰 기반 요구사항 분석, HTML5 위치 정확도 문제 → Flutter 전환, **MS 바우처 투자 유치** |
| 기술 스택 | Spring Boot, JPA, MariaDB, Flutter |

#### 광주은행 R&D (2024.06 ~ 2024.10)

| 항목 | 내용 |
|------|------|
| 역할 | 차장 / 백엔드 개발자 (파견: 가람정보통신) |
| 핵심 성과 | JB지주 산하 Mendix Low-Code 공통 프레임워크 구축 (국내 금융권 최초), 지멘스 코리아 협업, 사내 결재 UI 컴포넌트 모듈화, Crew AI 리서치 자동 생성 PoC |
| 기술 스택 | Mendix, Java, Crew AI |

#### (주)홍카 — hupple(휴플) 1인 기획·설계·개발 (2017.03 ~ 2018.09)

| 항목 | 내용 |
|------|------|
| 역할 | 대리 → 팀장 / 1인 기획·설계·풀스택 개발 |
| 서비스 | **hupple(휴플)** — "전국 휴게소 파헤치기!" ([hupple.net](https://www.hupple.net)) |
| 핵심 성과 | 서비스 기획부터 FO/BO/REST API/앱 전체를 1인 전담 설계·개발. **현대자동차 납품 MOU** 체결(휴게소 정보 데이터 제공). **우아한형제들(배달의민족)** 멘토 기업 지원. BM 재설계 → **2억원 외부 투자 유치**. 한국도로공사 공공데이터 + OPINET 유가 API + IoT 화장실 청결도 센서 통합 |
| 기술 스택 | Spring, JSP, jQuery, MariaDB, AWS EC2, RESTful API, Android, WordPress |

---

## 프로젝트: hupple(휴플) — 첫 서비스, 1인 기획·설계·개발

### 전국 휴게소 정보 플랫폼

> **"직업전문학교 졸업 후 첫 서비스를 혼자 기획하고, 설계하고, 만들었다"**

| 항목 | 내용 |
|------|------|
| 기간 | 2017.03 ~ 2018.09 (1년 7개월) |
| 회사 | (주)홍카 |
| 역할 | 서비스 기획 → 아키텍처 설계 → 풀스택 개발 → 운영 **1인 전담** |
| 서비스 | [hupple.net](https://www.hupple.net) — "전국 휴게소 파헤치기!" |
| 성과 | **현대자동차 납품 MOU** · **우아한형제들 멘토링** · **2억원 투자 유치** |

### Situation

직업전문학교를 졸업하고 스타트업 (주)홍카에 합류. 기존에 휴게소 정보를 체계적으로 제공하는 서비스가 없는 상황에서, 음식 추천·최저가 주유소·화장실 청결도까지 통합하는 B2C 플랫폼을 기획해야 했음. 개발자가 본인 1명뿐인 환경에서 서비스 전체를 기획부터 운영까지 혼자 담당.

### 문제 정의

1. 고속도로 휴게소 정보가 분산되어 있어 (도로공사, OPINET, 개별 휴게소) 통합 조회 불가
2. 기존 BM의 기술적 한계로 투자 유치 실패 상태
3. IoT 화장실 청결도 데이터를 서비스에 통합하는 기술적 과제

### 해결 과정

#### 1. 아키텍처 설계 (1인 전체 담당)

```
┌─────────────────────────────────────────────┐
│               hupple.net (FO)                │
│        JSP + jQuery + Spring MVC             │
├─────────────────────────────────────────────┤
│           REST API Layer                     │
│    휴게소 정보 │ 메뉴 추천 │ 화장실 청결도      │
├─────────────────────────────────────────────┤
│           Spring + MariaDB                   │
│              AWS EC2                         │
├──────────┬──────────┬───────────────────────┤
│ 도로공사   │ OPINET   │ IoT 센서              │
│ 공공데이터  │ 유가 API  │ 화장실 오염도          │
│ (data.ex) │          │                       │
└──────────┴──────────┴───────────────────────┘
       + Android App + Back Office (BO)
       + WordPress 정보 포털 + Tistory 블로그
```

#### 2. 공공데이터 연계

| 데이터 소스 | 연계 내용 |
|------------|-----------|
| **한국도로공사 API** (data.ex.co.kr) | 휴게소 기본정보, 편의시설 현황, 푸드메뉴·영양성분·가격 |
| **OPINET API** (한국석유공사) | 실시간 주유소 유가 정보 → 위치 기반 최저가 주유소 추천 |
| **영양성분표 공공데이터** | 음식 영양정보 수집·가공 → 메뉴 추천 기능 |
| **IoT 센서** | 화장실 오염도/청결도 데이터 수집·표시 |

#### 3. BM 재설계 → 투자 유치

기존 BM의 기술적 한계를 분석하고 플랫폼 아키텍처를 전면 재설계. 이를 기반으로 **2억원 외부 투자 유치**에 성공하고, **현대자동차와 휴게소 정보 데이터 납품 MOU**를 체결.

### 정량적 결과

| 지표 | 수치 |
|------|------|
| 개발 범위 | FO + BO + REST API + Android App + WordPress + 회사 홈페이지 **1인 전담** |
| 투자 유치 | **2억원** |
| 기업 파트너십 | **현대자동차** 납품 MOU |
| 멘토 기업 | **우아한형제들(배달의민족)** |
| 공공데이터 연계 | 3개 소스 (도로공사 + OPINET + 영양성분표) |
| 서비스 URL | [hupple.net](https://www.hupple.net) — [Wayback Machine 아카이브 (2018.09)](https://web.archive.org/web/20180929005638/http://www.hupple.net:80/) |

### 외부 참고 자료

| 항목 | URL |
|------|-----|
| **hupple.net Wayback Machine 아카이브** | [web.archive.org (2018.09 스냅샷)](https://web.archive.org/web/20180929005638/http://www.hupple.net:80/) |
| hupple.net 서비스 (도메인 만료) | [hupple.net](https://www.hupple.net) — Google 인덱스 잔존 |
| hupple 블로그 (Tistory) | [hupple.tistory.com](https://web.archive.org/web/20190717111810/https://www.hupple.net/notice) |
| 한국도로공사 공공데이터 포털 | [data.ex.co.kr](https://data.ex.co.kr) |
| 도로공사 휴게소 푸드메뉴 API | [data.go.kr/data/15076643](https://www.data.go.kr/data/15076643/openapi.do) |
| OPINET 유가정보 API | [opinet.co.kr](https://www.opinet.co.kr/user/custapi/custApiInfo.do) |
| 휴게소 혁신 마스터플랜 2018 | [korea.kr 보도자료](https://www.korea.kr/briefing/pressReleaseView.do?newsId=156295345) |
| LoRa IoT 고속도로 네트워크 | [Semtech 보도자료](https://www.semtech.com/company/press/semtech-deploys-lora-based-network-for-south-korean-expressways) |
| 스마트 화장실 관리서버 특허 | [KR101889913B1](https://patents.google.com/patent/KR101889913B1/ko) |

### 내가 배운 것

- **0→1 서비스 설계**: 기획서 없이 시작해서 아키텍처 문서, API 설계, DB 스키마, UI/UX까지 모두 스스로 결정하는 경험. 이후 그리너랩 CTO, 널코드 CTO에서 반복 활용.
- **공공데이터 활용**: 한국도로공사, OPINET 등 공공 API를 연계하는 경험이 이후 우체국금융 마이데이터 API 설계에 직접적 도움.
- **B2B 파트너십**: 현대자동차 같은 대기업과 MOU를 체결하는 과정에서 사업 제안서 작성, 기술 시연, 데이터 규격 협의 경험 → 이후 모든 고객사 대응력의 기반.
- **투자 유치 경험**: 기술적 한계를 분석하고 대안을 제시해 투자자를 설득하는 과정 → 이후 그리너랩 MS 바우처 투자 유치에 활용.

---

## 프로젝트: MeowRo

### 길고양이 급식소 관리 앱

> **"기록되지 않는 돌봄은 정책에 반영될 수 없다"**

| 항목 | 내용 |
|------|------|
| 기간 | 2024.01 ~ 현재 (운영 중) |
| 역할 | 기획 → 디자인 → 개발 → 배포 → 운영 **1인 풀스택** |
| 플랫폼 | iOS + Android (Flutter 크로스플랫폼) |
| 상태 | App Store + Google Play **출시 완료** |
| GitHub | [github.com/byseungje/meowro-app](https://github.com/byseungje/meowro-app) |

### 기술 아키텍처

```
┌──────────────────────────────────────────┐
│              Flutter 3.41                │
│         Riverpod + Clean Architecture    │
│    (iOS WidgetKit / Android Glance)      │
└───────────────────┬──────────────────────┘
                    │ REST / Realtime
┌───────────────────┴──────────────────────┐
│              Supabase                     │
│  Auth │ PostgreSQL │ Storage │ Realtime   │
│            Edge Functions                 │
└───────────────────┬──────────────────────┘
                    │
┌───────────────────┴──────────────────────┐
│          Firebase (FCM only)              │
│     Push Notifications via APNs           │
└───────────────────┬──────────────────────┘
                    │
┌───────────────────┴──────────────────────┐
│      Fastlane CI/CD (GitHub Actions)      │
│   iOS TestFlight + App Store              │
│   Android Internal Test + Production      │
└──────────────────────────────────────────┘
```

### 주요 기능

- 급식소 생성/관리 + 멤버 초대
- 사진 기반 급식 기록 (AI 카메라 + 직접 기록)
- 돌봄 여정 (포인트, 레벨, 스트릭, 히트맵)
- 커뮤니티 (게시물, 댓글)
- 고양이 목격 기록
- 푸시 알림 (FCM) — iOS APNs 연동 트러블슈팅 해결
- 홈 화면 위젯 (iOS WidgetKit + Android Glance)
- Deep Link (meowro:// 스킴)

### 기술적 도전과 해결

| 도전 | 문제 | 해결 | 성과 |
|------|------|------|------|
| iOS FCM 토큰 3중 장애 | entitlements 누락 + APNs 키 미등록 + swizzling 깨짐 | AppDelegate 수동 APNs 처리 | 3시나리오 푸시 정상 수신 |
| iOS TestFlight 하얀 화면 | Flutter 3.32.8 + iOS 26.2.1 Dart VM Assert 실패 | Flutter 3.41.1 업그레이드 | UIScene lifecycle 정상 |
| 양대 마켓 자동 배포 | altool deprecated로 기존 스크립트 무효화 | Fastlane + iTMSTransporter | 빌드~업로드 **5분 이내** |
| 홈 위젯 크로스플랫폼 | Flutter ↔ 네이티브 데이터 동기화 | App Groups / SharedPreferences | iOS + Android 모두 지원 |

### 성과

| 지표 | 수치 |
|------|------|
| 마케팅 비용 | **0원** |
| 다운로드 | **432건** |
| B2G 예산 확보 | 창원시 **3,000만원** |
| NTIS 유사도 | **0점** (완전 독창적) |
| 도입 검토 | 10개 동물보호협회 + 창원시 |

### 비즈니스 모델

> 시민 무료 기록 → 지자체 구독 (B2G SaaS)

---

## 리더십 경험

| 유형 | 횟수/규모 | 사례 |
|------|-----------|------|
| **CTO** | 2회 | **널코드**: 3개 서비스 출시, 공공 클라이언트 납품 / **그리너랩**: 스타트업 첫 개발자, 제로부터 설계·구축, MS 바우처 투자 유치 |
| **PM** | 2회 | **KISA**: 8개 사이트 4인 팀 운영 총괄, 신입 3명 직접 채용·교육 / **한전 AMI**: 회선관리 시스템 PL 및 개발팀 리딩 |
| **PL** | 1회 | **한전KDN 차세대 4.0**: 5명(주니어 3 + 6년차 2) Spring Batch 기술 교육·코드 리뷰·리딩 |
| **B2G** | 1건 | **창원시**: 동물 관리 시스템 수주, **3,000만원** 예산 확보 |
| **B2B/MOU** | 1건 | **홍카**: 1인 개발 hupple 서비스로 **현대자동차 납품 MOU** 체결, 우아한형제들 멘토링 |
| **투자 유치** | 2건 | **홍카**: BM 재설계로 **2억원** 투자 유치 / **그리너랩**: MS 바우처 투자 유치 |

### 리더십 스타일

- **주니어 교육**: 매일 1~2시간 기술 교육, 수준별 업무 분배, 코드 리뷰
- **채용**: KISA 프로젝트에서 신입 3명 + 중급 1명 직접 채용
- **고객사 시연**: 한전+KDN 합동 시연회에서 운영 데이터로 직접 증명
- **지명 실적**: 한전 3회 지명, 우체국금융 2회 직접 호출

---

## 학력 & 자격증

### 자격증

| 자격증 | 발급 기관 | 취득일 |
|--------|-----------|--------|
| **정보처리기사** | 한국산업인력공단 | 2020.11 |
| **Oracle OCP 11g** | Oracle | 2017.01 |

### 학력

| 학교 | 전공 | 학위 | 기간 |
|------|------|------|------|
| 학점은행제 | 경영학 | **학사** | 2012 ~ 2022 |
| 순천대학교 | 분자화학 | 중퇴 | 2007 ~ 2011 |

### 언어

| 언어 | 수준 |
|------|------|
| 한국어 | Native |
| English | Intermediate (Technical Reading/Writing) |

---

## 연락처 & 링크

| 채널 | 링크 |
|------|------|
| **Email** | [byseungje@gmail.com](mailto:byseungje@gmail.com) |
| **GitHub** | [github.com/byseungje](https://github.com/byseungje) |
| **LinkedIn** | [linkedin.com/in/seungje-ji](https://www.linkedin.com/in/seungje-ji/) |
| **Velog** | [velog.io/@byseungje](https://velog.io/@seungje_labs/posts) |
| **Resume (JSON)** | [raw.githubusercontent.com/byseungje/resume/main/resume.json](https://raw.githubusercontent.com/byseungje/resume/main/resume.json) |

---

> *Last Updated: 2026-02-20 | Based on resume.json v6.0.0*
