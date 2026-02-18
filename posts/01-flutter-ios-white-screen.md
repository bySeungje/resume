# Flutter iOS 하얀 화면 해결기 — 3.32.8에서 3.41.1로

> **타겟 플랫폼**: Velog (한글) → dev.to (영문 번역)
> **예상 키워드**: flutter ios white screen, flutter testflight blank, flutter UIScene

---

## 글 구조

### 1. 문제 상황 (Hook)
- MeowRo 앱을 TestFlight에 올렸더니 **iOS에서 하얀 화면만** 표시
- 시뮬레이터에서는 정상 동작, 실기기에서만 발생
- 에러 로그도 없어서 디버깅이 극도로 어려웠음

### 2. 삽질 과정 (공감 유발)
- `ErrorWidget.builder`로 에러 가시화 시도 → 에러 자체가 없음
- Flutter DevTools 연결 시도 → 앱이 시작 자체를 안 함
- Dart VM Assert 실패 의심 → iOS 26.2.1 + Flutter 3.32.8 조합 문제

### 3. 근본 원인 발견
- Flutter 3.32.8의 Dart VM이 iOS 26.2.1의 **UIScene lifecycle**에서 Assert 실패
- UIScene은 iOS 13부터 도입되었지만, iOS 26에서 기본값이 변경됨
- Flutter 엔진이 `UIApplication` 기반 lifecycle만 지원하던 것이 원인

### 4. 해결
- Flutter **3.32.8 → 3.41.1** 업그레이드
- 3.41.1에서 UIScene lifecycle 자동 마이그레이션 지원
- `Fastfile`도 `flutter build ipa` 방식으로 수정

### 5. 교훈 / 체크리스트
- TestFlight 배포 전 실기기 테스트 필수
- Flutter 버전과 최신 iOS 버전 호환성 확인
- `ErrorWidget.builder` 설정으로 프로덕션 에러 가시화

---

## 메타 정보
- **작성 예상 시간**: 2-3시간
- **예상 길이**: 1,500-2,000자
- **태그**: `flutter`, `ios`, `testflight`, `troubleshooting`, `uiscene`
- **썸네일 아이디어**: 하얀 화면 스크린샷 → 정상 화면 비포/애프터
