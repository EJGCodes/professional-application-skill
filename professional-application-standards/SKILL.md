---
name: professional-application-standards
description: Design, UX, writing, accessibility, legal, security and performance standards for building, editing or reviewing any website, web app or software application. Use whenever creating or changing an application's interface, content or backend, including landing pages, dashboards, SaaS products, admin tools, desktop and mobile apps, even if the user does not mention standards or quality. Does not apply to in-game UIs.
---

# Professional Application Standards

These rules keep applications professional, secure and clean, and avoid the common pitfalls of AI-built sites. Apply them to every website, web application or software application you build, edit or review.

## How to Apply This Skill

### Precedence
1. Explicit user instructions come first. When a request conflicts with a rule, mention the conflict once, then follow the user.
2. This skill comes second.
3. Any other design guidance (general frontend or artifact design skills) comes third. Where it suggests something this skill bans (such as subtle shadows or eyebrow labels), this skill wins.

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
- Follow the intent of every other rule through the platform's equivalent:
  - Native animation APIs instead of CSS transforms.
  - The OS keychain or platform secure storage instead of HttpOnly cookies.
  - Platform accessibility APIs instead of ARIA.
  - Platform text layout controls instead of `text-wrap`.
  - Platform tools for verification (see `references/testing-tools.md`).

### Creative Applications
- Creative applications are those whose main purpose is art, design, media, games, entertainment or personal expression. If unclear, ask.
- Several rules differ for creative applications (icon set, 404 tone, session length).

### Platform Limits
- Some environments cannot support every rule (for example, a single-file HTML page has no server for security headers or a sitemap).
- Never fake compliance. Implement the closest version the platform allows.
- List every applicable rule that could not be implemented, and why, in the delivery summary.

### Frontend Choice
Leave the frontend choice open unless the user specifies one. Recommend:
- **Next.js, SvelteKit or Nuxt** for apps with accounts or a backend. All three support secure cookie-based Supabase sessions.
- **Astro** for content-focused public sites.

When the app has accounts, recommend a frontend with a server layer. If the user chooses a pure client-side frontend anyway, follow the client-side auth rules in `references/supabase-security.md` and note the tradeoff in the delivery summary.

### Project Start
At the start of a new project, ask the builder (together with any other setup questions):
- The details needed for legal pages (see Section 10).
- Whether the application is creative, if unclear.
- Which frontend to use, if unclear, with the recommendations above.

If the builder does not answer the legal questions, build with labeled placeholder fields and ask again after the first build is done.

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
- `references/fonts.md`: before choosing any font.
- `references/supabase-security.md`: before building any backend, authentication, session or data storage.
- `references/testing-tools.md`: before testing performance, accessibility or security.
- `references/verification-checklist.md`: before delivering any build.

### Verification
- Before delivering, run every applicable check in `references/verification-checklist.md`.
- If a check cannot be run in the current environment, list it under "Unverified checks." Never report an unrun check as passed.

### Delivery Summary
End every build with a summary using these headings. Omit any heading with nothing to report.
- **Not implemented**: applicable rules the platform could not support, and why.
- **Unverified checks**: checks that could not be run.
- **Open legal fields**: placeholder fields the builder still needs to complete, with a recommendation for legal review before launch.
- **Security issues needing attention**: audit or scan findings that could not be fixed.
- **Existing violations**: rule breaks in code you did not write, with a recommendation to fix them.
- **Notes**: anything else the builder needs to know, such as assets loaded from a permitted external source.

## 1. Color and Visual Style

### Musts
- Use only one primary accent color. Differentiate with shades of that color for theming instead of introducing a second color (unless specified).
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
- No decorative pills or badges that exist purely for show.
- No gradients or gradient blobs, liquid glass, radial orbs, dot grids or grain textures.
- No colored left strips on any element, including cards, alerts, callouts, list items, navigation indicators and blockquotes. Show an active nav item with a tonal background shade, text color or weight instead.
- No dark or hidden patterns in backgrounds.

