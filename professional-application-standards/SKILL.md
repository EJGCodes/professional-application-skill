---
name: professional-application-standards
description: Design, UX, writing, accessibility, SEO, legal, security, sign-in and performance standards for building, editing or reviewing any website, web app or software application. Use whenever creating or changing an application's interface, content, accounts or backend, including landing pages, dashboards, SaaS products, admin tools, desktop and mobile apps, even if the user does not mention standards or quality. Does not apply to in-game UIs.
metadata:
  version: 1.1.0
---

# Professional Application Standards

These rules keep applications professional, secure and clean, and avoid the common pitfalls of AI-built sites. Apply them to every website, web application or software application you build, edit or review. Each section states the key rules; the reference files hold the full details and must be read where indicated.

## How to Apply This Skill

### Precedence
1. Explicit user instructions come first. When a request conflicts with a rule, mention the conflict once, then follow the user.
2. This skill comes second.
3. Any other design guidance (general frontend or artifact design skills) comes third. Where it suggests something this skill bans, this skill wins.

### Scope
- Applies to every type of web or software application: websites, web apps, desktop apps and mobile apps.
- Does not apply to in-game UIs (HUDs, menus inside a game, in-game stores).
- Everything around a game is included: its website, launcher, account system, admin tools and analytics dashboards.

### Applicability Tags
Each rule applies only when its tag's trigger is true. Untagged rules always apply.
- **[Accounts]**: the build has sign-up, login or user profiles.
- **[Data]**: the build collects personal data or sets non-essential cookies or trackers.
- **[Payments]**: anything can be purchased.
- **[Uploads]**: users can upload files.
- **[Messaging]**: the build sends email or text messages.
- **[Backend]**: the build has a server, database or API.
- **[Public]**: the site has publicly accessible pages, or displays public user content (such as profiles, posts or listings anyone can view).
- **[Web]**: the build runs in a browser. Skip these rules for native apps.

Never add a feature only to satisfy a rule. A static page with no data collection does not get a login system so that account rules can apply.

### Native and Desktop Applications
- Skip rules tagged **[Web]**.
- Follow the intent of every other rule through the platform's equivalent: native animation APIs instead of CSS transforms, the OS keychain instead of HttpOnly cookies, platform accessibility APIs instead of ARIA, platform text layout controls instead of `text-wrap`, a settings screen instead of an `/account` page, and each platform's native provider sign-in flow.
- Verify with the platform tools in `references/testing-tools.md`.

### Creative Applications
Creative applications are those whose main purpose is art, design, media, games, entertainment or personal expression. If unclear, ask. Several rules differ for them (icon set, 404 tone, session length).

### Platform Limits
- Some environments cannot support every rule (for example, a single-file HTML page has no server for headers or a sitemap).
- Never fake compliance. Implement the closest version the platform allows, and list what could not be implemented in the delivery summary.

### Frontend and Hosting
- Leave the frontend choice open unless the user specifies one, with one requirement: **[Web] [Public]** public pages must be server-rendered or statically generated, so search engines and social preview bots can read them. A client-only app is allowed only for pages behind login.
- Recommend **Next.js, SvelteKit or Nuxt** for apps with accounts or a backend, and **Astro** for content-focused public sites.
- When the app has accounts and the user still chooses a client-only frontend, follow the client-side rules in `references/security.md` and note the tradeoff in the delivery summary.
- **[Web]** Host on Vercel unless the user specifies otherwise. Always write the header, redirect and clean URL configuration for whichever host is used.

### Project Start
At the start of a new project, ask the builder (together with any other setup questions):
- The details needed for legal pages (listed in `references/legal-and-privacy.md`).
- Whether the application is creative, if unclear.
- Which frontend to use, if unclear, with the recommendations above.

If the builder does not answer the legal questions, build with labeled placeholder fields and ask again after the first build is done. Never ask for personal information about team members.

