# DaeMonScript Gaming — Product Plan

**Product:** All-in-one browser gaming storefront and community  
**Visual direction:** PC game storefront inspired by familiar digital game stores (Steam-like information architecture, original DaeMonScript visual identity)  
**Tagline:** Play Beyond Limits.

## Product vision
DaeMonScript Gaming is a browser-first platform where players discover games, inspect useful game details, launch browser games, build a personal library, and later connect with friends and multiplayer sessions.

## Storefront experience
- Store home with featured/recommended area, editorial shelves, recent additions, and genre discovery.
- Browse catalog with search and genre filters.
- Game cards use landscape artwork, title, genre, availability, and clear play/library actions.
- Game detail pages should include description, screenshots/artwork, controls, supported modes, credits/licensing, and status.
- Library shows saved games and recent play history.
- Never label a game as playable unless its launch route works.
- Never imply local browser saves are cloud-synced.

## Main sections
- Store: featured games, discovery shelves, genres.
- Browse: searchable catalog and filters.
- Library: saved titles and play history.
- Community: later profiles, reviews, activity, and friends.
- Multiplayer: later lobbies, invite codes, and real-time sessions.
- Rankings: global and per-game leaderboards after server-side score validation.
- Admin: game catalog, users, reports, rankings review, announcements, and operations.

## Initial playable titles
1. Snake — single-player arcade; local best score.
2. Tic Tac Toe — local two-player pass-and-play.
3. Additional games only after each title is fully playable and tested.

## Visual system
- Dark blue-grey storefront surfaces with cool blue navigation accents.
- Wide featured banner and horizontally organized game shelves.
- Landscape cover artwork; consistent cards and compact metadata.
- Desktop store navigation; mobile bottom navigation.
- Clear visual distinction between playable, in-development, and unavailable titles.
- Responsive layout, keyboard support, readable contrast, reduced-motion support.
- Use an original brand identity; do not copy Steam logos, proprietary artwork, or exact assets.

## Technical architecture
- GitHub Pages: static frontend and game clients.
- Cloudflare Workers: API, authentication, validation, and moderation endpoints.
- Cloudflare D1: users, catalog, library, scores, achievements, room metadata.
- Cloudflare R2: game artwork and approved static game assets.
- Durable Objects + WebSocket: real-time multiplayer room state.
- Secrets remain in Worker secrets; never commit credentials or expose private keys in client code.

This is the target architecture. Backend services are not considered deployed until configured and tested. The current library uses browser localStorage and is not account-synced.

## Delivery roadmap
1. Storefront visual foundation and responsive navigation.
2. Catalog, game detail pages, and initial playable games.
3. Account system, library sync, and play history.
4. Multiplayer lobby, invite codes, and real-time sessions.
5. Rankings, achievements, and score validation.
6. Community features and creator submissions.
7. Accessibility, security, performance, moderation, and release hardening.

## Release principles
- Do not present mock data or local-only behavior as a live server feature.
- Keep each game independently maintainable.
- Verify every launch route and mobile layout before release.
- Confirm licensing and provenance for third-party games and assets.
- Prefer a small set of complete, playable games over a large catalog of nonfunctional cards.
