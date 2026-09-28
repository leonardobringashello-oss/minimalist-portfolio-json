<div align="center">

<h2>
  <em>Résumé</em> minimalista maquetado para web y PDF — Portfolio de Leonardo Bringas
</h2>
<p>
  Portfolio/CV imprimible gestionado con un único archivo <code>cv.json</code>, construido con Astro.
</p>

</div>

<div align="center">
  <a href="#-empezar">
    Empezar
  </a>
  <span>&nbsp;✦&nbsp;</span>
  <a href="#-comandos">
    Comandos
  </a>
  <span>&nbsp;✦&nbsp;</span>
  <a href="#-estructura">
    Estructura
  </a>
  <span>&nbsp;✦&nbsp;</span>
  <a href="#-personalizar">
    Personalizar
  </a>
  <span>&nbsp;✦&nbsp;</span>
  <a href="#-origen-y-créditos">
    Créditos
  </a>
</div>

<p></p>

<div align="center">

![Astro Badge](https://img.shields.io/badge/Astro-BC52EE?logo=astro&logoColor=fff&style=flat)
![JavaScript Badge](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=000&style=flat)
![TypeScript Badge](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=fff&style=flat)
![HTML5 Badge](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=fff&style=flat)
![CSS3 Badge](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=fff&style=flat)
![JSON Badge](https://img.shields.io/badge/JSON-000?logo=json&logoColor=fff&style=flat)
![Node.js Badge](https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=fff&style=flat)

</div>

## 🛠️ Stack

- [**Astro**](https://astro.build/) — framework web, render estático sin JS innecesario.
- [**TypeScript**](https://www.typescriptlang.org/) — tipado estricto (`astro/tsconfigs/strict`).
- **Menú de comandos propio** (`src/components/KeyboardManager.astro`) — paleta con `Ctrl`/`Cmd + J`, sin dependencias externas.
- **Diseño** guiado por la skill `.agents/skills/emil-design-eng` (detalles invisibles, animaciones < 300 ms, `prefers-reduced-motion`).

## 🚀 Empezar

### 1. Requisitos

- Node.js `>=22.12.0` (ver `engines` en `package.json`).

### 2. Instalar dependencias

```bash
npm install
```

### 3. Lanza el servidor de desarrollo

```bash
npm run dev
```

Abre [**http://localhost:4321**](http://localhost:4321/) en tu navegador para ver el resultado 🚀

## 🧞 Comandos

|     | Comando     | Acción                                                              |
| :-- | :---------- | :------------------------------------------------------------------ |
| ⚙️  | `dev`       | Lanza el servidor de desarrollo en `localhost:4321`.                |
| ⚙️  | `build`     | Genera el sitio estático de producción en `./dist/`.                |
| ⚙️  | `preview`   | Vista previa local del build de producción.                         |
| ⚙️  | `astro`     | Acceso directo al CLI de Astro.                                     |

```bash
npm run dev      # desarrollo
npm run build    # producción en ./dist/
npm run preview  # previsualizar el build
```

## 📁 Estructura

```text
.
├── astro.config.mjs              # Config de Astro (toolbar desactivada)
├── cv.json                       # Todo el contenido del CV/portfolio
├── tsconfig.json                 # Paths: @cv -> cv.json, @/* -> src/*
├── public/                       # Estáticos (favicon, imágenes)
├── src/
│   ├── assets/                   # Foto de perfil, etc.
│   ├── components/
│   │   ├── KeyboardManager.astro # Paleta de comandos (Ctrl/Cmd + J) + imprimir
│   │   ├── Section.astro         # Wrapper de sección (título + scroll-margin)
│   │   └── sections/
│   │       ├── Hero.astro        # Nombre, rol, ubicación, contacto
│   │       ├── About.astro       # Resumen (basics.summary)
│   │       ├── Experience.astro  # work[]
│   │       ├── Education.astro   # education[]
│   │       ├── Skills.astro      # skills[] con iconos + stagger
│   │       └── Projects.astro    # projects[]
│   ├── icons/                    # Iconos SVG propios (html, css, js, astro, python…)
│   ├── layouts/Layout.astro      # HTML base, fuentes Geist, tokens de easing
│   └── pages/index.astro         # Composición: Hero → About → Experience → Education → Skills → Projects
└── .agents/skills/emil-design-eng/SKILL.md  # Filosofía de polish UI aplicada
```

Los alias están definidos en `tsconfig.json`:

```json
{
  "compilerOptions": {
    "paths": {
      "@cv": ["./cv.json"],
      "@/*": ["./src/*"]
    }
  }
}
```

## ✏️ Personalizar

### 1. Editá `cv.json`

Todo el contenido sale de ahí. Secciones principales:

- `basics` — nombre, label, imagen, email, teléfono, ubicación, `profiles` (GitHub/X/LinkedIn).
- `work[]` — `name`, `position`, `startDate`, `endDate` (`null` = "Actual"), `summary`.
- `education[]` — `institution`, `area`, `studyType`, `startDate`, `endDate` (`null` = "Actualidad").
- `skills[]` — lista de `{ "name": "..." }`.
- `projects[]` — `name`, `description`, `highlights[]`, `url`, `isActive` (punto verde).

Fechas: se acepta `"YYYY-MM-DD"` o `null`. El código usa `String(fecha)` antes de `slice`/`new Date` para no romper el tipado cuando el JSON trae `null` literales.

### 2. Iconos de Skills

`src/components/sections/Skills.astro` mapea cada nombre a un icono de `src/icons/`:

| Skill en `cv.json` | Icono |
| :----------------- | :---- |
| HTML / CSS / JavaScript | `html` / `css` / `javascript` |
| Astro / TypeScript / Tailwind CSS | `astro` / `type` / `tailwind` |
| Git / GitHub | `git` / `GitHub` |
| Python / Node / SQL | `python` / `node` / `sql` |
| WebSockets / AI/LLMs | `plug` / `sparkles` |

Si agregás un skill nuevo, agregá su `.astro` en `src/icons/` (SVG 16×16, `stroke="currentColor"`) y una entrada en `SKILL_ICONS`.

### 3. Orden de secciones

Se cambia en `src/pages/index.astro` reordenando los componentes (`<Hero />`, `<About />`, …).

## ✨ Diseño y UX

La skill `emil-design-eng` se aplicó así:

- Tokens globales en `Layout.astro`: `--ease-out`, `--ease-in-out`, `--ease-drawer`.
- Transiciones con propiedades exactas (`transform`, `background-color`, `border-color`), nunca `transition: all`.
- Feedback de presión (`scale(0.97)`) y hover solo en `@media (hover: hover) and (pointer: fine)`.
- Entrada de Skills en cascada (35 ms por item, solo `transform` + `opacity`, sin `scale(0)`).
- `prefers-reduced-motion` desactiva movimiento; `print` deja el CV limpio en papel/PDF.

## 🖨️ Imprimir / PDF

- Presioná `Ctrl`/`Cmd + J` → "Imprimir CV", o `Ctrl/Cmd + P` directamente.
- Los estilos `@media print` ocultan el menú de comandos y dejan pills y tarjetas planas, sin sombras ni animaciones.

## 🌐 Deploy a GitHub Pages

El sitio se publica automáticamente en cada push a `main` con el workflow `.github/workflows/deploy.yml` (build de Astro + `actions/deploy-pages`).

- URL: <https://leonardobringashello-oss.github.io/minimalist-portfolio-json/>
- En `astro.config.mjs` están `site` y `base: "/minimalist-portfolio-json"` (requerido por ser project page, no user page).
- Los assets (`cv.json → image`, favicon) usan rutas relativas (`./...`) para que funcionen tanto en local como bajo el subpath de Pages.

## 📌 Origen y créditos

Contenido preservado del `README` original de este proyecto:

- Schema del JSON de CV:
  <https://jsonresume.org/schema/>
- Basado en el diseño de:
  <https://github.com/BartoszJarocki/cv>
  <https://cv.jarocki.me/>
- Vídeo de midudev "Crear portfolio minimalista Astro":
  <https://youtu.be/Zwh92LTB-Bk?t=4808>

Proyecto iniciado desde cero siguiendo el vídeo de midudev, personalizado para el portfolio de Leonardo Bringas, con secciones, iconos y polish propios.

## 🔑 Licencia

[MIT](LICENSE) — © 2026 Leonardo Bringas.
