# Spatial Workspace Android

Minimal WebView thin client for Rokid Max 2 / YodaOS-Master AR glasses. Connects to [spatial-workspace-web](https://github.com/aluminumio/spatial-workspace-web).

## Build

Debug APK (points to emulator localhost):
```bash
./gradlew assembleDebug
```

APK output: `app/build/outputs/apk/debug/app-debug.apk`

## Configure Server URL

Edit `app/build.gradle.kts`:

```kotlin
// In defaultConfig (production):
buildConfigField("String", "SERVER_URL", "\"https://your-server.example.com\"")

// In debug buildType (local dev):
buildConfigField("String", "SERVER_URL", "\"http://10.0.2.2:3000\"")
```

## CI

GitHub Actions builds debug APK on every push/PR. Release APKs require these repo secrets:

| Secret | Description |
|--------|-------------|
| `KEYSTORE_BASE64` | `base64 -i release.keystore` output |
| `KEYSTORE_PASSWORD` | Keystore password |
| `KEY_PASSWORD` | Key password |

Without signing secrets, CI falls back to debug APK.

## Features

- Fullscreen immersive mode (no status/nav bars)
- Screen always on (`FLAG_KEEP_SCREEN_ON`)
- WebRTC mic access auto-granted
- Custom UA: `SpatialWorkspace/1.0`
- Lifecycle-aware (resume/pause events dispatched to JS)
