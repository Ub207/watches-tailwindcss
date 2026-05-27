# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev      # Start development server at http://localhost:3000
npm run build    # Production build
npm run lint     # ESLint via next lint
npm run start    # Start production server (run build first)
```

No test suite is configured.

## Architecture

This is a **Next.js 14 App Router** project using TypeScript and Tailwind CSS. It is a static watch e-commerce showcase with no backend or database.

### Routing

Pages live in `src/app/` using the Next.js App Router file convention:
- `/` → `src/app/page.tsx` (delegates entirely to `HomeContent` component)
- `/about` → `src/app/about/page.tsx`
- `/watches` → `src/app/watches/page.tsx`
- `/contact` → `src/app/contact/page.tsx`

`src/app/layout.tsx` wraps every page with `<Header>` and `<Footer>`.

### Client vs. Server Components

- `Header` and `HomeContent` are `"use client"` components (use React state / AOS animations).
- All page components and `Footer` are server components (no directive needed).

### AOS Animations

AOS (Animate on Scroll) is initialized once in `HomeContent` via `useEffect`. The `data-aos="fade-up"` attribute is used on headings across pages, but AOS is only initialized in `HomeContent` — if a page is navigated to directly without visiting Home first, AOS attributes on other pages (`about`, `contact`) will not animate unless AOS is initialized in layout or those pages.

### Watch Data

Watch catalog is hardcoded as a local array in `src/app/watches/page.tsx`. Images are served from `public/`.

### Styling

Tailwind utility classes are used throughout. Global base styles (reset, font, background) are in `src/app/globals.css`. The Tailwind config (`tailwind.config.ts`) has no custom theme extensions beyond default gradient utilities.
