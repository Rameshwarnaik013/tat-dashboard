# TAT Dashboard

Streamlit web app for analyzing **Dispatch & Delivery Turnaround Time (TAT)** from a sales report.

## Features

- **Two parent toggles**: Dispatch TAT and Delivery TAT (separate bucket logic for each)
- **4 sub-views per TAT**: Invoice Date, MIS Item Group, Sales Channel, From Warehouse
- **Customer drill-down** inside the Sales Channel tab
- **Smart sidebar filters** with search, Select All / None, all-selected-by-default, cascading Customer from Sales Channel
- **Date presets**: All Time, Last 7 / 15 / 30 Days, Custom range
- **Dark bold table headers** in both the dashboard and Excel export
- **Pivot-only Excel download** with formatted sheets for both TAT types

## Bucket Logic

| TAT type     | Buckets                                                  | Source column   |
| ------------ | -------------------------------------------------------- | --------------- |
| Dispatch TAT | `0-2 Days`, `3-5 Days`, `>5 Days`                         | `Dis Days`      |
| Delivery TAT | `0-9 Days`, `10-12 Days`, `>12 Days`, `Delivery Pending` | `Delivery Days` |

## Required columns in upload

`Invoice Date`, `New MIS Item Group`, `Sales_Channel`, `From Warehouse`, `Customer`,
plus `Dis Days` / `Dis TAT` and `Delivery Days` / `Delivery TAT`.

## Install & run locally

```bash
pip install -r requirements.txt
streamlit run app.py
```

The app opens at http://localhost:8501.

---

## Deployment

> **Note on Vercel:** Vercel is built for serverless functions and does not support
> WebSocket-based servers like Streamlit. Use any of the platforms below instead.

### Option 1 — Render (recommended, Vercel-like UX)

1. Go to https://render.com and sign in with GitHub
2. Click **New +** → **Blueprint**
3. Connect this repo (`Rameshwarnaik013/tat-dashboard`)
4. Render reads `render.yaml` and provisions a free web service
5. Your app goes live at `https://tat-dashboard.onrender.com` in ~3 min

Auto-redeploys on every push to `main`. Free tier sleeps after 15 min idle.

### Option 2 — Streamlit Community Cloud (zero config)

1. Go to https://share.streamlit.io and sign in with GitHub
2. **Create app** → select `Rameshwarnaik013/tat-dashboard`
3. Main file: `app.py`, branch: `main`
4. Click **Deploy**

Free, no sleep, only Streamlit-branded URL.

### Option 3 — Railway

1. Go to https://railway.app, click **Deploy from GitHub repo**
2. Select this repo — Railway reads `Procfile` automatically
3. $5/mo free credit, custom domains, no sleep

## Files for deployment

| File                       | Used by                       |
| -------------------------- | ----------------------------- |
| `render.yaml`              | Render Blueprint              |
| `Procfile`                 | Railway, Heroku, Fly.io       |
| `runtime.txt`              | Render, Heroku Python version |
| `requirements.txt`         | All Python platforms          |
| `.streamlit/config.toml`   | Streamlit theme + upload size |
