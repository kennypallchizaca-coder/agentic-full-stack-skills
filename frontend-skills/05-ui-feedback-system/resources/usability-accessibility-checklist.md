# Usability and Accessibility Checklist for Feedback UI

Use this checklist for toasts, alerts, confirmation dialogs, loading overlays, and destructive-action flows.

## Message quality

- The message explains what happened in plain language
- The next action is obvious
- Destructive actions use explicit labels such as `Delete account`, not vague `Confirm`
- Error messages help the user recover instead of only saying `Something went wrong`

## Interaction safety

- Destructive flows require confirmation
- Long-running operations expose visible progress or pending state
- Duplicate submits are blocked or clearly throttled
- Undo or cancel exists where the action is reversible

## Accessibility checks

- Dialogs move focus to a meaningful element when opened
- Focus returns to the previous trigger when the dialog closes
- Escape or equivalent dismissal is supported when safe
- Buttons and close controls have clear labels
- Contrast remains readable in success, warning, and error states
- Loading states are not communicated by color alone

## Heuristic alignment

- Visibility of system status: loading, success, and failure are visible
- Error prevention: risky actions require confirmation or validation
- Consistency: the same event triggers the same feedback pattern across the app
- User control: the UI does not trap the user in irreversible states without warning

## Anti-patterns

- Toast-only handling for destructive failures that need user action
- Modal confirmations with no focus management
- Spinners with no text on slow operations
- Generic `Error` copy repeated across every failure path
