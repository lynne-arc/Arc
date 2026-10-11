# ARC — Ark Royal Closings · Setup Guide (Phase 1)

Three files, two homes:

| File | Lives in | What it is |
|---|---|---|
| `Code.gs` | Google (script.google.com, ARC account) | The engine: data, contacts, documents, contract reading, email drafts, morning reminders, nightly backup |
| `admin.html` | GitHub | **Your TC Dashboard** (private — needs your admin key) |
| `intake.html` | GitHub | **The agents' File Input page** (public link you share) |

Allow about 45 minutes the first time. Do it on a computer, signed in to Chrome as **lynne@arkroyalclosings.com**.

---

## Part A — Google (the engine)

1. Go to **script.google.com** → **New project**. Click "Untitled project" at the top and rename it **ARC Backend**.
2. Delete everything in the editor, paste in all of `Code.gs`, and click **Save** (💾).
3. In the function menu at the top, choose **setupARC** → click **Run**.
   - Google asks for permission → **Review permissions** → choose your ARC account.
   - You'll see "Google hasn't verified this app". That's normal for your own script → **Advanced** → **Go to ARC Backend (unsafe)** → **Allow**.
   - Check your inbox: **"ARC backend is set up ✔"** contains your **admin key**. Keep that email.
4. Add your Claude key: click **⚙ Project Settings** (left side) → scroll to **Script properties** → **Add script property**
   - Property: `ANTHROPIC_API_KEY`  Value: your `sk-ant-…` key → **Save script properties**.
   - (You'll also see `TEST_MODE = true` there. Leave it.)
5. Back in the editor (`< >` on the left), choose **testClaudeKey** → **Run** → the log at the bottom should say **✔ Your contract-reading key works.**
6. Click **Deploy** (top right) → **New deployment** → click the ⚙ next to "Select type" → **Web app**
   - Description: `ARC v1` · Execute as: **Me** · Who has access: **Anyone** → **Deploy**
   - Copy the **Web app URL** (ends in `/exec`). You need it in Part B.

## Part B — GitHub (the pages)

> Use a GitHub account that's yours/ARC's — **not** the Verani `cneregion` account. ARC must stay separate from Verani.

7. Open `admin.html` and `intake.html` in Notepad (right-click → Open with → Notepad). In each, find
   `PASTE_YOUR_WEB_APP_URL_HERE` and replace it with your Web app URL (keep the quote marks). Save both.
8. On github.com: **New repository** → name it `arc` → **Public** → **Create repository**.
9. Click **uploading an existing file** → drag in `admin.html`, `intake.html` and `README.md` (**not** Code.gs) → **Commit changes**.
10. **Settings** → **Pages** → Source: **Deploy from a branch** → Branch: **main** / **(root)** → **Save**. Wait 1–2 minutes.
11. Your links:
    - Dashboard: `https://YOUR-GITHUB-NAME.github.io/arc/admin.html` — bookmark it, open it, paste your admin key once.
    - File Input page for agents: `https://YOUR-GITHUB-NAME.github.io/arc/intake.html`
12. Optional: in Script properties add `DASHBOARD_URL` = your dashboard link, so "new file" emails link straight to it.

## Part C — Test it (10 minutes)

- Open the File Input page, fill it in as a pretend agent (use your own Gmail as the "agent" and "client"), attach any P&S PDF, send.
- You get a "New file ARC-0001" email. Open your dashboard → **Review & confirm** the dates → check the three emails → **Save as draft** → look in Gmail **Drafts** (it's addressed to you and starts with `[TEST]`).
- Tomorrow at 7am you'll get "ARC morning deadlines" if anything is due within 3 days.

---

## Everyday rules (the Scoreboard lessons, built in)

- **Updating the engine later** (when Claude gives you a new `Code.gs`): paste it in, Save, then **Deploy → Manage deployments → ✏️ edit → Version: New version → Deploy**. Never "New deployment" — that makes a new URL and the pages stop working.
- **Updating the pages**: on GitHub open the file → ✏️ → paste → Commit. Your Web app URL line must stay in it.
- **Never rename, move or delete** "ARC Data — do not edit, move or rename.json" (it lives in **_Processes - Don't Touch** in your ARC Drive). It's found by its ID; if it disappears the dashboard stops with an error (it will *never* silently start empty). Nightly copies are in **ARC Backups** (last 30 days).
- **Going live** (only after the Commission/Maggie answers): Script properties → `TEST_MODE` → `false`. From then on drafts are addressed to the real people — still drafts, you still press Send.
- **Claude key renewal**: before 31 Jan 2027 make a new key and replace `ANTHROPIC_API_KEY`. If it expires, the dashboard tells you and you type dates in meanwhile.
- **Lost the admin key?** In the script editor run **showMyDetails** — it's printed in the log.

## Tagging emails you write yourself

Start the subject with the file tag, e.g. **`[ARC-0007] 10 Morgan Way`**. The dashboard's drafts do this automatically. (Phase 3 uses the tag to log your Gmail-sent emails on the file and show them to agents.)
