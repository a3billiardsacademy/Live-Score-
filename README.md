A3 Snooker Tournament Live Scoring

This is a real-time, live snooker scoring application built with HTML, Tailwind CSS, and Google Firebase. It provides a public-facing scoreboard that updates instantly, managed by a private, password-protected scorekeeper panel.

Designed by Md Maaz Alam.

Features

Real-time Scoring: All scores, frames, and breaks update instantly for all viewers using Firestore onSnapshot.

Public Scoreboard: A clean, read-only view for the public.

Private Admin Panel: A hidden, password-protected panel for the scorekeeper.

Login: User ID (maazalam04), Password (Maaz@2004)

Full Match Control:

Update player names.

Set the current tournament group/stage (e.g., "Group A", "Final").

Manually set the highest break score and player.

Log frame winners and display a match history.

Advanced Scoring:

"Undo Last Shot" button to correct mistakes.

Custom modal for handling tied frames (re-spotted black).

Firebase & Deployment

This application is a single HTML file designed to be deployed as a static site on platforms like Vercel or Netlify.

Firebase Setup

This app requires a Google Firebase project to function.

Create a Project: Go to the Firebase Console and create a new project.

Enable Firestore: In your project, create a Firestore Database.

Security Rules: For this public scoreboard to work, you must update your Firestore security rules to allow public read access to the data. Use the following rules, making sure to understand their public nature:

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow public read access to the match data
    match /artifacts/{appId}/public/data/snooker_matches/current_match {
      allow read: if true;
      allow write: if request.auth != null; // Only authenticated users can write
    }
  }
}


Get Config: In your project's "Project settings", find your web app's Firebase config object. It will look like this:

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT_ID.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};


Vercel Deployment

Add Your Config: Open the inde.html file and find the LOCAL_FIREBASE_CONFIG variable (around line 730). Paste your Firebase config object here.

Push to GitHub: Add inde.html, reme.md, and vercel.json to a GitHub repository.

Import to Vercel: Log in to Vercel, import your GitHub repository, and deploy. No special build commands are needed. Vercel will automatically serve inde.html as the root.
