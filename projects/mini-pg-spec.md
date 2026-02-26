# Mini PG (Payment Gateway) — 토이 프로젝트 기획서

## 목적

실무 결제 도메인 경험(우체국 쇼핑몰 PG 연동, 한전KDN 정산 배치)을 기반으로,
**Redis/Kafka/테스트 코드** gap을 자연스럽게 보완하는 토이 프로젝트.

> "아, 이 사람이 Redis/Kafka를 억지로 배운 게 아니라 결제 도메인에서 왜 필요한지 알고 쓴 거구나"
> — 채용 담당자가 이렇게 읽어야 한다.

## 배경 (멘토링 인사이트)

- **은탄환을 쫓지 마라**: MSA, Kafka 같은 기술을 이력서에 억지로 넣지 말고, 토이 프로젝트로 실증하라
- **부족한 건 토이 프로젝트를 첨부해서 올려라**: GitHub에 공개하고 resume repo에서 링크
- **이 프로젝트를 한 이유를 설명할 수 있어야 한다**: WHY가 있는 프로젝트

## 아키텍처

```
[Client]
   │
   ▼
[Payment API] ─── POST /payments (idempotency-key)
   │
   ├── Redis: 멱등성 키 검증 + 결제 상태 캐시
   │
   ▼
[Kafka] ─── payment.requested topic
   │
   ▼
[Payment Processor] ─── PG 승인/취소 (mock)
   │
   ▼
[Kafka] ─── payment.completed / payment.failed topic
   │
   ▼
[Settlement Batch] ─── Spring Batch 일마감 정산
```

## 기술 스택

| 카테고리 | 기술 | 사용 목적 |
|----------|------|-----------|
| **Backend** | Spring Boot 3, JPA | API 서버, 도메인 모델 |
| **Cache** | Redis | 멱등성 키, 결제 상태 캐시, 중복 결제 방지 |
| **Event** | Apache Kafka | 결제 이벤트 스트리밍 (요청→승인→정산) |
| **Batch** | Spring Batch | 일마감 정산 배치 (기존 강점 활용) |
| **DB** | PostgreSQL | 주문/결제/정산 데이터 |
| **Test** | JUnit 5, Testcontainers | Redis/Kafka/DB 통합 테스트 |
| **Infra** | Docker Compose | 전체 로컬 환경 구성 |

## 커버하는 Gap

| 현재 Gap | 이 프로젝트에서의 활용 | 면접 시 설명 |
|----------|----------------------|-------------|
| **Redis** | 멱등성 키 저장/검증, TTL 기반 결제 상태 캐시 | "결제 API에서 중복 요청을 방지하려면 멱등성 키가 필수인데, Redis의 SETNX + TTL이 가장 자연스러운 선택" |
| **Kafka** | 결제 요청→승인→정산 이벤트 비동기 파이프라인 | "PG 승인은 외부 호출이라 동기 처리 시 타임아웃 리스크, Kafka로 비동기 분리하면 장애 격리 가능" |
| **테스트 코드** | Testcontainers로 Redis/Kafka/PostgreSQL 통합 테스트 | "실제 인프라와 동일한 환경에서 테스트해야 결제 시스템의 신뢰성을 보장" |
| **Docker** | docker-compose로 전체 인프라 한 번에 구성 | "로컬 개발 환경과 CI 환경을 동일하게 유지" |

## 핵심 기능 (MVP)

### Phase 1: 결제 API + Redis 멱등성
- `POST /api/v1/payments` — 결제 요청 (idempotency-key 헤더)
- `GET /api/v1/payments/{id}` — 결제 상태 조회
- Redis SETNX로 멱등성 키 검증, TTL 30분
- 결제 상태 머신: REQUESTED → APPROVED → SETTLED / FAILED / CANCELLED

### Phase 2: Kafka 이벤트 기반 처리
- `payment.requested` topic — 결제 요청 이벤트 발행
- `payment.completed` topic — PG 승인 완료 이벤트
- `payment.failed` topic — PG 승인 실패 이벤트
- Consumer: PaymentProcessor — mock PG 승인 처리
- 재시도 로직 (RetryTemplate or Kafka retry topic)

