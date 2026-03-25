# Lazy Routing and Layouts Matrix

Lazy loading defers loading code until a specific route is visited. It reduces the initial load time of the application.

Use the framework sections below as translation examples, not as a universal folder structure. Replace route names, layout names, and file locations with the conventions of the target project.

## Universal Pattern

```text
{router-root}/routes.{ext}
├── public shell
│   ├── {public-home-route}
│   └── {sign-in-or-sign-up-route}
├── protected shell
│   ├── {feature-home-route}
│   └── {feature-detail-route}
└── fallback / not-found route
```

General rules:
- Keep layouts eager when they are reused on most pages.
- Lazy-load feature views or route modules at route boundaries.
- Keep route names and file paths aligned with the business language of the target app.

---

## Vue (Vue Router 4)

Vue uses standard ES modules dynamic imports.

Filename: `src/app/router/index.ts`
```typescript
import { createRouter, createWebHistory } from 'vue-router'

import PublicLayout from '@/app/layouts/PublicLayout.vue'
import ProtectedLayout from '@/app/layouts/ProtectedLayout.vue'

const routes = [
  {
    path: '/',
    component: ProtectedLayout,
    children: [
      {
        path: '',
        name: 'FeatureHome',
        component: () => import('@/features/{feature}/views/FeatureHomeView.vue')
      },
      {
        path: ':itemId',
        name: 'FeatureDetail',
        component: () => import('@/features/{feature}/views/FeatureDetailView.vue')
      }
    ]
  },
  {
    path: '/access',
    component: PublicLayout,
    children: [
      {
        path: 'sign-in',
        name: 'SignIn',
        component: () => import('@/features/access/views/SignInView.vue')
      }
    ]
  },
  {
    path: '/:pathMatch(.*)*',
    name: 'NotFound',
    component: () => import('@/app/views/NotFoundView.vue')
  }
]

export const router = createRouter({
  history: createWebHistory(),
  routes
})
```

---

## React (React Router v6+)

React requires `Suspense` wraps for components using `React.lazy()`. Modern Data Routers define routes as objects similar to Vue.

Filename: `src/app/router/index.tsx`
```tsx
import { lazy, Suspense } from 'react'
import { createBrowserRouter } from 'react-router-dom'

import PublicLayout from '@/app/layouts/PublicLayout'
import ProtectedLayout from '@/app/layouts/ProtectedLayout'
import LoadingFallback from '@/app/components/LoadingFallback'

const FeatureHomeView = lazy(() => import('@/features/{feature}/views/FeatureHomeView'))
const FeatureDetailView = lazy(() => import('@/features/{feature}/views/FeatureDetailView'))
const SignInView = lazy(() => import('@/features/access/views/SignInView'))
const NotFoundView = lazy(() => import('@/app/views/NotFoundView'))

export const router = createBrowserRouter([
  {
    path: '/',
    element: <ProtectedLayout />,
    children: [
      {
        index: true,
        element: (
          <Suspense fallback={<LoadingFallback />}>
            <FeatureHomeView />
          </Suspense>
        )
      },
      {
        path: ':itemId',
        element: (
          <Suspense fallback={<LoadingFallback />}>
            <FeatureDetailView />
          </Suspense>
        )
      }
    ]
  },
  {
    path: '/access',
    element: <PublicLayout />,
    children: [
      {
        path: 'sign-in',
        element: (
          <Suspense fallback={<LoadingFallback />}>
            <SignInView />
          </Suspense>
        )
      }
    ]
  },
  {
    path: '*',
    element: (
      <Suspense fallback={<LoadingFallback />}>
        <NotFoundView />
      </Suspense>
    )
  }
])
```

---

## Angular (Standalone Components)

Angular 15+ allows lazy loading entire routes using dynamic imports to standalone components.

Filename: `src/app/app.routes.ts`
```typescript
import { Routes } from '@angular/router';
import { PublicLayoutComponent } from '@/app/layouts/public-layout.component';
import { ProtectedLayoutComponent } from '@/app/layouts/protected-layout.component';

export const routes: Routes = [
  {
    path: '',
    component: ProtectedLayoutComponent,
    children: [
      {
        path: '',
        title: 'Feature Home',
        loadComponent: () => import('@/features/{feature}/views/feature-home.component')
          .then(m => m.FeatureHomeComponent)
      },
      {
        path: ':itemId',
        title: 'Feature Detail',
        loadComponent: () => import('@/features/{feature}/views/feature-detail.component')
          .then(m => m.FeatureDetailComponent)
      }
    ]
  },
  {
    path: 'access',
    component: PublicLayoutComponent,
    children: [
      {
        path: 'sign-in',
        title: 'Sign In',
        loadComponent: () => import('@/features/access/views/sign-in.component')
          .then(m => m.SignInComponent)
      }
    ]
  },
  {
    path: '**',
    title: 'Not Found',
    loadComponent: () => import('@/app/views/not-found.component')
      .then(m => m.NotFoundComponent)
  }
];
```

---

## File-Based Routers

If the stack uses file-based routing (for example Next.js, Nuxt, SvelteKit, Remix-style conventions, or Astro content routes), apply the same ideas at folder boundaries:

- Keep public and protected sections separated by route groups or top-level folders.
- Lazy-load only where the platform benefits from it.
- Keep a clear fallback or not-found entry point.
- Replace every placeholder in this document with project-specific names before shipping.
