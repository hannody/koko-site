# Koko Systems site: project notes for future agent sessions

Read CLAUDE.md first (the owner's rules and design tokens). This file records what exists, why, and how it works. It holds no secrets.

## What this is
- Static site for Koko Systems, a one-person indie game studio. First game: Critter Escape.
- Live at https://koko.systems (HTTPS). Repo: github.com/hannody/koko-site, public, `main` branch, GitHub Pages served from the repo root.
- Stack: plain HTML, CSS and vanilla JS only. No frameworks, no build step.

## Hard rules (from CLAUDE.md, summarized)
- Surgical changes only; reuse the tokens in `style.css`.
- Never edit or delete `CNAME` (contains `koko.systems`).
- Never suggest changing the domain's MX records (email forwarding depends on them).
- Ask before deleting files or making design changes.
- Short bullet answers; for ops/debugging give one command at a time and wait for output.
- The privacy policy (`privacy/`) must match the shipped game; flag any change that could make it inaccurate.
- Owner preference: no em dashes in written output.

## Files
- `index.html`: header, hero with a small playable board, Games section (lineup of 4 mini critters), contact section, footer. Two inline scripts.
- `style.css`: all styling and animations. Tokens: burrow, den, chalk, mute, fox, leaf, sky, sun, --line.
- `privacy/`: privacy policy page.
- `CNAME`, `CLAUDE.md`: see above.

## Hosting and DNS
- DNS at Spaceship: 4 A and 4 AAAA records for the apex pointing at GitHub Pages, `www` CNAME to `hannody.github.io`. MX records untouched (Spaceship email forwarding, catch-all).
- GitHub issues the TLS certificate (Let's Encrypt). A stuck certificate was fixed once by clearing and re-adding the custom domain through the Pages API, then waiting.
- GitHub Pages allows one custom domain per repo. Subdomains for other projects (for example a game build) would be a CNAME to `hannody.github.io` only if served from another repo, or elsewhere (see below).
- Future web builds of games: undecided. Notes: GitHub Pages cannot set custom headers (Unity compressed builds need Decompression Fallback), 1 GB site and 100 MB per-file limits. Candidates: Cloudflare Pages (`_headers` support, 25 MiB per file, commercial use ok), itch.io, Netlify. Avoid Vercel Hobby (non-commercial). Pointing `game01.koko.systems` via CNAME works with any of them.

## Interactive hero (what was built and why)
Goal: make the landing page feel alive and on-brand while staying dependency-free.
- Board: tap critters to send them off; "Play again" brings them back (`setup(true)` animates return).
- "Play with a critter" button: one critter becomes player-controlled (arrow keys/WASD on desktop, analog stick on touch). Features: trail, hearts and wink when it touches the header logo critter, nearby critters watch and get nudged away, bumping critters triggers a "!" fuss then reset.
- Ambient effects (run only when motion is allowed): small flyers on curved paths, a ship crossing slowly, glowing glints on empty cells, trails behind moving critters.
- Touch: analog stick (pointer events with capture), player size fitted to the board, movement slowed on small screens.
- Reduced motion: `prefers-reduced-motion: reduce` disables the ambient animations; touch UI is gated by `(hover: none) and (pointer: coarse)`.
- Techniques: separate CSS `translate`/`scale`/`rotate` properties, Web Animations API for flyers and ship, requestAnimationFrame for trails. The two inline scripts share global scope (`setup`, `board`, `calm`, `occupied`, `remaining`).
- Gotchas learned: `.mini` needs `flex: none` or it squashes into a rectangle; a "Stop playing" floating button was tried and reverted (owner did not want it, badly placed). On touch the only way to stop is the hero button.

## Open decisions
- Email spam: the hero has an "Email us" mailto link. Owner considered removing it, click-to-reveal, or changing the catch-all. CAPTCHA (Turnstile) is not viable on a static site without a server. No choice made yet.
- Web build hosting: see above.

## Workflow notes
- Owner runs `git push` from their own machine. Agent commits locally; check `git status` and `git log` before assuming something is pushed.
- Agent shell may leave `.git/*.lock` or `tmp_obj_*` files; clean with `find .git \( -name '*.lock' -o -name 'tmp_obj_*' \) -print -delete` (needs delete permission).

## Run locally
- `cd ~/dev/home/koko-site && python3 -m http.server` then open http://localhost:8000
