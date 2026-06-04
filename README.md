# SenseLive Invoice Scan — GitHub Pages

HR uploads a scanned vendor invoice (PDF or photo). The page POSTs to your n8n webhook; n8n runs Gemini, Odoo, and Google Sheets on the backend.

## Deploy to GitHub Pages

1. Create a new GitHub repo (e.g. `senselive-invoice-scan`).
2. Copy **`index.html`** into the repo root (only this file is required).
3. On GitHub: **Settings → Pages → Source** = `Deploy from branch` → branch `main` → folder `/ (root)`.
4. Your site will be live at:
   `https://YOUR_USERNAME.github.io/senselive-invoice-scan/`

## n8n webhook (must match)

| Mode | URL |
|------|-----|
| **Production** (workflow **Active**) | `https://ai.senselive.io/webhook/senselive-invoice-upload` |
| **Test** (Execute workflow once) | `https://ai.senselive.io/webhook-test/senselive-invoice-upload` |

Edit the `WEBHOOK_URL` constant at the top of `index.html` if you switch modes.

## Form fields sent to n8n

| Field | Required | Notes |
|-------|----------|--------|
| `invoice_file` | Yes | PDF, JPG, PNG, or WebP — must match n8n **Validate File Upload** node |
| `submitted_by` | No | Defaults to `HR Portal` |
| `invoice_source` | No | Set to `github_pages_scan` for logging |

## CORS (fix “Network or CORS error”)

Your live site: **https://jozybux.github.io/senselive-invoice-scan/**

In n8n → **Webhook – Invoice Upload2** → **Options** → **Allowed Origins**:

```
https://jozybux.github.io
```

Then **deactivate and re-activate** the workflow.

See **[CORS-FIX.md](CORS-FIX.md)** for step-by-step screenshots-level detail.

## Workflow checklist

- [ ] Import `Senselive – Invoice Scan → Odoo + Sheet (READY).json`
- [ ] Activate workflow
- [ ] Odoo credential **Odoo account** configured
- [ ] Google Sheet ID set in **Google Sheets** node
- [ ] Test upload from the GitHub Pages URL

## Local test before GitHub

```bash
cd github-pages
python -m http.server 8080
```

Open `http://localhost:8080` — note: CORS may still block localhost unless n8n allows `http://localhost:8080`.