### Existing Projects
- Apply every rule to anything new you build or change.
- Do not rewrite existing code only to fix rule violations unless asked.
- After completing your edits, list existing violations in the delivery summary and recommend that the user fix them.

### Writing Rule Scope
The writing rules in Section 7 apply to everything you create in the application: visible content, code comments, commit messages, READMEs and documentation, email templates and legal pages. They do not apply to the delivery summary or your chat messages after the build.

### Rule Organization
Each rule lives in one section. Other sections cross-reference it instead of repeating it.

### Reference Files
Read each file at the moment it is needed:

| File | Read before |
|---|---|
| `references/fonts.md` | Choosing any font |
| `references/writing.md` | Writing any content, labels, messages or emails |
| `references/ux-patterns.md` | Building loading states, interactions, notices or flows |
| `references/forms-and-data.md` | Building any form, input, data display or database schema |
| `references/accounts-and-onboarding.md` | Building sign-up, sign-in, onboarding or account pages |
| `references/legal-and-privacy.md` | Building legal pages, cookie consent, deletion, messaging or analytics |
| `references/security.md` | Building any backend, authentication, session or data storage |
| `references/web-developer-checklist.md` | Building any [Web] project |
| `references/testing-tools.md` | Testing performance, accessibility or security |
| `references/verification-checklist.md` | Delivering any build |

### Verification
- Before delivering, run every applicable check in `references/verification-checklist.md`.
- If a check cannot be run in the current environment, list it under "Unverified checks." Never report an unrun check as passed.

### Delivery Summary
End every build with a summary using these headings. Omit any heading with nothing to report.
- **Not implemented**: applicable rules the platform could not support, and why.
- **Unverified checks**: checks that could not be run.
- **Open legal fields**: placeholder fields the builder still needs to complete, with a recommendation for legal review before launch.
- **Open content placeholders**: marked content (such as "[Customer quote]") that must be replaced before launch.
- **Builder launch tasks**: every applicable task from `references/web-developer-checklist.md`.
- **Security issues needing attention**: audit or scan findings that could not be fixed.
- **Existing violations**: rule breaks in code you did not write, with a recommendation to fix them.
- **Notes**: anything else the builder needs to know.

## 1. Color and Visual Style

### Musts
- Use only one primary accent color. Differentiate with shades of that color instead of introducing a second color (unless specified).
- Neutrals (black, white, grays) and semantic status colors (error, success, warning) are allowed and do not count as a second color. Charts use shades of the accent first.
- If the user provides brand colors, use them. Otherwise, create original brand colors. Never copy colors from another similar brand.
- Maintain clean color contrast throughout (targets in Section 9).
- Separate layers and surfaces using clean page elements only: borders, dividers, tonal shades of the background, spacing, and a solid scrim behind modals.
- Use one corner radius scale across the whole app (for example: small for inputs, medium for cards, large for modals).

### Do's
- Use corner radius and smoothing to your advantage for modals, messages, buttons and similar elements.
- Use badges and chips only when they give the user information they need (such as an order status or an active filter).

### Don'ts
- No shadows of any kind: no box-shadow, text-shadow or drop-shadow filters, including subtle ones.
- No highlighter pills: no colored rounded backgrounds behind words in headings or body text.
- No decorative pills or badges that exist purely for show, including a chip that only holds step text (such as "Step 2 of 4").
- No gradients or gradient blobs, liquid glass, radial orbs, dot grids or grain textures.
- No colored left strips on any element, including cards, alerts, callouts, list items, navigation indicators and blockquotes. Show an active nav item with a tonal background shade, text color or weight instead.
- No dark or hidden patterns in backgrounds.

## 2. Typography

### Musts
- Use one main typeface (two maximum, only if necessary).
- Before choosing a font, read `references/fonts.md`. Use a font from its Approved list, a font the user specifies, or a font that passes every one of its criteria.
- Self-host font files where the platform allows.
- Establish a clear type (font size) hierarchy for all necessary elements.
- Keep text in clean contrast with the elements it sits in, so it stays visible wherever it is placed.
- **[Web]** Apply `text-wrap: balance` to headings and `text-wrap: pretty` to paragraphs, with fallbacks where unsupported.

