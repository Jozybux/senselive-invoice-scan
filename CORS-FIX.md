# Fix CORS error (GitHub Pages → n8n)

Your page: **https://jozybux.github.io/senselive-invoice-scan/**  
Webhook: **https://ai.senselive.io/webhook/senselive-invoice-upload**

Browsers block cross-origin requests unless n8n allows your GitHub origin.

## Fix in n8n (2 minutes)

1. Open workflow **Senselive – Invoice Scan → Odoo + Master Sheet (READY)** on https://ai.senselive.io
2. Click node **Webhook – Invoice Upload2**
3. Open **Options** (or **Settings** → **Access Control**)
4. Set **Allowed Origins** to exactly:
   ```
   https://jozybux.github.io
   ```
   (Optional, for local testing: add `,http://localhost:8080`)
5. **Save** the workflow
6. **Deactivate** the workflow, then **Activate** again (required so CORS uses the published version)
7. Test upload from GitHub Pages again

## If still failing

| Check | Action |
|-------|--------|
| Workflow active? | Toggle OFF → ON in n8n |
| Correct URL? | Production: `/webhook/...` not `/webhook-test/...` |
| Ad blocker | Disable for `jozybux.github.io` and `ai.senselive.io` |
| Server env | Ask host to set `N8N_DEFAULT_CORS=true` if Allowed Origins UI is missing |

## Re-import workflow JSON

Import `Senselive – Invoice Scan → Odoo + Sheet (READY).json` from Downloads — it already includes `allowedOrigins` for `https://jozybux.github.io`.

After import, **activate** the workflow again.
