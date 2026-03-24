# Component Primitives Matrix

Use this matrix to translate the same architectural idea across different frontend stacks.

| Concern | Angular | React | Vue | Astro |
|--------|---------|-------|-----|-------|
| Page entry | Route component / page | Route component / page | Route view | `.astro` page |
| Layout shell | Layout component / router outlet shell | Layout component | Layout component | Layout `.astro` component |
| Reusable UI unit | Standalone component | Function component | SFC component | `.astro` component or island component |
| Child composition | Content projection | `children` / render props | Slots | Slots / component composition |
| Local reactive state | signals / local state | hooks / local state | refs / reactive / computed | island-local state only |
| Feature orchestration | page component / service / resource | route component / custom hook | route view / composable | page load + island boundary |
| Server-provided data | resolver / API / SSR | loaders / SSR / props | SSR / route data / props | frontmatter server code |

## Portable rules

- Define the feature entry point first.
- Keep reusable UI units free from transport concerns whenever possible.
- Treat slots, children, content projection, and partial composition as the same architectural tool with different syntax.
- Keep framework-specific state close to the orchestration boundary.