### Do's
- Use monospace only for actual code and for codes, keys and IDs the user must read or copy (recovery codes, API keys, order IDs). Never as a UI or display font.
- Use italics only for titles of works, foreign terms and quotations.
- Place text under a heading only when it gives the user valuable information they cannot get anywhere else on the page.

### Don'ts
- Do not use Inter, Geist, Space Grotesk, monospace as a UI font, or any lookalike listed in `references/fonts.md`.
- Do not rely on the system UI font stack as the chosen typeface. It may appear only as a fallback.
- No double-accented phrases: at most one word per title may differ in color, size or rotation. This is optional, never a default.
- No headings followed by unnecessary explanations or summaries.
- No eyebrow labels (small text or badges above a heading). Step counts belong inside the progress component.
- No italics for emphasis.
- No orphan words: never separate words out of normal text for emphasis, never split a headline into separate lines word by word, and never leave a single word stranded on the last line of a heading or paragraph.

## 3. Layout and Responsiveness

### Musts
- All elements (text and non-text) must resize with device screen size and window resizing.
- Use percentages and other relative units (`%`, `fr`, `rem`, `clamp()`, viewport units) wherever they make sense. Reserve fixed pixel values for borders, hairlines and minimum tap targets.
- Keep spacing consistent across the entire application, and align elements of the same type.
- Handle long text cleanly on window resize and across platforms so the layout holds.
- When an input is focused on a device with an onscreen keyboard, scroll it into view so the keyboard sits below it and never covers it. Fixed or sticky elements must not overlap the focused input.
- Keyboard handling must not cause major layout shift or change element formatting. The page adjusts its scroll position only.
- Convert table rows to cards on mobile and on narrow window sizes. Cards keep the same fields, in the same order, labeled with the table's column headers.

### Do's
- Limit dead space: empty areas with no purpose, such as oversized hero padding, empty columns on wide screens, or sections stretched to fill the viewport. Normal spacing between elements is not dead space.
- Keep table rows industry-standard with short content.
- Verify layouts at 320, 375, 768, 1024, 1440 and 1920 pixel widths, plus continuous resizing between them.

### Don'ts
- No table rows that wrap or split text.
- No horizontal page scroll at any width.

## 4. Icons, Images and Media

### Musts
- Use only Material Symbols (professional websites and applications) or Font Awesome (creative applications) for icons. One icon set per project.
- Official brand logos are the one exception: use them wherever they represent a third-party service (sign-in buttons, social links), always preferring the brand's official assets over icon-set versions.
- Keep icons consistent across all pages and with the favicon.
- Use only images and media the user provides, or unlicensed (free-to-use, no paid license required) stock images and media when none are provided. This covers photos, illustrations, video, audio and any other media.
- When no approved image or media exists, use a neutral, clearly marked placeholder rather than an unrelated substitute.
- Charts must display real data, in the chart type that fits the data, styled with shades of the accent color.
- Compress all images and media following `references/web-developer-checklist.md` (including converting animated GIFs), and give every image and video `width` and `height` attributes.
- Video includes a poster image and captions.

### Do's
- **[Public]** Add a social preview image (see Section 8).

### Don'ts
- No emojis as icons, and no icons from any other set (this rules out Lucide, Feather, Heroicons and similar sets).
- No pulsing circle icon for dates, and no other meaningless icons.
- No non-approved images or media from outside sources, especially licensed ones.
- No AI-generated images or media unless the user requests them.
- No decorative charts or stat blocks that exist only to look busy, such as large "10k+ users" figures or filler graphs.
- No inverted bar charts: bars stepping from small to large that carry no real meaning and exist only to suggest growth.
- No decorative diagrams. Diagrams are allowed only when they explain something real.

## 5. Motion, Loading and Interaction

Before building loading states, interactions, notices or flows, read `references/ux-patterns.md`.

