# docs/

This is a static mirror of the **Training Control Center** dashboard, served via GitHub Pages at `training.techtheworld.win`.

The dashboard's source of truth is the published Claude Artifact — this folder is a snapshot, not the live copy. When the artifact gets updated (new hours logged, cert progress, skill scores, etc.), `index.html` here needs to be re-exported and re-pushed to match; it does not update automatically.

- `index.html` — the dashboard page (self-contained, no build step)
- `bg-room.jpg` — background texture the page references
- `CNAME` — tells GitHub Pages which custom domain to serve this under

## One-time setup (do once)

1. **Enable Pages:** repo Settings → Pages → Source: "Deploy from a branch" → Branch: `main`, folder: `/docs`.
2. **Point DNS at it:** in Cloudflare (or wherever `techtheworld.win` is managed), add a `CNAME` record — name `training`, target `quanwatson.github.io` — for the domain named in the `CNAME` file above. Use "DNS only" (grey cloud) rather than proxied while GitHub issues the TLS certificate; you can switch back to proxied after it's live if you want.
3. Back in repo Settings → Pages, confirm the custom domain shows as verified and enable "Enforce HTTPS" once it's available.
