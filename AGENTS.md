# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A landing page built with Astro and Tailwind CSS (v4, via the Vite plugin), used as a playground for Astro components, layouts, and props. Package manager is **pnpm**.

## Commands

```
pnpm install       # install dependencies
pnpm dev            # start dev server at localhost:4321
pnpm build          # build production site to ./dist/
pnpm preview        # preview the production build locally
pnpm astro ...       # run the Astro CLI, e.g. `pnpm astro add`, `pnpm astro check`
```

There is no test suite and no linter configured in this project.

### Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

## Architecture

- **Routing**: Astro file-based routing — any `.astro`/`.md` file under `src/pages/` becomes a route. Currently only `src/pages/index.astro`, which composes the page from layout + components and passes page-specific data (e.g. the `features` array) down as props.
- **Composition pattern**: `src/layouts/Layout.astro` provides the HTML shell (`<html>`, `<head>`, global styles import, dark-mode flash prevention) and a `<slot />`; pages wrap their content in it. Reusable sections live in `src/components/` (`Header`, `Hero`, `Features`, `Footer`) as plain `.astro` components taking typed `Props` interfaces — no framework (React/Vue/etc.) is installed; everything is server-rendered Astro components with vanilla `<script>` for client-side behavior.
- **Styling**: Tailwind CSS v4 is wired in via `@tailwindcss/vite` in `astro.config.mjs` (no `tailwind.config.js` — v4 uses CSS-based config). `src/styles/global.css` imports Tailwind and defines a custom `dark` variant (`@custom-variant dark (&:where(.dark, .dark *))`) driven by a `.dark` class on `<html>`, toggled by an inline script in `Header.astro` and persisted to `localStorage`; `Layout.astro` has its own early inline script to prevent a flash of the wrong theme on load.
- **Client-side scripts**: Component-local behavior (theme toggle, GSAP animations) is added via `<script>` tags directly in the relevant `.astro` file rather than separate framework components. Use `<script is:inline>` only for logic that must run synchronously/early (e.g. theme detection before paint); use plain `<script>` (ES module, processed by Vite) when importing modules like GSAP.
- **Animations**: GSAP (`gsap` + `ScrollTrigger`) is a project dependency. Shared setup (plugin registration) lives in `src/scripts/gsap-setup.ts`, imported by component scripts that need it (e.g. `Header.astro` for scroll-triggered header transitions, `Features.astro` for scroll-reveal of feature cards). Always guard animations against `prefers-reduced-motion` — see the existing patterns in those two files before adding new ones.
- **Assets**: No `src/assets/` directory yet; only `public/favicon.ico` and `public/favicon.svg` exist. Use `public/` for static passthrough assets or Astro's `astro:assets` pipeline (`src/assets/` + `<Image />`) for optimized images if/when images are added.

## Available skills

GSAP official skills (`gsap-core`, `gsap-timeline`, `gsap-scrolltrigger`, `gsap-plugins`, `gsap-utils`, `gsap-react`, `gsap-performance`, `gsap-frameworks`) are installed under `.claude/skills/` — consult them for idiomatic GSAP patterns before writing new animation code. `astro`, `accessibility`, `seo`, and `tailwind-css-patterns` skills are also available and relevant to this stack.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)
