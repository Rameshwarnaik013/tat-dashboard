# TAT Dashboard — Vercel (in-browser Streamlit)

This folder contains a Vercel-deployable version of the TAT dashboard.

## How it works

Vercel does not support persistent Python servers like Streamlit. To run Streamlit on Vercel, this folder uses **[stlite](https://github.com/whitphx/stlite)** — a build of Streamlit that runs **entirely in the browser** using [Pyodide](https://pyodide.org/) (Python compiled to WebAssembly).

The entire app — file parsing, pivots, Excel export — happens client-side. Vercel just serves static HTML + JS.

### Trade-offs vs Render / Streamlit Cloud

| Factor              | stlite on Vercel                  | Render / Streamlit Cloud           |
| ------------------- | --------------------------------- | ---------------------------------- |
| First page load     | ~30-60s (downloads Python + libs) | ~2s                                |
| Subsequent loads    | Instant (cached)                  | Instant                            |
| Cold start          | None                              | ~30s (free tier sleeps)            |
| Data privacy        | Files never leave the browser     | Files uploaded to server           |
| Server cost         | Zero (static)                     | Free tier or paid                  |

## Deploy to Vercel

1. Go to https://vercel.com and sign in with GitHub
2. Click **Add New** → **Project** → select `Rameshwarnaik013/tat-dashboard`
3. In **Configure Project**:
   - **Framework Preset:** Other
   - **Root Directory:** `web`
   - Build & install commands: leave blank
4. Click **Deploy**

App goes live at `https://<your-project>.vercel.app` in ~30 seconds.

## File map

- `index.html` — stlite browser bootstrap; loads Python runtime, mounts the Streamlit app, shows a spinner during first load
- `streamlit_app.py` — copy of the Streamlit app code (mirror of root `app.py`)
- `vercel.json` — explicit static-only deployment config

## Updating the app

Whenever you change the root `app.py`, also copy the same changes into `web/streamlit_app.py`. Commit and push — Vercel auto-redeploys.
