# Verification Checklist

Run every applicable check before delivering a build. Skip checks whose applicability tag does not apply, and skip **[Web]** checks for native apps (use the platform equivalents in `testing-tools.md`).

Use Playwright or another headless browser where available. Where none is available, run the static checks and list the visual checks under "Unverified checks" in the delivery summary. Never report an unrun check as passed.

## Color and Visual Style
- Search all CSS for `box-shadow`, `text-shadow`, `drop-shadow(`, `linear-gradient(`, `radial-gradient(` and `conic-gradient(`. Expect zero results.
- Search for colored `border-left` or `border-inline-start` rules on any element. Expect zero.
- List every color token. Confirm one accent hue plus its shades, with all remaining colors being neutrals or semantic status colors.
- Review each badge and chip. Remove any that do not tell the user something they need.
- Confirm all corner radii come from the defined radius scale.

## Typography
- Search all `font-family` declarations and font files for every banned font name in `fonts.md`. Expect zero results.
- Confirm no more than two typefaces are loaded.
- Search the markup for `<em>`, `<i>` and `font-style: italic`. Confirm each is a title of a work, a foreign term or a quotation.
- Check every heading for subtext or eyebrow labels. Remove any that do not add unique information.
- Take screenshots at each test width and look for single words stranded on their own line.

## Layout and Responsiveness
- At 320, 375, 768, 1024, 1440 and 1920 px, run `document.documentElement.scrollWidth <= document.documentElement.clientWidth` in the browser. Expect true.
- Screenshot at each test width and while resizing. Check alignment, spacing consistency and long-text handling.
- At mobile and narrow widths, confirm tables render as cards with the same fields in the same order as the table headers.
- In mobile emulation, focus each input, simulate the keyboard by reducing the visual viewport height, and confirm the input remains visible, no fixed element overlaps it, and the Cumulative Layout Shift score stays below 0.1.

## Icons, Images and Media
- Search markup, CSS and package files for Lucide, Feather, Heroicons and other non-approved icon sets, and for emoji characters used as icons. Expect zero results.
- Confirm only one icon set (Material Symbols or Font Awesome) is loaded, and that it matches the project type.
- List every image and media file with its source. Confirm each is user-provided or unlicensed stock, and none is AI-generated unless requested.
- Confirm images use WebP or AVIF, have `srcset`, and below-the-fold images use `loading="lazy"`. Flag any single image over 200 KB.
- Confirm every chart is bound to real data. Remove any decorative or growth-suggesting bar sequence.
- **[Public]** Confirm an `og:image` meta tag exists and the image loads.

## Motion, Loading and Interaction
- Search CSS keyframes and transitions for animated `top`, `left`, `right`, `bottom`, `width`, `height` or `margin`. Expect zero; movement uses `transform`.
- Confirm a `prefers-reduced-motion` media query exists and disables non-essential motion.
- Search for any fixed or sticky element at the top of the page under 8 px tall spanning the width. Expect zero.
- Throttle the network and load each page. Confirm skeletons match the size of the content that replaces them (no layout shift), loaders disappear on success or failure, and already-loaded content stays usable.
- Double-click every action button in the browser. Confirm only one network request and one resulting record per action.
- Intercept and fail each action's request. Confirm the UI rolls back, the user's input is preserved, and a clear message appears.
- Confirm payment and delete actions do not update the UI until the server responds.
- Type into every masked or formatted field, press Backspace, and confirm exactly one character is removed.
- Add several chips to each chip input, press Backspace on the empty input, and confirm only one chip is removed.
- Measure the bounding box of every interactive element. Confirm each is at least 44×44 px.
- Tab through every interactive element and confirm hover, pressed, focus-visible, disabled and loading states all render.
- Edit a form, navigate away, and confirm an unsaved-changes warning appears.
- Confirm all opt-in checkboxes default to unchecked, and Accept/Reject or Confirm/Decline buttons have equal visual weight.
- Load each page fresh and confirm no popup, modal, permission prompt or auto-playing audio appears. The cookie banner, if present, must be a non-blocking bottom bar.
- Paste into every field, including passwords. Confirm paste works.

## Forms and Input
- Tab past an untouched field without typing. Confirm no error appears.
- Enter invalid input, leave the field, confirm an error appears, then fix it and confirm the error clears while typing.
- Type a password character by character. Confirm the requirement checklist updates on every keystroke.
- Confirm every input has the correct `type`, `inputmode` and `autocomplete` attributes, and a computed font size of at least 16px.
- Type a search query and stop. Confirm exactly one request fires about 300 ms after the last keypress.
- Type a query and press Enter immediately. Confirm the search fires at once and no delayed duplicate follows.
- **[Accounts]** Submit sign-up with an age below the minimum. Confirm it is rejected with a clear message.
- **[Uploads]** Upload a file over the limit and a file of a disallowed type through the UI, then send both directly to the server bypassing the UI. Confirm all four are rejected.