## 2. Typography

### Musts
- Use one main typeface (two maximum, only if necessary).
- Before choosing a font, read `references/fonts.md`. Use a font from its Approved list, a font the user specifies, or a font that passes every one of its criteria.
- Self-host font files where the platform allows (see Section 12).
- Establish a clear type (font size) hierarchy for all necessary elements.
- Keep text in clean contrast with the elements it sits in, so it stays visible wherever it is placed.
- **[Web]** Apply `text-wrap: balance` to headings and `text-wrap: pretty` to paragraphs to prevent stranded single words.

### Do's
- Use monospace only to display actual code, never as a UI or display font.
- Use italics only for titles of works, foreign terms and quotations.
- Place text under a heading only when it gives the user valuable information they cannot get anywhere else on the page.

### Don'ts
- Do not use Monospace (as a UI or display font), Inter, Geist or Space Grotesk, or any lookalike listed in `references/fonts.md`.
- Do not rely on the system UI font stack (`system-ui`, `-apple-system`) as the chosen typeface. It may appear only as a fallback.
- No double-accented phrases: at most one word per title may differ in color, size or rotation. This is optional, never a default.
- No headings followed by unnecessary explanations or summaries (such as a title followed by medium or small text, shrunken type or small badges).
- No eyebrow labels (small text or badges above a heading).
- No italics for emphasis.
- No orphan words: never separate words out of normal text for emphasis, never split a headline into separate lines word by word, and never leave a single word stranded on the last line of a heading or paragraph.

## 3. Layout and Responsiveness

### Musts
- All elements (text and non-text) must resize with device screen size and window resizing.
- Use percentages and other relative units (`%`, `fr`, `rem`, `clamp()`, viewport units) wherever they make sense, so layouts hold at any window or screen size. Reserve fixed pixel values for borders, hairlines and minimum tap targets.
- Keep spacing consistent across the entire application.
- Align elements of the same type with each other.
- Handle long text cleanly on window resize and across platforms so the layout holds.
- When an input is focused on a device with an onscreen keyboard, scroll it into view so the keyboard sits below it and never covers it. Fixed or sticky bottom elements must not overlap the focused input.
- Keyboard handling must not cause major layout shift or change element formatting. The page adjusts its scroll position only.
- Convert table rows to cards on mobile and on narrow window sizes. Cards keep the same structure as the table: the same fields, in the same order, labeled with the table's column headers.

### Do's
- Limit dead space and make proper use of the available screen space. Dead space means empty areas with no purpose, such as oversized hero padding, empty columns on wide screens, or sections stretched to fill the viewport. Normal spacing between elements is not dead space.
- Keep table rows industry-standard with short content.
- Verify layouts at 320, 375, 768, 1024, 1440 and 1920 pixel widths, plus continuous resizing between them.

### Don'ts
- No table rows that wrap or split text.
- No horizontal page scroll at any width.

## 4. Icons, Images and Media

### Musts
- Use only Material Symbols or Font Awesome for icons:
  - **Material Symbols** for professional websites and applications.
  - **Font Awesome** for creative applications.
- Use one icon set per project. Never mix sets.
- Keep icons consistent across all pages and with the favicon.
- Use only images and media the user provides, or unlicensed (free-to-use, no paid license required) stock images and media when none are provided. This covers photos, illustrations, video, audio and any other media.
- When no approved image or media exists, use a neutral, clearly marked placeholder rather than an unrelated substitute.
- Charts must display real data. Choose the chart type that fits the data and style it with shades of the accent color.

### Do's
- Compress images and large media while preserving quality: use WebP or AVIF, serve responsive sizes with `srcset`, and lazy-load anything below the fold.
- Self-host icon fonts or SVGs where the platform allows (see Section 12).
- **[Public]** Add a social preview image to public sites and sites that include public user content. Skip it for internal tools and login-only apps.

