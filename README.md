# firebase-flutter

# Quick overview
1. Create Firebase project in Firebase Console and enable Authentication providers (Email/Password, Google, Facebook).
2. Add Android & iOS apps in Firebase, download google-services.json (Android) and GoogleService-Info.plist (iOS), and configure platform files (incl. Android SHA-1).
3. Install & run the FlutterFire CLI to generate firebase_options.dart and wire Firebase into your Flutter app.
4. Add dependencies: firebase_core, firebase_auth, google_sign_in, flutter_facebook_auth (and optional flutterfire_ui).
5. Implement auth flows in Dart:
    Email/password register & login + sendPasswordResetEmail.
    Google sign in (native plugin + Firebase credential).
    Facebook sign in (facebook plugin + Firebase credential).
6. Test

# Create Firebase project & enable providers
1. Open https://console.firebase.google.com
 → Add project → follow steps.
2. In the Firebase console, go to Build → Authentication → Sign-in method:
   Enable Email/Password.
   Enable Google (no extra info; but Android requires SHA-1). 
   Enable Facebook — you’ll enter App ID and App Secret from Facebook Developer Console (next section).

   (You’ll come back here after setting up Android package names / iOS bundle ids / Facebook App.)


# Create apps in Firebase (Android & iOS)
Android
1. In Firebase Console → Project Overview → Project settings → under your apps section click Android icon to add Android app.
2. Enter your Android package name (e.g. com.example.my_auth_app). You will get it from build.gradle.kts file.
then follow the instructions there.

iOS
1. In Firebase Console → add iOS app. Provide your app’s Bundle ID (e.g. com.example.myAuthApp).
2. follow instructions there
