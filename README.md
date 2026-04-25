# CineReels — Android App

A TikTok-style video reel player with SRT subtitle search, converted from HTML to a native Android WebView app.

---

## Requirements

- Android Studio Hedgehog (2023.1.1) or newer
- Android SDK 34
- Kotlin 1.9+
- A physical device or emulator running Android 8.0 (API 26)+

---

## How to Open & Run

1. **Open Android Studio**
2. Choose **File → Open** and select this `CineReels/` folder
3. Wait for Gradle sync to complete (first sync downloads dependencies — needs internet)
4. Connect an Android device via USB (or launch an emulator)
5. Press the **▶ Run** button

---

## How the App Works

| Layer | Detail |
|---|---|
| `MainActivity.kt` | Hosts a full-screen `WebView` with JS enabled |
| `WebViewAssetLoader` | Serves `cinemaseven.html` over a virtual `https://` origin so all browser APIs (IntersectionObserver, etc.) work correctly |
| File chooser | Native Android file picker is wired to `<input type="file">` so you can pick videos and `.srt` files from your device storage |
| Permissions | `READ_MEDIA_VIDEO` (Android 13+) / `READ_EXTERNAL_STORAGE` (older) requested at launch |
| Immersive mode | Status bar and nav bar are hidden for a full-screen reel experience |

---

## Permissions Declared

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.READ_MEDIA_VIDEO" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" android:maxSdkVersion="32" />
```

---

## Project Structure

```
CineReels/
├── app/
│   ├── src/main/
│   │   ├── assets/
│   │   │   └── cinemaseven.html       ← Your original app
│   │   ├── java/com/cinereels/app/
│   │   │   └── MainActivity.kt        ← WebView host + file picker
│   │   ├── res/
│   │   │   ├── layout/activity_main.xml
│   │   │   └── values/
│   │   │       ├── strings.xml
│   │   │       ├── themes.xml
│   │   │       └── colors.xml
│   │   └── AndroidManifest.xml
│   └── build.gradle
├── gradle/wrapper/gradle-wrapper.properties
├── build.gradle
├── settings.gradle
└── gradle.properties
```

---

## Usage in the App

1. Tap **📁 Videos** to pick one or more video files from your device
2. Tap **📄 SRTs** to load matching subtitle files (same order as videos)
3. Type a word or phrase in the search box and tap **Find**
4. Swipe up/down through matching reel clips — tap to pause/play
