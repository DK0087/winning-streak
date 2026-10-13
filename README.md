# Winning Streak 🌙

A nightly ritual app. Tick tonight's honest wins (each with its own streak), then
hold to affirm each dream goal over its own image or video, and close the night.
A daily notification reminds you (default **9:30 PM**, changeable on the home screen).
Everything you enter stays **on your phone** and works **offline**.

- **Android app:** full experience with the nightly reminder (survives reboot).
- **iPhone / any phone:** installable web app (PWA) via "Add to Home Screen".

## 📲 Install on Android (3 steps)

1. On your phone, open the **[download page](https://dk0087.github.io/winning-streak/download.html)** and tap **Download WinningStreak.apk**, then open it.
2. When Android says it can't install, tap **Settings** → turn on **Allow from this source** (*Install unknown apps*) for your browser, then go back.
3. Tap **Install**, open **Winning Streak**, and allow notifications.

Updates install right over the old app (same signing key, forever).
Direct links: **[download page](https://dk0087.github.io/winning-streak/download.html)** · **[latest Release](https://github.com/DK0087/winning-streak/releases/latest)**

## 🍎 Install on iPhone (and any phone)

Open **<https://dk0087.github.io/winning-streak/>** in Safari →
tap the **Share** button → **Add to Home Screen**. It then runs full‑screen and offline.
(Android Chrome: menu **⋮** → **Install app**.)

## 💾 Back up & restore

On the home screen, **Back up** saves a single file (your wins, goals, photos and
streak — media included). On a new phone, install the app, then **Restore** that
file. Nothing ever leaves your phone unless you share this backup yourself.

## 🔑 One‑time setup: signed APK

The app is built and signed automatically by GitHub Actions. So the signing key
stays out of this public repo, add two **repository secrets**
(Settings → Secrets and variables → Actions → *New repository secret*):

| Secret | Value |
| --- | --- |
| `ANDROID_KEYSTORE_BASE64` | base64 of the release keystore (provided to you separately) |
| `ANDROID_KEYSTORE_PASSWORD` | the keystore password (provided to you separately) |

Then push to `main` (or run **Actions → Build & Publish → Run workflow**). The build
signs **WinningStreak.apk**, attaches it to a Release, and deploys the download page.
Keep the keystore file and password forever — the same key means every future update
installs over the old app. Lose it and you'd have to uninstall/reinstall to update.

Until the secrets are set, the build can't produce the signed APK. If a secret is wrong,
the build log's "Prepare signing key" step says which one and why.

## ❓ Install troubleshooting

- **"App not installed":** an older copy signed with a different key is on the phone. Uninstall it once (use **Back up** first), then install the new APK. Later updates install over it.
- **No "Allow from this source" prompt:** open Android **Settings → Apps → Special access → Install unknown apps**, choose your browser, and turn it on.
- **No reminder at 9:30 PM:** allow notifications and **Alarms & reminders** for Winning Streak in Android settings, and exclude it from battery optimisation.

## 🛠️ Develop

The whole UI is one file: [`www/index.html`](www/index.html) (vanilla JS, no build step).

```
npm install
npx cap sync android          # copy web assets + plugins into the Android project
cd android && ./gradlew assembleRelease
```

Every push to `main` runs **[Build & Publish](../../actions)**:
signed APK → Release, and `www/` → GitHub Pages (PWA + public download).

Built with [Capacitor](https://capacitorjs.com/). App id `com.novateur.winningstreak`.
