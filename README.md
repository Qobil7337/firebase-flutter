# Firebase + Flutter Setup Guide

## Quick overview
1. Create Firebase project in Firebase Console and enable Authentication providers (Email/Password, Google, Facebook).  
2. Add Android & iOS apps in Firebase  
3. Install & run the FlutterFire CLI to generate `firebase_options.dart` and wire Firebase into your Flutter app.  
4. Add dependencies: `firebase_core`, `firebase_auth`, `google_sign_in`, `flutter_facebook_auth` (and optional `flutterfire_ui`).  
5. Implement auth flows in Dart:  
   - Email/password register & login + `sendPasswordResetEmail`.  
   - Google sign in (native plugin + Firebase credential).  
   - Facebook sign in (facebook plugin + Firebase credential).  
6. Test  

---

## Create Firebase project & enable providers
1. Open [Firebase Console](https://console.firebase.google.com)  
   → Add project → follow steps.  
2. In the Firebase console, go to **Build → Authentication → Sign-in method**:  
   - Enable Email/Password.  
   - Enable Google (no extra info; but Android requires SHA-1).  
   - Enable Facebook — you’ll enter App ID and App Secret from Facebook Developer Console (next section).  

   *(You’ll come back here after setting up Android package names / iOS bundle ids / Facebook App.)*

---

## Create apps in Firebase (Android & iOS)

### Android
1. In **Firebase Console → Project Overview → Project settings** → under your apps section click **Android icon** to add Android app.  
2. Enter your Android package name (e.g. `com.example.my_auth_app`). You will get it from `build.gradle.kts` file.  
   then follow the instructions there.  
   **but do not follow the instruction on how to add file to the project**, because that will be done using FlutterFire.

---

### iOS
1. In **Firebase Console → add iOS app.** Provide your app’s Bundle ID (e.g. `com.example.myAuthApp`).  
   **but do not follow the instruction on how to add file to the project**, because that will be done using FlutterFire.  
2. follow instructions there  

---

## FlutterFire setup

Run:
```bash
dart pub global activate flutterfire_cli
```

Then, add it to path  
open your terminal config:
```bash
nano ~/.zshrc
```

Add this line at the bottom:
```bash
export PATH="$PATH":"$HOME/.pub-cache/bin"
```

Then save and reload your shell:
```bash
source ~/.zshrc
```

Test it works:
```bash
flutterfire --version
```

Then, run:
```bash
flutterfire configure
```

If you see this error:
```
ERROR: The FlutterFire CLI currently requires the official Firebase CLI to also be installed
```
then, you need to install The FlutterFire CLI (`flutterfire configure`) depends on the official Firebase CLI (the Node.js command-line tool) to talk to your Firebase account.

Run:
```bash
npm install -g firebase-tools
```

Check it’s installed:
```bash
firebase --version
```

Log into Firebase:
```bash
firebase login
```

Once logged in, verify your projects list:
```bash
firebase projects:list
```

Re-run FlutterFire configure:
```bash
flutterfire configure
```

Select platforms.

---

## Add dependencies

Install:
```bash
flutter pub add firebase_core
```

Then add this code in your `main.dart` before `runApp(const MyApp());`:
```dart
WidgetsFlutterBinding.ensureInitialized();
await Firebase.initializeApp(
  options: DefaultFirebaseOptions.currentPlatform,
);
```

Add these dependencies:
```
firebase_auth
google_sign_in
flutter_facebook_auth
```

Create auth methods in a service file.

---

✅ **This README explains how to set up Firebase and Flutter for authentication (Email/Password, Google, Facebook).**