### Phase 3: Spring Batch 일마감 정산
- 일마감 정산 배치 (APPROVED 건 집계)
- 가맹점별 정산 금액 계산
- 수수료 계산 로직
- 정산 리포트 생성

### Phase 4: 테스트 + 문서화
- Testcontainers: Redis, Kafka, PostgreSQL 통합 테스트
- 결제 플로우 E2E 테스트
- API 문서 (Spring REST Docs 또는 Swagger)
- README: 아키텍처 다이어그램, 실행 방법, 설계 결정 기록

## 도메인 모델 (초안)

```
Payment
├── id (UUID)
├── orderId
├── amount
├── currency (KRW)
├── status (REQUESTED / APPROVED / FAILED / CANCELLED / SETTLED)
├── idempotencyKey
├── pgTransactionId
├── requestedAt
├── approvedAt
└── settledAt

Settlement
├── id
├── settlementDate
├── merchantId
├── totalAmount
├── feeAmount
├── netAmount
└── paymentCount
```

## 프로젝트 구조 (예상)

```
mini-pg/
├── docker-compose.yml
├── src/main/java/com/byseungje/minipg/
│   ├── payment/
│   │   ├── api/PaymentController.java
│   │   ├── domain/Payment.java
│   │   ├── domain/PaymentStatus.java
│   │   ├── service/PaymentService.java
│   │   ├── infra/RedisIdempotencyStore.java
│   │   └── event/PaymentEventPublisher.java
│   ├── processor/
│   │   ├── PaymentProcessorConsumer.java
│   │   └── MockPgClient.java
│   ├── settlement/
│   │   ├── batch/SettlementJobConfig.java
│   │   ├── domain/Settlement.java
│   │   └── service/SettlementService.java
│   └── config/
│       ├── RedisConfig.java
│       └── KafkaConfig.java
├── src/test/java/
│   ├── payment/PaymentApiIntegrationTest.java
│   ├── processor/PaymentProcessorTest.java
│   └── settlement/SettlementBatchTest.java
└── README.md
```

## 면접 대비 스토리

**Q: 왜 이 프로젝트를 만들었나요?**
> "실무에서 우체국 쇼핑몰에서 PG 연동과 정산 대사를 2년간 담당하고,
> 한전KDN에서 Spring Batch 정산 배치를 설계했습니다.
> 그 과정에서 '분산 환경에서 결제 멱등성을 어떻게 보장할 것인가',
> '정산 파이프라인을 이벤트 기반으로 구성하면 장애 격리가 가능하지 않을까'
> 라는 의문이 생겨서 직접 구현해봤습니다."

**Q: Redis를 왜 썼나요?**
> "결제 API에서 네트워크 장애 시 클라이언트가 동일 요청을 재전송할 수 있습니다.
> 이때 중복 결제를 방지하려면 멱등성 키를 원자적으로 검증해야 하는데,
> Redis의 SETNX + TTL 조합이 이 요구사항에 가장 정확히 부합합니다."

**Q: Kafka를 왜 썼나요?**
> "PG 승인은 외부 API 호출이라 응답 시간이 불확실합니다.
> 동기 처리하면 API 타임아웃으로 사용자 경험이 나빠지고,
> PG사 장애가 우리 시스템 전체로 전파됩니다.
> Kafka로 비동기 분리하면 결제 요청 접수와 PG 승인을 격리할 수 있습니다."

## GitHub 전략

- repo: `bySeungje/mini-pg`
- README에 아키텍처 다이어그램 + 설계 결정 기록 (ADR 스타일)
- resume.json의 projects 섹션에 추가
- 프로필 README의 Featured Project에 링크

## 참고

- 이 프로젝트는 resume v7.0 멘토링 인사이트 "부족한 건 토이 프로젝트로 보완"에서 출발
- K8s/MSA는 이 프로젝트 범위 밖 (오버엔지니어링 방지)
- 핵심은 Redis + Kafka + 테스트 코드 3가지 gap 해소
