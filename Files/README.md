# GAMBULL

A psychological game about staking your **pride** — not money — in social situations, climbing from Unknown to The Top, and knowing when to walk away before your ego crosses a hidden breaking point.

Static site. No build step, no dependencies, no backend. Two files:

```
index.html    the whole game (HTML + CSS + JS + SVG artwork, ~170 KB)
vercel.json   cache and security headers (optional)
```

The only network request is Google Fonts. If that is blocked, the game falls back to system fonts and still works.

---

## Deploy to Vercel

### Option 1 — drag and drop (fastest)

1. Go to <https://vercel.com/new>
2. Drop this folder onto the page
3. Framework preset: **Other**. Leave build command and output directory empty.
4. Deploy. You get a `*.vercel.app` URL in about twenty seconds.

### Option 2 — Vercel CLI

```bash
npm i -g vercel
cd gambull-vercel
vercel          # preview deployment
vercel --prod   # production
```

When asked, choose **Other** as the framework and skip the build settings.

### Option 3 — GitHub

```bash
cd gambull-vercel
git init
git add .
git commit -m "GAMBULL"
git branch -M main
git remote add origin git@github.com:<you>/gambull.git
git push -u origin main
```

Then import the repository at <https://vercel.com/new>. Every push to `main` redeploys.

---

## Running it locally

Open `index.html` in a browser, or serve it:

```bash
npx serve .
# or
python3 -m http.server 8000
```

---

## How the game works

- **Pride** is standing — confidence, reputation, face. You start each run with 1,000.
- A run is **15 situations across 3 rounds**: The room → The circle → The spotlight. Payoffs rise each round, and the ego traps only appear in round 3.
- Every situation shows a **Signal** that points at its hidden edge (+8%, 0, −8%) and is right about 70% of the time.
- Pick a move — **Safer / Balanced / All in** — then choose how much pride to stake. You can also **pass**.
- Winning buys **social height** (Unknown → Noticed → Recognized → Prominent → Influential → The top). Height raises **exposure**, which widens the luck swing.
- You may stake anything from 10 pride up to **everything in your wallet**.
- Cross the hidden **breaking point** and you fall: pride goes to **zero**, and you are grounded.
- **Three Humble Stones** per run reset your ego: less height, lower exposure, restored composure.
- The skill is leaving while you are still on top.

Outcomes are decided by a published formula — base chance, your skill influence, a seeded luck draw and the situation's hidden edge. Nothing adapts to whether you are winning or losing.

## Saved data

Progress (records, play patterns, the situations you have already seen, the run in progress) lives in the visitor's `localStorage` under the `gambull3.*` and `gambull4.*` keys. Nothing is sent anywhere. Clearing site data resets everything.

Situations you have seen are remembered **across runs**, so a restart deals situations you have not played yet until a round's deck is used up.

## Making changes

Everything is in `index.html`:

- `CONFIG` — every tunable number (starting pride, stake limits, odds curve, skill values, luck range, rounds, the ego reset)
- `SITUATIONS` / `REFLECTIONS` — the content. Add one and it joins the draw; set its round in `ROUND_OF` and its artwork in `SCENE_OF`.
- `SCENE_LIB` — the inline SVG scenes
- `Backend = LocalAdapter` — the single swap point if you ever put this behind an API or Supabase. The `SERVER NOTES` comment lists what a real backend must validate.

Press the **backtick** key in the game for the developer panel: set the seed, pride, standing, composure and breaking point, force wins and losses, and trigger the fall.

## Licence and content

Pride is a fictional measure of standing. There is no real money, no deposits, no purchases and no cash value anywhere in this game.
