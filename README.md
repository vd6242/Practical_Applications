# Shobhit & Neha Home Planner

An installable web app (PWA) for monthly budgeting, expense logging, statement import, savings and term insurance tracking, and analytics. No server and no build step: it is plain files.

## Files
- `index.html` – the app
- `config.js` – optional settings (Google Drive client ID)
- `manifest.webmanifest`, `sw.js`, `icons/` – make it installable and usable offline
- `vendor/xlsx.full.min.js` – Excel library (bundled so the app works offline)
- `home-finance-template.xlsx` – Excel template for first-time data load

## 1. Put it on GitHub Pages
1. Sign in to GitHub and create a new repository, for example `home-planner`.
2. Upload everything in this folder, keeping the `icons` and `vendor` folders. On github.com use Add file, then Upload files, and drag the contents in.
3. Open Settings, then Pages. Under Build and deployment choose Deploy from a branch, branch `main`, folder `/ (root)`, then Save.
4. After a minute the app is live at `https://YOUR-USERNAME.github.io/home-planner/`.

Notes
- A free GitHub account needs a public repository for Pages. That is fine: the repository holds only the app, never your financial data. Do not commit exports or statements to it.
- Do not put real data in `config.js` other than the Google client ID, which is not secret.

## 2. Install it
- Android Chrome: menu, then Install app.
- iPhone Safari: Share, then Add to Home Screen. Installing from the Home Screen also keeps your data more reliably than a normal Safari tab.
- Windows or Mac (Chrome or Edge): install icon in the address bar.

## 3. Where your data lives
Data is stored in the browser on each device. Each phone has its own copy unless you turn on Google Drive sync below. Browsers can clear storage, so use Export to Excel now and then as a backup.

To move data to a new address or device: Export to Excel on the old one, then Import from Excel on the new one.

## 4. iCloud
A web app cannot read or write iCloud directly; Apple offers no way to do that from a website. What works:
- Export to Excel, then save the file to iCloud Drive in the Files app. Import it on another Apple device when needed. This is manual, not automatic.
- On Apple devices use Home Screen install, not a Safari tab.

## 5. Google Drive sync (optional, automatic)
When on, the app keeps one file, `shobhit-neha-home-planner.json`, in the signed-in Google account's Drive. It loads the newest copy when you tap Sync and uploads changes about two seconds after each edit.

Setup (about 10 minutes, once)
1. Go to console.cloud.google.com and create a project.
2. APIs & Services, Library: enable Google Drive API.
3. OAuth consent screen: choose External, fill in the app name and your email, and add Neha and Shobhit's Google addresses under Test users. Leave it in Testing mode.
4. Credentials, Create credentials, OAuth client ID, type Web application. Under Authorized JavaScript origins add `https://YOUR-USERNAME.github.io` (the origin only, no path).
5. Copy the Client ID into `config.js` between the quotes and commit the change.
6. Open the app and tap Sync with Google Drive. Approve the access when asked.

Good to know
- The app asks only for the `drive.file` permission, so it can see only the file it creates, not the rest of your Drive.
- Because of that permission, a file made by one Google account cannot be opened by a different account. To share one set of data between you both, sign in with the same Google account on both phones (for example a shared family account). Separate accounts each keep their own copy.
- The sign-in lasts about an hour. If you edit after that, changes stay on the device and the app asks you to tap Sync. If two phones edit offline, the most recent save wins.
- In Testing mode Google may ask you to sign in again every week or so.

## 6. Updating the app
Replace `index.html` in the repository. To force devices to refresh the cached files, change `home-planner-v1` to `home-planner-v2` in `sw.js`.

## Statement import
Upload CSV or Excel statements from net banking on the Import statement tab. PDF statements are not supported. Review the suggested categories, fix any that are wrong, and add the approved rows. Your corrections are remembered per merchant.