### Musts
- Animate movement and scaling with CSS `transform`, and fades with `opacity`. Simple color transitions are allowed. JavaScript is only a helper, never the main source of an animation.
- Respect the user's reduced-motion setting by removing or minimizing non-essential motion.
- Prevent buttons from being double-clicked and creating duplicate actions. (IMPORTANT)
- Handle actions in this order: update the UI immediately, lock the control while the request runs, send an idempotency key so the server rejects duplicates, and roll back with a clear message if the server refuses.
- Payments, deletions and other irreversible actions wait for the server before updating the UI.
- Backspace deletes one character at a time in every field, including masked and formatted fields. In chip or tag inputs, it removes only one chip at a time.
- Skeletons match the dimensions of the content they replace, loaders end when loading ends, and loaders never block content that has already loaded.
- Use only the loaders, user-error safeguards and notice types defined in `references/ux-patterns.md`.

### Do's
- Add tap and click animations for every state: hover, active/pressed, focus-visible, disabled and loading.
- Minimum tap targets of 44×44 px. Links inside running text are exempt.

### Don'ts
- No looping arrow loading indicator.
- Never add a thin bar or line along the top edge of the page for any purpose, including scroll progress and page navigation loading.
- No dark or hidden UX patterns, and no harmful or unnecessary UX, as listed in `references/ux-patterns.md`.
- No popups, modals or prompts on page load. The only exceptions are the notices defined in `references/ux-patterns.md`.

## 6. Forms and Input

Before building any form, input or data display, read `references/forms-and-data.md`.

### Musts
- Follow the input reference table for `type`, `inputmode`, `autocomplete` and `enterkeyhint` on every field. Never use `type="number"` for digit-only values that aren't quantities.
- Every field has a visible label. Placeholder text never replaces a label.
- Input and textarea text is never smaller than 16px.
- Accept every correct way a user might type a value (such as phone numbers with dashes, spaces, dots, parentheses around the area code, or a country code), then normalize it on the server.
- Validate each field when the user leaves it, then re-check live while the user fixes an error. Never show errors on untouched fields.
- Password fields validate on every keystroke, with the requirement checklist shown underneath, and have a show/hide toggle. Requirements are in `references/accounts-and-onboarding.md`.
- Search results appear 300 ms after the last keypress. Pressing Enter searches immediately and cancels any pending delayed search.
- Use the native date input for simple dates. Custom pickers only for ranges or bookings, fully keyboard and screen reader accessible.
- **[Accounts]** Collect age (or a full birthday for apps handling sensitive data) at sign-up, and enforce a minimum age based on the builder's regions (13 when unknown). Sensitive data includes health, financial, precise location, government ID, and anything involving minors.
- **[Uploads]** Enforce a file size limit (10 MB per file unless specified), and check file format and size in the browser and again on the server.

## 7. Writing and Content

Before writing any content, labels, messages or emails, read `references/writing.md`.

### Musts
- All content must be truthful about the site.
- Every call to action, button and instruction must tell the user exactly what to do or what happens next.
- Every info and error message says what happened and the specific next step, in plain language, except where account privacy requires a generic message (see `references/accounts-and-onboarding.md`).
- When real content isn't available, use clearly marked placeholders (such as "[Customer quote]").
- Format displayed dates, numbers and currency following the data display rules in `references/forms-and-data.md`.

### Do's
- Include only as much content in each section as is necessary.
- Use three items only when the real content has exactly three.

### Don'ts
- No em dashes, en dashes used as dashes, or spaced hyphens used as dashes.
- No half-sentences or sentence fragments for emphasis.
- No content padded or trimmed to fit a rule of three.
- No banned calls to action, vague messages or writing clichés (lists in `references/writing.md`).
- No raw error codes or stack traces shown to users.
- No fake reviews, testimonials, user counts, client logos, statistics or other unsupported claims.

## 8. Navigation, Structure and Search

