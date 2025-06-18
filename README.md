# Ahoum Task – React Native App with Firebase Google OAuth

This is a React Native Android application built as part of the **Ahoum backend intern hiring assessment**. It showcases Google OAuth 2.0 authentication using **Firebase**, clean UI screens, and secure routing based on login state — all built without a custom backend.

---

## 🚀 Features

- 🔐 Google Sign-In via Firebase Authentication
- 🎯 Auth state handling and secure navigation
- 🧾 User profile screen showing Google account info
- 🔁 Session persistence and logout
- ⚠️ Loading and error handling

---

## 🛠️ Tech Stack

| Layer        | Technology                          |
|--------------|--------------------------------------|
| Framework    | React Native (CLI only, not Expo)    |
| Auth Service | Firebase Authentication              |
| Auth Provider| Google Sign-In (`@react-native-google-signin/google-signin`) |
| State Mgmt   | React Context API or Zustand         |
| Navigation   | React Navigation (Stack Navigator)   |
| Storage      | AsyncStorage                         |

---

## 📁 Folder Structure

```

ahoum\_project/
├── android/
├── ios/
├── assets/
├── components/
├── screens/
├── navigation/
├── Utils/
├── App.js
└── README.md

```

---

## 🔧 Prerequisites

- Node.js ≥ 18.x
- React Native CLI
- Android Studio with emulator or real device
- Firebase Console account
- Registered Android SHA-1 fingerprint

---

## 🔑 Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a project (e.g. `SampleProject`)
3. Add an Android app
   - Provide your app's package name
   - Register your **SHA-1** (use `./gradlew signingReport`)
4. Download `google-services.json` and place it in: android/app/
```

android/app/google-services.json

```
5. Enable **Google** Sign-In under:
```

Firebase Console → Authentication → Sign-in Method → Google

````

---

## 📦 Installation

```bash
git clone https://github.com/bharadwajchakka/ahoum_project.git
cd ahoum_project

npm install
````

---

## ▶️ Running the App

### 1. Start Metro

```bash
npm start
```

### 2. Run on Android

```bash
npm run android
```

> Emulator or device must be connected and authorized.

---

## 🧑‍💻 Implementation

### 🔐 Google OAuth + Firebase Authentication

* Uses `@react-native-google-signin/google-signin` for OAuth login
* Passes Google token to Firebase to sign in:

```js
const { idToken } = await GoogleSignin.signIn();
const googleCredential = auth.GoogleAuthProvider.credential(idToken);
await auth().signInWithCredential(googleCredential);
```

### 📲 Auth State Management

* Listens to Firebase auth state via `onAuthStateChanged()`
* Dynamically switches screens based on login status

```js
auth().onAuthStateChanged(user => {
  setUser(user); // stored in Context or Zustand
});
```

### 🧭 Navigation

* Uses Stack Navigator from `@react-navigation/native`
* Authenticated users → Dashboard
* Unauthenticated users → Login

```js
{user ? <AppStack /> : <AuthStack />}
```

### 👤 User Profile (not implemented)

* Displays name, email, and photo from Firebase user object

```js
const user = auth().currentUser;
<Text>{user.displayName}</Text>
<Image source={{ uri: user.photoURL }} />
```

### 🚪 Logout Functionality

* Clears session from both Google and Firebase:

```js
await GoogleSignin.signOut();
await auth().signOut();
```

---

## 🔐 Security Notes

* Firebase handles session and token storage securely
* Google Client ID is restricted via SHA-1 + package name
* No sensitive info (keys) committed to the repo
* Optionally use `.env` + `react-native-config` for environment variables

---

## ✅ Tested Scenarios

* Google Sign-In first login
* Auto re-auth on app restart
* Logout and re-login
* Invalid credential error handling
* UI state on loading/errors

---

## 📄 License

This project is developed as part of the **Ahoum Backend Intern Assessment Task**.

---

## 🙋 Contact

**Bharadwaj Chakka**
📧 [bharadwajchakka@gmail.com](mailto:bharadwajchakka10182004@gmail.com)

---

## 📚 Resources

* [React Native Docs](https://reactnative.dev/docs/getting-started)
* [Firebase Docs](https://firebase.google.com/docs)
* [React Native Firebase](https://rnfirebase.io/)
* [Google Sign-In for React Native](https://github.com/react-native-google-signin/google-signin)

```

---

Let me know if you'd like to:
- include a demo video/GIF in the README,
- auto-generate screenshots,
- or create a `firebaseConfig.js` starter with instructions.
```
