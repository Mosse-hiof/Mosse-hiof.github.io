# Digitekt Website

Static Netlify site for Digitekt (`digitekt.no`).

## Structure

- `index.html` - main one-page portfolio experience, including inline CSS, JavaScript, contact form, and EN/NO translations.
- `privacy.html` - privacy policy.
- `404.html` - custom not-found page.
- `og-image.html` / `og-image.png` - Open Graph image template and generated social preview image.
- `_headers` - Netlify response headers.
- `netlify.toml` - Netlify publish-root config.
- `robots.txt` / `sitemap.xml` - crawl and sitemap files.
- `image*.jpg`, `lms*.png`, `CV_Mustafa.pdf` - local static assets.

## Deployment Notes

The site is hosted on Netlify with `.` as the publish directory. The contact form in `index.html` uses Netlify Forms and posts to `/`.

Email shown publicly should use `info@digitekt.no`. Mail forwarding is handled outside the repo.

## Change Log

### 2026-04-22 - Foundation Pass

Goal: prepare the existing static Netlify site for larger upcoming improvements without changing the visual direction or pushing anything.

Files changed:

- `index.html`
- `privacy.html`
- `README.md`
- `netlify.toml`

Changes made:

- Added `netlify.toml` with `publish = "."` so Netlify has an explicit publish root before future restructuring.
- Improved the contact modal accessibility:
  - Added `role="dialog"`, `aria-modal="true"`, `aria-labelledby`, `aria-hidden`, and `inert`.
  - Added an `id` to the modal heading and connected it to the dialog.
  - Added an accessible label to the close button.
  - Added `for`/`id` associations for name, email, and message fields.
  - Added focus management: opening the modal moves focus inside it, Tab is trapped while open, Escape closes it, and focus returns to the opener when safe.
- Improved the mobile menu accessibility:
  - Added `aria-controls`, `aria-expanded`, `aria-hidden`, and `inert`.
  - Updated the menu button label between "Open menu" and "Close menu".
  - Changed mobile Contact behavior to close the menu before opening the contact modal.
- Centralized body scroll locking:
  - Replaced direct `document.body.style.overflow` toggles with a small lock set.
  - Fixes the bug where opening Contact from the mobile menu could unlock page scrolling while the modal was still open.
- Added `visibility` transitions to the modal and mobile menu so hidden overlays are not interactable while closed.
- Added `prefers-reduced-motion` CSS support and disabled the rotating hero word interval for reduced-motion users.
- Added image `width`, `height`, `loading="lazy"`, and `decoding="async"` attributes to current content images.
- Changed SPA view scrolling from `behavior: "instant"` to `behavior: "auto"` for browser compatibility.
- Changed the contact form submit loading text to plain ASCII (`Sending...` / `Sender...`).
- Changed the form failure alert to plain ASCII and kept the fallback email as `info@digitekt.no`.
- Fixed the Norwegian hero string by removing the stray combining accent from the O-slash character (`GJ\u00D8\u0301R DIN` -> `GJ\u00D8R DIN`).
- Updated `privacy.html`:
  - Public contact email is now `info@digitekt.no`.
  - Hosting provider text now says Netlify instead of GitHub Pages / future providers.
- Added this README context for future work and for other coding agents.

Verification already run:

- `git diff --check`
- Inline JavaScript syntax check with Node
- JSON-LD parse check
- EN/NO i18n key coverage check
- Image attribute coverage check
- Grep check for old private email, odd Norwegian accent string, `behavior: 'instant'`, and old non-ASCII submit/alert strings

Known notes:

- `lms2.png` and `lms3.png` are currently unused but intentionally kept. They may be useful when replacing Unsplash placeholder imagery with real project screenshots.
- `CV_Mustafa.pdf` is not linked from the site, but is documented as an available static asset.
- Git may warn that LF will be replaced by CRLF on Windows; this was present during checks and did not indicate a functional issue.

## Restructuring Notes

The current site intentionally has no build step. Before larger visual/content changes, good next moves are:

- Extract CSS and JavaScript from `index.html` into `assets/css/` and `assets/js/`.
- Move repeated content and translation strings into a separate data file.
- Replace remote Unsplash placeholders with local project/client imagery.
- Decide whether About should become a real route/page for SEO.