## Writing and Content
- Search all visible text, code comments, READMEs, email templates and legal pages for `—`, `–` and ` - ` used as dashes. Expect zero.
- Search the same content for every term on the cliché list in SKILL.md Section 7. Expect zero.
- List every button and link label. Confirm each states a specific action or outcome and none matches the banned CTA list.
- Force each error state and read the message. Confirm it names the cause and a specific next step.
- Search for testimonials, statistics, user counts and logos. Confirm each is real or a clearly marked placeholder.

## Navigation, Structure and SEO
- Crawl every internal link and confirm each returns a valid page matching its link text.
- At mobile widths, open and close the navbar and confirm every item is reachable.
- Click the logo logged out and logged in. Confirm it goes to home and dashboard respectively.
- Confirm the footer year is generated from the current date, not hardcoded.
- Visit a nonexistent URL and confirm the custom 404 page renders with a link home and navigation or search.
- Confirm every page has a unique title in the "Site Name - Page Name" format.
- Confirm an SVG favicon and an Apple touch icon exist and load.
- **[Web]** Confirm every page has an accurate meta description.
- **[Web] [Public]** Confirm sitemap.xml lists every public page and no private ones.
- **[Web]** Confirm robots.txt blocks private, account and admin routes.

## Accessibility and Theming
- Run axe-core on every page in light mode, dark mode and high-contrast mode. Expect zero violations.
- Tab through every page. Confirm the skip link appears first and every element shows a visible outline.
- Confirm every `<img>` has an `alt` attribute and every page has a `lang` attribute.
- Run a colorblindness simulation. Confirm no information is lost.
- Load the site fresh with the device set to dark mode. Confirm it still opens in light mode. Switch to dark mode, reload, and confirm the choice persists.
- Emulate `prefers-reduced-motion`, `prefers-contrast` and forced colors. Confirm the site adapts automatically.
- Toggle every theme and accessibility option. Screenshot each and confirm no broken layout or styling.

## Legal, Privacy and Compliance
- Confirm the builder was asked for legal details at the project start, and asked again after the first build if they did not answer.
- Search legal pages for open fields. Confirm each is listed in the delivery summary and no invented details appear.
- **[Web] [Data]** Load the site fresh and confirm no non-essential cookie or tracker is set before consent.
- **[Web] [Data]** Enable one cookie category, save, and confirm only that category's cookies load.
- **[Web] [Data]** Confirm the footer "Cookie settings" link reopens the preferences.
- **[Accounts]** Delete a test account and confirm all of its data is removed.
- **[Messaging]** Click an unsubscribe link while logged out. Confirm it works in one click.
- **[Messaging]** Opt out of one message type and confirm others still send.
- **[Payments]** Confirm the final total shown before payment matches the amount charged.

## Security
- **[Backend]** Run the Supabase Security Advisor. Expect zero issues.
- **[Backend]** Query every user-data table with the anon key while logged out. Expect zero rows.
- **[Backend]** Log in as user A and request user B's records through the API. Expect zero rows or an authorization error.
- Search the client bundle for `service_role`, API secrets and private keys. Expect zero.
- Request every admin route and API endpoint without authentication. Expect rejection.
- Exceed the rate limit on login and on each external-API feature. Confirm requests are blocked with a clear message.
- Submit `<script>alert(1)</script>` and similar payloads in every input. Confirm they render as plain text.
- Submit a state-changing request from a different origin using the logged-in user's cookies. Confirm the server rejects it.
- Submit a state-changing request with a missing or invalid CSRF token. Confirm the server rejects it.
- **[Payments]** Send a webhook with an invalid signature and replay a valid one. Confirm both are rejected.
- Inspect cookies and confirm session cookies are HttpOnly, Secure and SameSite.
- Inspect localStorage, sessionStorage and IndexedDB while logged in. Confirm only interface preferences are stored.
- Check URLs, page source, console output, error messages and API responses for user data, tokens or fields the screen does not need. Expect none.
- **[Web]** Check headers with Mozilla HTTP Observatory. Confirm all required headers are present.
- Run `npm audit` and Gitleaks. Expect zero high or critical issues.
- Search the production build for `.map` files, `console.log`, `debugger`, `localhost`, test keys and seed data. Expect zero.
- **[Web]** Request `/.git/`, `/.env` and common directory paths on the deployed site. Expect 404 or 403.

## Performance and Reliability
- Open the console on every page and through every main flow. Expect zero errors.
- **[Web]** Run Lighthouse on every main page. Confirm all four scores are 90+ and Core Web Vitals pass.
- Throttle the network and force request failures. Confirm retries stop at three and a clear message with a retry option appears.
- Take heap snapshots before and after opening and closing each major view several times. Confirm memory returns to baseline.
- If Sentry is used, trigger a test error and confirm the captured event contains no personal data.
- **[Accounts]** Sit idle past the warning time. Confirm the warning appears and a draft is saved.
- **[Accounts]** Log out, press the back button, and confirm no private page or data appears.
- **[Accounts]** Reuse an expired session token against the API. Expect rejection.
