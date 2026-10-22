# Forms and Data

Read this before building any form, input, data display or database schema.

## Input Reference

| Field | `type` | `inputmode` | `autocomplete` | `enterkeyhint` |
|---|---|---|---|---|
| Email | email | | email | next |
| Phone | tel | | tel | next |
| Website | url | | url | next |
| Full name | text | | name | next |
| First / last name | text | | given-name / family-name | next |
| Street address | text | | address-line1 | next |
| Postal code (US only) | text | numeric | postal-code | next |
| Postal code (international) | text | | postal-code | next |
| Card number | text | numeric | cc-number | next |
| Card expiry | text | numeric | cc-exp | next |
| Card security code | text | numeric | cc-csc | next |
| One-time code | text | numeric | one-time-code | done |
| Quantity or age | number | | | next |
| Birthday | date | | bday | next |
| Search | search | | off | search |
| Username | text | | username | next |
| New password | password | | new-password | done |
| Current password | password | | current-password | go |

- The last field in a form uses `enterkeyhint="send"`, `"go"` or `"done"` to match its action.
- Never use `type="number"` for digit-only values that aren't quantities (ZIP codes, card numbers, phone numbers).
- Every field has a visible label. Placeholder text never replaces a label.
- Input and textarea text is never smaller than 16px (smaller text makes iPhones zoom the page on focus).

## Flexible Input Formats
Accept every correct format, then normalize on the server.

| Field | Accepted examples | Stored as |
|---|---|---|
| Phone | (555) 123-4567, 555-123-4567, 555.123.4567, 555 123 4567, +1 555 123 4567 | E.164 (+15551234567), parsed with libphonenumber-js or similar |
| Card number | 4242 4242 4242 4242, 4242424242424242 | Never stored by the app; handled by the payment provider |
| Email | " Name@Example.com " | See email storage in `accounts-and-onboarding.md` |
| Dates typed as text | 10/20/2026, 2026-10-20, Oct 20 2026 (following the user's locale) | ISO 8601 |
| Postal code | 12345, 12345-6789, "sw1a 1aa" | Uppercased and trimmed for the country |

- Format values for display after the user leaves the field, not while typing.
- If a field formats while typing, Backspace must still remove exactly one character.

## Validation
- Validate each field when the user leaves it. Once an error shows, re-check live as the user types to fix it.
- Never show errors on fields the user hasn't touched.
- Password fields validate on every keystroke, with the requirement checklist underneath (requirements in `accounts-and-onboarding.md`) and a show/hide toggle.
- Validate on the server as well. Client validation is only for fast feedback.

## Search
- Results appear 300 ms after the last keypress.
- Pressing Enter searches immediately and cancels any pending delayed search.

## Dates
- Use the native date input for simple dates.
- Use a custom picker only for ranges or bookings, and it must be fully keyboard and screen reader accessible.

## Age and Birthday
- **[Accounts]** Collect age at sign-up, or a full birthday for apps handling sensitive data (health, financial, precise location, government ID, or anything involving minors).
- The minimum age follows the regions the builder gives in the legal questions (some regions set the age of digital consent at up to 16). Default to 13 when no region is known.
- Sign-up methods that skip the field (such as Google) collect it as the first onboarding step, and the app stays locked until it is provided.

## Uploads
- **[Uploads]** Enforce a file size limit (10 MB per file unless specified).
- Check file format and size in the browser for fast feedback, then again on the server to block dangerous files.

## Data Display
- Format dates, numbers and currency with the `Intl` APIs in the user's locale.
- Never show ambiguous dates such as 10/11/26. Write "Oct 11, 2026" or follow the user's locale.
- Show currency with its symbol or code.
- Put machine-readable values in `<time datetime>` and `<data value>`.
- Right-align numeric table columns and use tabular figures.
- Use one display format for each data type across the whole application.

## Data Storage
Backend and database formatting must be as clean as the frontend.
- Store timestamps as `timestamptz` in UTC. Convert to the user's time zone only for display.
- Store money as integer minor units (cents) or `numeric`, always with a currency code. Never as floating point.
- Store phone numbers in E.164.
- Use consistent `snake_case` names for tables and columns.
- Use foreign keys, `NOT NULL`, `CHECK` and unique constraints so invalid data cannot be saved.
- Use enums or lookup tables for fixed values such as statuses.
- Make every schema change through a versioned migration.
- API responses use one consistent JSON shape across all endpoints, with ISO 8601 dates and no fields the screen doesn't need.
