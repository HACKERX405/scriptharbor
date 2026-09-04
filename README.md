# ScriptHarbor V3 — real Cloudflare Pages deployment

V3 is no longer pretending that `*.sh.live` is a hosted URL. The HTML workspace can deploy a static project for real through a small Cloudflare Worker.

## Files

- `scriptharbor.html` — landing page + browser IDE + preview + deployment UI.
- `scriptharbor-cloudflare-worker.js` — secure deployment bridge.

## 1. Create a Cloudflare account

Use Cloudflare Workers/Pages. The Pages Direct Upload API supports uploading prebuilt assets and serving the project from a `*.pages.dev` URL.

## 2. Create an API token

Create an Account API Token with **Cloudflare Pages: Edit** permission. Do NOT put this token inside `scriptharbor.html`.

## 3. Deploy the worker

Create a Worker named something like `scriptharbor-deploy` and paste `scriptharbor-cloudflare-worker.js` into it.

Add:

- Worker variable: `ACCOUNT_ID` = your Cloudflare account ID
- Worker secret: `CLOUDFLARE_API_TOKEN` = your Pages Edit API token

The Worker must expose its `/deploy` route.

## 4. Connect ScriptHarbor

Open ScriptHarbor → Start building → Deploy.

Paste the Worker URL, for example:

`https://scriptharbor-deploy.<your-subdomain>.workers.dev/deploy`

Enter a project name and press **Deploy now**.

## 5. What V3 does

Browser → secure Worker → Cloudflare Pages asset store → production deployment → `https://PROJECT.pages.dev`

The browser never receives the Cloudflare API token.

## Important

V3 currently deploys static assets (HTML/CSS/JS/images). It does not execute arbitrary server-side Node/Python code. A future V4 can add GitHub OAuth, repositories, database-backed projects, isolated build sandboxes, team collaboration, and AI agents.
