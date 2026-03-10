# Smart & Dumb Component Pattern

Un "Smart Component" esconde la asincronía. Un "Dumb Component" asume que el mundo asíncrono no existe.

---

## Angular

**Dumb Component (Puro Input/Output)**
Filename: `src/features/users/components/user-card/user-card.component.ts`
```typescript
import { Component, input, output } from '@angular/core';

@Component({
  selector: 'app-user-card',
  standalone: true,
  template: `
    <div class="card">
       <!-- Pinta pasivamente lo que recibe -->
       <h2>{{ user().name }}</h2> 
       <button (click)="onDelete()">Delete</button>
    </div>
  `
})
export class UserCardComponent {
  user = input.required<User>();
  deleteAccount = output<number>(); // Angular 17.3+ new API

  onDelete() {
    this.deleteAccount.emit(this.user().id); // Delega la carga 
  }
}
```

**Smart Component (Padre Inyector)**
Filename: `src/features/users/pages/user-dashboard.component.ts`
```typescript
import { Component, inject } from '@angular/core';
import { UsersRepository } from '../../services/users.repo';
import { UserCardComponent } from '../../components/user-card.component';
import { rxResource } from '@angular/core/rxjs-interop';

@Component({
  standalone: true,
  imports: [UserCardComponent],
  template: `
    @if (usersResource.isLoading()) {
      <p>Cargando red...</p>
    } @else {
      @for (u of usersResource.value(); track u.id) {
         <app-user-card [user]="u" (deleteAccount)="handleDelete($event)" />
      }
    }
  `
})
export class UserDashboard {
  private repo = inject(UsersRepository);
  usersResource = rxResource({ loader: () => this.repo.getAll() });

  handleDelete(id: number) {
    this.repo.delete(id).subscribe(() => this.usersResource.reload());
  }
}
```

---

## React

**Dumb Component (Puro Props)**
Filename: `src/features/users/components/UserCard.tsx`
```tsx
interface Props {
  user: User;
  onDelete: (id: number) => void;
}

export const UserCard = ({ user, onDelete }: Props) => {
  return (
    <div className="card">
       <h2>{user.name}</h2> 
       <button onClick={() => onDelete(user.id)}>Delete</button>
    </div>
  );
};
```

**Smart Component (Container Hooks)**
Filename: `src/features/users/pages/UserDashboard.tsx`
```tsx
import { useState, useEffect } from 'react';
import { UserCard } from '../components/UserCard';
import { UsersRepo } from '../api/users.repo';

export const UserDashboard = () => {
  const [users, setUsers] = useState<User[]>([]);

  useEffect(() => {
    UsersRepo.getAll().then(setUsers); // Red cruda escondida aquí arriba
  }, []);

  const handleDelete = async (id: number) => {
    await UsersRepo.delete(id);
    setUsers(users.filter(u => u.id !== id));
  };

  return (
    <div>
      {users.map(u => (
         <UserCard key={u.id} user={u} onDelete={handleDelete} />
      ))}
    </div>
  );
};
```
