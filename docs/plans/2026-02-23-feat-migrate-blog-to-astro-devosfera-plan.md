---
title: "Migrate Blog from Eleventy to Astro with Devosfera Theme"
type: feat
date: 2026-02-23
---

# Migrate Blog from Eleventy to Astro with Devosfera Theme

## Overview

Migrate the existing Eleventy-based blog (blog.latentspaces.io) to Astro 5 using the [astro-devosfera](https://github.com/0xdres/astro-devosfera) template. This includes migrating all 17 existing blog posts, preserving the custom domain + GitHub Pages deployment, retaining Google Analytics / Web Vitals tracking, and adopting all devosfera features (terminal hero, glassmorphic UI, galleries, Pagefind search, aurora animations, cursor-glow effects).

## Problem Statement / Motivation

- The current Eleventy v0.12.1 setup is outdated (2021-era dependencies, Node 10/12/14 matrix)
- Astro 5 offers better DX: content collections with type safety, MDX support, faster builds, and a modern plugin ecosystem
- The devosfera theme provides a distinctive terminal/cyberpunk aesthetic with production-ready features (Pagefind search, OG image generation, light/dark mode, gallery system)
- Moving to Astro positions the blog for long-term maintainability with an actively maintained framework

## Proposed Solution

Replace the entire Eleventy stack with a fresh Astro project based on astro-devosfera, migrate all content, and adapt the deployment pipeline for GitHub Pages.

## Technical Approach

### Architecture Change

```
BEFORE (Eleventy)                    AFTER (Astro + Devosfera)
──────────────────                   ─────────────────────────
posts/*.md                    →      src/data/blog/*.md
_includes/layouts/*.njk       →      src/layouts/*.astro
_data/metadata.json           →      src/config.ts
css/main.css                  →      src/styles/global.css + typography.css
_11ty/ (plugins)              →      Astro integrations (MDX, Pagefind, Satori)
.eleventy.js                  →      astro.config.ts
rollup.config.js              →      (handled by Astro/Vite)
netlify.toml                  →      (removed - using GitHub Pages)
```

### Implementation Phases

#### Phase 1: Scaffold Astro Project

**Goal:** Get a working devosfera-based Astro project in the repo.

- [ ] Create a new branch `feat/astro-migration`
- [ ] Clone/download the astro-devosfera template into a temporary directory
- [ ] Remove all Eleventy-specific files from the repo:
  - `.eleventy.js`, `.eleventyignore`
  - `_11ty/` directory (custom plugins)
  - `_includes/` directory (Nunjucks templates)
  - `_data/` directory (metadata, CSP, analytics configs)
  - `css/`, `js/`, `src/` (old JS source), `fonts/`
  - `rollup.config.js`, `netlify.toml`
  - `functions/` (Netlify Functions)
  - `third_party/` (Eleventy plugins)
  - `test/` (Mocha tests)
  - `feed/` (old RSS config)
  - Old template files: `*.njk` (sitemap, archive, tags, etc.)
- [ ] Copy in the devosfera project structure:
  - `src/` (components, layouts, pages, styles, utils)
  - `public/` (static assets)
  - `astro.config.ts`
  - `tsconfig.json`
  - `eslint.config.js`
  - `.prettierrc.mjs`
- [ ] Copy `package.json` from devosfera and merge:
  - Keep devosfera dependencies as base
  - Add any analytics-related packages needed
- [ ] Install dependencies: `pnpm install`
- [ ] Verify the template builds: `pnpm run build`

**Files created/modified:**
- `package.json` (new, from devosfera)
- `pnpm-lock.yaml` (new)
- `astro.config.ts` (new)
- `tsconfig.json` (new)
- `src/**/*` (new, entire Astro source tree)

#### Phase 2: Configure Site Identity

**Goal:** Make the devosfera template reflect your blog identity.

- [ ] Update `src/config.ts` with site settings:
  ```typescript
  export const SITE = {
    website: "https://blog.latentspaces.io",
    author: "weirenlan",
    // ... timezone, toggle features
  };
  ```
- [ ] Update `src/constants.ts` with social links (GitHub, Twitter, etc.)
- [ ] Update any hardcoded site references in components
- [ ] Preserve the `CNAME` file in the repo root for GitHub Pages custom domain
- [ ] Update `public/robots.txt` or `src/pages/robots.txt.ts` with correct domain
- [ ] Test locally: `pnpm run dev` and verify site loads at localhost:4321

**Files modified:**
- `src/config.ts`
- `src/constants.ts`

#### Phase 3: Migrate Blog Posts (17 posts)

**Goal:** Convert all existing posts from Eleventy frontmatter format to Astro-devosfera format.

**Frontmatter Mapping:**

```yaml
# BEFORE (Eleventy)              # AFTER (Astro-devosfera)
---                               ---
title: "Post Title"               title: "Post Title"
description: "Desc"              description: "Desc"
date: 2023-02-25                  pubDatetime: 2023-02-25 00:00:00 UTC
tags:                             tags:
  - gpt                             - gpt
layout: layouts/post.njk          # REMOVED (Astro uses file-based routing)
---                               ---
```

**Migration steps for each post:**

- [ ] Copy all 17 `.md` files from `posts/` to `src/data/blog/`
- [ ] Rename files: remove leading underscore (e.g., `_chatgpt_hung_yi_lee.md` → `chatgpt-hung-yi-lee.md`)
- [ ] Transform frontmatter in each file:
  - `date: YYYY-MM-DD` → `pubDatetime: YYYY-MM-DD 00:00:00 UTC`
  - Remove `layout: layouts/post.njk` line
  - Keep `title`, `description`, `tags` as-is
  - Add `draft: false` explicitly
- [ ] Verify markdown content renders correctly (check for any Eleventy-specific shortcodes or Nunjucks syntax that needs conversion)
- [ ] Move any images referenced in posts to `src/assets/` or `public/` as appropriate
- [ ] Verify all 17 posts appear on the site: `pnpm run dev`

**Complete file list to migrate:**

| Old Path | New Path |
|----------|----------|
| `posts/_bose_soundcontrol.md` | `src/data/blog/bose-soundcontrol.md` |
| `posts/_build_blog_by_eleventy.md` | `src/data/blog/build-blog-by-eleventy.md` |
| `posts/_change_to_use_iterm2.md` | `src/data/blog/change-to-use-iterm2.md` |
| `posts/_chatgpt_hung_yi_lee.md` | `src/data/blog/chatgpt-hung-yi-lee.md` |
| `posts/_coscup_2022_risc_v_ai_ml.md` | `src/data/blog/coscup-2022-risc-v-ai-ml.md` |
| `posts/_coscup_2022_risc_v_instruct_emulator.md` | `src/data/blog/coscup-2022-risc-v-instruct-emulator.md` |
| `posts/_dsp_concepts.md` | `src/data/blog/dsp-concepts.md` |
| `posts/_enhance_plus.md` | `src/data/blog/enhance-plus.md` |
| `posts/_fda_orc_proposed_rules.md` | `src/data/blog/fda-orc-proposed-rules.md` |
| `posts/_git_use_resources.md` | `src/data/blog/git-use-resources.md` |
| `posts/_install_zsh_to_terminal.md` | `src/data/blog/install-zsh-to-terminal.md` |
| `posts/_knowles_aisonic.md` | `src/data/blog/knowles-aisonic.md` |
| `posts/_mlops_resources.md` | `src/data/blog/mlops-resources.md` |
| `posts/_note_of_effective_engineer.md` | `src/data/blog/note-of-effective-engineer.md` |
| `posts/_pytorch_pylightening_source.md` | `src/data/blog/pytorch-pylightening-source.md` |
| `posts/_source_share_to_college.md` | `src/data/blog/source-share-to-college.md` |
| `posts/_vscode_pylint.md` | `src/data/blog/vscode-pylint.md` |

#### Phase 4: Integrate Google Analytics & Web Vitals

**Goal:** Preserve analytics tracking in the new Astro site.

- [ ] Install analytics integration: consider `@astrojs/partytown` for non-blocking GA script loading, or use a direct `<script>` approach
- [ ] Add GA tracking snippet to `src/layouts/Layout.astro` (or equivalent base layout):
  ```astro
  <!-- Google Analytics -->
  <script async src="https://www.googletagmanager.com/gtag/js?id=GA_ID"></script>
  <script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', 'GA_ID');
  </script>
  ```
- [ ] Add Web Vitals tracking (use `web-vitals` npm package):
  ```typescript
  import { onCLS, onFID, onLCP } from 'web-vitals';
  ```
- [ ] Retrieve your actual GA ID from the old `_data/metadata.json` config (currently shows placeholder - update with real ID)
- [ ] Verify analytics events fire in dev tools Network tab

**Files modified:**
- `src/layouts/Layout.astro` (or base layout component)
- `package.json` (add web-vitals dependency if needed)

#### Phase 5: Update GitHub Actions for Astro Deployment

**Goal:** Deploy the Astro site to GitHub Pages with custom domain.

- [ ] Replace `.github/workflows/build-and-test.yml` with an Astro-specific GitHub Pages workflow:

  ```yaml
  # .github/workflows/deploy.yml
  name: Deploy to GitHub Pages

  on:
    push:
      branches: [main]

  permissions:
    contents: read
    pages: write
    id-token: write

  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v4
        - uses: pnpm/action-setup@v4
        - uses: actions/setup-node@v4
          with:
            node-version: 20
            cache: pnpm
        - run: pnpm install
        - run: pnpm run build
        - uses: actions/upload-pages-artifact@v3
          with:
            path: dist/

    deploy:
      needs: build
      runs-on: ubuntu-latest
      environment:
        name: github-pages
        url: ${{ steps.deployment.outputs.page_url }}
      steps:
        - id: deployment
          uses: actions/deploy-pages@v4
  ```

- [ ] Update `astro.config.ts` with correct `site` value:
  ```typescript
  export default defineConfig({
    site: "https://blog.latentspaces.io",
    // ... rest of config
  });
  ```
- [ ] Ensure `CNAME` file is in `public/` directory (so it copies to `dist/` on build)
- [ ] Remove old workflow file (`.github/workflows/build-and-test.yml`)
- [ ] Remove CodeQL workflow if not needed (`.github/workflows/codeql-analysis.yml`)
- [ ] Enable GitHub Pages with "GitHub Actions" as source in repo settings (Settings → Pages → Source: GitHub Actions)

**Files created/modified:**
- `.github/workflows/deploy.yml` (new)
- `.github/workflows/build-and-test.yml` (deleted)
- `astro.config.ts` (updated site URL)
- `public/CNAME` (moved from root)

#### Phase 6: SEO & Meta Preservation

**Goal:** Maintain search engine rankings and social sharing functionality.

- [ ] Verify sitemap generation works at `/sitemap-index.xml`
- [ ] Verify RSS feed at `/rss.xml`
- [ ] Check Open Graph meta tags render correctly for each post
- [ ] Verify `robots.txt` is correct
- [ ] Ensure Bing Webmaster and Azure verification meta tags are added to the base layout if still needed
- [ ] Consider adding URL redirects if post slugs change (old: `/posts/_chatgpt_hung_yi_lee/` → new: `/posts/chatgpt-hung-yi-lee/`)

**Files modified:**
- `src/layouts/Layout.astro` (add verification meta tags if needed)

#### Phase 7: Clean Up & Final Verification

**Goal:** Remove all Eleventy remnants and verify everything works.

- [ ] Delete remaining Eleventy-era files:
  - `posts/` directory (content moved to `src/data/blog/`)
  - `posts.json`
  - `img/` (unless images are referenced - move needed ones to `public/`)
  - `.nvmrc` (update to Node 20+ if keeping)
  - Old config files
- [ ] Update `.gitignore` for Astro (add `dist/`, `node_modules/`, `.astro/`)
- [ ] Update `README.md` with new development instructions
- [ ] Run full build: `pnpm run build`
- [ ] Run preview: `pnpm run preview` and test:
  - [ ] Homepage loads with terminal hero
  - [ ] All 17 posts are listed and accessible
  - [ ] Post content renders correctly (markdown, code blocks, links)
  - [ ] Tags/archives pages work
  - [ ] Search (Cmd+K) works and indexes all posts
  - [ ] Light/dark mode toggle works
  - [ ] Responsive layout works (mobile/tablet/desktop)
  - [ ] RSS feed is valid
  - [ ] Sitemap is valid
  - [ ] GA tracking fires
- [ ] Push to `feat/astro-migration` branch
- [ ] Test deployment via GitHub Actions
- [ ] Verify live site at blog.latentspaces.io
- [ ] Merge to `main` when verified

**Files deleted:**
- All files listed in Phase 1 removal
- `posts/` directory
- Old Eleventy-specific files

## Acceptance Criteria

### Functional Requirements

- [ ] All 17 blog posts are accessible at their new URLs
- [ ] Homepage displays post listing with devosfera terminal-style hero
- [ ] Full-text search works via Cmd+K / Ctrl+K (Pagefind)
- [ ] Tags and archives pages function correctly
- [ ] Light/dark mode toggle works
- [ ] RSS feed generates valid XML at `/rss.xml`
- [ ] Sitemap generates at `/sitemap-index.xml`
- [ ] OG images are dynamically generated for social sharing
- [ ] Google Analytics tracks page views
- [ ] All glassmorphic UI effects, aurora animations, and cursor-glow render

### Non-Functional Requirements

- [ ] Lighthouse score >= 90 on all categories
- [ ] Site builds in under 30 seconds
- [ ] Deployed via GitHub Actions to GitHub Pages
- [ ] Custom domain `blog.latentspaces.io` resolves correctly
- [ ] Node 20+ required (documented in README)

### Quality Gates

- [ ] `pnpm run build` succeeds with zero errors
- [ ] All posts render without broken links or missing images
- [ ] No console errors in browser dev tools
- [ ] Search indexes all posts correctly

## Dependencies & Prerequisites

- **Node.js 20+** must be available
- **pnpm** package manager must be installed
- GitHub Pages must be configured to use "GitHub Actions" as deployment source
- DNS for `blog.latentspaces.io` must continue pointing to GitHub Pages

## Risk Analysis & Mitigation

| Risk | Impact | Mitigation |
|------|--------|------------|
| Post URL slugs change, breaking old links | Medium | Add redirect rules or keep similar slugs |
| Some markdown content uses Eleventy-specific syntax | Low | Audit all posts for Nunjucks/shortcode usage |
| GA tracking ID is placeholder in current config | Low | User needs to provide actual GA ID |
| Image paths may break after migration | Medium | Audit image references in all posts and move assets |
| devosfera template updates after cloning | Low | Pin to specific commit/version |

## References & Research

### Internal References
- Current site config: `_data/metadata.json`
- Current post format: `posts/_chatgpt_hung_yi_lee.md` (representative example)
- Current deployment: `.github/workflows/build-and-test.yml`
- Custom domain: `CNAME` → `blog.latentspaces.io`

### External References
- Astro-devosfera template: https://github.com/0xdres/astro-devosfera
- Astro documentation: https://docs.astro.build
- Astro GitHub Pages deployment guide: https://docs.astro.build/en/guides/deploy/github/
- Pagefind documentation: https://pagefind.app
