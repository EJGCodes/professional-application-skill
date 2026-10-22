# Verification Checklist

Run every applicable check before delivering a build. Skip checks whose applicability tag does not apply, and skip [Web] checks for native apps (use the platform equivalents in `testing-tools.md`).

Use Playwright where available, running visual and interaction checks in Chromium, Firefox and WebKit. Where no browser is available, run the static checks and list the rest under "Unverified checks" in the delivery summary. Never report an unrun check as passed.

## 1. Color and Visual Style
- Search all CSS for `box-shadow`, `text-shadow`, `drop-shadow(`, `linear-gradient(`, `radial-gradient(` and `conic-gradient(`. Expect zero results.
- Search for colored `border-left` or `border-inline-start` rules on any element. Expect zero.
- List every color token. Confirm one accent hue plus its shades, with all remaining colors being neutrals, semantic status colors or official brand colors on provider buttons and brand logos.
- Review each badge and chip. Remove any that do not tell the user something they need, including chips holding only step text.
- Confirm all corner radii come from the defined radius scale.

## 2. Typography
- Search all `font-family` declarations and font files for every banned font name in `fonts.md`. Expect zero results.
- Confirm no more than two typefaces are loaded, and monospace appears only on code, codes, keys and IDs.
- Search the markup for `<em>`, `<i>` and `font-style: italic`. Confirm each is a title of a work, a foreign term or a quotation.
- Check every heading for subtext or eyebrow labels. Remove any that do not add unique information.
- Take screenshots at each test width and look for single words stranded on their own line.

## 3. Layout and Responsiveness
- At 320, 375, 768, 1024, 1440 and 1920 px, run `document.documentElement.scrollWidth <= document.documentElement.clientWidth`. Expect true.
- Screenshot at each test width and while resizing. Check alignment, spacing consistency and long-text handling.
- At mobile and narrow widths, confirm tables render as cards with the same fields in the same order as the table headers.
- In mobile emulation, focus each input, reduce the visual viewport height to simulate the keyboard, and confirm the input stays visible, nothing overlaps it, and Cumulative Layout Shift stays below 0.1.

## 4. Icons, Images and Media
- Search markup, CSS and package files for Lucide, Feather, Heroicons and other non-approved icon sets, and for emoji characters used as icons. Expect zero results.
- Confirm only one icon set is loaded and it matches the project type. Brand logos use official brand assets.
- List every image and media file with its source. Confirm each is user-provided or unlicensed stock, and none is AI-generated unless requested.
- Confirm images use WebP or AVIF, have `srcset`, `width` and `height`, and below-the-fold images use `loading="lazy"`. Flag any single image over 200 KB.
- Confirm no unconverted GIF is over 200 KB, and converted GIF videos are muted and pause with reduced motion.
- Confirm videos have a poster image and captions.
- Confirm every chart is bound to real data. Remove any decorative or growth-suggesting bar sequence.

## 5. Motion, Loading and Interaction
- Search CSS keyframes and transitions for animated `top`, `left`, `right`, `bottom`, `width`, `height` or `margin`. Expect zero.
- Confirm a `prefers-reduced-motion` media query exists and disables non-essential motion.
- Search for any fixed or sticky element at the top of the page under 8 px tall spanning the width. Expect zero.
- Throttle the network and load each page. Confirm skeletons match the size of the content that replaces them, loaders disappear on success or failure, and already-loaded content stays usable.
- Double-click every action button. Confirm only one network request and one resulting record per action.
- Intercept and fail each action's request. Confirm the UI rolls back, the user's input is preserved, and a clear message appears.
- Confirm payment and delete actions do not update the UI until the server responds.
- Type into every masked or formatted field, press Backspace, and confirm exactly one character is removed.
- Add several chips to each chip input, press Backspace on the empty input, and confirm only one chip is removed.
- Measure every interactive element outside running text. Confirm each is at least 44×44 px.
- Confirm hover, pressed, focus-visible, disabled and loading states all render.
- Edit a form, navigate away, and confirm an unsaved-changes warning appears.
- Confirm all opt-in checkboxes default to unchecked, and Accept/Reject or Confirm/Decline buttons have equal visual weight.
- Load each page fresh. Confirm nothing appears except the allowed notices in `ux-patterns.md`, in their defined form.
- Paste into every field, including passwords. Confirm paste works.
- Go offline mid-action. Confirm the offline notice appears and the action is kept in memory and retried when the connection returns.

## 6. Forms and Input
- Confirm every field matches the input reference table in `forms-and-data.md`, has a visible label, and has a computed font size of at least 16px.
- Tab past an untouched field without typing. Confirm no error appears.
- Enter invalid input, leave the field, confirm an error appears, then fix it and confirm the error clears while typing.
- Enter a phone number in each accepted format. Confirm all are accepted and stored in the same E.164 format.
- Type a search query and stop. Confirm exactly one request fires about 300 ms after the last keypress. Press Enter on a new query and confirm it fires at once with no delayed duplicate.
- **[Accounts]** Submit sign-up with an age below the minimum. Confirm it is rejected with a clear message.
- **[Uploads]** Upload a file over the limit and a disallowed type through the UI, then send both directly to the server. Confirm all four are rejected.

