# Avilon Drone Dashboards — Unified Hub

One link for **all** Avilon Photon customer drone dashboards, behind a single master password.

🔗 **Live:** https://cart-kart.github.io/Avilon-Drone-Dashboard/
🔑 **Master password:** `avilon1205`

## How it works

- A single `index.html` shell: master-password gate → top tab bar → the selected customer dashboard loads **live** in a full-screen `<iframe>`.
- Each customer dashboard keeps its **own engine** (their column mapping / features are all different), so nothing is duplicated or re-coded here — the hub just frames the live site.
- All customer dashboards are on the **same origin** (`cart-kart.github.io`), so the hub automatically dismisses each dashboard's own PIN — **you never enter a second password.**
- The master gate is remembered for the browser tab (`sessionStorage`). Click **🔒 Lock** to sign out.

> ⚠️ Security note: the master password is client-side obfuscation only (same model as the individual dashboards). This is an **internal control panel**, not a real auth boundary. Don't treat it as protecting sensitive data.

## ➕ Adding a new customer (one line)

Open `index.html`, find the `SITES` list near the top of `<script>`, and add an entry:

```js
const SITES = [
  ...
  { key: 'newco', label: 'New Customer', url: 'https://cart-kart.github.io/NewCustomer-Drone-Dashboard/' },
];
```

- `key` — short unique id (lowercase; becomes the `#hash` in the URL, e.g. `…/#newco`)
- `label` — the text shown on the tab
- `url` — the customer dashboard's published Pages URL (keep the trailing `/`)

That's it — the tab, routing, loading spinner, and PIN auto-unlock are all generated automatically. Commit & push; GitHub Pages redeploys in ~1 minute.

> Auto-unlock requires the dashboard to be on `cart-kart.github.io` (same origin). A dashboard hosted elsewhere will still load, but will show its own login.

## Direct links

You can deep-link straight to a customer with the hash:
`https://cart-kart.github.io/Avilon-Drone-Dashboard/#pcg`

## Repo notes

- `_src/` (git-ignored) holds local reference copies of the customer dashboards — not deployed.
- Pages source: branch `main`, path `/`.
