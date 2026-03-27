# AGENTS.md - Guía para Agentes de Código

Este documento establece las directrices para agentes que trabajan en el proyecto **estelar-docs**, un sitio de documentación construido con Docusaurus 3.9.2 y React 19.

---

## 1. Comandos de Construcción y Verificación

| Comando | Descripción |
|---------|-------------|
| `npm install` | Instala dependencias |
| `npm start` | Servidor desarrollo (http://localhost:3000) |
| `npm run build` | Genera archivos estáticos en /build |
| `npm run typecheck` | Verifica tipos TypeScript |
| `npm run serve` | Sirve el build local |
| `npm run deploy` | Despliega a GitHub Pages |
| `npm run clear` | Limpia caché de Docusaurus |

**Testing**: Este proyecto no tiene tests automatizados. La calidad se verifica con:
- `npm run typecheck` - Verificación de tipos
- `npm run build` - Verificación de compilación
- Verificación visual con `npm start`

---

## 2. Estructura del Proyecto

```
estelar-docs/
├── docs/                 # Documentación MDX
├── blog/                 # Posts del blog
├── src/
│   ├── pages/            # Páginas React/TSX
│   ├── components/       # Componentes reutilizables
│   └── css/              # Estilos CSS
├── static/               # Assets estáticos
├── docusaurus.config.ts  # Configuración principal
├── sidebars.ts           # Configuración de sidebars
└── tsconfig.json         # Configuración TypeScript
```

---

## 3. Convenciones de Código

### TypeScript
- Tipado estricto: usar tipos explícitos para props y funciones
- Preferir `interface` para objetos, `type` para uniones
- Nunca usar `any` sin justificación documentada
- Usar optional chaining (`?.`) y nullish coalescing (`??`)

```typescript
interface Props {
  title: string;
  subtitle?: string;
  onAction: () => void;
}
```

### Componentes React
- Usar exclusivamente componentes funcionales con hooks
- PascalCase para componentes, camelCase para funciones
- Tipar siempre las props con interfaces

### Imports - Orden recomendado
1. React/core imports
2. Librerías externas
3. Componentes internos
4. Estilos

### Convenciones de Nomenclatura
- Componentes: PascalCase (`FeatureCard`)
- Funciones/Variables: camelCase (`getTitle`)
- Constantes: UPPER_SNAKE_CASE (`MAX_ITEMS`)
- Archivos: kebab-case (`my-component.tsx`)

### Formato
- Sangría: 2 espacios
- Punto y coma: requerido
- Comillas: simples (`'`)
- Líneas en blanco: máximo 1 entre bloques
- Longitud de línea: máximo 100 caracteres

### Manejo de Errores
- Usar tipos discriminados para manejo de errores
- Try/Catch con logging apropiado
- Docusaurus: `onBrokenLinks: 'throw'`

---

## 4. Configuración de Docusaurus

### docusaurus.config.ts
El archivo ejecuta en **Node.js** (no código del cliente). No usar:
- APIs del navegador (window, document)
- JSX directo
- Código asíncrono que dependa del DOM

```typescript
// ❌ Incorrecto
const handle = () => <div>JSX aquí falla</div>

// ✅ Correcto
const config: Config = { /* configuración pura */ };
```

### Best Practices para Documentación
- Frontmatter: siempre incluir `sidebar_position` en docs
- MDX: usar componentes React directamente
- Imágenes: guardar en `static/img/` y referenciar con `/img/nombre.png`
- Links: usar rutas absolutas `/docs/intro`

---

## 5. Estilos y CSS

Usar CSS Modules para scoping de estilos:

```typescript
import styles from './MyComponent.module.css';

export default function MyComponent() {
  return <div className={styles.container}>...</div>;
}
```

El proyecto usa variables CSS definidas en `src/css/custom.css`.

---

## 6. Reglas de Contribución

### Antes de modificar código
1. Ejecutar `npm run typecheck` para verificar tipos
2. Ejecutar `npm run build` para verificar compilación
3. Probar cambios localmente con `npm start`

### Commits
- Mensajes claros y descriptivos
- Formato: `tipo: descripción` (ej: `docs: agregar guía de inicio`)

### Prohibido
- Modificar archivos en `/node_modules`
- Agregar dependencias sin justificación
- Hacer commit de credenciales o secrets
- Modificar la estructura de `/build` (generado automáticamente)

---

## 7. Recursos

- [Documentación Docusaurus](https://docusaurus.io/docs)
- [React 19](https://react.dev/blog/2024/04/25/react-19)
- [TypeScript](https://www.typescriptlang.org/docs/)