## 7. Writing and Content
- Search all visible text, code comments, READMEs, email templates and legal pages for `—`, `–` and ` - ` used as dashes. Expect zero.
- Search the same content for every term on the cliché list in `writing.md`. Expect zero.
- List every button and link label. Confirm each states a specific action or outcome and none matches the banned CTA list.
- Force each error state and read the message. Confirm it names the cause and a specific next step (except the generic account-privacy messages).
- Search for testimonials, statistics, user counts and logos. Confirm each is real or a clearly marked placeholder listed in the delivery summary.
- Confirm dates, numbers and currency are formatted with `Intl` and no ambiguous dates appear.
- **[Backend]** Review the schema. Confirm UTC `timestamptz` dates, no floating-point money, consistent naming, constraints, and migrations for every change.

## 8. Navigation, Structure and Search
- Run a link checker on every internal and external link. Expect zero broken links and zero redirect chains.
- Confirm external links open in a new tab, links to non-function pages open in a new tab only from inside a task, and all other internal links open in the same tab. Every new-tab link has `rel="noopener noreferrer"` and a visible indicator.
- At mobile widths, open and close the navbar and confirm every item is reachable.
- Click the logo logged out and logged in. Confirm it goes to home and dashboard respectively (or home, when the app lives on a subdomain).
- Confirm the footer year is generated from the current date.
- Request a nonexistent URL and confirm the custom 404 page with a 404 status. Trigger a server error and confirm the 500 page.
- Confirm every page has a unique title in the "Site Name - Page Name" format.
- **[Web]** Confirm no page URL shows a file extension or trailing slash, and that the www variant, trailing slash and extension URLs each 301-redirect in one step to the canonical URL.
- **[Web]** Confirm every page has a canonical tag and an accurate meta description within the length limits.
- **[Web] [Public]** Fetch each public page's raw HTML without running JavaScript. Confirm the main content and links are present.
- **[Web] [Public]** Run every page through the Rich Results Test or Schema Markup Validator. Expect zero errors and no placeholder values.
- **[Web] [Public]** Confirm every page has the full Open Graph and Twitter Card set. For shareable items, confirm tags come from the item, preview images are 1200×630, and private items fall back to generic tags.
- **[Web] [Public]** Confirm sitemap.xml lists every public page and no private ones, robots.txt blocks private routes and points to the sitemap, and humans.txt exists and is linked.
- **[Web]** If a security contact was confirmed, confirm /.well-known/security.txt has valid `Contact` and `Expires` fields.
- **[Web]** For multilingual sites, confirm `hreflang` tags and a `lang` attribute on every page.

## 9. Accessibility and Theming
- Run axe-core on every page in light mode, dark mode and high-contrast mode. Expect zero violations.
- Complete every main flow using only the keyboard. Confirm nothing is unreachable, tab order matches visual order, there are no keyboard traps, focus returns after closing modals, and Escape closes menus and modals.
- Confirm the skip link appears first and every focusable element shows a visible outline.
- Confirm every page has at least one `<h1>`, no skipped heading levels, and a `lang` attribute.
- Confirm every `<img>` has an `alt` attribute.
- **[Web]** Confirm the accessibility tree shows the expected landmarks, exactly one `<main>`, and every content element inside a landmark.
- **[Web]** Run the W3C Nu HTML Checker on every page. Expect zero errors.
- Zoom to 400% at 1280 px width. Confirm content reflows without loss or horizontal scrolling.
- Run a colorblindness simulation. Confirm no information is lost.
- Emulate `prefers-reduced-motion`, `prefers-contrast` and forced colors. Confirm the site adapts automatically.
- Load the site fresh with the device set to dark mode. Confirm it opens in light mode. Switch to dark mode, reload, and confirm the server renders dark mode with no flash.
- Toggle every theme and accessibility option. Screenshot each and confirm no broken layout or styling.

## 10. Legal, Privacy and Compliance
- Confirm the builder was asked for legal details at the project start, and asked again after the first build if they did not answer.
- Search legal pages for open fields. Confirm each is listed in the delivery summary and no invented details appear.
- **[Web] [Data]** Load the site fresh and confirm no non-essential cookie or tracker is set before consent.
- **[Web] [Data]** Enable one cookie category, save, and confirm only that category's cookies load. Visit another subdomain and confirm the choice carries over.
- **[Web] [Data]** Confirm the footer "Cookie settings" link reopens the preferences.
- **[Accounts]** Delete a test account. Confirm the confirmation shows the completion date, signing in during the grace period cancels deletion, and after deletion only legally required records remain, with personal details removed.
- **[Messaging]** Click an unsubscribe link while logged out. Confirm it works in one click. Opt out of one message type and confirm others still send.
- **[Accounts]** Trigger a password reset and email confirmation. Confirm both arrive through the production email provider.
- **[Payments]** Confirm the final total shown before payment matches the amount charged.

