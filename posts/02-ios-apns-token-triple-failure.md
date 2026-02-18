# iOS APNs 토큰 발급 실패의 숨겨진 원인 3가지

> **타겟 플랫폼**: Velog (한글) → dev.to (영문 번역)
> **예상 키워드**: flutter fcm token ios, apns token null, firebase ios push notification

---

## 글 구조

### 1. 문제 상황 (Hook)
- Flutter 앱에서 FCM 토큰이 iOS에서만 `null` 반환
- Android는 정상, iOS만 문제 → APNs 체인 어딘가가 끊어진 것
- 구글링해도 "하나의 원인"만 나오는데, 우리는 **3개가 동시에** 고장

### 2. 원인 1: aps-environment 엔트리먼트 누락
- `Runner.entitlements`에 `aps-environment` 키가 없으면 APNs 등록 자체가 안 됨
- Xcode에서 Push Notification capability를 추가해도 자동으로 안 들어가는 경우 있음
- 확인 방법과 수동 추가 방법 코드 첨부

### 3. 원인 2: Firebase Console에 APNs 키 미등록
- Apple Developer Console에서 .p8 키를 만들었지만 Firebase에 업로드를 안 했음
- Firebase Console → Project Settings → Cloud Messaging → APNs Authentication Key
- 키 ID, Team ID 매칭 확인 방법

### 4. 원인 3: UIScene lifecycle에서 Firebase swizzling 실패
- Flutter 3.41+ 에서 UIScene lifecycle이 기본값
- Firebase의 method swizzling이 UIApplication 기반이라 깨짐
- `AppDelegate.swift`에 수동 APNs 등록/전달 코드 추가

```swift
// 핵심 코드 스니펫 첨부
func application(_ application: UIApplication,
    didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    Messaging.messaging().apnsToken = deviceToken
}
```

### 5. 해결 확인
- FCM 토큰 142자 정상 발급 확인
- Supabase DB에 토큰 저장 성공
- 포그라운드/백그라운드/종료 상태 3시나리오 푸시 수신 확인

### 6. 체크리스트 정리
- [ ] Runner.entitlements에 aps-environment 있는가?
- [ ] Firebase Console에 .p8 키 업로드했는가?
- [ ] AppDelegate에 수동 APNs 전달 코드 있는가?
- [ ] Info.plist에 FirebaseAppDelegateProxyEnabled = NO 인가?

---

## 메타 정보
- **작성 예상 시간**: 3-4시간
- **예상 길이**: 2,000-2,500자
- **태그**: `flutter`, `fcm`, `apns`, `ios`, `push-notification`, `firebase`
- **썸네일 아이디어**: FCM 토큰 흐름도 (APNs → Firebase → Flutter)
