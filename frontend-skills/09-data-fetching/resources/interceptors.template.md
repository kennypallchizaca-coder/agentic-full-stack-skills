# HTTP Interceptors Matrix

Interceptors are the professional way to manipulate HTTP traffic globally without touching each component's fetch calls.

---

## Axios (React, Vue, Node, Astro)

Axios is the most common HTTP client. It has native support for interceptors out of the box.

Filename: `src/shared/api/api-client.ts`
```typescript
import axios from 'axios';
// Assume we have an auth store or utility
import { useAuthStore } from '@/shared/stores/auth.store';

// 1. Create central instance
export const apiClient = axios.create({
  baseURL: import.meta.env.VITE_API_URL || 'http://localhost:8080/api',
  timeout: 10000,
});

// 2. Request Interceptor: Attach Token
apiClient.interceptors.request.use((config) => {
  const token = localStorage.getItem('token');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// 3. Response Interceptor: Global Error Handling
apiClient.interceptors.response.use(
  (response) => {
    // If it's a 2xx status, just return the data normally
    return response;
  },
  (error) => {
    // If it's a 4xx or 5xx error
    if (error.response?.status === 401) {
      // Unauthorized -> Token expired or invalid
      console.warn("Session expired. Logging out.");
      
      // Clear token globally and redirect to login
      const logout = useAuthStore.getState().logout; // If React/Zustand
      logout();
      window.location.href = '/auth/login';
    }

    if (error.response?.status >= 500) {
       // Fire a global toast notification for Server Errors
       // toast.error('Server is down, try again later');
    }

    // Still reject the promise so the specific component can catch it if needed
    return Promise.reject(error);
  }
);
```

Usage in a specific Repository:
```typescript
// src/features/users/users.repository.ts
import { apiClient } from '@/shared/api/api-client';

export const UsersRepo = {
  findAll: async () => {
    const response = await apiClient.get('/users');
    return response.data; // Already bears the Auth token and handles 401 globally
  }
}
```

---

## Angular (Native HttpClient)

Angular uses RxJS and functional interceptors (`HttpInterceptorFn`) configured globally in the application providers.

Filename: `src/shared/api/auth.interceptor.ts`
```typescript
import { HttpInterceptorFn, HttpErrorResponse } from '@angular/common/http';
import { inject } from '@angular/core';
import { Router } from '@angular/router';
import { catchError, throwError } from 'rxjs';
import { AuthService } from '../services/auth.service';

export const authInterceptor: HttpInterceptorFn = (req, next) => {
  const router = inject(Router);
  const authService = inject(AuthService);
  
  // 1. Check token in localStorage/Service
  const token = authService.getToken();
  
  // 2. Clone request and inject token
  const authReq = token 
    ? req.clone({ setHeaders: { Authorization: `Bearer ${token}` } })
    : req;

  // 3. Forward request and intercept response errors
  return next(authReq).pipe(
    catchError((error: HttpErrorResponse) => {
      // If server responds with 401 Unauthorized
      if (error.status === 401) {
        authService.logout();
        router.navigate(['/auth/login']);
      }
      return throwError(() => error);
    })
  );
};
```

Activation:
Filename: `src/app/app.config.ts`
```typescript
import { provideHttpClient, withInterceptors } from '@angular/common/http';
import { authInterceptor } from '@/shared/api/auth.interceptor';

export const appConfig = {
  providers: [
    provideHttpClient(
      withInterceptors([authInterceptor]) // Global activation
    )
  ]
};
```

Usage in a specific Repository / Service:
```typescript
// src/features/users/users.service.ts
import { HttpClient } from '@angular/common/http';
import { inject } from '@angular/core';

export class UsersService {
  private http = inject(HttpClient);

  findAll() {
    return this.http.get<User[]>('/api/users'); // Token injection is invisible here
  }
}
```
