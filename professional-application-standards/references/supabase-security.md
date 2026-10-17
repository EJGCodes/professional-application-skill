# Supabase, Authentication and Sessions

Read this before building any backend, authentication, session or data storage.

## Default Backend Standards

Use Supabase (Postgres) as the backend in most cases, unless the user specifies otherwise or the project requires something else. Follow these standard Supabase security practices:

- Enable row-level security on every table in an exposed schema, with policies that limit each user to their own rows (using `auth.uid()`).
- Give the `anon` role no access to any user data. Logged-out visitors must have no access to any data that would normally require an account.
- Use Supabase Auth for sign-up, login and sessions.
- The `anon` key may appear in the client only because RLS protects every table. The `service_role` key stays on the server and never reaches the client.
- Run privileged operations in Edge Functions or server-side code, never in the client.
- Keep user files in private storage buckets with access policies.
- Place `SECURITY DEFINER` functions in a non-exposed schema with a fixed `search_path`.
- Enforce idempotency for actions that must not run twice (for example, a unique constraint on an idempotency key column, or a database function that checks it).
- Run the Supabase Security Advisor and Performance Advisor before delivery and fix every issue they report.

When a different backend is used, apply the equivalent per-user authorization check on every query.

## Sessions and Storage

- Use cookie-based sessions with `@supabase/ssr` instead of the default localStorage session storage.
- Session cookies are HttpOnly, Secure and SameSite.
- Never store user data, auth tokens or anything from the secure database in localStorage, sessionStorage or IndexedDB. Local storage may hold only non-sensitive interface preferences, such as theme choice or a dismissed notice.
- In native apps, store tokens in the OS keychain or the platform's secure storage.

## Client-Side-Only Frontends

When the app has accounts, recommend a frontend with a server layer (Next.js, SvelteKit or Nuxt). If the user chooses a pure client-side frontend anyway (such as React with Vite):
- Route authentication through a small server-side function (such as a Supabase Edge Function) that sets HttpOnly session cookies.
- Never fall back to storing tokens or user data in browser storage.
- Note the tradeoff in the delivery summary.

## CSRF Protection

Protect every state-changing request (create, update, delete, payments, settings changes) against cross-site request forgery:
- Set session cookies with SameSite.
- Also verify a CSRF token or the request's Origin header on the server.

## Idle Timeouts

Apply idle timeouts by application type:

| Application type | Idle timeout | Maximum session |
|---|---|---|
| Financial, health, admin panels | 15 min | 12 hours |
| Business and productivity apps | 30 min | 24 hours |
| E-commerce and general consumer apps | 24 hours | 30 days |
| Creative and low-risk apps | 7 days | 30 days |

- Supabase's built-in inactivity timeout and session time-box are paid-plan features. Use them when available. Otherwise, enforce these timeouts in the application itself.
- Warn the user 2 minutes before an idle logout, and save their unsaved work as a draft.
- Require the user to re-enter their password before changing their password or email, deleting their account, or changing payment details, regardless of session age.

## Logout and Expiry

Private data must never be accessible after logout or session expiry:
- The server rejects every request from an expired session.
- Clear all in-memory and cached user data on logout.
- Send `Cache-Control: no-store` on private pages so the back button cannot show them after logout.
- Exclude private data from service worker caches.
