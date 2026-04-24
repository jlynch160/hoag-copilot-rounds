# Easy Health · Microsoft 365 + Copilot demo

Single-file static demo. Drop this folder on any static host and you're live.

## What's in here

- `index.html` — the entire demo (HTML + inline CSS + inline JS)
- `copilot-logo.png`, `logo-*.png` — product icons (referenced by relative path from `index.html`)
- `staticwebapp.config.json` — config for Azure Static Web Apps (safe to ignore on other hosts)

## Deploy options

### 1. Azure Static Web Apps (best for the Easy Health / Microsoft narrative) — 5 min

1. Push this folder to a new GitHub repo.
2. Azure portal → Create a resource → Static Web App.
3. Build details: App location `/`, Output location `/` (no build step).
4. Azure creates a GitHub Action automatically. First deploy takes ~2 min.
5. Free tier supports a custom domain (`demo.easyhealth.ai` or similar).

**Why this one for Easy Health:** the demo is telling a Microsoft story — hosting it on Azure reinforces it, and Purview/Entra governance claims you make in the demo are actually enforceable on this platform.

### 2. Netlify Drop (fastest — 60 seconds, no account required for preview)

1. Visit <https://app.netlify.com/drop>.
2. Drag this folder onto the page.
3. You get a `random-name.netlify.app` URL immediately.
4. Optional: sign in to claim the site and add a custom domain.

### 3. Vercel (easy CI/CD, great preview URLs)

1. Push to GitHub.
2. <https://vercel.com/new> → Import the repo → Deploy. No build settings needed.
3. Every git push gets its own preview URL — handy for iterating during sales cycles.

### 4. GitHub Pages (free, slowest iteration)

1. Push to GitHub.
2. Settings → Pages → Source: `main` branch, `/` folder. Save.
3. Live at `https://<user>.github.io/<repo>/` within ~1 min of each push.

### 5. Local preview (no deploy)

Open `index.html` directly in a browser — everything works locally.

## Notes

- **No backend, no secrets.** Everything is client-side; you can share the URL freely.
- **"Time saved today" counter, persona switcher, published agents, etc. are all local state.** Refreshing resets.
- **Dark-mode preference persists** via localStorage, scoped per-origin.
- **Logos** are from Icons8 (M365 product family). The Copilot logo PNG is the same. If you need the real Microsoft brand assets for customer-facing use, source them from your Microsoft partner portal.
- **PHI in the demo is fictional.** Patient names, MRNs, medications, and scenarios are invented for the demo narrative.

## Sharing the demo in a room

- Open in Edge or Chrome, press F11 for fullscreen.
- Click the "Guided tour" button bottom-left to auto-walk the golden path (~2 min).
- Avatar (top-right) swaps between 4 personas — each shows a different home page.
- The guided tour, role switcher, and dark mode toggle are the three "wow" moments.