### Musts
- The navbar must be mobile compatible.
- The logo must be clickable and responsive. It links to the home page, or to the dashboard when the user is logged in. When the app lives on a subdomain, the marketing site's logo always goes home and its nav shows a "Sign in" link that sends signed-in users to their dashboard.
- Footers and footer links must be functional and professional, with the copyright year generated automatically.
- Every link must match what its text says and be fully functional. Link text must make sense out of context.
- External links always open in a new tab.
- Internal links open in the same tab, except links inside a task (such as a form, checkout, sign-up or settings flow) that lead to a non-function page (FAQ, help center, legal pages), which open in a new tab. Links to those pages from the nav, footer or any non-task page open in the same tab.
- Every link that opens a new tab has `rel="noopener noreferrer"` and a visible icon with accessible text.
- Include custom error pages that match the site's design and tone: a 404 page (returning a real 404 status) with a link home and navigation or search, a 500 page, and **[Backend]** a 503 maintenance page with `Retry-After`. Creative applications may give them more personality.
- Use dynamic page titles (such as "Site Name - Page Name").
- **[Web]** Use clean URLs: lowercase, hyphenated, descriptive, shallow, with no trailing slash and no file extensions on pages. Standard files and downloads (robots.txt, sitemap.xml, favicon.ico, PDF invoices) keep their extensions.
- **[Web]** Give every page a canonical tag, and 301-redirect the non-canonical www version and trailing slash URLs in a single step.
- **[Web]** Unique meta titles (about 60 characters or fewer) and meta descriptions (about 155 or fewer) that accurately reflect each page.
- **[Web]** Navigation uses real `<a href>` links. Private and utility pages get `noindex`.
- **[Web] [Public]** Add JSON-LD structured data (never microdata), Open Graph and Twitter Card tags, a sitemap.xml, robots.txt and humans.txt.
- **[Web] [Accounts or Backend]** Add `/.well-known/security.txt` once a real contact is confirmed.
- **[Web]** Multilingual sites use `hreflang`, a URL per language and the correct `lang` on every page.
- Follow `references/web-developer-checklist.md` for every item above.

### Do's
- Recommend a FAQ page for any application that may benefit from one. Answers come from the builder or are clearly marked placeholders.
- Add breadcrumbs to any page more than two levels deep.
- Use subdomains to organize the site where appropriate (rules in `references/web-developer-checklist.md`).

### Don'ts
- No orphan pages, redirect chains, or important content reachable only behind interactions.
- No FAQPage or HowTo rich result markup, and no review markup unless real reviews are shown on the page.
- No placeholders in public machine-readable data (JSON-LD, Open Graph, security.txt). Leave unconfirmed fields out.
- No automatic language switching by IP address without a visible way to change it.

## 9. Accessibility and Theming

### Musts
- Meet WCAG 2.2 AA contrast: 4.5:1 for body text, 3:1 for large text and UI elements. The high-contrast mode meets AAA (7:1).
- Every application must be fully keyboard accessible:
  - Every interactive element can be reached and used with the keyboard alone, in an order that matches the visual order. Never use a positive `tabindex`.
  - No keyboard traps. Modals keep focus inside while open and return it to the opener when closed. Escape closes menus, modals and popovers.
  - Custom widgets follow the WAI-ARIA Authoring Practices keyboard patterns.
  - Nothing works only on hover.
  - Every focusable element shows a visible solid outline.
