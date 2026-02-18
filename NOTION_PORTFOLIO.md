# 지승제 — Backend Developer

## About Me

> 11년차 백엔드 개발자. 금융·공공 대형 시스템의 설계부터 운영까지 경험하며, 조직의 요구를 기술로 구조화하는 일을 해왔습니다.

---

### Contact

| 항목 | 내용 |
|------|------|
| Email | byseungje@gmail.com |
| GitHub | [github.com/byseungje](https://github.com/byseungje) |
| LinkedIn | [linkedin.com/in/seungje-ji](https://www.linkedin.com/in/%EC%8A%B9%EC%A0%9C-%EC%A7%80-495412386/) |
| Blog | [velog.io/@byseungje](https://velog.io/@byseungje) |

---

### Tech Stack

**Backend (Expert)**
`Java` `Spring Boot` `Spring Batch` `Spring Data JPA` `MyBatis` `RESTful API` `eGov Framework`

**Database (Advanced)**
`Oracle` `MariaDB` `MySQL` `PostgreSQL`

**Mobile (Intermediate)**
`Flutter` `Dart`

**Frontend (Intermediate)**
`React` `Vue.js` `JavaScript` `jQuery`

**DevOps & Tools**
`Git` `GitHub Actions` `Fastlane` `Docker` `Linux` `AWS EC2`

**Etc**
`Supabase` `Firebase` `FCM` `Swagger` `CrewAI`

---

### Career Timeline

| 기간 | 회사 | 역할 | 핵심 프로젝트 |
|------|------|------|-------------|
| 2025.03~ | 앤솔루션 | 개발팀 팀장 | 팀 리딩 & 기술 의사결정 |
| 2024.01~2025.02 | 널코드 (자사) | CTO | 스타트업 플랫폼 + MeowRo 앱 출시 |
| 2024.06~2024.10 | 가람정보통신 | 차장 | 광주은행 Mendix 프레임워크 |
| 2023.11~2023.12 | 메타넷디지털 | 수석 | 우체국금융 마이데이터 2.0 |
| 2023.06~2023.12 | 그리너랩 | CTO | 농림부 나무의사 업무관리 |
| 2023.02~2023.08 | 라인정보통신 | PL | 한전KDN 영배 4.0 배치 |
| 2022.04~2023.01 | 아비도스 | PM | KISA 스팸신고·털린내정보·PMS |
| 2021.01~2022.03 | 범우정보기술 | 과장 | 한전KDN 영업시스템 운영 |
| 2018.11~2020.11 | 잡트러스트 | 주임 | 우체국 쇼핑 커머스 |
| 2017.03~2018.09 | (주)홍카 | 팀장 | 휴게소 정보 B2C 플랫폼 |

---

## Projects

---

### 01. MeowRo — 길고양이 급식소 관리 앱

> 기획부터 App Store/Play Store 출시까지 1인 풀스택으로 완성한 사이드 프로젝트

| 항목 | 내용 |
|------|------|
| 기간 | 2024.01 ~ 현재 (운영 중) |
| 역할 | 기획, 디자인, 개발, 배포 — 1인 전담 |
| 기술 | Flutter 3.41, Riverpod, Supabase, FCM, Fastlane |
| GitHub | [github.com/byseungje/meowro-app](https://github.com/byseungje/meowro-app) |

**배경**
한국에 추정 200만 마리의 길고양이가 있고, 전국의 급식소를 자원봉사자들이 관리합니다. 하지만 "오늘 누가 밥을 줬는지" 확인할 방법이 없어 중복 급식이나 급식 누락이 발생하는 문제가 있었습니다.

**아키텍처**

```
Flutter 3.41 (Riverpod + Clean Architecture)
  ├── iOS WidgetKit (SwiftUI)
  └── Android Glance
          │
          ▼  REST / Realtime
Supabase (Auth, PostgreSQL, Storage, Edge Functions, Realtime)
          │
          ▼
Firebase (FCM Push Notifications)
          │
          ▼
Fastlane CI/CD → App Store + Google Play 자동 배포
```

**기술적 도전과 해결**

| 문제 | 원인 | 해결 |
|------|------|------|
| iOS TestFlight 하얀 화면 | Flutter 3.32.8 Dart VM이 iOS 26의 UIScene lifecycle에서 Assert 실패 | Flutter 3.41.1 업그레이드 |
| iOS FCM 토큰 null (3중 장애) | aps-environment 누락 + Firebase APNs 키 미등록 + UIScene swizzling 깨짐 | 엔트리먼트 추가 + 키 업로드 + AppDelegate 수동 처리 |
| altool deprecated | 기존 배포 스크립트 전면 무효화 | Fastlane + iTMSTransporter 기반 원커맨드 배포 구축 |

**기술 선택 근거**

| 선택 | 이유 |
|------|------|
| Flutter (not React Native) | Dart 언어 친숙도, 단일 코드베이스로 iOS/Android + 위젯까지 |
| Supabase (not Firebase) | PostgreSQL 직접 접근, RLS 기반 보안, 넉넉한 무료 tier |
| OpenStreetMap (not Google Maps) | 무료, 상업적 사용 제한 없음 |
| Riverpod (not Bloc) | 코드 생성 기반, 타입 안전, 보일러플레이트 적음 |

**핵심 기능**: 급식소 관리, 사진 기반 급식 기록, 돌봄 여정(포인트/레벨/스트릭), 커뮤니티, 고양이 목격 기록, 푸시 알림, 홈 위젯, Deep Link

---

### 02. 널코드 — 스타트업 플랫폼 서비스 구축

> 스타트업 CTO로서 전체 기술 스택을 설계하고 프로덕트를 출시한 경험

| 항목 | 내용 |
|------|------|
| 기간 | 2024.01 ~ 2025.02 |
| 역할 | CTO / 풀스택 개발자 |
| 기술 | Spring Boot, JPA, Flutter, React.js, Firebase, GitHub Actions, Fastlane |
| 고객사 | 창원시 (동물 관리 시스템) |

**주요 성과**

- Flutter + Spring Boot 기반 앱/웹/API 전체 아키텍처 직접 설계 및 개발
- JWT 인증 구조, API 버전 관리, 로깅/모니터링까지 고려한 설계
- GitHub Actions + Fastlane으로 Spring(Prop/Dev) + Android/iOS 자동 배포 파이프라인 구축
- 배포 리드타임 대폭 단축
- 사용자 피드백 기반 반복 릴리즈로 서비스 품질 지속 개선

**내가 배운 것**
스타트업 환경에서 기술 선택의 트레이드오프를 직접 경험했습니다. 빠른 MVP 출시와 코드 품질 사이의 균형, 1인 개발에서의 CI/CD 자동화의 가치, 사용자 피드백을 기능으로 전환하는 프로세스를 체득했습니다.

---

### 03. 광주은행 — Mendix 공통 프레임워크 구축

> 레거시 시스템을 분석해 새로운 Low-Code 환경에 맞게 최적화하고, AI 도입 가능성까지 검증

| 항목 | 내용 |
|------|------|
| 기간 | 2024.06 ~ 2024.10 |
| 역할 | 차장 / DevOps팀 백엔드 개발자 |
| 기술 | Mendix, React.js, Oracle, CrewAI |
| 고객사 | 광주은행 |

**Phase 1: Mendix 공통 프레임워크 구축**
광주은행은 전사 시스템 효율화를 위해 엔터프라이즈 로우코드 Mendix 도입을 추진했고, 저는 지멘스 코리아와 협업하여 광주은행 전용 Mendix 공통 프레임워크 구축에 참여했습니다.

- Mendix 코어 소스 수정 및 패키징으로 은행 업무 전용 프레임워크 완성
- 레거시 결재 프로세스를 분석하고 로우코드 환경에 최적화
- 재사용 가능한 결재 상태 UI 레이아웃 설계 → 이후 개발자들이 그대로 활용

**Phase 2: 상시감사 내부통제 시스템 오픈**
프레임워크가 단순한 실험으로 끝나지 않고, 법령에 근거한 상시감사 내부통제 시스템에 적용되어 실제 금융 서비스로 성공적으로 오픈.

- 결재 프로세스 영역 개발
- 신규 개발팀 대상 UI 레이아웃 활용 교육 및 지원
- 프레임워크가 다른 팀에서도 재사용·확산 가능한 자산으로 정착

**Phase 3: AI/LLM 업무 적용 실험**
시스템 오픈 이후, 은행 내부에서 AI를 실제 업무에 적용하자는 니즈가 있었습니다.

- **CrewAI**를 활용해 Mendix 도입 효과를 주제로 리서치 보고서 자동 생성
- AI가 은행 내부 리서치·분석 업무에 활용될 수 있다는 가능성 입증
- 기존에는 외부 리서치 기업에 의뢰하던 작업을 AI로 대체할 수 있음을 시연

**핵심 역량**: 기존 시스템 분석 → 새로운 환경 최적화 → 기술 확산 지원 → 신기술(AI) 검증

---

### 04. 우체국 쇼핑 커머스 — 백엔드 개발 및 2년 운영

> 실 사용자 대상 커머스 시스템을 설계하고 2년간 안정적으로 운영한 경험

| 항목 | 내용 |
|------|------|
| 기간 | 2018.11 ~ 2020.11 (2년 1개월) |
| 역할 | 주임 / 백엔드 개발자 |
| 기술 | Java, JSP, Spring, Oracle, eGov Framework, RESTful API |
| 고객사 | 한국우편사업진흥원 |

**주요 성과**

- 우체국 쇼핑 결제/클레임 처리 시스템 백엔드 담당
- **외부 마켓 연계** — 11번가, 옥션, G마켓과의 연동 시스템 안정적 운영
  - 마켓별 정책 차이 (주문 구조, 쿠폰, 클레임 방식 등)를 통합 관리하는 유연한 설정 구조 설계
- e콜센터 시스템 개발 (xplatform, laf-j)
- 주문/클레임 처리 로직 개선으로 **CS 응대 건수 약 30% 감소**
- 사용자/운영자 피드백 기반 기능 개선 반복

**내가 배운 것**
2년간의 운영 경험에서 "만드는 것"과 "운영하는 것"의 차이를 체감했습니다. 장애 대응, 외부 시스템과의 연계에서 발생하는 예외 처리, 사용자 관점에서의 CS 개선 — 이 모든 것이 백엔드 개발자의 역량을 넓히는 경험이었습니다.

---

### 05. KISA 인터넷진흥원 — 다수 프로젝트 PM 및 개발

> PM과 개발을 겸하며 3개 프로젝트를 동시 수행한 경험

| 항목 | 내용 |
|------|------|
| 기간 | 2022.04 ~ 2023.01 (10개월) |
| 역할 | PM / 과장 |
| 기술 | Flutter, Spring Boot, Vue.js, jQuery, Oracle, MySQL |
| 고객사 | KISA 한국인터넷진흥원 |

**수행 프로젝트 3건**

**1) 스팸 신고 앱 (Flutter + Spring Boot)** — 단독 개발
- 기획부터 배포까지 혼자 수행 (PM겸 개발)
- Flutter 앱 + Spring Boot API 서버 구축
- App Store / Play Store 배포

**2) 인터넷진흥원 메인 홈페이지 리뉴얼**
- jQuery + Spring Boot + Oracle
- 기존 레거시 구조를 최신 프레임워크로 전환

**3) 털린 내정보 찾기 서비스**
- Vue.js + Spring Boot + Oracle
- 개인정보 유출 조회 서비스 프론트엔드 + 백엔드

**내가 배운 것**
다수 프로젝트를 동시에 관리하면서 우선순위 조정과 리소스 배분의 중요성을 체감했습니다. PM 역할과 개발 역할을 동시에 수행하면서, 커뮤니케이션과 기술적 판단을 균형 있게 하는 능력을 길렀습니다.

---

### 06. 한전KDN — 영배 4.0 결재정산 배치 개발

> Spring Batch 기반 대용량 배치 시스템 개발

| 항목 | 내용 |
|------|------|
| 기간 | 2023.02 ~ 2023.08 |
| 역할 | PL / 과장 |
| 기술 | Java, Spring Batch, Oracle |
| 고객사 | 한전 KDN |

**주요 성과**

- 영업배전 시스템 차세대 4.0 — 결재 정보 정산 배치 개발
- 농어촌융자금, 카카오페이, 네이버페이 등 외부 결제 수단 연동 배치 구현
- 개발팀 교육 및 관리 (PL 역할)

---

## Education & Certifications

| 구분 | 내용 | 기간 |
|------|------|------|
| 학력 | 학점은행제 경영학 학사 졸업 | 2022.03 |
| 자격증 | 정보처리기사 | 2020.11 |
| 자격증 | Oracle OCP 11g | 2017.01 |
| 수상 | KOEN 한국남동발전 표창장 | 2017.10 |

---

## What I Value

**정직한 기술 스택**
실무에서 사용한 기술만 이야기합니다. 학습한 것과 실전에서 검증한 것을 구분합니다.

**운영 경험의 가치**
만드는 것보다 운영하는 것이 어렵다는 것을 압니다. 2년간 우체국 쇼핑 커머스를 운영하면서, 장애 대응과 사용자 피드백 반영의 중요성을 체감했습니다.

**기술을 넘어 조직에 기여**
광주은행에서 프레임워크를 만들고 끝내는 것이 아니라, 다른 팀이 활용할 수 있도록 교육하고 확산을 지원했습니다. 기술은 혼자 쓰는 것이 아니라 조직 전체가 활용할 수 있어야 합니다.

---

> 마지막 업데이트: 2026년 2월