### Don'ts
- No emojis as icons, and no icons from any set other than Material Symbols or Font Awesome (this rules out Lucide, Feather, Heroicons and similar sets).
- No pulsing circle icon for dates, and no other meaningless icons.
- No non-approved images or media from outside sources, especially licensed ones.
- No AI-generated images or media unless the user requests them.
- No decorative charts or stat blocks that exist only to look busy, such as large "10k+ users" figures or filler graphs.
- No inverted bar charts: bars stepping from small to large that carry no real meaning and exist only to suggest growth.
- No decorative diagrams. Diagrams are allowed only when they explain something real.

## 5. Motion, Loading and Interaction

### Musts
- Animate movement and scaling with CSS `transform`, and fades with `opacity`. Simple color transitions are allowed. JavaScript is only a helper, never the main source of an animation.
- Respect the user's reduced-motion setting (`prefers-reduced-motion`) by removing or minimizing non-essential motion.
- Prevent buttons from being double-clicked and creating duplicate actions. (IMPORTANT)
- Handle actions in this order:
  1. Update the UI immediately (optimistic update).
  2. Lock the control while the request runs.
  3. Send an idempotency key so the server rejects duplicates.
  4. If the server refuses, roll back the UI and show a clear message (see Section 7).
- Payments, deletions and other irreversible actions wait for the server before updating the UI. They never update optimistically.
- Backspace deletes one character at a time in every field, including masked phone, date and similar formatted fields. It never clears a whole field.
- In chip or tag inputs, backspace removes only one chip at a time. It never removes all chips in the field.
- Skeletons and all other loaders must work properly with the page content:
  - Skeletons match the dimensions of the content they replace, so nothing shifts when content arrives.
  - Loaders appear only while something is loading and are replaced by the content or a clear error message when loading ends. They are never left running.
  - Loaders never block interaction with content that has already loaded.

### Do's
- Use these loaders:
  - Skeleton screens for loading content. Keep every element responsive while loading.
  - A simple circular spinner inside a button for short actions.
  - A determinate progress bar for measurable progress, such as uploads or multi-step forms.
- Add tap and click animations that respond at every state: hover, active/pressed, focus-visible, disabled and loading.
- Account for user error in every interaction:
  - Minimum tap targets of 44×44 px.
  - A short delay before hover menus close.
  - Invisible triangles (safe zones) that keep submenus open while the pointer moves toward them.
  - Undo for destructive actions where possible, and confirmation for irreversible ones.
  - Warnings before leaving a page with unsaved changes, and saved drafts for long forms.
  - User input preserved when a submission fails.
  - Tolerant input parsing (for example, accept phone numbers with or without spaces, dashes or parentheses).

### Don'ts
- No looping arrow loading indicator.
- Never add a thin bar or line at the top of the page, or anything similar, for any purpose. This includes scroll progress and page navigation loading.
- No dark or hidden UX patterns, including:
  - Pre-checked opt-in boxes.
  - Confirmshaming (such as "No thanks, I don't like saving money").
  - Hidden or hard-to-find cancel, unsubscribe or account deletion options.
  - Fake urgency, countdowns or scarcity.
  - Visually weaker "reject" or "decline" buttons.
  - Trick questions and double negatives.
  - Items or add-ons sneaked into a cart.
  - Ads disguised as content or navigation.
- No other harmful or unnecessary UX, including:
  - Popups, newsletter modals or permission prompts on page load. The only exception is the cookie consent banner (Section 10), which appears as a non-blocking bar at the bottom of the screen, never a modal, and never covers a focused input.
  - Auto-playing media with sound.
  - Forced account creation just to browse.
  - Disabled paste in any field, including passwords.
  - Scroll-jacking.
  - Infinite scroll that makes the footer unreachable.

## 6. Forms and Input

