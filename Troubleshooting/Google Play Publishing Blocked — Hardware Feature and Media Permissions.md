---
type: troubleshooting
created: 2026-11-18
status: in-progress
tags:
  - troubleshooting
  - android
  - gradle
  - play-store
---

# Google Play publishing blocked — hardware feature & media permissions

## Problem
Google Play Console "Publishing overview" showed 2 blocking issues on the
Android release, preventing it from being sent for review:

1. **Required hardware feature declarations are restricting your app's
   availability** — the manifest declared a hard requirement on
   `android.hardware.wifi`, which made the app unavailable to Phone, Tablet,
   Desktop, and Android XR users whose devices don't support that feature as
   required.
2. **Use alternative system pickers for photos / videos** — the app requested
   the broad `READ_MEDIA_IMAGES` / `READ_MEDIA_VIDEO` (and
   `READ_EXTERNAL_STORAGE`) permissions instead of using the Android system
   photo/video picker, which Play's policy for API 33+ apps disallows unless
   the system picker is technically insufficient.

## Root Cause
`android/app/src/main/AndroidManifest.xml` declared `android.hardware.wifi`
as a required `<uses-feature>` (default `required="true"`) even though Wi‑Fi
is not essential to core app functionality, and still carried the legacy
broad media/storage permissions alongside (or instead of) the system photo
picker flow.

## Solution
In `android/app/src/main/AndroidManifest.xml`:
- Added `<uses-feature android:name="android.hardware.wifi" android:required="false" />`
  so the feature is marked optional instead of blocking install on
  unsupported devices.
- Removed `READ_MEDIA_IMAGES`, `READ_MEDIA_VIDEO`, and
  `READ_EXTERNAL_STORAGE` permissions via `tools:node="remove"`, relying on
  the system picker for photo/video selection instead.

```xml
-<manifest xmlns:android="http://schemas.android.com/apk/res/android">
+<manifest xmlns:android="http://schemas.android.com/apk/res/android"
+    xmlns:tools="http://schemas.android.com/tools">

   <!-- Internet Permission -->
   <uses-permission android:name="android.permission.INTERNET" />

   <!-- Camera Permission -->
   <uses-permission android:name="android.permission.CAMERA" />

-  <!-- Photo and Video Permissions (Android 13+) -->
-  <uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />
-  <uses-permission android:name="android.permission.READ_MEDIA_VIDEO" />
+  <!-- Photo picking uses the system Android Photo Picker (react-native-image-picker 8.x),
+       which needs none of READ_MEDIA_IMAGES / READ_MEDIA_VIDEO / READ_EXTERNAL_STORAGE; Play
+       Console disallows requesting them when a system picker already covers the feature. -->
+  <uses-permission android:name="android.permission.READ_MEDIA_IMAGES" tools:node="remove" />
+  <uses-permission android:name="android.permission.READ_MEDIA_VIDEO" tools:node="remove" />
+  <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" tools:node="remove" />

-  <!-- Photo Permission (Android 14+) -->
-  <uses-permission android:name="android.permission.READ_MEDIA_VISUAL_USER_SELECTED" />
-
-  <!-- Storage Permission (Android 12 and below) -->
-  <uses-permission
-      android:name="android.permission.READ_EXTERNAL_STORAGE"
-      android:maxSdkVersion="32" />
+  <!-- A dependency implicitly requires wifi hardware; the app works fine on cellular-only or
+       wifi-less devices (Desktop, Android XR), so it's declared optional to avoid restricting
+       the Play Store listing to wifi-capable devices only. -->
+  <uses-feature android:name="android.hardware.wifi" android:required="false" />

   <application
     android:name=".MainApplication"
```

## Verification
Rebuild the AAB with this manifest, re-test image picking end-to-end, and
upload a new release to Play Console, then re-run the Play Console
pre-launch/publishing checks to confirm both blocking issues clear.

## Resolution Status
Manifest change committed and pushed (`07d662e` on `dev_ravikant`). Not yet
live — pending rebuild, re-test, and a new Play Console upload.

## References
- [[Android Build Naming and Version Tracking (Flutter)|Android Build Naming and Version Tracking]]
