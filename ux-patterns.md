# UX Patterns

Read this before building loading states, interactions, notices or flows.

## Loaders
Use only these:
- **Skeleton screens** for loading content. Skeletons match the dimensions of the content they replace so nothing shifts when it arrives. Server-rendered content does not need skeletons.
- **A simple circular spinner** inside a button for short actions.
- **A determinate progress bar** for measurable progress, such as uploads or onboarding steps. It sits within the content, never as a strip along the top edge of the page. Step counts ("Step 2 of 4") live inside the progress component, never in a separate chip or above a heading.

Every loader:
- Appears only while something is loading.
- Is replaced by the content or a clear error message when loading ends.
- Never blocks interaction with content that has already loaded.

Banned: looping arrow indicators, and any thin bar or line along the top edge of the page.

## Action Handling
1. Update the UI immediately (optimistic update).
2. Lock the control while the request runs.
3. Send an idempotency key so the server rejects duplicates.
4. If the server refuses, roll back the UI, preserve the user's input, and show a clear message.

Payments, deletions and other irreversible actions wait for the server before updating the UI.

## Interaction States
Every interactive element has distinct hover, active/pressed, focus-visible, disabled and loading states.

## User-Error Safeguards
- Minimum tap targets of 44×44 px. Links inside running text are exempt.
- A short delay before hover menus close.
- Invisible triangles (safe zones) that keep submenus open while the pointer moves toward them.
- Undo for destructive actions where possible, and confirmation for irreversible ones.
- Warnings before leaving a page with unsaved changes.
- Saved drafts for long forms: on the server for logged-in users, in memory only for logged-out users.
- User input preserved when a submission fails.
- Flexible input formats (see `forms-and-data.md`).

## Allowed Notices
Nothing appears on page load except these state-triggered notices:

| Notice | Trigger | Form |
|---|---|---|
| Cookie consent | First visit with non-essential cookies | Non-blocking bar at the bottom of the screen |
| Email verification reminder | Signed in with an unverified email | Inline non-modal banner |
| Offline message | Connection lost | Inline non-modal banner |
| Idle warning | 2 minutes before idle logout | Modal (it needs a response) |

- No notice ever covers a focused input.
- No notice is a thin strip along the top edge of the page.
- The PWA install option, when a PWA exists, sits in a menu and never appears as a prompt.

## Dark and Hidden UX Patterns
Never use:
- Pre-checked opt-in boxes.
- Confirmshaming (such as "No thanks, I don't like saving money").
- Hidden or hard-to-find cancel, unsubscribe or account deletion options.
- Fake urgency, countdowns or scarcity.
- Visually weaker "reject" or "decline" buttons.
- Trick questions and double negatives.
- Items or add-ons sneaked into a cart.
- Ads disguised as content or navigation.

## Harmful or Unnecessary UX
Never use:
- Popups, newsletter modals or permission prompts on page load.
- Auto-playing media with sound.
- Forced account creation just to browse.
- Disabled paste in any field, including passwords.
- Scroll-jacking.
- Infinite scroll that makes the footer unreachable.
- Product tours that start on their own. A guided tour is allowed only when the user starts it, and it must be keyboard accessible and close with Escape.

## Offline and Slow Networks
- Detect when the connection drops and show the offline notice.
- Keep actions taken offline in memory, with a message that they will be lost if the tab closes. Never store them in browser storage.
- Retry automatically when the connection returns, following the retry rules in SKILL.md Section 12.
