# URL-Driven Pagination Matrix

La paginacion agnostica moderna NO actualiza una variable local de `page` que obliga a hacer prop-drilling. Actualiza la URL para que cualquier cambio persista entre recargas.

Las clases CSS y el mecanismo de recarga de datos son placeholders. Adaptalos al design system, router y capa de datos del proyecto objetivo.

---

## React (React Router DOM)

Filename: `src/shared/components/pagination/Pagination.tsx`
```tsx
import { useSearchParams } from 'react-router-dom';

interface Props {
  totalPages: number;
}

export const Pagination = ({ totalPages }: Props) => {
  const [searchParams, setSearchParams] = useSearchParams();
  const currentPage = Number(searchParams.get('page')) || 1;

  const pages = Array.from({ length: totalPages }, (_, i) => i + 1);

  const goToPage = (page: number) => {
    setSearchParams({ page: page.toString() });
    // The parent screen reacts to the URL and asks the repository/query layer for the new page.
  };

  return (
    <nav className="pagination" aria-label="Pagination">
      {pages.map((p) => (
        <button
          key={p}
          onClick={() => goToPage(p)}
          className={`pagination__button ${p === currentPage ? 'is-active' : ''}`}
        >
          {p}
        </button>
      ))}
    </nav>
  );
};
```

---

## Angular (Signals + RouterLink)

Angular can bind `[queryParams]` naturally to `[routerLink]` bindings without manual URL string manipulation.

Filename: `src/app/shared/components/pagination.component.ts`
```typescript
import { Component, computed, input, linkedSignal } from '@angular/core';

@Component({
  selector: 'app-pagination',
  standalone: true,
  template: `
    <nav class="pagination" aria-label="Pagination">
      @for (page of getPagesList(); track page) {
        <button
          class="pagination__button"
          [class.is-active]="page === activePage()"
          [routerLink]="[]"
          [queryParams]="{ page: page }"
          (click)="activePage.set(page)"
        >
          {{ page }}
        </button>
      }
    </nav>
  `
})
export class PaginationComponent {
  pages = input(0);
  currentPage = input<number>(1);
  activePage = linkedSignal(this.currentPage);

  getPagesList = computed(() => {
    return Array.from({ length: this.pages() }, (_, i) => i + 1);
  });
}
```

---

## Vue (Vue Router)

Filename: `src/shared/components/Pagination.vue`
```vue
<script setup lang="ts">
import { computed } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const props = defineProps<{ totalPages: number }>();
const route = useRoute();
const router = useRouter();

const currentPage = computed(() => Number(route.query.page) || 1);
const pages = computed(() => Array.from({ length: props.totalPages }, (_, i) => i + 1));

const goToPage = (page: number) => {
  router.push({ query: { ...route.query, page } });
};
</script>

<template>
  <nav class="pagination" aria-label="Pagination">
    <button
      v-for="p in pages"
      :key="p"
      @click="goToPage(p)"
      :class="['pagination__button', { 'is-active': p === currentPage }]"
    >
      {{ p }}
    </button>
  </nav>
</template>
```
