# Streakora — Android app

A personal self-improvement app: daily habits & streaks, goals, mood journal,
focus timer, progress charts, and a steps tracker. Native Android wrapper around
the Streakora UI, built automatically by GitHub Actions.

## How the APK is built

Every push to `main` runs `.github/workflows/build.yml`, which:
1. Sets up JDK 17 + the Android SDK on a GitHub runner
2. Builds a debug APK (`gradle assembleDebug`)
3. Publishes it to the **"latest" Release** and as a build **Artifact**

**Download the APK:** open this repo on your phone → **Releases** → `latest` →
download `app-debug.apk` → install (allow "install unknown apps" for your browser).

## Project layout

- `app/src/main/assets/streakora.html` — the whole app UI (offline, data saved on device)
- `app/src/main/java/.../MainActivity.kt` — a WebView host that loads the UI
- `app/src/main/AndroidManifest.xml`, `res/` — Android app shell
- `.github/workflows/build.yml` — the cloud build

## Steps / Google Fit

Stage 1 (this version): steps are entered manually on the Today screen
(tap **Edit** on the Steps card) with a daily goal, km and kcal estimate.

Stage 2 (planned): read today's steps automatically from **Health Connect**
(which holds Google Fit's step data) with on-device permission, and push them
into the UI via `window.setSteps(n)`.

## Notes

- Data is stored on the device (in the WebView). It persists across app restarts.
- Debug-signed build, for personal use.
