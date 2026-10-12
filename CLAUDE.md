# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static marketing site for Max3D, a 3D printing and design business in the Greater Moncton / Dieppe area (owners: Maxime Boudreau and Seena Ajorloo). It's served by GitHub Pages from the `main` branch at the custom domain `max3d.ca` (set in `CNAME`). Pushing to `main` deploys.

There's no build step, package manager, linter, or test suite. Everything is hand-written HTML/CSS/JS plus vendored libraries. To preview locally, serve the repo root:

```
python3 -m http.server 8000
```

## Hosting and DNS

DNS is on Cloudflare (proxied). `max3d.ca` has the four GitHub Pages A records (185.199.108–111.153) and `www` is a CNAME to `mxboud.github.io`; GitHub redirects `www` to the apex, so `https://max3d.ca` is the canonical URL. Cloudflare SSL mode must stay on Full, not Full (Strict): GitHub serves its `*.github.io` certificate rather than one for `max3d.ca`, so Strict would break the site. Always Use HTTPS is on. `n8n.max3d.ca` is an unrelated Cloudflare Tunnel.

## Structure

`index.html` is the whole live site: one page with anchor sections (`#welcome-hero`, `#services`, `#about`, `#contact`) and a nav that smooth-scrolls between them. The SEO block in `<head>` (description, keywords, Open Graph, Twitter card, canonical URL) is maintained by hand, so keep it in sync when business details like the service area change.

The design is adapted from the ThemeSine "Khanas" HTML template (Bootstrap 3 + jQuery). Site-specific styling lives in `assets/css/style.css` and `assets/css/responsive.css`; the rest of `assets/css` and `assets/js` are vendored libraries and shouldn't be edited. `assets/js/custom.js` wires up the template behaviour (sticky header, scrollspy, smooth scroll, scroll-to-top, owl carousel, progress bars).

Images are in two places: logos/favicon under `assets/logo/` (what `index.html` actually references) with partial duplicates in `assets/images/logo/`, and section photos and owner headshots under `assets/images/about/`.

## Known gaps

- `portfolio/index.html` is an unfinished draft. It isn't linked from the main page, and its `assets/...` paths resolve relative to `portfolio/`, so its CSS/JS don't load as written (they'd need `../assets/...`).
- The `og:image` / `twitter:image` tags point to `assets/images/thumbnail.jpg`, which doesn't exist in the repo.
