# Legal and Privacy

Read this before building legal pages, cookie consent, deletion, messaging or analytics.

## Required Pages
- **[Data]** Privacy policy, terms of service and a data deletion request system.
- **[Web] [Data]** Cookie policy and consent banner whenever non-essential cookies or trackers are used. A site using only essential cookies does not show a banner.
- **[Payments]** Refund policy, and the full total (including taxes and fees) shown before the user commits to paying. No hidden fees.

## Legal Questions
At the start of the project, ask the builder whether they want to provide these details, so they don't have to fill them in manually later:
- Legal business name, address and contact email.
- Countries or regions where the site operates or has users.
- Third-party services that receive user data (payments, analytics, email, error monitoring and similar).
- Data retention periods.
- **[Payments]** Refund window, cancellation terms and dispute process.

If the builder does not answer, build with labeled placeholder fields and ask again after the first build is done.

## Legal Page Content
- Generate every legal page with complete structure and plain-language content, styled to match the site, with a dedicated print layout.
- Fill in only details confirmed by the builder or by the build itself (for example, naming Stripe if the build uses Stripe).
- Mark every remaining detail as a clearly labeled field, such as "[Company legal name]."
- List all open fields under "Open legal fields" in the delivery summary and recommend legal review before launch.
- Never invent business names, addresses, jurisdictions, retention periods or third-party services.

## Cookie Consent
- Show the banner as a non-blocking bar at the bottom of the screen, never a modal.
- Group non-essential cookies into categories (such as analytics, marketing and preferences), each with its own toggle. All are off by default.
- "Accept all," "Reject all" and "Save choices" have equal visual weight.
- Nothing non-essential loads before consent.
- Store the consent choice on the parent domain so it applies to every subdomain.
- Include a "Cookie settings" link in the footer so users can change their choices at any time.
- The cookie policy lists every cookie by name, purpose, category and duration.
- The theme preference cookie is essential, because the user explicitly chose it.

## Data Deletion
- **[Accounts]** Self-serve "Delete my account and data" in the account section.
- **[Data]** A deletion request form for people without accounts.
- Account deletion takes effect after a 14-day grace period. Signing back in during that period cancels it. The confirmation states the exact date deletion completes.
- Delete everything except legally required records (such as invoices kept for tax purposes), which are kept with personal details removed. State this on the deletion confirmation and in the privacy policy.
- Deletion follows the easy-exit rules in `accounts-and-onboarding.md`.

## Messaging
- **[Messaging]** Every email and text includes an unsubscribe link. Unsubscribing takes one click, requires no login and is honored immediately.
- **[Messaging]** When more than one message type is sent, provide a preferences page where users choose which types they still want, alongside an option to unsubscribe from all.
- Required transactional messages (receipts, password resets, verification, security alerts) are not part of unsubscribe options.

## Email Deliverability
**[Accounts] [Messaging]** Configure a production email system that reliably delivers password resets, email confirmations, sign-in links and security alerts:
- Use a transactional email provider (such as Resend, Postmark or Amazon SES) through custom SMTP. Supabase's built-in email is rate-limited and meant only for development.
- Send from a dedicated subdomain (such as `mail.` or `notify.`).
- Add SPF, DKIM and DMARC records (start DMARC at `p=none` and tighten after monitoring).
- Keep transactional and marketing email on separate streams so marketing problems can't block account emails.
- Email templates follow the design and writing rules in this skill.

## Analytics
- Add analytics only when they are necessary to the site or improve it.
- Prefer privacy-friendly analytics that don't need cookie consent (such as Plausible or Fathom), and list them in the privacy policy.
- Use Google Analytics only when the user asks for it, and only behind the cookie consent categories.
- Sentry is optional for error monitoring. When used, configure it to strip personal data and list it in the privacy policy.

## Data Collection
Collect only what a feature requires.