## 11. Security
- **[Backend]** Run the Supabase Security Advisor. Expect zero issues.
- **[Backend]** Query every user-data table with the anon key while logged out. Expect zero rows.
- **[Backend]** Log in as user A and request user B's records through the API. Expect zero rows or an authorization error.
- Search the client bundle for `service_role`, API secrets and private keys. Expect zero.
- Request every admin route and API endpoint without authentication. Expect rejection.
- Exceed the rate limit on sign-in, code sending and each external-API feature. Confirm requests are slowed or blocked with a clear message.
- Submit `<script>alert(1)</script>`, `javascript:` URLs and similar payloads in every input. Confirm they render as plain text or are blocked.
- Submit a state-changing request from a different origin, and one with a missing or invalid CSRF token. Confirm the server rejects both.
- **[Payments]** Send a webhook with an invalid signature and replay a valid one. Confirm both are rejected.
- Inspect cookies and confirm session cookies are HttpOnly, Secure, SameSite and scoped to the right subdomain.
- Inspect localStorage, sessionStorage and IndexedDB while logged in. Confirm only interface preferences are stored.
- Check URLs, page source, console output, error messages and API responses for user data, tokens or unneeded fields. Expect none.
- **[Web]** Confirm the CSP has no `'unsafe-inline'` or `'unsafe-eval'` for scripts, static pages use hashes, and dynamic pages use nonces.
- **[Web]** Check headers with Mozilla HTTP Observatory. Confirm all required headers are present and no `X-Powered-By` or versioned `Server` header appears.
- **[Web]** Complete each provider sign-in and payment flow. Confirm the Cross-Origin-Opener-Policy does not break it.
- Run `npm audit` and Gitleaks. Expect zero high or critical issues.
- Search the production build for `.map` files, `console.log`, `debugger`, `localhost`, test keys and seed data. Expect zero.
- **[Web]** Request `/.git/`, `/.env` and common directory paths on the deployed site. Expect 404 or 403.

## 12. Performance and Reliability
- Open the console on every page and through every main flow. Expect zero errors.
- **[Web]** Run PageSpeed Insights (public pages) or Lighthouse (other pages) for mobile and desktop. Confirm Performance, Accessibility and Best Practices are 90+ everywhere, SEO is 90+ on indexable public pages, and Core Web Vitals pass.
- **[Web]** Measure first-party initial JavaScript. Confirm it is at or under 170 KB compressed.
- Throttle the network and force request failures. Confirm retries stop at three and a clear message with a retry option appears.
- Take heap snapshots before and after opening and closing each major view several times. Confirm memory returns to baseline.
- If Sentry is used, trigger a test error and confirm the captured event contains no personal data.
- **[Accounts]** Sit idle past the warning time. Confirm the warning appears and a server-side draft is saved.
- **[Accounts]** Log out, press the back button, and confirm no private page or data appears.
- **[Accounts]** Reuse an expired session token against the API. Expect rejection.

## 13. Web Compatibility and Delivery
- Run the Playwright checks in Chromium, Firefox and WebKit.
- **[Public]** Disable JavaScript and load each public page. Confirm core content and navigation show with clean formatting.
- Confirm the viewport meta tag is present on every page and does not disable zoom.
- Emulate print media on each page and save a PDF. Confirm hidden elements leave no gaps, formatting stays consistent, and dedicated print layouts render correctly.
- Request each page and a hashed asset twice with `curl`. Confirm caching headers match the table, ETags return 304 on the second request, and responses are Brotli-compressed.
- Confirm the full favicon set and web manifest exist and load.

## 14. Accounts, Sign-In and Onboarding
- Sign up with "Name@Example.com", then try "name@example.com". Confirm the second is treated as the same account and the response does not reveal that the account exists.
- Try signing in with a wrong password and resetting the password for an unregistered email. Confirm both messages are generic.
- Sign up with email, then sign in with Google using the same verified email. Confirm it lands in the same account.
- Sign up with Google. Confirm age is collected as the first onboarding step and the app stays locked until it is given.
- Confirm sign-up shows terms and privacy links (including next to provider buttons) and an unchecked marketing opt-in.
- Confirm every provider button follows its brand guidelines and all share one size and layout.
- Enter passwords that miss each requirement and a known breached password. Confirm each is rejected and the checklist updates on every keystroke.
- Try to disconnect the last sign-in method. Confirm it is blocked.
- Enable each two-factor method. Confirm sign-in requires it, recovery codes work only once, and "Trust this device" is absent where it should be.
- Complete onboarding, and leave halfway through on a second account and return. Confirm progress resumes from the server and every step involves a real action.
- Before verifying an email, confirm the app opens with an inline reminder and that messaging, payments and sensitive features stay locked.
- Change the email and password. Confirm each requires the password, the old address gets a notification, other sessions are signed out after the password change, and a security email is sent.
- Download the user's data. Confirm the file includes everything stored about the user and no other users' personal data.
- Count the steps to cancel, delete the account and request data deletion. Confirm each is no more than sign-up took (excluding one re-authentication and one confirmation) and none requires contacting support.
