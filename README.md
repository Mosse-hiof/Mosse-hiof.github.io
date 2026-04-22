# Digitekt Website

Static Netlify site for Digitekt (`digitekt.no`).

## Structure

- `index.html` - home page with hero, service preview, work, testimonials, FAQ, contact form, and sharing.
- `services.html` - dedicated services page.
- `about.html` - dedicated about/history/founder page.
- `news.html` - news/blog hub with curated external reads and room for future Digitekt posts.
- `privacy.html` - privacy policy.
- `404.html` - custom not-found page.
- `assets/css/site.css` - shared custom styling.
- `assets/js/site.js` - shared contact modal, navigation, language switching, reveals, sharing, and EN/NO translations.
- `og-image.html` / `og-image.png` - Open Graph image template and generated social preview image.
- `_headers` - Netlify response headers.
- `netlify.toml` - Netlify publish-root config.
- `robots.txt` / `sitemap.xml` - crawl and sitemap files.
- `image*.jpg`, `lms*.png`, `CV_Mustafa.pdf` - local static assets.

## Deployment Notes

The site is hosted on Netlify with `.` as the publish directory. The shared contact form markup uses Netlify Forms and posts to `/`.

Email shown publicly should use `info@digitekt.no`. Mail forwarding is handled outside the repo.

## Current Site State

The site has been restructured from a compact one-page portfolio into a static multi-page company site. It still has no build step; each `.html` page contains shared header/contact/footer markup manually, while common CSS and JavaScript live in `assets/css/site.css` and `assets/js/site.js`.

Public content is bilingual through the existing `data-i18n` pattern:

- English is the default language.
- Norwegian is auto-detected for `no`, `nb`, and `nn` browser languages.
- Language preference is stored in `localStorage` under `digitekt-lang`.
- New visible strings should be added to both `translations.en` and `translations.no` in `assets/js/site.js`.

Current public pages:

- Home: hero, compact services preview, selected work, testimonials, FAQ, CTA, and sharing.
- Services: dedicated service hub with six service groups, editorial hero image, process section, capacity note, contact CTA, and expanded service SEO.
- About: founder-led Digitekt story, Bergen roots, history, values, founder context, experience, education, and technical background.
- News: curated external reads for AI, web development, and SEO, plus category placeholders for future Digitekt posts.
- Privacy and 404: updated to use the shared navigation, footer, language switcher, and contact modal.

Important conventions for future agents:

- Keep public brand spelling as `Digitekt`; avoid the old one-letter-off spelling from the Swedish notes.
- Keep public email as `info@digitekt.no`; the private forwarding address is intentionally not in public copy.
- Keep the Netlify contact form name `contact`, existing fields, honeypot, hidden `form-name`, and POST target behavior.
- Do not add fake Digitekt news posts. Use curated external reads or real authored content only.
- Remote Unsplash imagery is currently acceptable as placeholder stock imagery and can be replaced later with local/client assets.
- The repeated header/contact/footer markup is intentional for now because there is no static-site generator or build process.

## Change Log

### 2026-04-22 - Services/News Polish and Curated Reads

Goal: improve the new Services and News pages after visual review, add stronger service SEO, and make the News page useful without inventing fake Digitekt articles.

Files changed:

- `services.html`
- `news.html`
- `assets/css/site.css`
- `assets/js/site.js`
- `README.md`

Changes made:

- Replaced the oversized Services and News hero headings with a calmer shared editorial hero layout.
- Added relevant stock imagery to the Services and News hero areas.
- Added shared CSS for editorial page heroes and external article cards.
- Expanded Services SEO with richer title/description metadata, robots hints, Open Graph/Twitter metadata, breadcrumb JSON-LD, provider data, and an `OfferCatalog` for the six service groups.
- Updated News SEO to describe curated reads and future Digitekt notes around AI, web development, SEO, and digital platforms.
- Seeded the News page with three external curated reads:
  - McKinsey: The state of AI in 2025.
  - MDN: Learn web development.
  - Google Search Central: SEO Starter Guide.
- Added EN/NO translations for all new visible strings.
- Kept the curated reads clearly marked as external resources rather than Digitekt-authored posts.

Verification run after this pass:

- `git diff --check`
- `assets/js/site.js` syntax check with Node
- JSON-LD parse check across HTML pages
- EN/NO i18n key coverage check
- Local reference check for internal `href` and `src` values
- Image attribute check for `src`, `alt`, `width`, `height`, and `decoding`
- `rg -n "Digit[e]c|digit[e]x|mosse01[_]" .`

### 2026-04-22 - Services, News, and About Expansion

Goal: turn the compact one-page portfolio into a more complete static Netlify site with real Services, News, and About pages while keeping Digitekt positioned as a founder-led digital partner from Bergen.

Files changed or added:

- `index.html`
- `services.html`
- `about.html`
- `news.html`
- `privacy.html`
- `404.html`
- `assets/css/site.css`
- `assets/js/site.js`
- `sitemap.xml`
- `README.md`

Changes made:

- Replaced the hidden About SPA view with real static `.html` pages.
- Added a dedicated Services page with six service groups: web/system development, e-commerce/platforms, mobile/custom software, AI/automation, design/communication, and operations/infrastructure/support.
- Added a dedicated About page with accurate Digitekt positioning, history, values, founder context, experience, education, and technical background.
- Added a polished News page as an empty hub for future company updates, guides, and case notes.
- Reworked the home page to keep the hero, selected work, testimonials, FAQ, share block, and CTA while replacing the large sticky services area with a compact services preview.
- Extracted shared custom CSS into `assets/css/site.css`.
- Extracted shared JavaScript and translation handling into `assets/js/site.js`.
- Updated navigation across public pages to include Home, Services, News, About, Contact, and language switching.
- Kept the Netlify contact form name, fields, honeypot, and POST behavior.
- Added EN/NO translations for new public content and shared UI strings.
- Added page-specific SEO metadata and simple JSON-LD for Services, About, and News.
- Updated `sitemap.xml` with the new public pages.
- Kept the site static with no build step.

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

The current site intentionally has no build step. Good next moves are:

- Reduce repeated header/contact/footer markup with a future build step or lightweight templating if the site keeps growing.
- Replace remote Unsplash placeholders with local project/client imagery.
- Replace curated external reads with original Digitekt News articles when useful content is ready.
- Consider a small content data layer for services/news if the manual HTML pages become hard to maintain.
