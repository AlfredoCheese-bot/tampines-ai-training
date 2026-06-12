# Tampines AI Exhibition — Promoter Training Site

## What this is
Single-file educational HTML site (`tampines-ai-exhibition-promoter-training.html`) that trains booth promoters for the Metapod booth at the Tampines AI Exhibition. No build step, no dependencies — vanilla HTML/CSS/JS + Google Fonts (Exo 2, Inter, Space Grotesk).

## Event facts (do not change without confirmation)
- Tampines AI Exhibition, Our Tampines Hub, 16–21 June 2026, 12pm–8pm
- Static displays: 16–18 Jun. **Our booth window: Interactive Experience, 19–21 Jun**
- Organised by People's Association / Our Tampines Hub, in partnership with NCS
- Booth: Metapod. Promoter scope: explain AI products, direct purchase via **QR scan → iShopChangi** (GST savings is the key closing angle)
- No payments at the booth, ever

## Products (6) — iShopChangi links + verified SG price refs
1. Steed AI Emotional Companion Robot — price unpublished, "scan QR for price"
   https://www.ishopchangi.com/en/product/steed-ai-emotional-companion-robot-mp00877705
   Brand page: https://steedtech.sg/?product/120
2. PLAUD Note Pro (black magnetic case) — SG RRP S$259
   https://www.ishopchangi.com/en/product/plaud-note-pro-with-black-magnetic-case-mp00794707
   Video: https://youtu.be/KeUKbw2DeRs
3. PLAUD NotePin S — SG RRP ref S$249
   https://www.ishopchangi.com/en/product/plaud-notepin-s-mp00873091
   Video: https://youtu.be/RBREYDEblsg
4. Soundcore Liberty 5 Pro Max — SG launch S$299
   https://www.ishopchangi.com/en/product/soundcore-liberty-5-pro-max---earbuds-with-ai-note-taker-smart-case-mp00891812.html
   Video: https://youtu.be/DfPw-D4WCDQ
5. iFLYTEK AINOTE 2 — price unpublished, "scan QR for price"
   https://www.ishopchangi.com/en/product/iflytek-ainote-2-mp00867833
   Video: https://youtu.be/UCwhHaNuTUo
6. iFLYTEK AINOTE Air 2 — SG retail ref S$549
   https://www.ishopchangi.com/en/product/iflytek-ainote-air-2-mp00866914
   Video: https://youtu.be/covNhxCefto

All prices are RRP references; site instructs promoters to quote the live iShopChangi price (GST savings). iShopChangi pages are JS-rendered — fetching them server-side returns an empty shell, so prices/images cannot be scraped directly.

## Key spec facts already verified (keep accurate)
- Note Pro: 2.99mm, 30g, 4 MEMS + AI beamforming, 5m pickup, 0.95" AMOLED, up to 50hr recording, 112-language transcription, 300 free mins/mo. Officially sold at Changi via Metapod.
- NotePin S: ~17g, 4 wearing accessories included, tactile button + Press to Highlight, 20hr/40-day standby, 64GB.
- Liberty 5 Pro Max: 1.78" AMOLED touchscreen case with built-in AI note-taker (in-person audio ONLY — not calls/online; must disclose honestly), Thus AI chip, Guinness World Record speech quality (Liberty 5 Pro buds, same units), ANC 4.0, 6.5/28hr, 120 free transcription mins/mo for 24 months.
- AINOTE Air 2: 8.2" E-Ink 293 PPI, 4096-level stylus, 17-language voice transcription, 83-language handwriting conversion (cannot run both simultaneously), ~7-day battery, 108-day standby.
- AINOTE 2: newest/thinnest iFLYTEK flagship, LLM-powered; fewer published specs — keep claims general.
- Steed: Steed Innovation, SG company founded 2022, "IoT + AI + People's Care", eldercare ecosystem.

