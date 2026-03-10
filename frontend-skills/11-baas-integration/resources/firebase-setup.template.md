# Firebase & Firestore Matrix

Las aplicaciones Serverless sin backend de Node.js consumen la API de firebase inyectando App, Auth y Database como singletons globales.

---

## AngularFire (Oficial SDK)

Filename: `src/app/app.config.ts`
```typescript
import { ApplicationConfig } from '@angular/core';
import { provideFirebaseApp, initializeApp } from '@angular/fire/app';
import { provideAuth, getAuth } from '@angular/fire/auth';
import { provideFirestore, getFirestore } from '@angular/fire/firestore';
import { environment } from '../environments/environment';

export const appConfig: ApplicationConfig = {
  providers: [
    provideFirebaseApp(() => initializeApp(environment.firebase)),
    provideAuth(() => getAuth()),
    provideFirestore(() => getFirestore())
  ]
};
```

Filename: `src/app/core/services/firebase/auth.service.ts`
```typescript
import { Injectable, inject, signal } from '@angular/core';
import { Auth, signInWithEmailAndPassword, user, signOut } from '@angular/fire/auth';
import { from } from 'rxjs'; // To convert raw Web Promises to RxJS

@Injectable({ providedIn: 'root' })
export class AuthService {
  private auth = inject(Auth);
  
  // Reactivo: Si FirebaseAuth cambia el status lo emite a los Guardias de Rutas (Skill 04)
  user$ = user(this.auth); 

  login(email: string, pass: string) {
    return from(signInWithEmailAndPassword(this.auth, email, pass));
  }

  logout() {
    return from(signOut(this.auth));
  }
}
```

---

## React / Astro (Firebase SDK V9)

En ecosistemas Vanilla, React o Vue, exportamos los punteros singletons desde un archivo `firebase.ts` en `api` o `services`.

Filename: `src/shared/api/firebase.ts`
```typescript
import { initializeApp } from 'firebase/app';
import { getAuth } from 'firebase/auth';
import { getFirestore } from 'firebase/firestore';

const firebaseConfig = {
  apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
  authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN,
  projectId: import.meta.env.VITE_FIREBASE_PROJECT_ID,
  storageBucket: import.meta.env.VITE_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: import.meta.env.VITE_FIREBASE_MESSAGING_SENDER_ID,
  appId: import.meta.env.VITE_FIREBASE_APP_ID
};

const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);
export const db = getFirestore(app);
```

Filename: `src/features/favorites/services/favorites.service.ts`
```typescript
import { collection, getDocs, addDoc } from 'firebase/firestore';
import { db } from '@/shared/api/firebase';

const favCollection = collection(db, 'favoritos');

export const FavoritesResource = {
  getAll: async () => {
    const snapshot = await getDocs(favCollection);
    return snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
  },
  
  create: async (data: any) => {
    return await addDoc(favCollection, data);
  }
};
// Then in a Smart Dashboard Component, you just say:
// const data = await FavoritesResource.getAll();
// sin jamás tocar axios.
```