- Include a "Skip to content" link as the first focusable element.
- Every page has at least one `<h1>`, and headings follow a logical order without skipping levels.
- Use semantic elements: lists, real tables with `<th scope>` and `<caption>`, links to navigate and buttons to act, `<address>`, `<figure>` and `<time>` where they apply. **[Web]** Pages pass the W3C Nu HTML Checker with zero errors.
- **[Web]** Use landmarks: `<header>`, `<nav>`, exactly one `<main>`, `<footer>`, plus `<aside>` and `<search>` where they apply. All content sits inside a landmark, and multiple navs each get a distinct `aria-label`.
- Prefer native elements over ARIA. Add ARIA only when no native element exists.
- Provide alt text for every meaningful image, and `alt=""` for decorative ones. Set the `lang` attribute on every page.
- Never convey information by color alone.
- Support screen readers (VoiceOver, NVDA, JAWS, TalkBack), zoom to 400% with reflow at 320 px, voice control (visible labels match accessible names) and browser translation tools. Announce dynamic updates through live regions.
- Provide accessibility options (high-contrast mode, adjustable text size, reduced motion). Device accessibility settings (`prefers-reduced-motion`, `prefers-contrast`, forced colors) apply automatically.
- Default to light mode regardless of the device setting. Provide a dark mode toggle, and remember the choice in a small essential preference cookie so the server renders the right theme with no flash.
- Every theme and accessibility option works without breaking the layout or styling.

## 10. Legal, Privacy and Compliance

Before building legal pages, cookie consent, deletion, messaging or analytics, read `references/legal-and-privacy.md`.

### Musts
- **[Data]** Include a privacy policy, terms of service and a data deletion request system.
- **[Web] [Data]** Include a cookie policy and a consent banner whenever non-essential cookies or trackers are used, with a toggle for each category and the choice shared across subdomains.
- **[Payments]** Include a refund policy, and show the full total, including taxes and fees, before the user commits to paying.
- Generate legal pages with complete structure, filling in only confirmed details, and never invent business names, addresses, jurisdictions, retention periods or third-party services.
- **[Accounts]** Account deletion has a 14-day grace period (cancelled by signing back in), keeps only legally required records with personal details removed, and says so on the confirmation and in the privacy policy.
- **[Messaging]** Every email and text includes a one-click unsubscribe, with per-type preferences when more than one message type is sent. Required transactional messages cannot be unsubscribed from.
- **[Accounts] [Messaging]** Configure a production email system that reliably delivers password resets, confirmations, sign-in links and security alerts.
- Add analytics only when they are necessary to the site or improve it, preferring privacy-friendly tools.

### Don'ts
- Do not collect unnecessary data. Collect only what a feature requires.

## 11. Security

Before building any backend, authentication, session or data storage, read `references/security.md`.

### Musts
- **[Backend]** Use Supabase (Postgres) in most cases, following the Supabase standards in `references/security.md`, including row-level security on every table. Logged-out visitors have no access to any data that would normally require an account.
- Require authentication and authorization on API endpoints. Keep API keys and sensitive info on the server, and enforce server-side authority on every action.
- Protect admin routes and permission-restricted content on the server, not only by hiding them in the UI.
- Rate-limit everything possible, strictest on sign-in, sign-up, password reset, form submissions, and every feature that calls an external API or sends email or text messages.
- Sanitize all user content, encode output for its context, and never render user content with `innerHTML` or its framework equivalents without DOMPurify.
- Protect every state-changing request against cross-site request forgery.
- **[Payments]** Verify every payment webhook signature and process each event only once.
- Encrypt sensitive data in transit and at rest. Hash passwords with Argon2id or bcrypt.
- Set session cookies as HttpOnly, Secure and SameSite, and force HTTPS.
- **[Web]** Use a strict Content-Security-Policy and the full security header set (details in `references/web-developer-checklist.md`).
- Never expose user data, tokens or secure database content anywhere a user could find it, including browser storage. Browser storage holds only non-sensitive interface preferences.
- Guard against the OWASP Top 10 risks, scan dependencies and secrets, and remove everything on the Never Ship list in `references/security.md`.

## 12. Performance and Reliability

