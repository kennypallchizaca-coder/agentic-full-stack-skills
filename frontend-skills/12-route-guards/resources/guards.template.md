# Route Guards Matrix

Pattern to block or allow routes based on shared session state.

## Universal Truth Source

Do not use `localStorage.getItem('token')` as the primary truth source.
Assume there is a shared auth store or auth service exposing:

```typescript
type SessionStatus = 'unknown' | 'authenticated' | 'guest';

const sessionStatus = () => authStore.status;
const isAuthenticated = () => sessionStatus() === 'authenticated';
const isBootstrapping = () => sessionStatus() === 'unknown';
```

Assume `bootstrapSession()` asks the backend for `/me` or an equivalent endpoint and updates the shared auth store.

Replace the route placeholders below with the real auth entry path and post-login landing route used by the target project.

---

## Vue (Vue Router 4)

Filename: `src/app/router/index.ts`
```typescript
import { router } from './router-definition';
import { useAuthStore } from '@/shared/stores/auth.store';

const authEntryPath = '/sign-in';
const authenticatedHomePath = '/';

router.beforeEach(async (to) => {
  const authStore = useAuthStore();

  if (authStore.status === 'unknown') {
    await bootstrapSession();
  }

  if (to.meta.requiresAuth && authStore.status !== 'authenticated') {
    return { path: authEntryPath, query: { returnUrl: to.fullPath } };
  }

  if (to.meta.requiresGuest && authStore.status === 'authenticated') {
    return { path: authenticatedHomePath };
  }
});
```

---

## React (React Router v6+)

Filename: `src/app/router/guards/RequireAuth.tsx`
```tsx
import { Navigate, Outlet, useLocation } from 'react-router-dom';
import { useAuthStore } from '@/shared/stores/auth.store';

const authEntryPath = '/sign-in';

export const RequireAuth = () => {
  const location = useLocation();
  const status = useAuthStore((state) => state.status);

  if (status === 'unknown') {
    return <div>Loading session...</div>;
  }

  if (status !== 'authenticated') {
    return <Navigate to={authEntryPath} replace state={{ returnTo: location.pathname }} />;
  }

  return <Outlet />;
};
```

---

## Angular (Standalone / Functional Guards)

Filename: `src/app/router/guards/auth.guard.ts`
```typescript
import { inject } from '@angular/core';
import { CanActivateFn, Router } from '@angular/router';
import { AuthStore } from '@/shared/stores/auth.store';

const authEntryRoute = ['/sign-in'];

export const requireAuthGuard: CanActivateFn = async (_, state) => {
  const authStore = inject(AuthStore);
  const router = inject(Router);

  if (authStore.status() === 'unknown') {
    await bootstrapSession();
  }

  if (authStore.status() !== 'authenticated') {
    return router.createUrlTree(authEntryRoute, {
      queryParams: { returnUrl: state.url },
    });
  }

  return true;
};
```
