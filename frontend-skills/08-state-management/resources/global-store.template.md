# Global Stores Matrix

Modern frontend relies on decentralized, atomic stores rather than one giant "Redux-like" state.

## React (Zustand)

Zustand prevents unnecessary re-renders automatically without Context providers.

Filename: `src/shared/stores/auth.store.ts`
```typescript
import { create } from 'zustand';

interface User {
  id: number;
  email: string;
  role: string;
}

interface AuthState {
  user: User | null;
  token: string | null;
  login: (user: User, token: string) => void;
  logout: () => void;
  isAuthenticated: () => boolean;
}

export const useAuthStore = create<AuthState>((set, get) => ({
  user: null,
  token: localStorage.getItem('token'),
  login: (user, token) => {
    localStorage.setItem('token', token);
    set({ user, token });
  },
  logout: () => {
    localStorage.removeItem('token');
    set({ user: null, token: null });
  },
  isAuthenticated: () => !!get().token
}));
```

## Vue (Pinia)

Pinia is the official Vue 3 state manager. It maps perfectly to Vue's Composition API (`ref` = state, `computed` = getters, `function` = actions).

Filename: `src/shared/stores/auth.store.ts`
```typescript
import { defineStore } from 'pinia';
import { ref, computed } from 'vue';

export const useAuthStore = defineStore('auth', () => {
  // State
  const user = ref(null);
  const token = ref(localStorage.getItem('token'));

  // Getters
  const isAuthenticated = computed(() => !!token.value);

  // Actions
  function login(newUser, newToken) {
    localStorage.setItem('token', newToken);
    token.value = newToken;
    user.value = newUser;
  }

  function logout() {
    localStorage.removeItem('token');
    token.value = null;
    user.value = null;
  }

  return { user, token, isAuthenticated, login, logout };
});
```

## Angular (Signals / Services)

In modern Angular (16+), a global state is simply an `@Injectable` mapped with `Signals` (similar to Vue's `ref`).

Filename: `src/shared/stores/auth.store.ts`
```typescript
import { Injectable, signal, computed } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class AuthStore {
  // State
  user = signal<User | null>(null);
  token = signal<string | null>(localStorage.getItem('token'));

  // Getters
  isAuthenticated = computed(() => !!this.token());

  // Actions
  login(newUser: User, newToken: string) {
    localStorage.setItem('token', newToken);
    this.token.set(newToken);
    this.user.set(newUser);
  }

  logout() {
    localStorage.removeItem('token');
    this.token.set(null);
    this.user.set(null);
  }
}
```

## Astro (NanoStores)

Astro islands (React, Vue, Svelte components within the same page) can only share state using framework-agnostic stores like NanoStores.

Filename: `src/shared/stores/auth.store.ts`
```typescript
import { atom, computed } from 'nanostores';

export const $token = atom<string | null>(typeof window !== 'undefined' ? localStorage.getItem('token') : null);
export const $user = atom<User | null>(null);

export const $isAuthenticated = computed($token, token => !!token);

export function login(newUser: User, newToken: string) {
  if (typeof window !== 'undefined') localStorage.setItem('token', newToken);
  $token.set(newToken);
  $user.set(newUser);
}

export function logout() {
  if (typeof window !== 'undefined') localStorage.removeItem('token');
  $token.set(null);
  $user.set(null);
}
```
