# Koko Systems website

Static site for Koko Systems, a one-person indie game studio. Live at https://koko.systems via GitHub Pages.
First game: Critter Escape (tap-to-escape animal puzzle, Unity, Android).

## Structure
- `index.html`: home page (hero mini-puzzle, Games, Contact)
- `privacy/index.html`: privacy policy, linked from Google Play Console. Must stay live at `/privacy`.
- `style.css`: the only stylesheet, shared by every page
- `CNAME`: custom domain. Never edit or delete.

## Rules
- KISS. Plain HTML + CSS + vanilla JS. No frameworks, build steps, npm or bundlers.
- Surgical changes only: touch only the files the task needs, and don't reformat or refactor unrelated code.
- Reuse existing classes and tokens in `style.css`. Add new CSS only when nothing existing fits.
- Relative links only (`../style.css`, `privacy/`), so pages work locally and on Pages.
- New page = new folder with `index.html` (e.g. `projects/index.html` → `/projects`). Copy `privacy/index.html` as the template (same header, footer, fonts).
- Add a nav link only when asked.
- Keep it accessible: real buttons and links, visible focus, alt text, respect `prefers-reduced-motion`.

## Design tokens (don't change without asking)
- Colors: burrow `#1E1A2B` (bg), den `#2A2440` (surfaces), chalk `#F2EDE4` (text), mute `#B9B0C9` (secondary text)
- Critter colors: fox `#FF7A3D` (main accent), leaf `#8FD37E`, sky `#7FB0FF`, sun `#FFD25E`
- Fonts: Bricolage Grotesque (headings, 700/800), DM Sans (body, 400/500), via Google Fonts
- Copy: sentence case, plain words, no hype, no ALL-CAPS labels, no arrows in button text

## Privacy policy
- Must match what the shipped game actually does. If an SDK is added (ads, analytics, crash reporting), list it with a link to its privacy policy and update the "Last updated" date.
- Flag it to me if a game change might make the policy inaccurate.

## Email and DNS
- Email: catch-all forwarding at Spaceship; any `@koko.systems` address forwards to my Gmail. Receive-only.
- DNS lives at Spaceship. Never suggest changing the MX records.

## Working with me
- Short, direct answers in bullet points.
- For debugging or ops: one command at a time, then wait for my output.
- Preview locally with `python3 -m http.server` before committing.
- Ask before deleting files or making design changes.
