# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

@AGENTS.md

## Status

This is a fresh `create-next-app` scaffold (package name `infius8-system`): only `app/layout.tsx`, `app/page.tsx`, and `app/globals.css` exist. There is no application code, test framework, or test script yet.

## Commands

- `npm run dev`: dev server on http://localhost:3000 (Turbopack)
- `npm run build`: production build (also type-checks)
- `npm run start`: serve the production build
- `npm run lint`: ESLint 9 flat config (`eslint.config.mjs`, extends `eslint-config-next` core-web-vitals + typescript)

## Stack and non-default configuration

- **Next.js 16.4 / React 19.3, App Router only** (`app/`). Per AGENTS.md, check `node_modules/next/dist/docs/01-app/` before using any Next API instead of relying on memory.
- **`cacheComponents: true`** in `next.config.ts`: caching is opt-in through `"use cache"` and dynamic data has to sit inside `<Suspense>`. Read `node_modules/next/dist/docs/01-app/01-getting-started/08-caching.md` before adding data fetching. Patterns from the older rendering model (route segment config, `caching-without-cache-components.md`) don't apply here.
- **`partialPrefetching: true`** and **`experimental.agentFeedback: true`** are also on.
- **Tailwind CSS v4 runs through a Turbopack loader** (`@tailwindcss/turbopack`, configured under `turbopack.rules` for `*.css`), not PostCSS. There is no `postcss.config` or `tailwind.config`. Theme tokens are defined in CSS with `@theme inline` in `app/globals.css`.
- Layouts and pages use the globally generated route types (for example `LayoutProps<"/">`), produced by Next into `.next/types` and `next-env.d.ts`.
- Path alias: `@/*` maps to the repo root.
- Fonts: Geist and Geist Mono via `next/font/google`, exposed as the CSS variables `--font-geist-sans` and `--font-geist-mono`.
