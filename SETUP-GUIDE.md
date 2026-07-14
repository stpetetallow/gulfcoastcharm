# Gulfcoast Charm — Launch Guide
*GitHub Pages + Formspree + DNS, step by step (same flow as your previous sites)*

---

## Part 1 — Put the site on GitHub Pages

1. **Sign in** at github.com (same account as your previous two sites).
2. Click **+ → New repository** (top right).
   - Name: `gulfcoastcharm` (anything works)
   - Visibility: **Public** (required for free Pages)
   - Don't add a README — leave it empty. Click **Create repository**.
3. On the new repo page, click **uploading an existing file**.
4. Drag in the **contents** of the `gulfcoastcharm-site` folder — the files and the
   `css` + `images` folders, NOT the parent folder itself. (`index.html` must sit at
   the top level of the repo.)
5. Click **Commit changes** and wait for the upload (the images take a minute).
6. Go to **Settings → Pages** (left sidebar).
   - Source: **Deploy from a branch**
   - Branch: **main**, folder **/ (root)** → **Save**
7. Wait ~2 minutes, refresh — you'll get a live URL like
   `https://YOURUSERNAME.github.io/gulfcoastcharm/`. **Check the site works there first.**

## Part 2 — Point gulfcoastcharm.com at it

> ⚠️ Do Part 4 (Shopify subdomain move) BEFORE this step, or your store
> will briefly go dark. Order: move Shopify → then repoint the root domain.

1. In the repo: **Settings → Pages → Custom domain** → enter `www.gulfcoastcharm.com` → Save.
   GitHub adds a CNAME file to the repo automatically.
2. At your domain registrar (wherever you manage gulfcoastcharm.com DNS), add:

   | Type | Host/Name | Value |
   | --- | --- | --- |
   | CNAME | `www` | `YOURUSERNAME.github.io` |
   | A | `@` | `185.199.108.153` |
   | A | `@` | `185.199.109.153` |
   | A | `@` | `185.199.110.153` |
   | A | `@` | `185.199.111.153` |

   (Delete any old A/CNAME records on `@` and `www` that pointed to Shopify first.)
3. Back in GitHub Pages settings, tick **Enforce HTTPS** once the domain verifies
   (can take 15 min – 24 hrs).

## Part 3 — Formspree (2 forms)

1. Sign in at formspree.io (same account as before).
2. **New form** → name it `Court Rentals` → copy its endpoint, which looks like
   `https://formspree.io/f/abcd1234`.
3. **New form** again → name it `Celebrations & Contact` → copy that endpoint too.
4. In the site files, replace `YOUR_FORM_ID`:
   - `play.html` → the Court Rentals ID
   - `celebrations.html` → the Celebrations ID
   (Edit right on GitHub: open the file → pencil icon → find `YOUR_FORM_ID` → replace → Commit.)
5. Submit each form once from the live site; Formspree emails you a confirmation
   link the first time — click it and you're live.
6. Free plan = 50 submissions/month per account. Fine to start; upgrade if court
   requests take off.

## Part 4 — Move Shopify to shop.gulfcoastcharm.com (do FIRST)

1. Shopify admin → **Settings → Domains → Connect existing domain** →
   enter `shop.gulfcoastcharm.com`.
2. At your registrar, add: **CNAME | `shop` | `shops.myshopify.com`**
3. Back in Shopify, verify the connection, then click **Change primary domain** →
   set `shop.gulfcoastcharm.com` as primary.
4. Shopify auto-redirects its internal links. Old outside links to
   `gulfcoastcharm.com/products/...` are handled by the site's 404 page, which
   forwards `/products`, `/collections`, `/cart`, `/pages`, `/blogs`, `/checkout`,
   and `/account` URLs to the shop subdomain automatically.

## Part 5 — Redirect gulfcoastcharms.com (the plural)

At the registrar for gulfcoastcharms.com, turn on **domain forwarding**
(sometimes called URL redirect): `gulfcoastcharms.com → https://www.gulfcoastcharm.com`,
type **301 (permanent)**, and include the `www` subdomain in the forward.
No hosting needed — registrar forwarding is free.

## Part 6 — When the booking engine is ready

1. Sign up for the engine (OwnerRez / Lodgify / Hospitable), connect Airbnb + VRBO
   calendars, and set up its hosted booking page.
2. Add DNS: **CNAME | `stay` | (the hostname the engine gives you)**.
3. The site already links to `https://stay.gulfcoastcharm.com` — no site edits needed.
   Optionally swap the button in `stay.html` for the engine's embed widget
   (marked with a comment in the file).

## Checklist (in order)

- [ ] Part 4: Shopify → shop.gulfcoastcharm.com
- [ ] Part 1: Repo + Pages live on github.io URL
- [ ] Part 2: Custom domain + HTTPS
- [ ] Part 5: Plural domain 301
- [ ] Part 3: Formspree IDs in play.html & celebrations.html, test both forms
- [ ] Part 6: Booking engine on stay. subdomain
- [ ] Update Airbnb/VRBO links in stay.html footer notice once relisted
