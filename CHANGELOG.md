# Changelog

## 1.1.0

### New
- Section 13: Web Compatibility and Delivery (browser support, no-JavaScript fallbacks, viewport, print styles, caching headers, favicon set and web manifest).
- Section 14: Accounts, Sign-In and Onboarding (email normalization, provider sign-in, password requirements, two-factor authentication, interactive onboarding, account section, data export, easy exit, security notifications).
- Reference files: `web-developer-checklist.md`, `writing.md`, `ux-patterns.md`, `forms-and-data.md`, `accounts-and-onboarding.md` and `legal-and-privacy.md`.
- Link behavior rules, clean URLs with no trailing slash or extensions, subdomain organization, JSON-LD structured data, Open Graph tags, humans.txt, security.txt, and 500 and 503 error pages.
- FAQ page recommendation.
- Input reference table, flexible input formats, data display formatting and backend data storage standards.
- Keyboard accessibility, landmarks, and screen reader support including JAWS.
- Strict CSP strategy, OWASP Top 10 coverage, email deliverability, analytics and offline rules.
- Account deletion 14-day grace period and legal record retention.
- Vercel as the default host.
- Delivery summary headings for "Open content placeholders" and "Builder launch tasks."
- `metadata.version` in the frontmatter and this changelog.

### Changed
- Public pages now require server rendering or static generation.
- Performance targets use the right measurement tool per page and platform; the SEO target applies only to indexable public pages.
- Official brand logos are allowed wherever they represent a third-party service.
- Monospace is allowed for codes, keys and IDs as well as code.
- Theme preference is stored in an essential cookie so server-rendered pages show the right theme with no flash.
- `supabase-security.md` is renamed to `security.md` and now holds all security rules; account rules moved to `accounts-and-onboarding.md`.
- SKILL.md now states the key rules for each section, with full details in the reference files.
- Description updated to cover SEO, sign-in and accounts.

## 1.0.0
- Initial release.