### Musts
- Validate each field when the user leaves it. Once an error shows, re-check live as the user types to fix it. Never show errors on fields the user hasn't touched.
- Password fields validate on every keystroke, with the requirement checklist shown underneath and each item updating as it is met.
- Provide a show/hide toggle on password fields.
- Use the correct `type`, `inputmode` and `autocomplete` attributes on every field, so the right mobile keyboard appears and password managers can fill fields.
- Input and textarea text is never smaller than 16px (smaller text makes iPhones zoom the page on focus).
- Search results appear 300 ms after the last keypress. Pressing Enter searches immediately and cancels any pending delayed search.
- **[Accounts]** Include an age field on sign-up and enforce a minimum age. If the application handles possibly sensitive data, use a full birthday field instead.
  - The minimum age follows the regions the builder gives in the legal questions (some regions set the age of digital consent at up to 16). Default to 13 only when no region is known.
  - Sensitive data includes health, financial, precise location, government ID, and anything involving minors.
- **[Uploads]** Enforce a file size limit (10 MB per file unless specified).
- **[Uploads]** Check file format and size in the browser for fast feedback, then check again on the server to block dangerous files.

## 7. Writing and Content

See "Writing Rule Scope" above for where these rules apply.

### Musts
- All content must be truthful about the site.
- Every call to action and instruction must tell the user exactly what to do or what happens next (for example, "Create account," "Download the report," "Book a 30-minute call").
- Every info and error message must say what happened and the specific next step, in plain language. Any button in a message names its action (for example, "Retry upload" or "Re-enter card number").
- When real content isn't available, use clearly marked placeholders (such as "[Customer quote]").

### Do's
- Include only as much content in each section as is necessary.
- Use three items only when the real content has exactly three, such as three genuine pricing tiers.

### Don'ts
- No em dashes, en dashes used as dashes, or spaced hyphens used as dashes. Use commas, colons, periods or parentheses instead.
- No half-sentences or sentence fragments for emphasis.
- No content padded or trimmed to fit a rule of three.
- No calls to action or instructions that don't tell the user what to do next, such as "Get Started," "Learn More," "Click Here," "Submit," "Continue" (without context) or "Explore."
- No vague messages such as "Something went wrong" or "An error occurred" without a cause and next step.
- No raw error codes or stack traces shown to users.
- No fake reviews, testimonials, user counts, client logos, statistics or other unsupported claims.
- No writing clichés, including:
  - Verbs: unlock, elevate, supercharge, empower, unleash, harness, leverage, revolutionize, transform, streamline, delve, dive in.
  - Adjectives: seamless, effortless, cutting-edge, next-level, game-changing, best-in-class, world-class, robust, powerful, intuitive.
  - Phrases: "In today's fast-paced world," "It's not just X, it's Y," "Whether you're X or Y," "Look no further," "Say goodbye to X," "Take X to the next level," "The future of X," "Designed with you in mind," "Your all-in-one X," "Imagine a world where," "At the heart of," "Ready to X?"

## 8. Navigation, Structure and SEO

### Musts
- The navbar must be mobile compatible.
- The logo must be clickable and responsive. It links to the home page, or to the dashboard when the user is logged in.
- Footers and footer links must be functional and professional.
- The footer includes the copyright year, generated automatically so it never goes stale.
- Every link must match what its text says and be fully functional for its purpose.
- Include a custom 404 page that matches the site's design, explains the page wasn't found, links home, and offers site navigation or search. Creative applications may give the message more personality, but it must still include a clear way back.
- Use dynamic page titles (such as "Site Name - Page Name").
- Provide an SVG favicon plus an Apple touch icon.
- **[Web]** Include meta titles and meta descriptions that accurately reflect each page's content.
- **[Web] [Public]** Include a sitemap.xml listing every public page.
- **[Web]** Include a robots.txt that blocks private, account and admin routes from indexing.

## 9. Accessibility and Theming

