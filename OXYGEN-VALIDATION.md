# Validation

- Android SDK 35 resource compilation and manifest linking: passed.
- Java compilation and Android DEX generation: passed.
- APK alignment and Android v3 signature verification (minimum Android 10): passed.
- Package: com.av.oxygenhome; version 0.1 / code 1; min API 29; target API 35.
- Declared permissions: CALL_PHONE, POST_NOTIFICATIONS, USE_FULL_SCREEN_INTENT. Notification listener uses Android's user-controlled binding permission. No Internet, storage, contacts, call-history, accessibility, or overlay permissions.
- Calls and full-screen notifications are gated by Android's default-phone role and permission settings.
- Existing Pixel build is unchanged and remains separately installable.
- Compiler warnings concern older Telecom APIs retained for Android 13 compatibility.

Runtime checks remain pending unless separately recorded below. The cloud host has no KVM device. Its adb tool could not write authentication files to the read-only home directory, and the software emulator did not provide a usable Android testing connection during validation. Compilation and signing do not prove incoming-call delivery, notification-listener access, audio routing, emergency fallback, dual-SIM handling, or OxygenOS gesture behavior.

Before using AV as your regular phone app, test incoming/outgoing non-emergency calls, answer/decline/end, lock-screen delivery, permission denial, mute/speaker, keypad tones, SIM selection, role removal, and switching back to the original Phone app. Do not call emergency services for testing.
