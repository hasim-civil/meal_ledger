# 🍱 Meal Ledger

A simple, free web app for households and roommates to track daily meal attendance (Day/Night) and shared market spending — built with Firebase so multiple people can each have their own private login.

**Live demo:** `https://hasim-civil.github.io/meal_ledger/`

---

## ✨ Features

- 🔐 **Multi-user accounts** — each person signs up with their own email/password. Nobody can see anyone else's data.
- 🔄 **Real-time sync** — toggle a meal and it saves instantly, no page refresh needed.
- ☀️ **Day & Night meal tracking** — tap to mark attendance for each day of the month.
- 🛒 **Market spend tracker** — log shared grocery/market expenses with running monthly totals.
- 🔑 **Forgot password** — built-in password reset via email.
- 🙍 **Editable profile** — set a display name and profile photo (via image URL).
- 🌙 **Dark mode** — toggle and saved automatically for next visit.
- 📱 **Works on any device** — phone, tablet, or laptop, just open the link in a browser.
- 💸 **100% free to run** — built entirely on free tiers (GitHub Pages + Firebase Spark plan).

---

## 🧱 Tech stack

| Layer | Tool |
|---|---|
| Hosting | GitHub Pages |
| Auth | Firebase Authentication (Email/Password) |
| Database | Firebase Firestore (real-time) |
| Frontend | Plain HTML, CSS, JavaScript — no build step, no frameworks |

---

## 🚀 Setup guide

### 1. Create a Firebase project
1. Go to [console.firebase.google.com](https://console.firebase.google.com) → **Add project**.
2. Name it anything (e.g. `meal-ledger`) → finish the setup wizard.

### 2. Enable Email/Password sign-in
- **Build → Authentication → Get started → Email/Password → Enable → Save**

### 3. Create the database
- **Build → Firestore Database → Create database**
- Pick a location close to you → **Start in production mode** → Create

### 4. Set Firestore security rules
In Firestore → **Rules** tab, paste:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```
Click **Publish**. This makes sure each person can only read/write their own data.

### 5. Get your config keys
- ⚙️ **Project settings → Your apps → `</>` (Web) → Register app**
- Copy the `firebaseConfig` object it gives you.

### 6. Add the config to the app
Open `index.html`, find this near the bottom of the `<script>` section, and paste your values in:

```js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

### 7. Deploy with GitHub Pages
1. Push this repo to GitHub.
2. Go to **Settings → Pages** in your repo.
3. Under **Source**, select your main branch → **Save**.
4. Your site will be live at `https://<your-username>.github.io/<repo-name>/` within a minute or two.

---

## 👤 Using the app

1. Open the site → **Sign up** with any email and a password (6+ characters).
2. Once logged in, use the **Attendance** tab to tap Day/Night for each date.
3. Use the **Market** tab to log shared expenses with a date and amount.
4. Tap your name/avatar in the top bar to set a display name or photo.
5. Forgot your password? Use the **Forgot password?** link on the login screen.
6. Each person who signs up gets their own private space — no setup needed per person beyond creating an account.

---

## 📁 Project structure

```
.
├── index.html   # the entire app — HTML, CSS, and JS in one file
└── README.md
```

There is no backend server and no build step. Firebase handles authentication and data storage directly from the browser.

---

## 🔒 Privacy & data

- All data is stored in your own Firebase project — not on any third-party server beyond Firebase/Google Cloud.
- Each user's attendance and spending records are isolated by their account (enforced by the Firestore security rules above).
- No analytics, tracking, or ads.

---

## 🛠️ Customizing

- **Colors / theme:** edit the CSS variables at the top of `index.html` inside `:root` and `[data-theme="dark"]`.
- **Year range:** change `YEAR_MIN` / `YEAR_MAX` / `YEAR_DEFAULT` near the top of the `<script>` section.
- **App name:** update the `<title>` tag and the `.brand-name` text in the header.

---

## 💛 Credits

Created by **Hasim**