### Musts
- Leave no fixable console errors behind.
- Handle failed requests and API timeouts cleanly on both frontend and backend. Retry only safe requests, with increasing delays and at most three attempts, then show a clear message with a manual retry option.
- Prevent memory leaks: clean up event listeners, timers, observers and pending requests when a component or page closes.
- **[Web]** Score 90+ in Performance, Accessibility and Best Practices on every page, and in SEO on every indexable public page. Measure public pages with PageSpeed Insights (mobile score for mobile, desktop score for desktop) and other pages with Lighthouse. Core Web Vitals stay in the "good" range.
- **[Web]** Keep first-party initial JavaScript at or under 170 KB compressed, and follow the performance techniques in `references/web-developer-checklist.md`.
- When the connection drops, show a clear offline message and keep the user's actions in memory until it returns.
- **[Accounts]** Manage sessions with the idle timeout table and logout rules in `references/security.md`. Private data is never accessible after logout or expiry.

### Do's
- Write efficient scripts and bundles, optimize database queries, cache repeat requests, and self-host assets where the platform allows.
- Native apps measure performance with platform metrics (Android vitals, Xcode Organizer).

## 13. Web Compatibility and Delivery

Before building any [Web] project, read `references/web-developer-checklist.md`.

### Musts
- **[Web]** Support the last two versions of Chrome, Edge, Firefox, Safari (macOS and iOS), Samsung Internet, other Chromium-based browsers and Firefox-based browsers, on Windows, macOS, Linux, iOS and Android.
- **[Web]** Use Browserslist `defaults`, Autoprefixer, `@supports` fallbacks and feature detection. Never detect browsers by user agent.
- **[Web] [Public]** Public pages display core content and navigation with clean formatting when JavaScript fails to load. Logged-in apps may require JavaScript, with a clean `<noscript>` message.
- **[Web]** Every page uses `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover, interactive-widget=resizes-content">` and respects safe-area insets.
- **[Web]** Include print styles on every page and dedicated print layouts for receipts, invoices, order confirmations, tickets and legal pages. Printed pages keep consistent formatting when elements are excluded, with no gaps or leftover spacing.
- **[Web]** Set caching, validation and compression headers and confirm they work on the deployed site.
- **[Web]** Provide the full favicon set and a web app manifest. Build a full installable PWA only when the user asks for one.

### Don'ts
- Never disable zoom (`user-scalable=no` or `maximum-scale=1`).
- No browser-specific features without a fallback.

## 14. Accounts, Sign-In and Onboarding

Before building sign-up, sign-in, onboarding or account pages, read `references/accounts-and-onboarding.md`.

### Musts
- **[Accounts]** Store each email as entered (for sending) and fully lowercased with a unique constraint (for lookups). Never strip Gmail dots or `+tags` except for duplicate detection in apps where repeat sign-ups are abused.
- **[Accounts]** Always offer email and password sign-in (plus phone and password when an SMS provider is configured), alongside Google and the other providers that fit the app type.
- **[Accounts]** Provider buttons follow each provider's official branding and wording, share one size and layout, and request only email and profile scopes. A matching verified email lands in the existing account, never a duplicate.
- **[Accounts]** Passwords are at least 12 characters, include at least one capital letter, number and symbol, and are checked against known breached passwords.
- **[Accounts]** Sign-in, sign-up and password reset never reveal whether an account exists.
- **[Accounts]** Offer two-factor authentication (authenticator app, text message, email code or passkey) in every app with accounts. Require it for admins and for every user in apps handling sensitive data.
- **[Accounts]** Sign-up shows links to the terms and privacy policy, keeps marketing opt-in as a separate unchecked box, and collects age in onboarding for any sign-up method that skipped it.
- **[Accounts]** Onboarding is interactive (users do real tasks, never just click through slides), asks only for what the app needs, lets optional steps be skipped, saves progress on the server, and ends with one specific next action. Add multi-step onboarding only when the app needs setup or its first use isn't obvious.
- **[Accounts]** Provide a dedicated account section, reachable from the user menu on every page, with "Download my data" and account deletion in every app with accounts.
- **[Accounts]** Cancelling, deleting an account and requesting data deletion each take no more steps than signing up did (one re-authentication and one confirmation don't count), and never require contacting support.
- **[Accounts]** Email the user about every security change and new-device sign-in.
