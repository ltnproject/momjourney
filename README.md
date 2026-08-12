# Mom's Little Journey 🌷

A static, no-backend Mother's Day QR scavenger hunt. Ten steps, one JS file, no login, no database.

## Files

- `index.html` — the entire site (styles, routing, and all content). This is the only file you need to edit.
- `404.html` — a small fallback so links like `/mom/5` still work on hosts with zero routing config (e.g. GitHub Pages). Not needed on Netlify/Vercel if you use the config files below, but safe to leave in either way.
- `_redirects` — for **Netlify**. Makes `/mom/N` route cleanly without the 404 bounce.
- `vercel.json` — for **Vercel**. Same purpose, Vercel's format.

## How it works

- Each QR code you create should point to `https://yourdomain.com/mom/1`, `/mom/2`, … `/mom/10`.
- There's no server and no database — `index.html` reads the number at the end of the URL and shows the matching step. Nothing is stored, nothing is tracked.
- Step 10 is the final page and does **not** point to another QR.

## Editing content

Everything you'll want to change lives in one place near the top of the `<script>` tag in `index.html`, inside the `JOURNEY` object:

```js
const JOURNEY = {
  momName: "Mom",        // 1. Mom's name
  yourName: "Jacob",     // 2. Your name (signs the final message)
  home: { ... },         // homepage copy
  finalSurpriseUrl: "#", // 5. Point this at a gallery/video link when ready, or leave as "#"
  steps: [
    { id: 1, title: "...", message: "...", location: "The Mirror" },
    // 3 & 4. messages + locations for each step — edit freely
    ...
  ]
};
```

To add or remove steps, add/remove objects in `steps` — the progress indicator (`n / total`) and the growing garland graphic update automatically. Just make sure the last step keeps `isFinal: true` and `location: null`.

## Deploying (pick one)

**Netlify (recommended, easiest):**
1. Drag the whole folder onto [app.netlify.com/drop](https://app.netlify.com/drop).
2. Done — `_redirects` is already set up. Your QR codes can point to `https://your-site.netlify.app/mom/1`, etc.

**Vercel:**
1. `vercel deploy` from this folder, or import the folder in the Vercel dashboard.
2. `vercel.json` handles the routing automatically.

**GitHub Pages / any plain static host:**
1. Upload all files (including `404.html`) as-is.
2. Direct links to `/mom/N` will briefly redirect through `404.html` before landing on the right step — this is invisible in practice (well under a second) and needs no configuration.

## Before you print the QR codes

Open `https://yourdomain.com/mom/1` through `/mom/10` once each in your own browser to confirm every step shows the right message before you generate the QR codes for print.

Happy Mother's Day. 🌷
