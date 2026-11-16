# DaeMonScript Gaming — Product Plan

**Status:** Approved direction  
**Product:** All-in-one browser gaming platform  
**Visual direction:** Console dashboard  
**Tagline:** Play Beyond Limits.

## Product vision
Transform DaeMonScript from a developer knowledge/community preview into a browser-first gaming platform where players discover games, launch them, keep a personal library, play with friends, and track achievements.

## Main navigation
- Home: console dashboard, featured games, continue playing, new and popular titles.
- Discover: searchable and filterable catalog across genres.
- Library: saved games and recent play history.
- Multiplayer: room creation, invite codes, lobby, and real-time sessions.
- Rankings: global, per-game, weekly, monthly, and friends leaderboards.
- Profile: player identity, play history, statistics, and achievements.
- Store: curated game listings and later creator submissions.
- Settings: accessibility, privacy, account, and preferences.
- Admin: game catalog, users, reports, rankings review, announcements, and operations.

## Game genres
Arcade, Action, Strategy, Simulation, Puzzle, Racing, Sports, Board, Adventure, and Multiplayer.

## Initial playable titles
1. Snake — single-player arcade with local best score.
2. Tic Tac Toe — local two-player pass-and-play.
3. Additional titles will be added after the shared game shell and catalog conventions are established.

## Core product requirements
- Responsive PC and mobile layouts.
- Console-inspired focus states and keyboard navigation.
- Game details with instructions, controls, supported modes, and credits.
- Personal library and recent-play data.
- Account-backed records when the backend is ready.
- Server-validated scores and achievements.
- Multiplayer rooms using server-authoritative state and WebSocket transport.
- Reporting, blocking, moderation, and privacy controls before public social features.

## Visual system
- Dark navy/charcoal surfaces with restrained violet/blue accents.
- Large featured-game area and horizontal game shelves.
- Consistent cover ratios, metadata, badges, and clear launch actions.
- Desktop sidebar/top navigation; mobile bottom navigation.
- Respect reduced-motion preferences and maintain keyboard/touch accessibility.

## Technical architecture
- GitHub Pages: static frontend and game clients.
- Cloudflare Workers: API, authentication, validation, and moderation endpoints.
- Cloudflare D1: users, catalog, library, scores, achievements, rooms metadata.
- Cloudflare R2: game artwork and approved static game assets.
- Durable Objects + WebSocket: real-time multiplayer room state.
- Secrets remain in Worker secrets; never commit credentials or expose private keys in client code.

This is the target architecture. Backend services are not considered deployed until configured and tested.

## Delivery roadmap
1. Console UI foundation and responsive navigation.
2. Game catalog, game detail pages, and initial playable games.
3. Accounts, library sync, and play history.
4. Multiplayer lobby, invite codes, and real-time sessions.
5. Rankings, achievements, and score validation.
6. Store/creator submissions and administration.
7. Accessibility, security, performance, moderation, and release hardening.

## Release principles
- Do not present mock data or local-only behavior as a live server feature.
- Keep each game independently maintainable.
- Verify every launch route and mobile layout before release.
- Confirm licensing and provenance for third-party games and assets.
- Prefer a small set of complete, playable games over a large catalog of nonfunctional cards.
