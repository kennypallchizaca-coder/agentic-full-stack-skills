# Component Composition Pattern

Use this template when a feature benefits from separating orchestration from reusable rendering. Treat it as one valid pattern, not as a mandatory rule for every component tree.

## Universal rule

- The orchestration boundary owns route state, repository calls, and feature-level side effects.
- The reusable UI boundary receives explicit data and emits explicit interactions.
- The exact shape of the boundary changes by framework and by feature.

---

## Angular

**Reusable rendering component**
```typescript
@Component({
  selector: 'app-resource-card',
  standalone: true,
  template: `
    <article class="card">
      <h2>{{ item().title }}</h2>
      <button type="button" (click)="primaryAction.emit(item().id)">Open</button>
    </article>
  `,
})
export class ResourceCardComponent {
  item = input.required<ResourceSummary>();
  primaryAction = output<string>();
}
```

**Feature orchestration view**
```typescript
@Component({
  standalone: true,
  imports: [ResourceCardComponent],
  template: `
    @if (itemsResource.isLoading()) {
      <p>Loading...</p>
    } @else {
      @for (item of itemsResource.value(); track item.id) {
        <app-resource-card [item]="item" (primaryAction)="handlePrimaryAction($event)" />
      }
    }
  `,
})
export class FeaturePage {
  private repo = inject(FeatureRepository);
  itemsResource = rxResource({ loader: () => this.repo.findAll() });
}
```

---

## React

**Reusable rendering component**
```tsx
type Props = {
  item: ResourceSummary;
  onPrimaryAction: (id: string) => void;
};

export function ResourceCard({ item, onPrimaryAction }: Props) {
  return (
    <article className="card">
      <h2>{item.title}</h2>
      <button type="button" onClick={() => onPrimaryAction(item.id)}>
        Open
      </button>
    </article>
  );
}
```

**Feature orchestration page**
```tsx
export function FeaturePage() {
  const { items, isLoading, openItem } = useFeatureViewModel();
  if (isLoading) return <p>Loading...</p>;
  return items.map((item) => (
    <ResourceCard key={item.id} item={item} onPrimaryAction={openItem} />
  ));
}
```

---

## Vue

**Reusable rendering component**
```vue
<script setup lang="ts">
defineProps<{ item: ResourceSummary }>();
const emit = defineEmits<{ primaryAction: [id: string] }>();
</script>

<template>
  <article class="card">
    <h2>{{ item.title }}</h2>
    <button type="button" @click="emit('primaryAction', item.id)">Open</button>
  </article>
</template>
```

---

## Astro

**Server shell plus interactive island**
```astro
---
import FeatureIsland from '../islands/feature-island';
const items = await loadFeatureItems();
---

<Layout title="{Feature}">
  <FeatureIsland items={items} client:load />
</Layout>
```

## When to skip this pattern

- The component is already tiny and purely visual.
- The framework page/layout model already gives enough separation.
- Splitting the component would add ceremony without isolating side effects.
