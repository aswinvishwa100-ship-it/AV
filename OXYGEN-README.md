# AV Oxygen Home + Phone (prototype)

An independent OnePlus-inspired launcher and default phone app for the original Nord CE (EB2101), OxygenOS 13 / Android 13. Installs separately from AV Pixel Home, under `com.av.oxygenhome`. Supports Android 10+. This is not OnePlus software, a firmware update, or an Android 16 upgrade.

## Features and boundaries

- Light home screen, red-accent stacked clock, app search, four favorites, calendar shortcut, and a Phone shortcut.
- Swipe up on the home background for apps; swipe down for the in-app control center. Tap the footer or long-press the home background for settings.
- Wi-Fi, Bluetooth, and Display cards open Android's settings. They do not pretend to be live toggles.
- Optional notification center shows current active notifications, opens their supplied actions, and dismisses clearable notifications. Android notification access must be granted explicitly. Content is not written to files, analytics, or a server; no Internet permission is requested. AV can see private notification text when access is enabled. Disable access in Android settings whenever desired.
- The notification center is inside AV Home. The actual system notification shade, lock screen, and other apps remain OxygenOS. Replacing the system shade requires system-level access or firmware changes.
- Separate default Phone role: dial pad, incoming-call screen, answer/decline, hang up, mute, speaker, call DTMF keypad, hold/resume when provided by the network, and held-call selection. Caller identity comes only from Android Telecom. No call recording, contacts database, or call-history permissions.
- Emergency calling remains subject to Android Telecom and the preinstalled emergency phone UI. Do not test by calling emergency numbers. Dual-SIM selection, Bluetooth switching, video calls, conference management, carrier services, and OxygenOS-specific behavior need physical-device testing; there are no dedicated controls for these features.
- No app widgets, folders, wallpaper rendering, custom icon packs, notification badges, or weather data yet. The wallpaper settings shortcut changes Android's wallpaper but AV uses its own background.

## Install and enable

1. Download `AV-Oxygen-Home.apk` to the phone. Allow installation from your chosen file manager only when prompted; turn that permission back off afterward.
2. Open **AV Oxygen Home**. Choose it in **Settings > Apps > Default apps > Home app**, or tap the home footer and select **Set default Home app**.
3. Tap **Phone > Setup > Choose default phone app** and select AV. Grant call permission when placing your first call; after granting, tap Call again to confirm. Set up call notifications via **Phone > Setup > Allow call notifications**.
4. On Android 14+, check **Incoming call full-screen settings** as well. On Android 13, make sure the Phone calls notification channel is enabled and permits incoming-call notifications.
5. For notification cards, open **Notifications > Enable notification access**. Android 13 may block sideloaded notification listeners until you explicitly use **App info > three-dot menu > Allow restricted settings**. Only enable this if you trust this app's access to notification content.
6. Make a non-emergency test call with a trusted contact. Test receiving, answering, declining, ending, speaker, mute, keypad, screen off, and lock-screen calls before using this prototype as your usual phone app. Carrier and hardware behavior cannot be established from compilation alone.

## Revert

Choose the original OnePlus Home app and original Phone app in Android's Default apps settings. Revoke AV's notification access, then uninstall AV Oxygen Home. AV Pixel Home, if installed, remains a separate app. Keep the original phone app enabled.

## Build

Standard project: Gradle 8.9, Android Gradle Plugin 8.7.3, JDK 17 or 21, SDK platform 35, build tools 35.0.0:

```sh
cd oneplus
gradle :app:assembleDebug :app:lintDebug
```

The cloud instance uses the tested alternative build path because Java-based package downloads are blocked:

```sh
cd /workspace/AV/oneplus
ANDROID_HOME=/workspace/tooling/android-sdk ECJ_JAR=/workspace/tooling/ecj.jar ./scripts/build-apk.sh
```

With a full JDK installed, omit `ECJ_JAR`. Alternative build requires Python 3 and zip. Output: `app/build/manual/av-oxygen-home-debug.apk`.

This is a debug-signed prototype, not a Play Store release. Keep the ignored debug keystore to update this installation without uninstalling. Do not publish keystores or private keys.
