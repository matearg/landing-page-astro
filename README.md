# MiProyecto — Landing Page con Astro

Landing page simple construida con [Astro](https://astro.build) y [Tailwind CSS](https://tailwindcss.com), pensada para explorar componentes, layouts y props de Astro.

## 🚀 Estructura del proyecto

```text
/
├── public/
│   ├── favicon.ico
│   └── favicon.svg
├── src/
│   ├── components/
│   │   ├── Header.astro
│   │   ├── Hero.astro
│   │   ├── Features.astro
│   │   └── Footer.astro
│   ├── layouts/
│   │   └── Layout.astro
│   ├── pages/
│   │   └── index.astro
│   └── styles/
│       └── global.css
└── package.json
```

Astro busca archivos `.astro` o `.md` dentro de `src/pages/`. Cada página se expone como una ruta según su nombre de archivo.

Los componentes reutilizables viven en `src/components/` (`Header`, `Hero`, `Features`, `Footer`), y `Layout.astro` define la estructura HTML base e importa los estilos globales (`src/styles/global.css`), donde se configura Tailwind CSS a través del plugin de Vite.

## 🧞 Comandos

Este proyecto usa **pnpm** como gestor de paquetes. Todos los comandos se ejecutan desde la raíz del proyecto:

| Comando                | Acción                                              |
| :---------------------- | :--------------------------------------------------- |
| `pnpm install`           | Instala las dependencias                             |
| `pnpm dev`               | Inicia el servidor de desarrollo en `localhost:4321` |
| `pnpm build`             | Compila el sitio de producción en `./dist/`          |
| `pnpm preview`           | Previsualiza el build localmente antes de deployar   |
| `pnpm astro ...`         | Ejecuta comandos de la CLI, como `astro add`         |
| `pnpm astro -- --help`   | Muestra la ayuda de la CLI de Astro                  |

## 👀 ¿Querés aprender más?

Consultá la [documentación oficial de Astro](https://docs.astro.build) o unite al [servidor de Discord](https://astro.build/chat).
