# UX Heuristics Reference

Use these heuristics to review feedback flows independently from the UI library or framework.

## Core heuristics

1. **Visibility of system status**
   - Loading, success, and failure states are visible.
   - Long waits show progress or explain what is happening.

2. **Match between system and user language**
   - Error and success copy uses domain language, not internal codes.
   - Actions use labels users understand immediately.

3. **User control and freedom**
   - Destructive actions can be cancelled.
   - Users can dismiss non-critical feedback.

4. **Consistency and standards**
   - Similar outcomes reuse the same feedback channel and tone.
   - Confirmation patterns are predictable across features.

5. **Error prevention**
   - The UI warns before destructive or irreversible actions.
   - Dangerous options are clearly distinguished.

6. **Recognition over recall**
   - The UI shows what happened and what the user can do next.
   - Important state changes do not depend on memory alone.

7. **Flexibility and efficiency**
   - Keyboard users can navigate dialogs and dismiss feedback.
   - Repeated users are not blocked by unnecessary ceremony.

8. **Aesthetic and minimal design**
   - Feedback is noticeable but not noisy.
   - Multiple message layers do not compete at once.

9. **Help users recover from errors**
   - Error copy suggests a next step when possible.
   - Field-level problems stay near the field.

10. **Help and guidance**
   - Empty states and blocked flows explain what to do.
   - Long-lived failures offer support or retry paths.
