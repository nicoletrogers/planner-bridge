# Planner Bridge

**Scan your daily planner → AI extracts events → push directly to Google Calendar.**

A single-file progressive web app. No backend, no database, no monthly cost.

---

## Live Demo

Once deployed to GitHub Pages, your app lives at:
`https://<your-username>.github.io/<your-repo-name>/`

---

## Deploy to GitHub Pages (5 minutes)

### Step 1 — Fork or create the repository

1. Go to [github.com](https://github.com) and create a new repository (e.g. `planner-bridge`)
2. Upload `index.html` and `README.md` to the root of the repository

### Step 2 — Enable GitHub Pages

1. In your repository, go to **Settings → Pages**
2. Under **Source**, select **Deploy from a branch**
3. Set branch to `main` (or `master`) and folder to `/ (root)`
4. Click **Save**

GitHub will show your live URL — usually within 60 seconds.

### Step 3 — Configure Google OAuth (for direct calendar push)

The Google Calendar push feature requires a Client ID registered to your live domain.

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project (or use an existing one)
3. Go to **APIs & Services → Enable APIs** → search for **Google Calendar API** → Enable it
4. Go to **APIs & Services → Credentials → Create Credentials → OAuth 2.0 Client ID**
5. Application type: **Web application**
6. Under **Authorised JavaScript origins**, add your GitHub Pages URL:
   ```
   https://<your-username>.github.io
   ```
7. Copy the **Client ID** (looks like `123456789-abc.apps.googleusercontent.com`)
8. Open Planner Bridge → tap **Settings** → paste the Client ID into **Google Client ID**

That's it. The OAuth consent screen will appear on first use.

### Step 4 — Configure Gemini API (for AI event extraction)

Extraction is powered by Google Gemini 1.5 Flash — generous free tier, no credit card required for basic use.

1. Go to [aistudio.google.com/apikey](https://aistudio.google.com/apikey)
2. Click **Create API Key**
3. Copy the key
4. Open Planner Bridge → tap **Settings** → paste into **Gemini API Key**

---

## Cost

| Feature | Cost |
|---|---|
| GitHub Pages hosting | Free |
| Gemini 1.5 Flash (text) | Free up to 15 requests/minute |
| Gemini 1.5 Flash (image/scan) | Free up to 15 requests/minute |
| Google Calendar API | Free (personal use) |

For a single user scanning one page per day, this runs at **$0/month**.

---

## Architecture

Everything runs in the browser. The only external calls are:
- `generativelanguage.googleapis.com` — Gemini event extraction
- `googleapis.com/calendar/v3` — Google Calendar write (optional)
- `accounts.google.com` — OAuth popup (optional)

No data is stored server-side. History is saved to `localStorage` in your browser.

---

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire application |
| `README.md` | This file |

---

## Usage

1. **Print the template** (Settings → Print daily planner template)
2. Fill it in by hand each morning
3. Open Planner Bridge on your phone
4. Tap **Photo / upload** and photograph your planner page
5. Review and edit extracted events
6. Tap **Push to Google Calendar**
