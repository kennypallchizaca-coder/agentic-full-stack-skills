# Styling Strategy Matrix

Use this matrix to choose a styling stack without confusing framework syntax with architecture.

| Strategy | Typical stacks | Strengths | Watch-outs |
|---------|----------------|-----------|------------|
| Utility CSS | Tailwind, UnoCSS, atomic classes | Fast composition, consistent spacing, shared tokens | Class-heavy templates if component boundaries are weak |
| Scoped CSS / CSS Modules | Vue scoped CSS, CSS Modules, Astro component styles | Strong local isolation, simple mental model | Token duplication if globals are not defined well |
| Styled APIs / CSS-in-JS | React ecosystems, design-system wrappers | Dynamic variants, theme composition in code | Runtime overhead or stack coupling if overused |
| Component-library theming | Material, Prime, DaisyUI, Chakra, Radix wrappers | Fast UI delivery, built-in patterns | Easy to drift visually if tokens do not govern overrides |
| Hybrid token-first setup | Any stack | Balances portability and growth | Requires explicit rules about where each strategy is allowed |

## Portable rules

- Tokens should outlive the styling library choice.
- Responsive layout primitives should be shared, not page-specific.
- Theme persistence should be documented, not hidden in one component.
- Library overrides should align with tokens instead of ad-hoc colors and spacing.
