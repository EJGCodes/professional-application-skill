# Security

Read this before building any backend, authentication, session or data storage.

## Default Backend: Supabase
Use Supabase (Postgres) in most cases, unless the user specifies otherwise or the project requires something else.
- Enable row-level security on every table in an exposed schema, with policies that limit each user to their own rows (using `auth.uid()`).
- Give the `anon` role no access to any user data. Logged-out visitors have no access to any data that would normally require an account.
- Use Supabase Auth for sign-up, sign-in and sessions (account rules in `accounts-and-onboarding.md`).
- The `anon` key may appear in the client only because RLS protects every table. The `service_role` key stays on the server.
- Run privileged operations in Edge Functions or server-side code, never in the client.
- Keep user files in private storage buckets with access policies.
- Place `SECURITY DEFINER` functions in a non-exposed schema with a fixed `search_path`.
- Enforce idempotency with a unique constraint on an idempotency key column (or a database function that checks it).
- Run the Supabase Security Advisor and Performance Advisor before delivery and fix every issue they report.

With a different backend, apply the equivalent per-user authorization check on every query.

## Server Rules
- Require authentication and authorization on API endpoints to send a request or return data.
- Keep API keys and sensitive info on the server, and allow changes only through server-side access.
- The server makes the final decision on every action.
- Protect admin routes and permission-restricted content on the server, not only by hiding them in the UI.
- Encrypt sensitive data in transit and at rest, and lock record access.
- Hash passwords with Argon2id or bcrypt (Supabase Auth does this by default).
- **[Payments]** Verify the signature on every payment webhook and process each event only once.

## Rate Limiting
- Rate-limit everything possible, strictest on sign-in, sign-up, password reset and form submissions.
- Rate-limit every feature that connects to an external API or service (AI, email, SMS, payments, maps and similar), with per-user limits and an overall cap, within each provider's limits.
- Sign-in and code-sending limits are in `accounts-and-onboarding.md` (brute-force protection).

## Sessions and Storage
- Use cookie-based sessions with `@supabase/ssr`, never the default localStorage session storage.
- Session cookies are HttpOnly, Secure and SameSite. Scope them to the exact subdomain that needs them.
- In native apps, store tokens in the OS keychain or platform secure storage.
- Browser storage (localStorage, sessionStorage, IndexedDB) holds only non-sensitive interface preferences.
- Drafts and onboarding progress for logged-in users save to the server. Drafts for logged-out users stay in memory only.
- Offline actions stay in memory until the connection returns.
- PWA offline caching covers only public pages and the app shell, never user data.

## Client-Only Frontends
When the app has accounts and the user chooses a client-only frontend (such as React with Vite):
- Route authentication through a small server-side function (such as a Supabase Edge Function) that sets HttpOnly session cookies.
- Never fall back to storing tokens or user data in browser storage.
- Note the tradeoff in the delivery summary.

## CSRF Protection
Protect every state-changing request (create, update, delete, payments, settings changes): SameSite session cookies, plus a CSRF token or Origin header check on the server.

## Data Exposure
Never expose user data, tokens or secure database content anywhere a user could find it:
- localStorage, sessionStorage or IndexedDB.
- URL parameters or query strings.
- Page source or JavaScript bundles.
- Console output.
- Cookies without the HttpOnly flag.
- Error messages.
- API responses that return more fields than the screen needs.

## Cross-Site Scripting
- Sanitize all user content and submissions.
- Encode output for its context (HTML, attribute, URL, JavaScript).
- Never use `innerHTML`, `dangerouslySetInnerHTML`, `v-html` or `eval` on user content. When user HTML or Markdown must be rendered, sanitize it with DOMPurify.
- Use Trusted Types where supported.
- Block `javascript:` URLs anywhere user input becomes a link.

## Content-Security-Policy
- Never allow `'unsafe-inline'` or `'unsafe-eval'` for scripts.
- Statically generated pages use a hash-based CSP, so they stay fully cacheable.
- Server-rendered dynamic pages use a nonce-based CSP, set in middleware so each response gets a fresh nonce.
- Allow `'unsafe-inline'` for styles only when the framework requires it, and note it in the delivery summary.
- Auth and payment provider scripts (Google and Apple sign-in, Stripe.js) must load from the provider's servers. They are allowed by name in the CSP, exempt from self-hosting and Subresource Integrity, and loaded only on the pages that use them.

## OWASP Top 10
- **Injection:** parameterized queries only, never string-built SQL.
- **Cross-site scripting:** see above.
- **Broken access control:** row-level security and server-side authorization checks.
- **Server-side request forgery:** block internal and private addresses in any feature that fetches a user-supplied URL.
- **Mass assignment:** the server accepts only the fields it expects.
- **Insecure deserialization:** never deserialize untrusted data into objects or code.
- **Clickjacking:** `frame-ancestors` in the CSP.
- **Vulnerable components:** dependency scanning (below).

## Dependency and Integration Scanning
- Run the package manager's audit (such as `npm audit`). Fix every high or critical issue, and report any that cannot be fixed.
- Also treat these as high risk and fix or report them:
  - Secrets committed to code or config (scan with Gitleaks).
  - Abandoned or unmaintained packages, and packages with suspicious install scripts or names resembling popular packages.
  - Third-party scripts loaded without Subresource Integrity (except the provider scripts above).
  - Wildcard CORS (`*`) on authenticated endpoints.
  - Open redirects.
  - Public storage buckets holding user files.
  - OAuth or API permissions broader than the feature needs.
  - Webhooks without signature verification.
- Confirm every external API integration works and fails cleanly.

## Never Ship to Production
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

## Idle Timeouts

| Application type | Idle timeout | Maximum session |
|---|---|---|
| Financial, health, admin panels | 15 min | 12 hours |
| Business and productivity apps | 30 min | 24 hours |
| E-commerce and general consumer apps | 24 hours | 30 days |
| Creative and low-risk apps | 7 days | 30 days |

- Supabase's built-in inactivity timeout and session time-box are paid-plan features. Use them when available; otherwise enforce these timeouts in the application.
- Warn the user 2 minutes before an idle logout, and save their unsaved work as a server-side draft.

## Logout and Expiry
Private data is never accessible after logout or session expiry:
- The server rejects every request from an expired session.
- Clear all in-memory and cached user data on logout.
- Send `Cache-Control: no-store` on private pages so the back button cannot show them.
- Exclude private data from service worker caches.
