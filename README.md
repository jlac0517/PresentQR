# ClassCheck — QR Attendance System

A lightweight, QR-based classroom attendance tracker. No backend needed — all data is stored in **localStorage** in the browser.

## Features

- 📱 Students scan a QR code with their phone camera — no app install required
- ⏱ QR auto-refreshes every 30–120 seconds to prevent screenshot sharing
- 🗄 All attendance data saved locally in the teacher’s browser (localStorage)
- 📋 View past sessions and export any session to CSV
- 🚫 Duplicate check-in prevention per session
- ✅ Works 100% offline after first load (except Google Fonts)

-----

## Deploy to GitHub Pages (step by step)

### 1. Create the repository

1. Go to [github.com](https://github.com) and sign in
1. Click **New repository** (the green button or the `+` icon → New repository)
1. Name it exactly: `classcheck`
1. Set it to **Public** (required for free GitHub Pages)
1. Leave everything else as default → click **Create repository**

-----

### 2. Upload the file

1. Inside your new repository, click **Add file → Upload files**
1. Drag and drop `index.html` into the upload area
1. Scroll down → click **Commit changes**

-----

### 3. Enable GitHub Pages

1. Go to your repository **Settings** tab
1. In the left sidebar click **Pages**
1. Under **Branch**, select `main` and leave the folder as `/ (root)`
1. Click **Save**
1. Wait ~60 seconds, then refresh the page

GitHub will show a green banner:

```
Your site is live at https://YOUR-USERNAME.github.io/classcheck/
```

-----

### 4. Use the app

|Who        |What to do                                                                                                                 |
|-----------|---------------------------------------------------------------------------------------------------------------------------|
|**Teacher**|Open `https://YOUR-USERNAME.github.io/classcheck/` on laptop/projector → Teacher Dashboard → Start Session → project the QR|
|**Student**|Point phone camera at QR → tap the link → enter name → Check In                                                            |


> **Important:** Teacher and students must be on the **same GitHub Pages URL** (same origin) for localStorage to be shared between devices on the same browser profile. For cross-device check-ins, see the note below.

-----

## How localStorage sync works

Because GitHub Pages serves the same origin to everyone, `localStorage` is **per-browser, per-device**.

This means:

- ✅ The teacher’s laptop stores all session data
- ✅ Students who scan on the **same device** (e.g. a class tablet) check in locally
- ⚠️ Students scanning on their **own phones** write to *their own* localStorage — the teacher won’t see those entries in real time on their laptop

### Recommended classroom setup

**Option A — Shared device (simplest)**
Have one shared tablet/laptop near the door. Students walk up and type their name after scanning or just typing the URL.

**Option B — Personal phones + manual export**
Students check in on their own phones. At the end of class, each student’s check-in is recorded locally on their device. The teacher collects CSVs or uses a sign-in sheet as backup.

**Option C — Full cross-device sync (advanced)**
Replace `localStorage` calls in `index.html` with a free backend like [Supabase](https://supabase.com) or [Firebase Realtime Database](https://firebase.google.com) for true multi-device sync with no server cost.

-----

## Updating the app

To update `index.html` after making changes:

1. Open your repository on GitHub
1. Click `index.html`
1. Click the ✏️ pencil (Edit) icon
1. Paste the new content → **Commit changes**

Or use Git:

```bash
git clone https://github.com/YOUR-USERNAME/classcheck.git
cd classcheck
# replace index.html with new version
git add index.html
git commit -m "update app"
git push
```

-----

## File structure

```
classcheck/
└── index.html   ← entire app (HTML + CSS + JS, single file)
```

-----

## Local storage schema

All data lives under the key `classcheck_sessions` in `localStorage` as a JSON array:

```json
[
  {
    "sessionId": "CC-LX4F2A",
    "className": "Math 101 — Period 3",
    "teacherName": "Ms. Garcia",
    "date": "May 19, 2026",
    "students": [
      { "name": "Juan dela Cruz", "time": "08:04 AM", "date": "May 19, 2026" },
      { "name": "Maria Santos",   "time": "08:05 AM", "date": "May 19, 2026" }
    ]
  }
]
```

To **back up** all data: open browser DevTools → Application → Local Storage → copy the value of `classcheck_sessions`.

To **restore**: paste it back into the same key.

-----

## License

MIT — free to use, modify, and share.