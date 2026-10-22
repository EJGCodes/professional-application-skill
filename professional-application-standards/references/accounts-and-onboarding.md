# Accounts and Onboarding

Read this before building sign-up, sign-in, onboarding or account pages. Every rule here applies to [Accounts] builds.

## Email Normalization
- Store two columns: `email` (as entered, trimmed, Unicode NFC-normalized) for sending, and `email_normalized` (fully lowercased, unique) for lookups.
- Look up accounts by `email_normalized` on sign-in, sign-up and password reset.
- Never strip Gmail dots or `+tags` by default. In apps where repeat sign-ups are abused (free trials, referral rewards, giveaways), also store a duplicate-detection key with dots and `+tags` removed, and check it on sign-up.
- Changing an email requires the password and a confirmation link sent to the new address. The old address gets a notification with a way to undo the change.

## Sign-In Methods
- Always offer email and password. Also offer phone number and password when an SMS provider is configured (phone numbers stored in E.164).
- Offer these providers through Supabase Auth:

| Provider | When |
|---|---|
| Google | Every app with accounts |
| Apple | Whenever an iOS app offers any other third-party sign-in; recommended for consumer apps |
| Microsoft | Business and productivity apps |
| GitHub | Developer tools |
| Discord | Gaming and community apps |

- Prefer redirect-based provider sign-in. Pages that need a popup flow use `Cross-Origin-Opener-Policy: same-origin-allow-popups`.
- Request only email and profile scopes unless a feature needs more.
- Enable automatic identity linking for verified emails, so a provider sign-in with a matching verified email lands in the existing account.
- In native apps, use each platform's native provider sign-in flow.

## Provider Buttons
- Use each provider's official logo, colors and required wording (such as "Continue with Google"), following the Google Identity branding guidelines and Apple's Human Interface Guidelines. This is an exception to the icon set and single-accent-color rules.
- All provider buttons share the same size and layout, and none is styled to look more important than the others.

## Passwords
- At least 12 characters, with a maximum of at least 64.
- At least one capital letter, one number and one symbol.
- Checked against known breached passwords (Supabase leaked password protection, or the Have I Been Pwned range API).
- All characters allowed, paste always allowed, and no forced periodic changes.
- The checklist under the field shows each requirement, including "Not found in known data breaches," updating on every keystroke.

## Account Privacy in Messages
These flows never reveal whether an account exists:
- **Sign-in:** "Email or password is incorrect."
- **Password reset:** "If an account exists for that email, we sent a reset link."
- **Sign-up with a registered email:** show the normal "Check your email" screen. The email says "You already have an account" with a sign-in link.

## Brute-Force Protection
- Slow down repeated failed sign-ins with increasing delays per account and per IP address. Never lock accounts outright.
- Apply strict per-recipient and per-country limits to text message codes and per-address limits to email codes, to block fraud and runaway sending costs.

## Two-Factor Authentication
- Offer it in every app with accounts, supporting authenticator app codes, text message codes, email codes and passkeys.
- Require it for admins, and for every user in apps handling sensitive data.
- Authenticator codes and text message codes: Supabase Auth MFA. Email codes and passkeys: Supabase Auth where supported, otherwise a well-maintained library (such as SimpleWebAuthn for passkeys).
- Users can register more than one method, and get one-time recovery codes when they first enable it. Recovery codes are shown once, stored hashed, and each works only once.
- Offer "Trust this device for 30 days," except in apps handling sensitive data and for admins.

## Sign-Up
- Show "By creating an account, you agree to the Terms of Service and Privacy Policy" with working links (opening in a new tab, since they are inside a task), including next to provider buttons.
- Marketing opt-in is a separate, unchecked checkbox.
- Collect age or birthday (see `forms-and-data.md`). Provider sign-ups collect it as the first onboarding step.

## Email Verification
- Users can enter the app and start onboarding before verifying their email, with an inline reminder banner.
- Messaging other users, payments and sensitive features stay locked until the email is verified.
- Apps handling sensitive data require verification before any access.

## Onboarding
- Add multi-step onboarding only when the app needs setup information or its first use isn't obvious. Never pad it with unnecessary steps.
- Onboarding is interactive: users do real tasks (such as creating their first item, or choosing settings with a live preview), never just click through slides.
- It runs right after sign-up and asks only for what the app needs to work. Optional steps can be skipped ("Skip for now").
- Show a determinate progress bar within the content, with the step count inside the progress component.
- Step buttons name the next step or action ("Next: Choose your workspace," "Save and continue").
- Save progress on the server so a user who leaves resumes where they stopped.
- End with one specific next action (such as "Create your first project").
- After onboarding, guide users with inline help and empty states that explain the first action. Guided tours start only when the user chooses.

## Account Section
A dedicated account area (such as `/account`; a settings screen in native apps), reachable from the user menu on every page. Include each area only when the app uses that feature:
- **Profile:** name, avatar and email.
- **Security:** password, connected sign-in providers, two-factor methods, passkeys, trusted devices, and active sessions with "Sign out of all other devices."
- **Notifications:** message preferences (see `legal-and-privacy.md`).
- **Appearance and accessibility:** theme and accessibility options.
- **Privacy and data:** cookie settings, "Download my data" and account deletion.
- **[Payments] Billing:** current plan, payment method, printable invoices and cancellation.

Rules:
- Users can connect and disconnect sign-in providers. Disconnecting the last sign-in method is blocked.
- Changing the password, email, two-factor settings or connected providers, deleting the account, and changing payment details all require re-entering the password (or a two-factor check for accounts without a password).
- After a password change or "Sign out of all other devices," revoke every other session immediately.

## Data Export
- "Download my data" is included in every app with accounts.
- It contains everything the user created and everything stored about them, never other users' personal data. Messages the user exchanged are included, with only display names shown for other people.
- Package it as JSON or CSV and deliver it through a private, expiring download link. Rate-limit exports per user.

## Easy Exit
Cancelling a subscription, deleting an account and requesting data deletion each:
- Take no more steps than signing up did. One re-authentication and one confirmation don't count.
- Never require contacting support.
- Clearly state what will happen and when.

Account deletion details (14-day grace period, retained records) are in `legal-and-privacy.md`.

## Security Notifications
Email the user when their password, email, two-factor settings or connected providers change, and when someone signs in from a new device. These are required transactional messages and cannot be unsubscribed from.
