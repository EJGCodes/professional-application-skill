# Web Developer Checklist

Read this before building any [Web] project. It holds the implementation details for the web rules in SKILL.md. The final section lists tasks only the human builder can do; copy every applicable one into the delivery summary under "Builder launch tasks."

## Links
- External links always open in a new tab.
- Internal links open in the same tab, except links inside a task (form, checkout, sign-up, settings) that lead to a non-function page (FAQ, help center, legal pages), which open in a new tab so the user keeps their progress.
- Links to non-function pages from the nav, footer, home page or any other non-task page open in the same tab.
- Every new-tab link has `rel="noopener noreferrer"` and a visible icon with accessible text (such as "opens in a new tab"). Hide the icon in print.
- Link text makes sense out of context (no "here" or "read more").
- Before delivery, crawl every internal and external link with a link checker (lychee or linkinator). Expect zero broken links and zero redirect chains.

## Subdomains
Use subdomains to separate apps and audiences:
- `app.` for the logged-in product, `api.` for the API, `admin.` for admin tools, `status.` for a status page, and `mail.` (or similar) for sending email.

Content placement:
- **Blog:** its own subdomain (`blog.`) once it has enough content to warrant multiple pages. On portfolio and personal sites, the blog is always a folder (`/blog`).
- **Help center:** its own subdomain (`help.`) once it has enough content to warrant multiple pages.
- **Docs:** always a folder (`/docs`).
- Smaller blogs and help sections stay as folders until they grow.

Rules:
- Scope cookies to the exact subdomain that needs them. The cookie consent choice is the exception: store it on the parent domain.
- When the app lives on `app.`, the marketing site's logo always goes home, and its nav shows a "Sign in" link that sends signed-in users straight to their dashboard.
- Each subdomain follows every rule in this skill (headers, robots.txt, error pages).
- Claude cannot create DNS records. Configure the code, and list the DNS steps under Builder launch tasks.

## URLs and Page Organization
- URLs are lowercase, use hyphens, describe the page and stay shallow (`/guides/pricing`, not `/p?id=82`).
- Never use a trailing slash. 301-redirect any trailing slash URL (`/about/`) to its clean version (`/about`). The home page (`/`) is the only exception.
- Pages never show file extensions (`.html`, `.php`, `.aspx`). Configure the host or framework to serve clean paths, and 301-redirect extension URLs to clean ones.
- Standard machine-readable files and downloads keep their extensions: robots.txt, sitemap.xml, humans.txt, security.txt, site.webmanifest, favicon.ico, RSS feeds and downloadable files such as PDF invoices.
- Choose www or non-www and 301-redirect the other version.
- Every page has a canonical tag pointing to its own clean URL.
- Moved pages 301-redirect straight to the new address, with no chains.
- Every page is linked from at least one other page.
- Breadcrumbs on pages more than two levels deep, with BreadcrumbList structured data.
- Titles about 60 characters or fewer; meta descriptions about 155 characters or fewer; both unique per page.

## Crawlability
- Public pages are server-rendered or statically generated.
- Navigation uses real `<a href>` links, never click handlers.
- Important content is in the HTML on page load, not only behind tabs, accordions or other interactions.
- `noindex` on account, cart, checkout, search results, error pages and other private or utility pages.
- robots.txt blocks private, account and admin routes and points to the sitemap.

## Structured Data (JSON-LD)
Use JSON-LD only. Add a type only when the page actually shows that content:

| Page | Type |
|---|---|
| Home page | Organization or LocalBusiness, WebSite |
| Pages with breadcrumbs | BreadcrumbList |
| Product pages | Product (with Offer) |
| Blog posts and articles | Article or BlogPosting |
| Events | Event |
| Videos | VideoObject |
| Apps and software | SoftwareApplication |
| Recipes | Recipe |

- Every value must match the visible content exactly.
- Leave out unconfirmed fields. Never publish placeholders.
- Review and rating markup only for real reviews shown on the page.
- No FAQPage or HowTo markup for rich results (Google limits FAQ results to government and health sites and has retired HowTo results).
- Validate with Google's Rich Results Test and the Schema Markup Validator.

## Multilingual Sites
- Each language has its own URL (such as `/es`).
- Add `hreflang` tags for every language version, plus `x-default`.
- Set the correct `lang` attribute on every page.
- Never switch languages automatically by IP address without a visible way to change it.

## Sitemap
- Generated automatically at build time.
- Lists only canonical, indexable URLs, with accurate `lastmod` dates.
- Referenced in robots.txt.
- Over 50,000 URLs: split into multiple sitemaps with a sitemap index.

