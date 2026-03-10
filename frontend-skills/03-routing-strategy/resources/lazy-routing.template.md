# Lazy Routing and Layouts Matrix

Lazy loading defers loading code until a specific route is visited. It reduces the initial load time of the application.

## Vue (Vue Router 4)

Vue uses standard ES modules dynamic imports.

Filename: `src/app/router/index.ts`
```typescript
import { createRouter, createWebHistory } from 'vue-router'

// Eager load layouts (always needed)
import MainLayout from '@/app/layouts/MainLayout.vue'
import AuthLayout from '@/app/layouts/AuthLayout.vue'

const routes = [
  {
    path: '/',
    component: MainLayout, // Renders the navbar/sidebar
    children: [
      {
        path: '',
        name: 'Dashboard',
        // Lazy load the view only when visited
        component: () => import('@/features/dashboard/views/DashboardView.vue')
      },
      {
        path: 'invoices',
        name: 'Invoices',
        component: () => import('@/features/invoices/views/InvoiceListView.vue')
      }
    ]
  },
  {
    path: '/auth',
    component: AuthLayout, // Centered empty layout
    children: [
      {
        path: 'login',
        name: 'Login',
        component: () => import('@/features/auth/views/LoginView.vue')
      }
    ]
  },
  {
    path: '/:pathMatch(.*)*',
    name: 'NotFound',
    component: () => import('@/app/layouts/NotFoundView.vue')
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

import MainLayout from '@/app/layouts/MainLayout'
import AuthLayout from '@/app/layouts/AuthLayout'
import LoadingFallback from '@/app/components/LoadingFallback'

// Lazy load views
const DashboardView = lazy(() => import('@/features/dashboard/views/DashboardView'))
const InvoiceListView = lazy(() => import('@/features/invoices/views/InvoiceListView'))
const LoginView = lazy(() => import('@/features/auth/views/LoginView'))
const NotFoundView = lazy(() => import('@/app/layouts/NotFoundView'))

export const router = createBrowserRouter([
  {
    path: '/',
    element: <MainLayout />,
    children: [
      {
        index: true, // Same as path: ''
        element: (
          <Suspense fallback={<LoadingFallback />}>
            <DashboardView />
          </Suspense>
        )
      },
      {
        path: 'invoices',
        element: (
          <Suspense fallback={<LoadingFallback />}>
            <InvoiceListView />
          </Suspense>
        )
      }
    ]
  },
  {
    path: '/auth',
    element: <AuthLayout />,
    children: [
      {
        path: 'login',
        element: (
          <Suspense fallback={<LoadingFallback />}>
            <LoginView />
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

Angular 15+ allows lazy loading entire routes using dynamic imports to Standalone Components.

Filename: `src/app/app.routes.ts`
```typescript
import { Routes } from '@angular/router';
import { MainLayoutComponent } from '@/app/layouts/main-layout.component';
import { AuthLayoutComponent } from '@/app/layouts/auth-layout.component';

export const routes: Routes = [
  {
    path: '',
    component: MainLayoutComponent,
    children: [
      {
        path: '',
        title: 'Dashboard',
        loadComponent: () => import('@/features/dashboard/views/dashboard.component')
          .then(m => m.DashboardComponent)
      },
      {
        path: 'invoices',
        title: 'Invoices',
        loadComponent: () => import('@/features/invoices/views/invoice-list.component')
          .then(m => m.InvoiceListComponent)
      }
    ]
  },
  {
    path: 'auth',
    component: AuthLayoutComponent,
    children: [
      {
        path: 'login',
        title: 'Login',
        loadComponent: () => import('@/features/auth/views/login.component')
          .then(m => m.LoginComponent)
      }
    ]
  },
  {
    path: '**',
    title: 'Not Found',
    loadComponent: () => import('@/app/layouts/not-found.component')
      .then(m => m.NotFoundComponent)
  }
];
```
