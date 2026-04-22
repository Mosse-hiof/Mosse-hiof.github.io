# Digitekt Site Improvement Ideas

This document captures recommended next improvements for `digitekt.no` after the Services, News, and About expansion. The site is already usable and production-ready; these ideas are mainly about improving search visibility, trust, performance, and conversion.

## Highest-Value Next Moves

1. Add Norwegian SEO pages

The current site uses client-side `data-i18n` translations. That works for visitors, but search engines primarily see the default English HTML. If Norway is the main market, consider adding real Norwegian static pages or language-specific URLs later, for example:

- `no/index.html`
- `no/tjenester.html`
- `no/om-oss.html`
- `no/nyheter.html`

Add `hreflang` links between English and Norwegian versions if this route is chosen.

2. Add real case study pages

Case studies will likely improve trust more than adding more generic service copy. Suggested first pages:

- `case-jetski-lms.html`
- `case-mgb-truck-lms.html`

Recommended structure:

- Client/project context
- Problem
- Solution
- Screenshots
- Stack
- Result
- Testimonial
- CTA to contact

3. Replace remote stock images with optimized local assets

Current Unsplash images are acceptable placeholders. Later, replace them with local WebP/AVIF assets and responsive `srcset` variants. Keep real project screenshots where possible, especially on case study pages.

Useful reference: https://web.dev/learn/design/responsive-images/

4. Set up Search Console after deploy

After production deploy, submit `sitemap.xml`, inspect the new pages, and monitor indexing/search queries.

Useful reference: https://developers.google.com/search/docs/fundamentals/seo-starter-guide

5. Run Lighthouse/PageSpeed after deploy

Check mobile performance in particular. Watch Core Web Vitals:

- LCP: main content/image loading speed
- INP: interaction responsiveness
- CLS: layout stability

Useful reference: https://web.dev/articles/vitals

## Content Improvements

1. Add original Digitekt news posts

The News page currently uses curated external reads and clearly marks them as external. Replace or supplement them with original posts when useful content is ready.

Suggested first articles:

- "Hva bor en liten bedrift ha pa nettsiden sin i 2026?"
- "Nar holder WordPress, og nar trenger du et skreddersydd system?"
- "Praktisk AI for sma bedrifter uten hype"
- "Hvordan velge mellom en enkel nettside og en digital plattform"

2. Add a "typical project fit" section

This could live on the Home or Services page and help visitors self-identify quickly.

Suggested items:

- New company website
- Existing site cleanup
- LMS/course platform
- AI/workflow automation
- E-commerce/platform work
- Ongoing support

3. Add more proof

Useful proof can include:

- Short client quotes
- Before/after notes
- Screenshots of delivered systems
- Concrete outcomes, such as faster workflow, fewer manual steps, or smoother launch

## SEO Improvements

1. Add FAQ structured data on the home page

The FAQ already exists visibly on the page. Adding matching `FAQPage` JSON-LD would help search engines understand it. Keep the structured data in sync with visible FAQ text.

2. Add stronger image SEO

When stock images are replaced:

- Use descriptive filenames.
- Keep useful `alt` text.
- Avoid huge source images.
- Prefer local optimized formats.

3. Add dedicated metadata for future case studies

Each case page should have:

- Unique title
- Unique description
- Canonical URL
- Open Graph title/description/image
- Simple JSON-LD where appropriate

## Technical Improvements

1. Consider a lightweight build step later

The site intentionally has no build step right now. If the site grows, repeated header/contact/footer markup will become harder to maintain. A future static-site generator or light templating layer could reduce duplication.

Do not add this until the manual static setup becomes painful.

2. Keep the contact form stable

The contact form is tied to Netlify Forms. Future edits should preserve:

- `name="contact"`
- `data-netlify="true"`
- `netlify-honeypot="bot-field"`
- hidden `form-name`
- current fields: name, email, message
- POST behavior

3. Keep accessibility checks part of review

Before pushing larger changes:

- Check keyboard navigation.
- Check mobile menu behavior.
- Check contact modal focus trapping.
- Check reduced motion behavior.
- Check that text does not overflow on mobile.

## Good Future Validation Commands

Run these before pushing meaningful changes:

```powershell
git diff --check
node -e "const fs=require('fs'); new Function(fs.readFileSync('assets/js/site.js','utf8')); console.log('site.js syntax OK')"
rg -n "Digit[e]c|digit[e]x|mosse01[_]" .
```

Also re-run the JSON-LD, i18n coverage, local reference, and image attribute checks used in the README when SEO/translation/image markup changes.
