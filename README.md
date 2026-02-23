# Weiren's Blog

Personal blog built with [Astro](https://astro.build) using the [astro-devosfera](https://github.com/0xdres/astro-devosfera) theme.

Live at: https://blog.latentspaces.io

## Prerequisites

- Node.js 20+
- pnpm

## Development

```bash
pnpm install
pnpm run dev
```

## Build

```bash
pnpm run build
pnpm run preview
```

## Adding a new post

Create a new `.md` file in `src/data/blog/` with this frontmatter:

```yaml
---
title: Your Post Title
description: A brief description
pubDatetime: 2026-01-01T00:00:00Z
tags:
  - your-tag
draft: false
---
```

## Deployment

Deployed automatically to GitHub Pages via GitHub Actions on push to `main`.
