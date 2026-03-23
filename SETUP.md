# 🚩 Flag the Code — Setup Guide

## Files
- `index.html` — Participant-facing website (register, submit codes, leaderboard)
- `admin.html` — Admin dashboard (real-time leaderboard, reset scores, activity feed)

---

## Step 1: Create a Firebase Project

1. Go to https://console.firebase.google.com
2. Click **Add Project** → name it `flag-the-code`
3. Disable Google Analytics (optional) → **Create Project**

---

## Step 2: Enable Authentication

1. In Firebase Console → **Authentication** → **Get Started**
2. Enable **Email/Password** provider
3. Go to **Users** tab → **Add User**:
   - Email: `admin@flagthecode.com` (or your preferred admin email)
   - Password: a strong password (this is your admin login)

---

## Step 3: Enable Realtime Database

1. In Firebase Console → **Realtime Database** → **Create Database**
2. Choose **Start in test mode** (we'll lock it down below)
3. Select your region → **Done**

### Set Database Rules (paste this):
```json
{
  "rules": {
    "participants": {
      "$uid": {
        ".read": true,
        ".write": "auth != null && auth.uid === $uid"
      },
      ".read": true,
      ".write": "auth != null"
    }
  }
}
```

---

## Step 4: Get Your Firebase Config

1. In Firebase Console → **Project Settings** (gear icon) → **General**
2. Scroll to **Your apps** → click **</>** (Web app)
3. Register app → copy the `firebaseConfig` object

---

## Step 5: Paste Config into Both HTML Files

Replace the placeholder `firebaseConfig` in **both** `index.html` and `admin.html`:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyDctNHWnkY8G4g7K_-zIrtsrp4AmRkjx3w",
  authDomain: "points-tracker-2f024.firebaseapp.com",
  databaseURL: "https://points-tracker-2f024-default-rtdb.asia-southeast1.firebasedatabase.app",
  projectId: "points-tracker-2f024",
  storageBucket: "points-tracker-2f024.firebasestorage.app",
  messagingSenderId: "683402475231",
  appId: "1:683402475231:web:0ab91357d452322e0a9b6a",
  measurementId: "G-NPBS9D4MPZ"
};
```

Also update `ADMIN_EMAIL` in `admin.html`:
```javascript
const ADMIN_EMAIL = "admin@flagthecode.com"; // your admin email
```

---

## Step 6: Customize Bug Codes

In both files, edit the `BUG_CODES` object:

```javascript
const BUG_CODES = {
  "BUG001": { points: 10, description: "SQL Injection vulnerability" },
  "BUG002": { points: 20, description: "XSS vulnerability" },
  // ... add your own codes
};
```

These codes are what participants find on your teammate's website and enter here.

---

## Step 7: Deploy

**Option A — Free hosting with Firebase Hosting:**
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
# Set public directory, answer prompts
firebase deploy
```

**Option B — Any static host:**
Upload both HTML files to GitHub Pages, Netlify, Vercel, etc.

---

## How It Works

| Flow | Description |
|------|-------------|
| Participant registers | Account created in Firebase Auth + entry added to Realtime DB |
| Participant submits code | Code validated, points added instantly to their DB record |
| Leaderboard | All clients listen to DB via `onValue()` — updates in real-time |
| Admin logs in | Must match `ADMIN_EMAIL` — unauthorized users are rejected |
| Admin resets score | Wipes a participant's points/bugs in the DB |
| Activity feed | Admin sees every new bug submission as it happens |

---

## Total Bug Codes = 8
Points range from 10–30 per bug. Edit freely in `BUG_CODES`.
