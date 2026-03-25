# HTTP Interceptors Matrix

Interceptors are the right place to centralize credentials, retries, normalization, and shared error handling.

Security preference:
- Prefer `httpOnly` secure cookies and `withCredentials` over tokens persisted in `localStorage`.
- If bearer tokens are required, keep them in controlled memory or a dedicated auth service, not ad-hoc component code.

---

## Axios (React, Vue, Astro, Node-compatible frontends)

Filename: `src/shared/api/api-client.ts`
```typescript
import axios from 'axios';
import { authState } from '@/shared/auth/auth-state';
import { apiConfig } from '@/shared/config/api-config';

export const apiClient = axios.create({
  baseURL: apiConfig.baseUrl,
  timeout: 10000,
  withCredentials: true,
});

const redirectToAuthEntry = () => {
  // Replace with the router or navigation primitive used by the target project.
  window.location.assign('/sign-in');
};

apiClient.interceptors.response.use(
  (response) => response,
  async (error) => {
    if (error.response?.status === 401) {
      authState.markGuest();
      redirectToAuthEntry();
    }

    return Promise.reject(error);
  }
);
```

Optional bearer-token request hook:
```typescript
apiClient.interceptors.request.use((config) => {
  const accessToken = authProvider.getAccessToken();

  if (accessToken) {
    config.headers.Authorization = `Bearer ${accessToken}`;
  }

  return config;
});
```

Usage in a repository:
```typescript
import { apiClient } from '@/shared/api/api-client';

export const {Feature}Repository = {
  async findAll() {
    const { data } = await apiClient.get('/{resource-path}');
    return data;
  },
};
```

---

## Angular (Native HttpClient)

Filename: `src/shared/api/auth.interceptor.ts`
```typescript
import { HttpErrorResponse, HttpInterceptorFn } from '@angular/common/http';
import { inject } from '@angular/core';
import { Router } from '@angular/router';
import { catchError, throwError } from 'rxjs';
import { AuthStateStore } from '@/shared/stores/auth-state.store';

const authEntryRoute = ['/sign-in'];

export const authInterceptor: HttpInterceptorFn = (req, next) => {
  const router = inject(Router);
  const authStore = inject(AuthStateStore);

  const authReq = req.clone({
    withCredentials: true,
  });

  return next(authReq).pipe(
    catchError((error: HttpErrorResponse) => {
      if (error.status === 401) {
        authStore.setGuest();
        router.navigate(authEntryRoute);
      }

      return throwError(() => error);
    })
  );
};
```

Optional bearer-token variant:
```typescript
const accessToken = authProvider.getAccessToken();

const authReq = accessToken
  ? req.clone({
      withCredentials: true,
      setHeaders: { Authorization: `Bearer ${accessToken}` },
    })
  : req.clone({ withCredentials: true });
```

Register the interceptor in the HTTP bootstrap point used by the project.

Example filename in Angular: `src/app/app.config.ts`
```typescript
import { provideHttpClient, withInterceptors } from '@angular/common/http';
import { authInterceptor } from '@/shared/api/auth.interceptor';

export const appConfig = {
  providers: [
    provideHttpClient(withInterceptors([authInterceptor])),
  ],
};
```

---

## Adaptation Reminder

- Replace `/sign-in` and `/{resource-path}` with the real auth entry route and resource path of the target app.
- Keep navigation side effects behind the project's router abstraction when possible.
- If the stack uses fetch wrappers, generated clients, or server loaders, apply the same responsibilities there instead of copying Axios or Angular literally.