### Musts
- Meet WCAG 2.2 AA contrast: 4.5:1 for body text, 3:1 for large text and UI elements. The high-contrast mode meets AAA (7:1 for body text).
- Support full keyboard navigation, with a visible solid outline on every focusable element (shadows are not allowed, see Section 1).
- Include a "Skip to content" link as the first focusable element.
- Provide alt text for every meaningful image, and empty alt text (`alt=""`) for decorative ones.
- Never convey information by color alone. Pair color with text, icons or patterns so colorblind users get the same information.
- Use semantic HTML and correct ARIA labels so screen readers can navigate the site.
- Set the `lang` attribute on every page.
- Provide accessibility options: high-contrast mode, adjustable text size and reduced motion.
- Accessibility settings follow the device automatically (`prefers-reduced-motion`, `prefers-contrast`, and Windows high-contrast/forced colors), since users rely on them to use the site at all.
- Default to light mode regardless of the device setting. Provide a toggle to switch to dark mode, and remember the user's choice on return visits.
- Light mode, dark mode and every accessibility option must work without breaking the layout or styling when toggled.

## 10. Legal, Privacy and Compliance

### Musts
- **[Data]** Include a privacy policy, terms of service and a data deletion request system.
- **[Web] [Data]** Include a cookie policy and consent banner whenever the site uses non-essential cookies or trackers. A site using only essential cookies does not show a banner.
- **[Payments]** Include a refund policy.
- **[Payments]** Show the full total, including taxes and fees, before the user commits to paying. No hidden fees.

### Legal Page Content
- At the start of the project, ask the builder whether they want to provide the details needed to complete the legal pages, so they don't have to fill them in manually later. Ask for:
  - Legal business name, address and contact email.
  - Countries or regions where the site operates or has users.
  - Third-party services that receive user data (payments, analytics, email, error monitoring and similar).
  - Data retention periods.
  - **[Payments]** Refund window, cancellation terms and dispute process.
- If the builder does not answer, ask again after the first build is done.
- Generate every legal page with complete structure and plain-language content, styled to match the site.
- Fill in only details confirmed by the builder or by the build itself (for example, naming Stripe if the build uses Stripe).
- Mark every remaining detail as a clearly labeled field, such as "[Company legal name]."
- List all open fields in the delivery summary and recommend legal review before launch.
- Never invent business names, addresses, jurisdictions, retention periods or third-party services.

### Cookie Consent
- **[Web] [Data]** Show the banner as a non-blocking bar at the bottom of the screen, never a modal.
- Group non-essential cookies into categories (such as analytics, marketing and preferences), each with its own toggle so the user picks which ones to enable.
- All non-essential categories are off by default.
- "Accept all," "Reject all" and "Save choices" have equal visual weight.
- Nothing non-essential loads before the user consents.
- Include a "Cookie settings" link in the footer so users can change their choices at any time.
- The cookie policy lists every cookie by name, purpose, category and duration.

### Data Deletion
- **[Accounts]** Provide a self-serve "Delete my account and data" option in account settings, with a confirmation step.
- **[Data]** Provide a deletion request form for people without accounts.

### Messaging
- **[Messaging]** Include an unsubscribe link in every email and text message. Unsubscribing takes one click, requires no login and is honored immediately.
- **[Messaging]** If the service sends more than one type of message, provide a preferences page where users choose which types they still want, alongside an option to unsubscribe from all.
- **[Messaging]** Required transactional messages (receipts, password resets, security alerts) are not part of unsubscribe options.

### Don'ts
- Do not collect unnecessary data. Collect only what a feature requires.

## 11. Security

Before building any backend, authentication, session or data storage, read `references/supabase-security.md`.

### Default Backend
- **[Backend]** Use Supabase (Postgres) as the backend in most cases, unless the user specifies otherwise or the project requires something else.
- **[Backend]** Follow the Supabase security standards in `references/supabase-security.md`.
- **[Backend]** Logged-out visitors must have no access to any data that would normally require an account.
- When a different backend is used, apply the equivalent per-user authorization check on every query.