## Open Graph
**Every [Public] page:**
- `og:title`, `og:description`, `og:url`, `og:type` and `og:site_name`.
- `og:image` at 1200×630 with `og:image:alt`.
- `twitter:card` set to `summary_large_image`.

**Multi-user content sharing apps:** every shareable item (post, profile, listing) gets its own server-rendered tags built from that item's content.
- The preview image is the item's own image. When it has none, use the site's default image.
- When an image is uploaded, crop and resize a copy to 1200×630 on the server for previews, keeping the original untouched.
- Generate custom per-item preview images only when the builder asks for them.

**Privacy:** private, unlisted, deleted and logged-in-only content never appears in Open Graph tags. Those URLs fall back to generic site tags.

## Public Files
**humans.txt** (every [Public] site):
- Create `/humans.txt` with the standard TEAM, THANKS and SITE sections, linked with `<link rel="author" href="/humans.txt">`.
- Fill in the SITE section from the build (language, standards, tools used).
- Leave TEAM and THANKS as labeled placeholders. Never ask the builder for personal information to fill them.

**security.txt** (sites with [Accounts] or [Backend]):
- Create `/.well-known/security.txt` with the required `Contact` and `Expires` fields (Expires no more than one year ahead).
- Publish it only once a real contact is confirmed. Until then, list it under Builder launch tasks.

## Error Pages
- 404: returns a real 404 status. A single-page app's catch-all route must also return 404, never a 200 "soft 404."
- 500: custom server error page.
- 503: maintenance page with a `Retry-After` header.
- Error pages get `noindex`.

## Browser Support
- Last two versions of Chrome, Edge, Firefox, Safari (macOS and iOS) and Samsung Internet.
- Other Chromium-based browsers: Opera, Brave, Vivaldi.
- Firefox-based browsers: Firefox ESR, LibreWolf, Waterfox, Tor Browser (whose stricter security levels disable JavaScript, which the no-JavaScript rules cover).
- Platforms: Windows, macOS, Linux, iOS and Android.
- Browserslist `defaults`, Autoprefixer, `@supports` fallbacks and feature detection. Never detect browsers by user agent.

## Without JavaScript
Public pages display core content and navigation with clean formatting when JavaScript fails to load:
- Content that JavaScript would reveal is visible by default.
- Layout never depends on JavaScript.
- Menus fall back to a visible list or a native `<details>` element.
- Images use native `loading="lazy"`, never JavaScript-only lazy loading.
- Interactive features may require JavaScript, but show a clean message instead of breaking.

Logged-in apps may require JavaScript, with a clean, styled `<noscript>` message.

## Viewport
- `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover, interactive-widget=resizes-content">` on every page.
- Respect safe-area insets with `env(safe-area-inset-*)`.
- Never disable zoom.

## Print Styles
**Every page:**
- Hide the nav, footer, buttons, cookie banner, new-tab icons and interactive controls.
- Black text on a white background, even when dark mode is on.
- Print the URL after each external link.
- Keep cards, images and table rows from splitting across pages, and repeat table headers on every page.
- Set page margins with `@page`, and show the site name and page URL at the top.
- Remaining content reflows to fill the page with no empty gaps, leftover spacing or stray borders, keeping the same type hierarchy, spacing and alignment as on screen.

**Dedicated print layouts:** receipts, invoices, order confirmations, tickets and legal pages, each laid out to print cleanly on a single standard page where possible.

## Media Compression

| Media | Format | Settings |
|---|---|---|
| Photos | AVIF or WebP, with a JPEG fallback where needed | Visually lossless (about quality 75 to 85) |
| Logos, screenshots, line art, text graphics | Lossless WebP or PNG | Lossless |
| Icons and illustrations | SVG | Optimized with SVGO |
| Animated GIFs | MP4 (H.264) plus WebM, or animated WebP | Convert with ffmpeg. Play as `<video autoplay muted loop playsinline>`, paused when reduced motion is on |
| GIFs that must stay GIFs | GIF | Compress with gifsicle (`-O3 --lossy=30`), reduce colors and frame count |
| Video | MP4 (H.264) plus WebM or AV1 | Poster image, `preload="none"` or `"metadata"`, captions |
| Audio | AAC or Opus | Compressed, never auto-playing with sound |

- Serve responsive sizes with `srcset` and `sizes`.
- Lazy-load everything below the fold with native `loading="lazy"`.
- Give every image and video `width` and `height` attributes.
- Flag any single image over 200 KB.

