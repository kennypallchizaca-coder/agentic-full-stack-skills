# Dynamic Form Patterns

Use these patterns when a form goes beyond a flat list of text inputs.

## Repeatable groups

- Model repeatable rows explicitly as arrays of objects.
- Add and remove rows through form helpers, not manual DOM cloning.
- Keep per-row validation attached to the row model.

## Nested groups

- Group related sub-fields into one nested object when the payload is nested.
- Keep naming aligned with the backend DTO or command shape.
- Reset nested groups through the form engine, not through scattered manual mutations.

## Conditional fields

- Use one source of truth for visibility rules.
- Hidden fields should either reset or remain intentionally preserved; document the rule.
- Do not let hidden stale values leak into the final payload silently.

## Server error mapping

- Map backend validation errors back to field names when possible.
- Use a global alert only for form-level failures that cannot attach to one field.
- Normalize backend error shapes through a helper before touching the UI.

## Anti-patterns

- Cloning DOM nodes instead of modeling repeatable state.
- Mixing schema validation, submit logic, and view copy in one function.
- Treating async validation as a button-click side effect instead of part of the form lifecycle.
