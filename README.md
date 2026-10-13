# Pet Compatibility App — Firebase Lab (Experiment 03)

A minimal HTML, CSS, and JavaScript app demonstrating Firebase Authentication, Cloud Firestore, Cloud Storage, and Firebase Hosting.

## Features
- Register and log in with email/password
- Add pet records (name, age, breed)
- List the signed-in user's pet records
- Delete a pet record
- Optionally upload a pet photo to Firebase Storage
- Deploy the static site with Firebase Hosting

## 1. Create/configure Firebase
1. Open https://console.firebase.google.com/ and create a project.
2. Register a **Web app** in Project settings → General → Your apps.
3. Copy the web app configuration into `public/index.html` where the `YOUR_...` placeholders appear.
4. Build → Authentication → Get started → Sign-in method → enable **Email/Password**.
5. Build → Firestore Database → Create database.
6. Build → Storage → Get started.
7. In Authentication → Settings → Authorized domains, ensure `localhost` is listed for local testing.

## 2. Run locally
You need Node.js and npm installed. From this project folder:

```bash
npm install -g firebase-tools
firebase login
firebase emulators:start
```

The emulator command requires emulator configuration, so for the simplest local preview use VS Code's **Live Server** extension and open `public/index.html`. Alternatively, use any static HTTP server. Firebase Auth/Firestore/Storage requests still go to your real Firebase project when using Live Server.

Important: do not open the HTML file directly as `file://`; serve it over HTTP.

## 3. Deploy to Firebase Hosting
From the project root:

```bash
npm install -g firebase-tools
firebase login
firebase init hosting
```

During initialization:
- Select your existing Firebase project.
- Set the public directory to `public`.
- Configure as a single-page app: **No**.
- If asked to overwrite `public/index.html`, choose **No**.

Then deploy:

```bash
firebase deploy
```

The CLI may create/update `.firebaserc` and `firebase.json`. This repository already includes a basic `firebase.json`.

## 4. Firestore and Storage rules
The repository includes `firestore.rules` and `storage.rules`. Deploy the rules with:

```bash
firebase deploy --only firestore:rules,storage
```

If Firebase CLI says a service is not configured, run `firebase init firestore` and/or `firebase init storage`, keeping the existing rules files.

## Notes
- Firebase web API keys in the client configuration identify the project; they are not server passwords. Access must be protected with Authentication and Security Rules.
- Never commit private keys, service-account JSON files, database passwords, or other secrets.
- This is a teaching/demo application, not a production-ready application.