## Design system (inspired by PLAUD-AI-Poster-updated.jpg, redesigned 2026-06-13)
- Palette: near-black bg #04040c/#0a0c1e, electric blue #4d7dff, violet #8b5cf6, cyan #38e1ff, accent gradient cyan→blue→violet, text #f2f5ff, dim #8e96bb, gold #ffd166 (GST/price only), danger #ff6b6b, ok #34d399
- Fonts: Space Grotesk (display + mono/labels), Inter (body). Letterspaced uppercase overlines, gradient-clipped display text
- Look: poster-style dark panels, faint grid backdrop, real lifestyle product photos in img/ (one per product, 4:3 cover panels; steed.jpg was cropped with sips to remove baked-in marketing text), icon sprite (`<symbol>`/`<use>`), scrolling marquee, live D/H/M/S countdown
- Product sections are infographic-style, not text-heavy (redesigned 2026-06-13): big-number stat tiles (.statgrid/.stat), small fact chips, emoji persona chips (.personas), chat-style objection bubbles (.duo/.bub they|you), numbered 60-second demo steps (.demosteps), gold honesty badges (.honesty) for the Liberty in-person-only and AINOTE simultaneity disclosures. Keep new copy in this compressed format — no bullet walls
- Motion (Emil Kowalski design-engineering rules — preserve): custom curves `--ease: cubic-bezier(.23,1,.32,1)` / `--ease-io: cubic-bezier(.77,0,.175,1)`; UI transitions ≤300ms; `scale(.97)` on :active for all pressables; no `transition: all`; hover effects gated behind `@media (hover:hover) and (pointer:fine)`; staggered scroll reveals (50ms steps, IntersectionObserver, once); accordion via `grid-template-rows: 0fr→1fr`
- Accessibility: focus-visible gold outlines, prefers-reduced-motion (keeps fades, drops movement/marquee/flip) — preserve these
- Affordance conventions (preserve): everything clickable carries an explicit cue — gold "TAP TO FLIP ⇄" badge on flip cards, cyan TAP/CLOSE pill on accordions, radio circles on quiz/roleplay options, "↓ TAP TO JUMP" on product index cards, underline-on-hover nav links. Non-clickable chips/personas/badges use near-invisible borders (rgba(125,145,255,.10)) so they don't read as buttons. Flip cards use grid-stacked faces (grid-area:1/1) so the card grows with its content — never absolute-position the faces

## Site structure (8 modules, in-page anchors)
1. #flow — 5-step sales flow + GST-savings close banner
2. #products — quick-jump index grid + 6 full poster-style product sections (all visible, no tabs): lifestyle photo panel, price bar, stat tiles + fact chips, flip card (pitch front / "why it works" back), persona chips, they-say/you-say bubbles, 60-second demo steps, honesty badge where needed, buy+video links
3. #handson — Hands-on lab / device playbook: per-device accordion (controls table, money-demo steps, "confirm on the real unit" checkboxes for anything unit-specific — never state unverified operation details as fact) + gold "demo rescue" card
4. #compare — spec cheat-sheet table
5. #matcher — accordion "customer says → recommend"
6. #roleplay — 3-scenario simulator with graded options (best/meh/bad) + coaching
7. #quiz — 10 questions, instant feedback, score ≥9 = certified, retake button
8. #conduct — Do's/Don'ts + logistics cards
Plus: sticky nav with module progress pill (in-memory only), event countdown to 2026-06-19T12:00+08:00.

## Constraints
- Keep it a single self-contained HTML file unless asked otherwise (exception: product photos live in img/, referenced relatively)
- No localStorage/sessionStorage if it will ever be loaded in claude.ai artifacts; current progress tracking is in-memory by design
- Never invent prices, discounts, or specs; unverified = "scan QR for price"
- Local preview: `.claude/launch.json` runs `npx http-server -p 8765` (server takes a few seconds on first npx fetch)
- Maintain honest-disclosure copy (Liberty case limitation, AINOTE simultaneity limit)

## Backlog / next steps
- [x] Real product photos added (2026-06-13) in img/ — replaced the SVG renders
- [ ] Confirm SGD prices for Steed robot and AINOTE 2; update price boxes
- [ ] Embed the actual booth QR code image in the hero/close sections (need asset)
- [x] Deployed to GitHub Pages (2026-06-13): https://alfredocheese-bot.github.io/tampines-ai-training/ — repo github.com/AlfredoCheese-bot/tampines-ai-training (account AlfredoCheese-bot, gh CLI authed). To update: commit + `git push` (Pages rebuilds in ~1 min). Root index.html is a meta-refresh redirect to the training HTML. Poster jpg + .claude/ are gitignored.
- [ ] Optional: print-friendly one-page cheat sheet (@media print stylesheet)
- [ ] Optional: track quiz completion per promoter (would need a backend or form)
