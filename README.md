# Pharmasuticals — Marketing Site (pre-launch)

Pre-launch interest site for **pharmasuticals.com**. No build step, no framework. Just HTML +
Tailwind via CDN. Deploys to GitHub Pages out of the box.

## Pages

| Route                  | File                  | Purpose                                                     |
| ---------------------- | --------------------- | ----------------------------------------------------------- |
| `/`                    | `index.html`          | Landing — hero, 6 differentials, compliance, pre-launch CTA |
| `/features.html`       | `features.html`       | Module-by-module feature breakdown                          |
| `/early-access.html`   | `early-access.html`   | Register-interest page · what you get + launch timeline + form |
| `/demo.html`           | `demo.html`           | Book-a-demo form (Web3Forms → hello@pharmasuticals.com)     |
| `/404.html`            | `404.html`            | Friendly fallback for unknown routes                        |

## Local preview

No build needed. Open `index.html` directly in a browser, or run a tiny dev server:

```bash
# Python (any version)
python3 -m http.server 4000

# Node
npx serve .
```

Then visit `http://localhost:4000`.

## Forms (1-minute setup)

Both the **interest registration** (`early-access.html`) and the **demo request** (`demo.html`)
forms post to [Web3Forms](https://web3forms.com), which relays submissions to
**hello@pharmasuticals.com** as nicely-formatted emails.

**One-time setup:**

1. Go to [web3forms.com](https://web3forms.com).
2. Enter `hello@pharmasuticals.com` → click **Create Access Key**.
3. Check that inbox — Web3Forms emails the access key (UUID-style string).
4. Open both `early-access.html` and `demo.html`, find:
   ```html
   <input type="hidden" name="access_key" value="YOUR_WEB3FORMS_ACCESS_KEY" />
   ```
   Replace `YOUR_WEB3FORMS_ACCESS_KEY` with the actual key.
5. Submit a test from your local preview to confirm the email lands.

Free tier: 250 submissions/month. Built-in honeypot (`botcheck` field) for spam protection.

### Want to change the destination email?

You'll need a new access key from web3forms.com for the new email address — they're 1:1 bound.
Repeat the steps above with the new address.

## Deploy to GitHub Pages

### One-time setup

1. Create a new repo on GitHub — `pharmasuticals-site` (any name works).
2. Push this folder to the repo:
   ```bash
   cd pharmasuticals-site
   git init
   git add .
   git commit -m "Initial marketing site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/pharmasuticals-site.git
   git push -u origin main
   ```
3. Go to **Settings → Pages** on the repo.
4. Source: **Deploy from a branch**.
5. Branch: **main** · folder: **/ (root)** · Save.
6. GitHub builds and publishes within ~1 minute.
   - URL: `https://<your-username>.github.io/pharmasuticals-site/`

### Custom domain (pharmasuticals.com)

1. Create a `CNAME` file at the repo root containing just `pharmasuticals.com`:
   ```bash
   echo "pharmasuticals.com" > CNAME
   git add CNAME && git commit -m "Add custom domain" && git push
   ```
2. In **Settings → Pages**, set Custom domain to `pharmasuticals.com` and tick **Enforce HTTPS**.
3. At your DNS provider, add:
   - `A` records pointing the apex to GitHub Pages IPs:
     - `185.199.108.153`
     - `185.199.109.153`
     - `185.199.110.153`
     - `185.199.111.153`
   - `CNAME` record for `www` → `<your-username>.github.io`
4. DNS can take up to an hour. Once propagated, GitHub auto-issues a Let's Encrypt cert.

## Editing tips

- **Brand color** lives in `assets/styles.css` (`--brand: #047857`). Change once, applies
  everywhere.
- **Logo** is an inline SVG (the green activity-pulse mark). Search for `logo-mark` to swap.
- All pages share the same header + footer markup — keep them in sync when adding nav items.
- Tailwind is pulled from CDN, so any utility class works out of the box. No build step.

## File structure

```
pharmasuticals-site/
├── index.html             # Landing · 6 differentials + pre-launch CTA
├── features.html          # Full feature breakdown
├── early-access.html      # Register-interest page + launch timeline
├── demo.html              # Book a demo (Web3Forms relay)
├── 404.html               # Not-found fallback
├── .nojekyll              # Tells GitHub Pages to skip Jekyll
├── assets/
│   ├── styles.css         # Small CSS layer on top of Tailwind CDN
│   └── favicon.svg        # Brand mark
└── README.md
```

## License

Proprietary. © 2026 Pharmasuticals.
