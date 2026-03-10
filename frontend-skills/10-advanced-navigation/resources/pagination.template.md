# URL-Driven Pagination Matrix

La paginación agnóstica moderna NO actualiza una variable local de `page` que obliga a hacer prop-drilling. Actualiza la URL para que cualquier cambio persista entre recargas.

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

  // Render logic blocks for 5 buttons
  const pages = Array.from({ length: totalPages }, (_, i) => i + 1);

  const goToPage = (page: number) => {
    setSearchParams({ page: page.toString() }); 
    // This updates '?page=X' instantly without a hard reload.
    // The parent component listens to searchParams logic and triggers Axios.
  };

  return (
    <div className="join">
      {pages.map((p) => (
        <button
          key={p}
          onClick={() => goToPage(p)}
          className={`join-item btn ${p === currentPage ? 'btn-primary' : ''}`}
        >
          {p}
        </button>
      ))}
    </div>
  );
};
```

---

## Angular (Signals + RouterLink)

Angular is able to bind the `[queryParams]` naturally to `[routerLink]` bindings without manual functions.

Filename: `src/app/shared/components/pagination.component.ts`
```typescript
import { Component, computed, input, linkedSignal } from '@angular/core';

@Component({
  selector: 'app-pagination',
  standalone: true,
  template: `
    <div class="join">
      @for (page of getPagesList(); track page) {
        <button
          class="join-item btn"
          [class.btn-primary]="page === activePage()"
          [routerLink]="[]"
          [queryParams]="{ page: page }"
          (click)="activePage.set(page)"
        >
          {{ page }}
        </button>
      }
    </div>
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
  <div class="join">
    <button 
      v-for="p in pages" 
      :key="p"
      @click="goToPage(p)"
      :class="['join-item btn', { 'btn-primary': p === currentPage }]"
    >
      {{ p }}
    </button>
  </div>
</template>
```
