# MeowRo — 길고양이 급식소 관리 앱

## 한 줄 소개
길고양이 돌보미 커뮤니티를 위한 크로스플랫폼 앱을 기획부터 App Store/Play Store 출시까지 1인 풀스택으로 완성

## 프로젝트 개요

| 항목 | 내용 |
|------|------|
| 기간 | 2024.01 ~ 현재 (운영 중) |
| 역할 | 기획, 디자인, 개발, 배포 — 1인 풀스택 |
| 플랫폼 | iOS + Android (Flutter 크로스플랫폼) |
| 상태 | App Store + Google Play 출시 완료 |

## 왜 만들었나 (Problem)

한국에 추정 200만 마리의 길고양이가 있고, 전국의 급식소를 자원봉사자들이 관리합니다.
하지만 급식 기록은 수기 또는 카카오톡 공유, 멤버 간 소통은 비체계적이었습니다.

**핵심 문제**: "오늘 누가 밥을 줬는지" 확인할 방법이 없어 중복 급식이나 급식 누락이 발생

## 기술 아키텍처

```
┌─────────────────────────────────────────┐
│              Flutter 3.41               │
│         Riverpod + Clean Architecture   │
│    (iOS WidgetKit / Android Glance)     │
└──────────────────┬──────────────────────┘
                   │ REST / Realtime
┌──────────────────┴──────────────────────┐
│              Supabase                    │
│  Auth │ PostgreSQL │ Storage │ Realtime  │
│           Edge Functions                 │
└──────────────────┬──────────────────────┘
                   │
┌──────────────────┴──────────────────────┐
│          Firebase (FCM only)             │
│     Push Notifications via APNs          │
└──────────────────┬──────────────────────┘
                   │
┌──────────────────┴──────────────────────┐
│      Fastlane CI/CD (GitHub Actions)     │
│   iOS TestFlight + App Store             │
│   Android Internal Test + Production     │
└─────────────────────────────────────────┘
```

## 기술적 도전과 해결

### 1. iOS TestFlight 하얀 화면
- **문제**: Flutter 3.32.8 + iOS 26.2.1에서 Dart VM Assert 실패
- **해결**: Flutter 3.41.1 업그레이드 (UIScene lifecycle 지원)
- **교훈**: Flutter 버전과 최신 iOS 호환성 사전 확인 필수

### 2. iOS FCM 토큰 발급 실패 (3중 장애)
- **원인 1**: Runner.entitlements에 `aps-environment` 누락
- **원인 2**: Firebase Console에 APNs .p8 키 미등록
- **원인 3**: UIScene lifecycle에서 Firebase swizzling 깨짐
- **해결**: 엔트리먼트 추가 + 키 업로드 + AppDelegate 수동 APNs 처리
- **결과**: FCM 토큰 정상 발급, 3시나리오(포그라운드/백그라운드/종료) 푸시 수신 확인

### 3. 양대 마켓 자동 배포
- **문제**: `altool` deprecated로 기존 배포 스크립트 전면 무효화
- **해결**: Fastlane + iTMSTransporter 기반으로 iOS/Android 원커맨드 배포 구축
- **성과**: 빌드~업로드 5분 이내 완료, 수동 작업 제로

### 4. 홈 위젯 크로스플랫폼
- iOS WidgetKit (SwiftUI) + Android Glance
- App Groups / SharedPreferences를 통한 Flutter ↔ 네이티브 데이터 동기화
- 빈 상태 감지 → 온보딩 뷰 표시

## 주요 기능
- 급식소 생성/관리 + 멤버 초대
- 사진 기반 급식 기록 (AI 카메라 + 직접 기록)
- 돌봄 여정 (포인트, 레벨, 스트릭, 히트맵)
- 커뮤니티 (게시물, 댓글)
- 고양이 목격 기록
- 푸시 알림 (FCM)
- 홈 화면 위젯 (iOS + Android)
- Deep Link (meowro:// 스킴)

## 기술 스택 선택 근거

| 선택 | 이유 |
|------|------|
| Flutter (not React Native) | Dart 언어 친숙도 + 단일 코드베이스로 iOS/Android + 위젯까지 |
| Supabase (not Firebase) | PostgreSQL 직접 접근, RLS 기반 보안, 무료 tier 넉넉 |
| OpenStreetMap (not Google Maps) | 무료, 상업적 사용 제한 없음 |
| Riverpod (not Bloc) | 코드 생성 기반, 타입 안전, 보일러플레이트 적음 |
| Fastlane (not 수동) | 반복 배포 시간 절약, 환경변수 주입 자동화 |

## 성과
- App Store + Google Play 양대 마켓 출시 완료
- 1인으로 기획 → 디자인 → 개발 → 배포 → 운영 전 과정 수행
- 실 사용자 피드백 기반 지속 개선 중
