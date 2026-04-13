# AGENTS.md - AlphaTech Landing Page

## Descripción del proyecto

Landing page para AlphaTech, empresa de desarrollo de software en Nicaragua. El objetivo es ofrecer soluciones de aplicaciones y web a personas y empresas. Proyecto pequeño, equipo compacto de desarrolladores entusiastas y modernos.

**Tecnologías**: Astro 6.x, JavaScript, CSS puro.

**Principio fundamental**: Código simple, sencillo, fácil de leer y comprender. Sin complicaciones.

---

## Comandos de Build y Desarrollo

```bash
# Instalar dependencias
bun install
# o
npm install

# Desarrollo - Iniciar servidor local en localhost:4321
bun dev
# o
npm run dev

# Build de producción - Genera archivo ./dist/
bun build
# o
npm run build

# Preview - Previsualizar build localmente antes de desplegar
bun preview
# o
npm run preview

# Comandos Astro CLI
bun astro add <integration>
bun astro check
bun astro --help
```

### Verificacion de Tipos

```bash
bun astro check    # Verifica tipos en archivos .astro y .ts
```

---

## Estructura del Proyecto

```
/
├── public/              # Archivos estáticos (favicon, imágenes públicas)
├── src/
│   ├── assets/          # Recursos compilados (SVG, imágenes)
│   ├── components/      # Componentes Astro reutilizables
│   ├── layouts/         # Layouts base para páginas
│   └── pages/           # Rutas y páginas (index.astro =/)
├── astro.config.mjs     # Configuración de Astro
├── tsconfig.json        # Configuración de TypeScript
└── package.json
```

---

## Convenciones de Codigo

### Reglas Generales

1. **Código en inglés**: Todas las variables, funciones, comentarios de código, clases y IDs en inglés
- **Documentación en español**: Comentarios explicativos y archivos .md en español
- **Simplicidad primero**: Evitar abstracciones innecesarias. Código simple > código inteligente
- **KISS (Keep It Simple, Stupid)**: Cada archivo, función y componente debe ser fácil de entender

### Archivos Astro (.astro)

- **Frontmatter (---)**: Imports al inicio, luego variables y lógica simple
- **Template**: HTML semántico, usar indentación de 2 espacios
- **Estilos**: CSS scoped dentro del componente, sin frameworks CSS

```astro
---
// Imports
import Layout from '../layouts/Layout.astro';
import Button from './Button.astro';

// Variables
const title = 'AlphaTech';
---

<div class="container">
    <h1>{title}</h1>
</div>

<style>
    .container {
        padding: 1rem;
    }
</style>
```

### Convenciones de Nomenclatura

| Elemento              | Convencion              | Ejemplo                    |
| :-------------------- | :---------------------- | :------------------------- |
| Componentes Astro     | PascalCase              | `Header.astro`, `Card.astro` |
| Archivos de utilidad  | kebab-case              | `date-utils.js`, `form-helpers.ts` |
| Variables/funciones   | camelCase               | `userName`, `getData()`    |
| Constantes            | UPPER_SNAKE_CASE        | `MAX_ITEMS`, `API_URL`      |
| Clases CSS            | kebab-case              | `.main-title`, `.card-container` |
| IDs HTML              | kebab-case              | `id="hero-section"`        |
| Rutas/URLs            | kebab-case              | `/about-us`, `/our-services` |

### CSS (Estilos)

- **CSS Puro**: No usar frameworks como Tailwind, Bootstrap, etc.
- **Scope por componente**: Usar `<style>` scoped en cada componente .astro
- **Variables CSS**: Definir variables en `:root` para colores y espaciado consistente
- **Mobile-first**: Desarrollar para móvil primero, luego media queries para desktop
- **Unidades relativas**: Preferir `rem` sobre `px` para tamanos de fuente

```css
:root {
    --color-primary: #3b82f6;
    --color-secondary: #64748b;
    --spacing-unit: 1rem;
}

.container {
    padding: var(--spacing-unit);
}
```

### JavaScript

- **Vanilla JS**: Sin frameworks de JS (React, Vue, etc.)
- **ES Modules**: Usar `import/export` en archivos .js/.ts
- **Funciones pequeñas**: Cada función hace una sola cosa
- **Nombres descriptivos**: Funciones con nombres claros como `validateEmail()` no `vE()`

```javascript
// Bueno
function calculateTotal(price, quantity) {
    return price * quantity;
}

// Evitar
function calc(p, q) {
    return p * q;
}
```

### TypeScript

- Extiende `astro/tsconfigs/strict`
- Usar `interface` para objetos, `type` para uniones
- Props de componentes tipadas

```typescript
interface ServiceProps {
    title: string;
    description: string;
    icon: string;
}
```

### HTML semántico

- Usar etiquetas semanticas: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
- Cada seccion debe tener un heading (`<h1>` - `<h6>`)
- Usar `<button>` para acciones, `<a>` para enlaces

---

## Pattern de Componentes

### Estructura basica de un componente

```astro
---
// 1. Imports
import Icon from './Icon.astro';

// 2. Props (si aplica)
interface Props {
    title: string;
    variant?: 'primary' | 'secondary';
}

const { title, variant = 'primary' } = Astro.props;

// 3. Logica simple (evitar logica compleja en template)
const cssClass = `btn btn-${variant}`;
---

<button class={cssClass}>
    {title}
</button>

<style>
    .btn {
        padding: 0.75rem 1.5rem;
        border-radius: 0.5rem;
    }
</style>
```

---

## Errores Comunes a Evitar

1. **No te compliques**: Si sientes que necesitas una abstracción, pregúntate si realmente la necesitas
2. **No repitas código**: Si ves CSS duplicado, considera una clase global o CSS custom properties
3. **No mezcles responsabilidades**: Un componente = una responsabilidad
4. **No optimices prematuramente**: Primero hazlo funcionar, luego optimiza si es necesario
5. **No ignores el mobile**: Siempre probar en vista móvil

---

## Recursos

- [Documentación Astro](https://docs.astro.build)
- [Sintaxis Astro](https://docs.astro.build/en/basics/astro-syntax/)
