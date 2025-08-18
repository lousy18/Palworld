# Our Space (Firebase + GitHub)

A role-based couple website with:
- Auth (Google sign-in)
- Roles: `public`, `friend`, `owner` (store in Firestore collection `roles` with doc ID = email)
- Gallery & Docs in Firebase Storage (`public/`, `friends/`, `private/` folders)
- Date Night Planner (Firestore `dateInvites`)
- Private Timeline, Letters (Firestore)
- Bucket List for friends+owners

## 1) Create Firebase Project
- Go to https://console.firebase.google.com
- Add project (no Google Analytics needed)
- In **Build → Authentication → Sign-in method**, enable **Google**
- In **Build → Firestore Database**, create database (Start in production mode)
- In **Build → Storage**, create storage
- In **Project Settings → General → Your apps**, add a **Web app** and copy the Firebase config

## 2) Paste Config
Open `index.html` and paste your Firebase config in the `firebaseConfig` object.

## 3) Deploy Security Rules
- In Firebase console:
  - Firestore rules: copy from `firestore.rules`
  - Storage rules: copy from `storage.rules`

## 4) Seed Roles
In Firestore, create collection `roles`.
Create document with **Document ID = your email** and fields:
```
role: "owner"
```
Create document with **Document ID = her email** and `role: "owner"`.
Add close friends:
```
Document ID = friend@email.com
role: "friend"
```

## 5) Hosting
You can deploy on **Firebase Hosting** or **GitHub Pages**.

### Option A) Firebase Hosting (recommended for auth)
- Install Node.js & Firebase CLI
- `npm install -g firebase-tools`
- `firebase login`
- `firebase init hosting` (use existing project, set public directory to `.`)
- `firebase deploy`

### Option B) GitHub Pages
GitHub Pages can host the static files, but **Authentication pop-ups sometimes require custom OAuth+domain whitelisting**.
For the smoothest login experience, use **Firebase Hosting**.

## 6) Using the App
- Sign in with Google
- Your role shows on the header
- Upload images to desired scope (public/friends/private)
- Create date invites (owners), add timeline/letters (owners), manage bucket list (owners add; friends view)
- Public visitors can only see public routes/data

## Notes
- This is a starter scaffold. You can expand sections and styling easily.
- Always keep `roles` doc IDs exactly equal to user email strings.
