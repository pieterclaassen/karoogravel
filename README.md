# Karoo Gravel — static GitHub Pages site

A GitHub Pages-compatible replacement for the current Google Sites website. No build system, Node, server, or database is needed. The website consists of plain HTML, CSS, photographs, and links to WhatsApp.

## What is included

- Home, tours listing, four individual tour pages, accommodation, maps, journal, gallery, bookings.
- Responsive navigation, search-engine descriptions, contact links, OpenStreetMap location embed.
- A GitHub Actions workflow for Pages hosting.
- A `.nojekyll` marker and local asset URLs compatible with either custom domains or project Pages.

## Publish for review

The Pages site is [https://pieterclaassen.github.io/karoogravel/](https://pieterclaassen.github.io/karoogravel/). It deploys from `main` on [github.com/pieterclaassen/karoogravel](https://github.com/pieterclaassen/karoogravel) via `.github/workflows/pages.yml`.

This photo project is not that repository. Copy these files onto a clone of it and keep that repository's git history:

```bash
set -euo pipefail
rm -rf karoogravel
git clone https://github.com/pieterclaassen/karoogravel.git karoogravel
find karoogravel -mindepth 1 -maxdepth 1 ! -name .git -exec rm -rf {} +
tar --exclude .git --exclude agent-tools --exclude karoogravel -cf - . | tar -C karoogravel -xf -
git -C karoogravel add -A
git -C karoogravel commit -m "Add photographs from karoogravel.co.za"
git -C karoogravel push origin main
```

Review [https://pieterclaassen.github.io/karoogravel/](https://pieterclaassen.github.io/karoogravel/) after the Pages action finishes. Check desktop and mobile, the photographs, WhatsApp links, the map, and the tour details.

## Custom domain (only when leaving Google Sites)

`https://www.karoogravel.co.za` still serves the Google Site. Point it at GitHub Pages only after the `github.io` review looks right.

1. In the karoogravel repository, Settings → Pages → Custom domain, set `www.karoogravel.co.za`.
2. Add a `CNAME` file at the repository root containing exactly `www.karoogravel.co.za`.
3. Update DNS to GitHub Pages per current GitHub instructions. Keep the Google Sites DNS until the switch.
4. Enable **Enforce HTTPS** only after the certificate is issued.

## Local preview

```bash
python -m http.server 8000
```

Then open http://localhost:8000. For best reliability, preview through a local server instead of double-clicking files.

## Important launch checklist

- **Photography**: photographs are copied from the published Google Site into `assets/photos`. The site does not hotlink `lh7-us.googleusercontent.com` URLs, because those signatures rotate. CSS backgrounds, including a page's `--hero`, are resolved from `assets/style.css`, so every hero uses `url('./photos/...')`. Image `src` attributes stay relative to the HTML file. Re-copy after new photos are published on karoogravel.co.za.
- **Maps and video**: the interactive map is the Google My Map embedded on the current site. Journal cards link to the Gravel Union article and the four YouTube films.
- **Schedule/pricing**: schedules, current availability and pricing have not been migrated. Verify all tour dates, inclusions and booking terms.
- **Tour figure discrepancy**: existing Explorer page advertises ~385 km/6190 m, while its listed four stages total 285 km/4395 m; resolve before final publication. Escape totals also differ between tour listing and detail page; detail-page figures used.
- **Booking**: WhatsApp enquiries work without a backend; no online payment or reservations are implemented.
- **Brand review**: illustrative visual redesign based on the content and structure, not a pixel-perfect Google Sites export.
- **SEO**: add a site-specific sitemap and canonical URLs after final host/domain confirmation.

Content was adapted from the public website as viewed in November 2026; confirm your rights to reuse all content and imagery.