## Favicon Set
- `favicon.ico` (32×32, with 16×16 inside).
- `favicon.svg`, adapting to dark mode with a `prefers-color-scheme` media query inside the SVG.
- `apple-touch-icon.png` (180×180).
- `site.webmanifest` with icons at 192×192 and 512×512, plus a 512×512 maskable icon.
- `theme-color` meta tags for light and dark, using the `media` attribute.

## Performance
- Preload the largest above-the-fold image (the LCP image) and set `fetchpriority="high"` on it.
- Inline critical CSS. Load fonts with `font-display: swap` and preload the main font file.
- Defer non-critical JavaScript and split code by route. First-party initial JavaScript stays at or under 170 KB compressed. Auth and payment provider scripts don't count, and load only on the pages that use them.
- Serve over HTTP/2 or HTTP/3 with Brotli compression and a CDN (Vercel provides all three).
- Add `preconnect` only for origins the page actually needs.
- Load third-party scripts only when required.

| What is measured | Tool |
|---|---|
| Public pages, mobile | PageSpeed Insights, mobile score |
| Public pages, desktop | PageSpeed Insights, desktop score |
| Login-only or undeployed pages | Lighthouse with mobile and desktop emulation |
| Real users after launch | Search Console Core Web Vitals report |

The SEO score target applies only to indexable public pages. Performance, Accessibility and Best Practices apply everywhere.

## HTTP Headers
**Caching and validation:**

| Response | Header |
|---|---|
| Static assets with a content hash in the filename | `Cache-Control: public, max-age=31536000, immutable` |
| HTML pages | `Cache-Control: no-cache`, with an `ETag` so unchanged pages return a fast 304 |
| Private pages | `Cache-Control: no-store` |
| API responses | Caching set explicitly on every endpoint |

- Compress text responses with Brotli, falling back to gzip.
- Set `Vary` correctly whenever content changes by language or encoding.

**Security:**
- Content-Security-Policy: hash-based on static pages, nonce-based on dynamic pages (rules in `security.md`), including `frame-ancestors`.
- Strict-Transport-Security, X-Content-Type-Options, Referrer-Policy and Permissions-Policy (enable only the features the site uses).
- Cross-Origin-Opener-Policy: `same-origin`, or `same-origin-allow-popups` on pages with popup sign-in or payment flows.
- Remove `X-Powered-By` and detailed `Server` values.
- HSTS preload only when the builder confirms it.

**Vercel configuration (default host):**

```json
{
  "cleanUrls": true,
  "trailingSlash": false,
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "Strict-Transport-Security", "value": "max-age=63072000; includeSubDomains" },
        { "key": "X-Content-Type-Options", "value": "nosniff" },
        { "key": "Referrer-Policy", "value": "strict-origin-when-cross-origin" },
        { "key": "Cross-Origin-Opener-Policy", "value": "same-origin" },
        { "key": "Permissions-Policy", "value": "camera=(), microphone=(), geolocation=()" }
      ]
    }
  ]
}
```

Add the Content-Security-Policy per the rules above (hashes in the static config, nonces in middleware). On other hosts, write the equivalent configuration.

## Builder Launch Tasks
Tasks Claude cannot complete. Add each applicable one to the delivery summary.

**Domains and hosting**
- Connect the domain and any subdomains in Vercel (or the chosen host), and create their DNS records.
- Add the email DNS records (SPF, DKIM, DMARC) and verify the sending domain with the email provider.

**Search and sharing**
- Submit the sitemap in Google Search Console and Bing Webmaster Tools.
- Run PageSpeed Insights on the deployed public pages, and check the Search Console Core Web Vitals report once real-user data is available.
- Check link previews with the Facebook Sharing Debugger and LinkedIn Post Inspector.

**Public files**
- Fill in the TEAM and THANKS sections of humans.txt.
- Confirm a security contact so security.txt can be published, and renew it before its `Expires` date.

**Accounts**
- Create OAuth apps with each sign-in provider (Google Cloud, Apple Developer, Microsoft Entra, GitHub, Discord) and add the credentials to Supabase.
- Set up an SMS provider (such as Twilio) to enable phone sign-in and text message codes.

**Testing**
- Test on real devices and browsers (for example with BrowserStack).
- Test with real screen readers: VoiceOver (macOS and iOS), NVDA, JAWS and TalkBack.

**Optional**
- Submit the domain to the HSTS preload list (hstspreload.org). Removal takes months, so only do this once every subdomain supports HTTPS.
- Make the site an installable PWA with offline support for public pages.
- Block disposable email addresses at sign-up, using a maintained blocklist.
