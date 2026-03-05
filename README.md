🚀 Flutter Firebase Google Login App
A clean, Material 3 Flutter application featuring Google Sign-In integration with Firebase Authentication. This app includes a secure Auth Gate, a beautiful Gradient Login Page, and a Dashboard displaying user profile information.

📌 Features
Automatic Auth State: Uses StreamBuilder to switch between Login and Home pages.

Full Sign-Out: Implements deep logout (Firebase + Google + Account Picker reset).

Material 3 UI: Clean, modern interface with adaptive color schemes.

Profile Integration: Displays Google profile picture, name, and email.

🛠️ Prerequisites
Before running the app, ensure you have:

Flutter SDK installed.

A Firebase Project created.

Google Sign-In enabled in the Firebase Authentication "Sign-in method" tab.

⚙️ Android Setup (Crucial for Release)
1. Internet Permission
To prevent the Black Screen issue in release mode, ensure android/app/src/main/AndroidManifest.xml includes:

XML
<uses-permission android:name="android.permission.INTERNET"/>
2. SHA-1 Fingerprints
Google Sign-In will fail on other devices if the SHA-1 keys are missing.

Run the signing report:

PowerShell
cd android
./gradlew signingReport
Copy the SHA-1 and SHA-256 from both debug and release variants.

Add them to your Firebase Project Settings and download the updated google-services.json.

3. Build Configuration (build.gradle.kts)
Ensure MultiDex is enabled and R8 shrinking is configured correctly to avoid PlatformException errors:

Kotlin
    defaultConfig {
        multiDexEnabled = true
        minSdk = 23
    }
    buildTypes {
        release {
            isMinifyEnabled = false
            isShrinkResources = false
            signingConfig = signingConfigs.getByName("debug")
        }
    }
🚀 How to Build & Run
For Development
PowerShell
flutter clean
flutter pub get
flutter run
For Sharing with Others (Universal APK)
Do not use --split-per-abi if you want a single file that works on all phones. Instead, use:

PowerShell
flutter build apk --release
Location of APK: build\app\outputs\flutter-apk\app-release.apk

📂 Project Structure
main.dart: Entry point and UI logic.

firebase_options.dart: Firebase configuration (generated via FlutterFire CLI).

pubspec.yaml: Project dependencies (Firebase, Google Sign-In).

⚠️ Troubleshooting
Black Screen on Start: Check if the device has internet and if you added the <uses-permission> tag.

Sign-in hangs/circles forever: This is a SHA-1 mismatch. Double-check your fingerprints in the Firebase Console.

App won't install: Ensure you are using the universal app-release.apk and not a split-ABI version.
