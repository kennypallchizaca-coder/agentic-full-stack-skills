# System Aliases Configuration

Para usar ruteo absoluto (evitar `../../../`), debemos decirle a Typescript y al empaquetador que `@/` apunta a `src/`.

---

## 1. Typescript (Agnóstico, para React/Vue/Angular/Astro)

Filename: `tsconfig.json` o `tsconfig.app.json`
```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```

---

## 2. Vite (React, Vue)

Vite necesita un resolver aparte para entender lo que configuramos en Typescript.

Filename: `vite.config.ts`
```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react'; // O Vue
import path from 'path';

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src')
    }
  }
});
```

---

## 3. Angular CLI

Angular CLI respeta automáticamente la configuración del `tsconfig.json`. En versiones recientes basta con declararlo allí y el compilador Webpack interno de Angular Builder lo adoptará nativamente sin requerir tocar el `angular.json` para los imports `.ts`.
