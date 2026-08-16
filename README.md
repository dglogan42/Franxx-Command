# FRANXX COMMAND

Offline Android mecha gacha: summon Franxx pilots, build a squad, and hunt a Klaxosaur.

Package: `com.franxx.command` · minSdk 26 (Android 8) · targetSdk 35 · version 1.0

**Sideload APK:** [FranxxCommand-release.apk](FranxxCommand-release.apk) (Android 8+)

This is an unofficial fan project. It is not affiliated with *Darling in the Franxx* or *Xenoblade Chronicles*.

## Features

- **Summon** — Strelizia Gate single (◆300) or multi (◆3000, +1 free). Rates: SSR 5% / SR 25% / R 70%
- **Squad** — collected pilots with ATK / DEF / SPD
- **Battle** — Klaxosaur Hunt using your top 3 units
- Progress saved on-device (`localStorage`). No internet permission.

## Project layout

```
android/                          native WebView app
  app/src/main/assets/www/        game (HTML / CSS / JS)
  app/src/main/java/.../          MainActivity
  keystore.properties             local signing config (gitignored)
  release/                        upload keystore (gitignored)
play-store/icon-512.png           Play Console high-res icon
```

## Requirements

- JDK 17
- Android SDK (platform 35, build-tools)
- `ANDROID_HOME` / `ANDROID_SDK_ROOT` set, or `android/local.properties` with `sdk.dir=`

## Build

```powershell
cd android
.\gradlew.bat assembleDebug
```

Debug APK: `android/app/build/outputs/apk/debug/app-debug.apk`

### Signed Play Store release

1. Keep `android/release/franxx-upload.p12` and `PLAY_STORE_SIGNING.txt` **off git and backed up**. Losing the upload key means you cannot update the same Play listing.
2. `android/keystore.properties` must point at that keystore (already used for the first release).
3. Bump `versionCode` (and `versionName`) in `android/app/build.gradle`.
4. Build:

```powershell
cd android
.\gradlew.bat bundleRelease assembleRelease
```

| Artifact | Path | Use |
| --- | --- | --- |
| AAB | `android/app/build/outputs/bundle/release/app-release.aab` | Upload to Play Console |
| APK | `android/app/build/outputs/apk/release/app-release.apk` | Sideload only |

Play Console will not accept an APK for a new app. Enable Play App Signing (default). Store listing still needs screenshots, a 1024×500 feature graphic, content rating, and a privacy policy if you declare data collection.

Upload-key fingerprints (App integrity):

- SHA-1: `BA:CD:09:EE:4E:F5:CC:95:D9:EA:99:24:00:56:1B:61:FF:A2:EA:AF`
- SHA-256: `9E:A1:4E:45:51:2E:FA:63:67:41:8B:52:4E:D6:0E:2F:5B:1A:70:83:B6:92:96:34:60:54:D0:31:71:97:1F:44`

## License

MIT. See [LICENSE](LICENSE). Character and series names remain the property of their owners.
