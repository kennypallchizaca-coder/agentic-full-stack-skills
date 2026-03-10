# Route Guards Matrix

Pattern to conditionally block views before they are rendered, based on auth state.

## Universal Truth Source
Assume we have an `authService` or global state that answers:
```typescript
const isAuthenticated = () => !!localStorage.getItem('token');
```

---

## Vue (Vue Router 4)

Vue Router provides global navigation guards `beforeEach`. You attach `meta` fields to the routes.

Filename: `src/app/router/index.ts`
```typescript
import { router } from './router-definition';
import { isAuthenticated } from '@/shared/services/auth.service';

router.beforeEach((to, from, next) => {
  // 1. Check if route requires auth
  if (to.meta.requiresAuth && !isAuthenticated()) {
    return next({ path: '/auth/login' }); // Force login
  }

  // 2. Check if route requires guest (like login page)
  if (to.meta.requiresGuest && isAuthenticated()) {
    return next({ path: '/' }); // Redirect logged users to dashboard
  }

  // 3. Let everyone else pass
  next();
});
```

Usage in routes definition:
```typescript
{
  path: '/',
  component: MainLayout,
  meta: { requiresAuth: true }, // Applies to all children automatically
  children: [ ... ]
}
```

---

## React (React Router v6)

React Router doesn't use interceptor functions. Instead, you wrap your layouts/routes in Higher Order Components (Guards) that read state and return a `<Navigate>` immediately if unauthorized.

Filename: `src/app/router/guards/RequireAuth.tsx`
```tsx
import { Navigate, Outlet } from 'react-router-dom';
import { useAuthStore } from '@/shared/store/auth.store';

export const RequireAuth = () => {
  // Replace with context, Redux, Zustand or raw localStorage check
  const isAuthenticated = useAuthStore(state => state.isAuthenticated);

  if (!isAuthenticated) {
    // If not logged in, redirect to login
    return <Navigate to="/auth/login" replace />;
  }

  // If yes, render the children routes (the MainLayout)
  return <Outlet />;
};
```

Usage in routes definition:
```tsx
{
  path: '/',
  element: <RequireAuth />, // Protects everything below
  children: [
    {
      element: <MainLayout />,
      children: [ ... ]
    }
  ]
}
```

---

## Angular (Standalone Components)

Angular uses functional Guards (`CanActivateFn`).

Filename: `src/app/router/guards/auth.guard.ts`
```typescript
import { inject } from '@angular/core';
import { CanActivateFn, Router } from '@angular/router';
import { AuthService } from '@/shared/services/auth.service';

export const requireAuthGuard: CanActivateFn = () => {
  const authService = inject(AuthService);
  const router = inject(Router);

  if (!authService.isAuthenticated()) {
    // Return a UrlTree to redirect
    return router.parseUrl('/auth/login');
  }
  return true;
};
```

Usage in routes definition:
```typescript
{
  path: '',
  component: MainLayoutComponent,
  canActivate: [requireAuthGuard], // Evaluated before loading the component or its lazy children
  children: [ ... ]
}
```
