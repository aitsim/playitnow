# PlayItNow — multi-game starter site

A static site for testing multiple original games at once, deployed on
Cloudflare Pages. Once one game is clearly winning on traffic/engagement,
see "Going single-game" below to trim it down to just that one.

## What's in here

```
index.html                    Homepage — grid of game cards
games/
  game-template.html          Blank template for adding a new game
  neon-slither.html           Neon Slither — Slither.io-style snake game
  neon-blob.html               Neon Blob — Agar.io-style eat & grow game
  neon-onslaught.html          Neon Onslaught — Vampire Survivors-style bullet heaven
  embed/
    slither-clone.html        Neon Slither's actual game code (self-contained)
    blob-eat.html               Neon Blob's actual game code (self-contained)
    bullet-heaven.html          Neon Onslaught's actual game code (self-contained)
contact.html                  Contact page — mailto + Formspree form
privacy.html                  Privacy policy
terms.html                     Terms of use
ads.txt                        Google AdSense verification line
robots.txt                     Crawler rules, points at sitemap.xml
sitemap.xml                    URL list for search engines
assets/                        Logos, icons, and game screenshots
css/style.css                  All styling (arcade marquee theme)
js/main.js                     Auto-fills footer year
```

## The three games (all built in, all real)

Each game is a self-contained, dependency-free HTML/CSS/JS file in
`games/embed/`, embedded via iframe in its own page under `games/`. No
external libraries or CDN calls — they work standalone once deployed.
Open any of them directly in a browser to test locally before pushing.

- **Neon Slither** (`games/neon-slither.html`) — mouse/touch to steer, eat
  orbs to grow, avoid trails, dodge AI rivals.
- **Neon Blob** (`games/neon-blob.html`) — mouse/touch to move, absorb
  smaller blobs and pellets to grow, avoid bigger ones.
- **Neon Onslaught** (`games/neon-onslaught.html`) — mouse/touch to dodge,
  auto-fires at enemies, level up and pick upgrades to survive longer.

## Adding a new game

1. Copy `games/game-template.html` to `games/your-game-slug.html` — use a
   descriptive slug (e.g. `neon-something.html`), not `game-4.html`.
2. Build the game itself as a self-contained file in `games/embed/`, then
   point the new page's iframe `src` at it.
3. Update the new page's `<title>`, meta description, `[Game Name]` text,
   and "how to play" copy.
4. Add a matching logo/icon pair in `assets/` (see the existing
   `neon-*-icon.svg` / `neon-*-logo.svg` files for the visual pattern).
5. Add a `<a class="game-card">` block in `index.html`'s game grid pointing
   at the new page.
6. Add the new page's URL to `sitemap.xml`.

To remove a game: delete its card from `index.html`, its file in `games/`,
its embed file in `games/embed/`, and its entry in `sitemap.xml`.

## Push to GitHub

```bash
cd game-site
git init
git add .
git commit -m "Initial multi-game site"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

## Deploy on Cloudflare Pages

1. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
2. Select your repo
3. Framework preset: **None**, build command: blank, output directory: `/`
4. **Save and Deploy** — live at `your-site.pages.dev` in a minute or two

Every `git push` to `main` auto-deploys after this.

## Point playitnow.io at it

In the Pages project → **Custom domains** → add `playitnow.io`. If the
domain's DNS is already on Cloudflare, this is a one-click connect.

## After going live

- Submit the site to [Google Search Console](https://search.google.com/search-console)
  and verify with the `sitemap.xml` already in place.
- Double-check `ads.txt` is reachable at `https://playitnow.io/ads.txt`.
- AdSense is already wired into every page, one ad unit per game plus one
  for the homepage — confirm real ads start filling once the domain is
  approved.

## Going single-game (later, on a new domain)

Once one game is clearly winning on traffic/engagement:

1. Pick that game's file in `games/your-winner.html`
2. Either rename it to `index.html` at the root (updating the CSS/JS
   paths inside from `../css/` to `css/`, and nav links from `../index.html`
   to `index.html`), or just keep the `games/` structure and redirect
   the homepage to it — whichever is less work at the time
3. Delete the other game pages, their embed files, and their cards
4. Buy the dedicated domain, connect it in Cloudflare Pages the same way
   as above, on a **new** Pages project (or repoint this one — your call,
   since you already have traffic data on `playitnow.io` worth preserving
   separately if you want to keep testing new games there)
# playitnow
# playitnow
