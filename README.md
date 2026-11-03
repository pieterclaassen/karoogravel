# Karoo Gravel — static GitHub Pages site

A GitHub Pages-compatible replacement for the current Google Sites website. No build system, Node, server, or database is needed. The website consists of plain HTML, CSS, local SVG illustrations, and links to WhatsApp.

## What is included

- Home, tours listing, four individual tour pages, accommodation, maps, journal, bookings.
- Responsive navigation, search-engine descriptions, contact links, OpenStreetMap location embed.
- A GitHub Actions workflow for Pages hosting.
- A `.nojekyll` marker and local asset URLs compatible with either custom domains or project Pages.

## Deploy acceptance (first)

1. Create a new GitHub repository, e.g. `karoogravel-acceptance`.
2. Upload all files in this directory **including `.github/workflows/pages.yml` and `.nojekyll`** to the `main` branch. Do not upload the parent folder itself.
3. In Settings → Pages → Build and deployment, choose **GitHub Actions**.
4. The action deploys to `https://YOUR-USERNAME.github.io/karoogravel-acceptance/`.
5. Review every page on desktop/mobile, WhatsApp links, map and tour details.

## Deploy production (after acceptance)

1. Create a second repository, e.g. `karoogravel-production`.
2. Promote the tested files to this repository's `main` branch (same files as acceptance).
3. Enable Pages via GitHub Actions. Test its initial GitHub Pages URL.
4. Set the custom domain `www.karoogravel.co.za` in production Settings → Pages. Create `CNAME` at the root containing exactly `www.karoogravel.co.za` **only in the production repo**.
5. Update DNS to GitHub Pages per current GitHub instructions; retain the old Google Sites DNS until you are ready to switch. Configure an apex redirect if needed.
6. Enable **Enforce HTTPS** only after the certificate is issued.

Do **not** set the production custom domain in acceptance. For an optional acceptance subdomain, use `acceptance.karoogravel.co.za` and configure its dedicated DNS CNAME, but a `github.io` address is safer for initial review.

## Recommended promotion using Git

Keep a local working copy, test it in acceptance and push the *same commit* to production:

```bash
git remote add acceptance git@github.com:YOUR-USERNAME/karoogravel-acceptance.git
git remote add production git@github.com:YOUR-USERNAME/karoogravel-production.git
git push acceptance main
# Review the acceptance URL before the next command
git push production main
```

If the repos are configured with separate histories, create both empty and push the same initial commit. Never overwrite a repo with unrelated work.

## Local preview

```bash
python -m http.server 8000
```

Then open http://localhost:8000. For best reliability, preview through a local server instead of double-clicking files.

## Important launch checklist

- **Photography**: the live Google Sites images could not be exported; the site uses original local SVG landscape/house illustrations, not the original photographs. Replace `assets/karoo-landscape.svg` and `assets/karoocible.svg` or update CSS with your owned photos.
- **Maps and video embeds**: original embedded routes and journal video URLs were not available; location map is a substitute, and the journal notes missing links.
- **Schedule/pricing**: schedules, current availability and pricing have not been migrated. Verify all tour dates, inclusions and booking terms.
- **Tour figure discrepancy**: existing Explorer page advertises ~385 km/6190 m, while its listed four stages total 285 km/4395 m; resolve before final publication. Escape totals also differ between tour listing and detail page; detail-page figures used.
- **Booking**: WhatsApp enquiries work without a backend; no online payment or reservations are implemented.
- **Brand review**: illustrative visual redesign based on the content and structure, not a pixel-perfect Google Sites export.
- **SEO**: add a site-specific sitemap and canonical URLs after final host/domain confirmation.

Content was adapted from the public website as viewed in November 2026; confirm your rights to reuse all content and imagery.