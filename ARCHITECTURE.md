# DaeMonScript architecture notes

## Planned backend

- The site is currently a static GitHub Pages project.
- Cloudflare Workers are planned for backend functionality.
- Implement login and other server-backed features through a Cloudflare Worker API rather than storing credentials or secrets in browser code or the repository.
- Keep secrets, such as authentication credentials and private API keys, in Cloudflare Worker secrets. Only public client configuration may be exposed to the browser.

This is a planned direction, not an indication that the Worker or authentication flow has already been deployed.
