# Cloudflare Setup — Bad Ace FM

## One-time (Jeremy, ~5 min)
1. Sign up free: dash.cloudflare.com/sign-up
2. Workers & Pages → Create → **Import a repository** → pick `weirdandstrong/bad-ace-martial-arts`
   - `wrangler.jsonc` in this repo pre-configures everything (static assets from `/site`, no build command)
3. Deploy → you get `badace-fm.workers.dev` (or choose Pages instead: framework None, build command empty, output dir `site` → `*.pages.dev`)

Every `git push` auto-deploys from then on.

## Let Claude operate Cloudflare (optional, recommended)
Add these as **custom connectors** in the Claude app (Settings → Connectors → Add custom connector), then authorize with your Cloudflare login:

- `https://mcp.cloudflare.com/mcp` — main API (DNS, redirects, domains)
- `https://builds.mcp.cloudflare.com/mcp` — inspect/manage deploys
- `https://docs.mcp.cloudflare.com/mcp` — docs (no auth needed)

After connecting, Claude can manage DNS, set up the shoushufm.com 301 redirect, and debug builds directly.

## Later: domain mapping (when badacefm.com is purchased)
1. Buy via Cloudflare Registrar (at-cost) — or point external nameservers at Cloudflare
2. Project → Custom domains → add `badacefm.com` (SSL + DNS automatic)
3. Add `shoushufm.com` as a zone → Bulk Redirects → 301 everything to badacefm.com
4. Retire the GitHub Pages workflow (delete `.github/workflows/deploy.yml`) so only one copy of the site is live
