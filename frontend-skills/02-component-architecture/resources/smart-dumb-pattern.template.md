# Component Composition Pattern

Use this template when a feature benefits from separating orchestration from reusable rendering. Treat it as one valid pattern, not as a mandatory rule for every component tree.

## Universal rule

- The orchestration boundary owns route state, repository calls, and feature-level side effects.
- The reusable UI boundary receives explicit data and emits explicit interactions.
- The exact shape of the boundary changes by framework.

---

## Angular

**Reusable rendering component**
```typescript
@Component({
  selector: 'app-user-card',
  standalone: true,
  template: `
    <article class="card">
      <h2>{{ user().name }}</h2>
      <button type="button" (click)="deleteRequested.emit(user().id)">Delete</button>
    </article>
  `,
})
export class UserCardComponent {
  user = input.required<User>();
  deleteRequested = output<number>();
}
```

**Feature orchestration view**
```typescript
@Component({
  standalone: true,
  imports: [UserCardComponent],
  template: `
    @if (usersResource.isLoading()) {
      <p>Loading...</p>
    } @else {
      @for (user of usersResource.value(); track user.id) {
        <app-user-card [user]="user" (deleteRequested)="handleDelete($event)" />
      }
    }
  `,
})
export class UserPage {
  private repo = inject(UsersRepository);
  usersResource = rxResource({ loader: () => this.repo.findAll() });
}
```

---

## React

**Reusable rendering component**
```tsx
type Props = {
  user: User;
  onDelete: (id: number) => void;
};

export function UserCard({ user, onDelete }: Props) {
  return (
    <article className="card">
      <h2>{user.name}</h2>
      <button type="button" onClick={() => onDelete(user.id)}>
        Delete
      </button>
    </article>
  );
}
```

**Feature orchestration page**
```tsx
export function UserPage() {
  const { users, isLoading, removeUser } = useUsersFeature();
  if (isLoading) return <p>Loading...</p>;
  return users.map((user) => <UserCard key={user.id} user={user} onDelete={removeUser} />);
}
```

---

## Vue

**Reusable rendering component**
```vue
<script setup lang="ts">
defineProps<{ user: User }>();
const emit = defineEmits<{ deleteRequested: [id: number] }>();
</script>

<template>
  <article class="card">
    <h2>{{ user.name }}</h2>
    <button type="button" @click="emit('deleteRequested', user.id)">Delete</button>
  </article>
</template>
```

---

## Astro

**Server shell plus interactive island**
```astro
---
import UsersIsland from '../islands/users-island';
const users = await getUsers();
---

<Layout title="Users">
  <UsersIsland users={users} client:load />
</Layout>
```

## When to skip this pattern

- The component is already tiny and purely visual.
- The framework page/layout model already gives enough separation.
- Splitting the component would add ceremony without isolating side effects.
