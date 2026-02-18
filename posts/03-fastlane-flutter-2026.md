# Fastlane + iTMSTransporter: 2026년 Flutter iOS/Android 자동 배포 완전 가이드

> **타겟 플랫폼**: Velog (한글) → dev.to (영문 번역)
> **예상 키워드**: fastlane flutter ios, altool deprecated, iTMSTransporter flutter, fastlane android aab

---

## 글 구조

### 1. 왜 이 글을 쓰는가 (Hook)
- `altool`이 deprecated되면서 기존 Fastlane 가이드가 다 깨짐
- 2026년 기준으로 **실제 동작하는** Flutter + Fastlane 설정을 정리
- iOS TestFlight + App Store, Android 내부테스트 + 프로덕션 전체 커버

### 2. 사전 준비
- Transporter.app 설치 필수 (/Applications에)
- App Store Connect API Key (JSON 형태)
- Google Play Service Account Key
- 환경변수 관리 (.env 파일 구조)

### 3. Fastfile 구조 (실제 코드)
```ruby
# iOS beta, release 레인
# Android beta, release 레인
# deploy_all 레인
# 실제 사용 중인 Fastfile 전문 첨부
```

### 4. iOS 배포 — 핵심 포인트
- `flutter build ipa` 사용 (archive 직접 안 함)
- `FASTLANE_ITUNES_TRANSPORTER_USE_SHELL_SCRIPT=1` 환경변수 필수
- `precheck_include_in_app_purchases: false` (IAP 미사용 시)
- `release_notes.txt` 매번 업데이트 필수 (누락 시 whatsNew 오류)
- build_number 자동 증가 로직

### 5. Android 배포 — 핵심 포인트
- `flutter build appbundle` → AAB 파일 경로
- 내부 테스트 트랙 업로드 → 프로덕션 승격 (재빌드 불필요)
- Google Play Service Account 설정 과정

### 6. dart-define 환경변수 주입
- `.env` 파일에서 읽어서 `--dart-define` 자동 주입
- Supabase URL, Anon Key, Kakao Key 등 민감정보 처리

### 7. 실전에서 만난 오류 10가지
1. Transporter.app 미설치 → 업로드 실패
2. release_notes.txt 누락 → whatsNew 오류
3. build_number 중복 → 업로드 거부
4. dart-define 누락 → 런타임 하얀 화면
5. IAP precheck → 불필요한 차단
6. copyright 2026 누락 → precheck 경고
7. support URL 접근불가 → precheck 경고
8. ... (실제 경험한 것들)

### 8. 원커맨드 배포
```bash
# iOS
cd fastlane && source .env && fastlane ios release

# Android
cd fastlane && source .env && fastlane android release
```

---

## 메타 정보
- **작성 예상 시간**: 4-5시간 (코드 정리 포함)
- **예상 길이**: 3,000-4,000자
- **태그**: `flutter`, `fastlane`, `ios`, `android`, `ci-cd`, `deployment`, `app-store`
- **썸네일 아이디어**: Fastlane → TestFlight + Play Store 배포 흐름도
