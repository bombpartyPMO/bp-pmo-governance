# PMO Governance Cloud Save Setup

This prototype saves through Cloudflare Worker into this GitHub repo:

https://github.com/bombpartyPMO/bp-pmo-governance

## 1. Put these files in GitHub

- `index.html`
- `data/governance-data.json`
- `cloudflare-worker.js`
- `wrangler.toml`
- `wrangler.toml.example`

## 2. Create a GitHub token

Create a fine-grained GitHub token with contents read/write access to:

`bombpartyPMO/bp-pmo-governance`

## 3. Configure Cloudflare Worker

The included `wrangler.toml` is already configured for:

- `GITHUB_OWNER = "bombpartyPMO"`
- `GITHUB_REPO = "bp-pmo-governance"`
- `GITHUB_BRANCH = "main"`
- `GITHUB_DATA_PATH = "data/governance-data.json"`

Then add secrets:

```bash
wrangler secret put GITHUB_TOKEN
wrangler secret put PMO_EDIT_KEY
wrangler deploy
```

`PMO_EDIT_KEY` is the shared edit key the page asks for when someone saves.

## 4. Connect the page to the Worker

`index.html` is already connected to:

```js
const API_BASE=window.PMO_GOVERNANCE_API||'https://pmo-governance.douglasf.workers.dev';
```

After that, the page loads from GitHub and saves changes back to `data/governance-data.json`.
