# FixTrack — Native Android MVP

A local-first Android app for recording products, purchase prices, warranty dates, repair costs, and notes. No account, API key, paid service, or network permission is required.

## Tech stack
- Kotlin
- Jetpack Compose + Material 3
- Room database
- ViewModel + Kotlin Flow
- Minimum Android version: Android 8.0 (API 26)

## Project structure
```
FixTrack/
├── settings.gradle.kts
├── build.gradle.kts
├── gradle.properties
└── app/
    ├── build.gradle.kts
    └── src/main/
        ├── AndroidManifest.xml
        └── java/com/fixtrack/app/
            ├── MainActivity.kt
            └── data/
                ├── Product.kt
                ├── ProductDao.kt
                └── FixTrackDatabase.kt
```

## Build instructions
This is a standard Android Studio/Gradle project. On a computer, open this folder in Android Studio, allow Gradle sync, then run the `app` configuration on a device/emulator. The first build needs internet access to download Gradle dependencies.

On Android phone only, a compatible cloud Android build environment may work, but many browser IDEs do not support Android SDK/Gradle builds. Do not pay for a service; if the environment cannot build APKs, keep the source and use a computer later or use a trusted free Android build workflow.

## MVP features
- Add product, category, purchase price, purchase date, warranty end date, repair cost and notes
- Persist records in Room on device
- Show product count, warranties expiring within 30 days, and total repair spending
- Show warranty status on each product
- Delete products

## Manual test checklist
1. Launch app; dashboard should show zero products.
2. Tap + and add a product with valid dates such as `2026-10-18` and `2027-10-18`.
3. Save; verify it appears in the product list and product count becomes 1.
4. Force-close and reopen the app; verify the record remains.
5. Add a product with a warranty date 10 days away; verify Expiring Soon count increments.
6. Add repair cost to a product; verify total repair spending updates.
7. Try an invalid date and a negative price; the form should reject them.
8. Delete a product; verify it disappears and totals update.

## Current MVP limitations
- No scheduled notifications yet; warranty status is calculated when the screen opens.
- Repair cost is a single total field, not individual repair events.
- No bill image attachments, cloud sync, authentication, or automatic OCR yet.
- Data is stored locally; uninstalling the app may remove it. Add export/backup before relying on it for important records.

## Build from your Android phone using GitHub Actions (free tier)
1. Create a **public** GitHub repository named `FixTrack` (public repositories can use standard GitHub-hosted Actions runners without a paid plan, subject to GitHub's current limits).
2. Upload the contents of this project folder to the repository root, keeping the `.github/workflows/android.yml` file and its folder.
3. Open the repository's **Actions** tab and choose **Build FixTrack APK**. If it has not run automatically after the push, tap **Run workflow**.
4. Wait for the workflow to finish successfully. Open the completed run and download the `FixTrack-debug-apk` artifact.
5. Extract the downloaded artifact on your phone, tap `app-debug.apk`, and allow installation from that source if Android asks.

If the workflow fails, open the failed step and read the first Gradle error. Do not share passwords, signing keys, or private personal data in the repository. The debug APK is for testing, not a signed Play Store release.
