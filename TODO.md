# Real-Time Firebase Leaderboard + Auth Implementation TODO

## Plan Breakdown (Approved: Firebase Realtime DB + Auth)

**Status: [ ] In Progress**

### Step 1: Create TODO.md
- [x] Completed

### Step 2: Add Firebase SDK Scripts
- [x] Insert Firebase App, Auth, Database compat SDKs in <head>

### Step 3: Initialize Firebase (Config + Globals)
- [x] Add firebaseConfig
- [x] firebase.initializeApp()
- [x] const auth = firebase.auth()
- [x] const database = firebase.database()

### Step 4: Update Authentication Functions
- [x] Replace doRegister/doLogin/doAdminLogin with Firebase Auth
- [x] Add onAuthStateChanged listener for session management
- [x] Admin check: email == ADMIN_EMAIL

### Step 5: Migrate Data Structures
- [x] Update db.players to use Firebase paths /players/{uid}
- [x] Modify submitFlag() to sync to Firebase

### Step 6: Implement Real-Time Leaderboard
- [x] Update renderLeaderboard() with onValue listener
- [x] Add unsubscribe on screen change

### Step 7: Update Admin Functions
- [x] clearLeaderboard(): Reset Firebase player scores
- [x] renderUserList(): List from /players

### Step 8: UI Updates
- [x] Auth forms: Use email/password
- [x] User chip: From Firebase user
- [x] Test screens/tabs

### Step 9: Testing & Demo
- [ ] Test register/login/submit → live leaderboard
- [ ] Run `start index.html` or browser open
- [ ] Complete task

**Next Step:** Step 9 - Testing & Demo

**Status: [x] Completed**