### Musts
- Require authentication and authorization on API endpoints to send a request or return data.
- Keep API keys and sensitive info on the server, and allow changes only through server-side access.
- Enforce server-side authority. The server makes the final decision on every action.
- Protect admin routes and any other permission-restricted content on the server, not only by hiding them in the UI.
- Add rate limiting and API limits wherever possible, strictest on login, sign-up, password reset and form submissions.
- Rate-limit every feature that connects to an external API or service (AI, email, SMS, payments, maps and similar), with per-user limits and an overall cap, staying within each provider's limits.
- Sanitize all user content and submissions to prevent cross-site scripting.
- Protect every state-changing request (create, update, delete, payments, settings changes) against cross-site request forgery. Use SameSite cookies together with CSRF tokens or Origin header verification on the server.
- **[Payments]** Verify the signature on every payment webhook and process each event only once.
- Encrypt sensitive data in transit and at rest, and lock record access.
- Hash passwords with Argon2id or bcrypt (Supabase Auth handles this by default).
- Set session cookies as HttpOnly, Secure and SameSite.
- Force HTTPS.
- **[Web]** Add security headers: Content-Security-Policy, Strict-Transport-Security, X-Content-Type-Options, Referrer-Policy, frame-ancestors and Permissions-Policy.

### Data Exposure
Never expose user data, auth tokens or anything from the application's secure database anywhere a user could find it, including:
- localStorage, sessionStorage or IndexedDB.
- URL parameters or query strings.
- Page source or JavaScript bundles.
- Console output.
- Cookies without the HttpOnly flag.
- Error messages.
- API responses that return more fields than the screen needs.

Local storage may hold only non-sensitive interface preferences, such as theme choice or a dismissed notice.

### Dependency and Integration Scanning
- Run the package manager's audit (such as `npm audit`). Fix every high or critical issue, and report any that cannot be fixed.
- Also treat these as high risk and fix or report them:
  - Secrets committed to code or config (scan with a tool such as Gitleaks).
  - Abandoned or unmaintained packages, and packages with suspicious install scripts or names resembling popular packages.
  - Third-party scripts loaded without Subresource Integrity.
  - Wildcard CORS (`*`) on authenticated endpoints.
  - Open redirects.
  - Public storage buckets holding user files.
  - OAuth or API permissions broader than the feature needs.
  - Webhooks without signature verification.
- Confirm every external API integration works and fails cleanly.

### Never Ship to Production
- Source maps (.map files), and builds configured to generate them.
- Exposed source directories, `.git`, `.env` files or server directory listings.
- `console.log`, `debugger` statements and verbose debug output.
- Test accounts, seed data, mock data and test API keys.
- Debug routes, test pages, Storybook and other development tools.
- Detailed error pages or stack traces.
- Development builds or unminified bundles.
- Hardcoded `localhost` URLs.
- Unfinished features reachable by users.
- Commented-out code containing credentials or internal details.

## 12. Performance and Reliability

### Musts
- Leave no fixable console errors behind.
- Handle failed requests and API timeouts cleanly on both frontend and backend.
- Retry only safe requests, with increasing delays and a maximum of three attempts. Then show a clear message with a manual retry option (see Section 7).
- Prevent memory leaks: clean up event listeners, timers, observers and pending requests when a component or page closes.
- **[Web]** Meet these targets: Lighthouse 90+ in Performance, Accessibility, Best Practices and SEO, and Core Web Vitals in the "good" range (LCP 2.5 s or less, INP 200 ms or less, CLS 0.1 or less).
- **[Accounts]** Manage sessions and idle users using the timeout table and logout rules in `references/supabase-security.md`. Private data must never be accessible after logout or session expiry.

### Do's
- Write efficient JS scripts and bundles.
- Optimize database queries and keep the database clean and organized.
- Cache repeat requests and handle them cleanly.
- Self-host fonts and assets where the platform allows. Otherwise, use the permitted source and note it in the delivery summary.
- Optimize performance as much as possible while maximizing quality across all features.
- Use the tools in `references/testing-tools.md` to test each area.
- Sentry is optional for production error monitoring. When used, configure it to strip personal data and list it in the privacy policy.
