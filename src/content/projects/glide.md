---
title: "Glide — Visual Editor for Web Dev Servers"
description: "Select elements, edit text, adjust spacing, and apply changes directly to your source files — all from the browser. Works with React, Vue, and Angular."
tags: ["TypeScript", "React", "Vue", "Angular", "Developer Tools"]
github: "https://github.com/ArjunSuraj/glide"
featured: true
order: 1
---

## Overview

Glide is a visual editor that sits on top of your running dev server. Select any element in the browser, edit text inline, adjust spacing, and confirmed changes are written back to your source files automatically.

## How It Works

1. Start your dev server as usual (`npm run dev`, `ng serve`, etc.)
2. Run `npx glide` in a second terminal
3. Glide opens a local proxy in your browser with an editing overlay
4. Select elements to see their component name, file path, and line number
5. Make changes visually — they get written to source

## Key Features

- **Element selection** — click any element to see its component, file path, and line number
- **Inline text editing** — double-click to edit text directly in the browser
- **Spacing controls** — adjust margins and padding visually
- **Property sidebar** — edit layout, typography, colors via a panel
- **Batch changes** — stage multiple edits and apply them together
- **Undo support** — revert individual changes or reset everything
- **Element reordering** — drag to reorder sibling elements (React)

## Framework Support

| Framework | Build Tool | Status |
|-----------|-----------|--------|
| React | Vite, Next.js, CRA | Full support |
| Vue | Vite, Nuxt | Full support |
| Angular | Angular CLI | Full support |

## Architecture

```
packages/
  cli/      # CLI, proxy server, and source transforms
  overlay/  # Injected browser overlay
  shared/   # Shared TypeScript types
```

The proxy intercepts the dev server output, injects the overlay script, and maps visual changes back to source file locations using source maps and AST analysis.

## Quick Start

```bash
npx glide-editor@latest
```

Or install as a dev dependency so the whole team gets it:

```bash
npm install -D glide-editor
npx glide init
```
