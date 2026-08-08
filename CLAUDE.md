# Knowledge Garden — Religion & Spirituality

A Quartz v5 digital garden: 140 research-grade markdown notes on world religions, esotericism, and
comparative religious studies, organized by region. Built with Quartz (static site generator on
Preact/TypeScript) and deployed to GitHub Pages.

- Live site: https://cfuentesb30.github.io/knowledge-garden/
- Repo: cfuentesb30/knowledge-garden

## Specialist subagents

This project has dedicated subagents in `.claude/agents/` — prefer delegating to the matching one
instead of doing cross-cutting work generically:

- **quartz-backend** — build pipeline, plugin loader, CLI, worker/concurrency, `quartz/util`
- **quartz-frontend** — Preact components, client-side inline scripts, component registry/types
- **quartz-ui** — SCSS, theme colors/typography, dark mode, responsive styling
- **quartz-ux** — layout/navigation config, information architecture, discoverability
- **obsidian-content** — writing/editing notes in `content/`, Obsidian markdown syntax, frontmatter

## Architecture

Two clearly separated halves:

1. **`quartz/`** — the site generator engine. Only a *small* local core lives here:
   - `processors/` (parse → filter → emit pipeline), `plugins/pageTypes|filters|transformers|emitters`
     (the few built-in, non-remote plugins), `components/` (a handful of local Preact components +
     the component registry/type contracts), `util/`, `cli/`, `build.ts`, `worker.ts`.
   - **Most functional plugins and nearly all visible UI components are NOT in this repo.** They're
     declared in `quartz.config.yaml` under `plugins:` as `source: github:quartz-community/<name>`,
     pinned by commit in `quartz.lock.json`, and fetched into `.quartz/plugins/` by
     `npx quartz plugin install`. This includes search, graph view, explorer, backlinks, table of
     contents, tag pages, comments (Giscus), footer, dark mode, breadcrumbs, note-properties, etc.
   - Before assuming something is "missing" or needs new code, check whether it's actually a remote
     plugin whose behavior is controlled via `quartz.config.yaml` options.

2. **`content/`** — the actual notes (markdown + YAML frontmatter), Obsidian-flavored. Organized as:
   `Africa/`, `Americas/`, `Asia/`, `Cross-Regional/`, `Europe/`, `Middle East/`, plus `index.md`
   (site homepage) and `Library Index.md`.

Configuration:
- `quartz.config.yaml` — the live config (site title, baseUrl, theme colors/typography, full plugin
  list with options, layout positions per component). `quartz.config.default.yaml` is the upstream
  template default — don't edit it; it's not what builds this site.
- `quartz.lock.json` — pinned remote-plugin commit SHAs (a lockfile; prefer `quartz plugin install`
  over hand-editing).

## Commands

```bash
npm run install-plugins   # fetch remote plugins into .quartz/plugins per quartz.config.yaml
npx quartz build --serve  # local dev server with live rebuild
npm run check              # tsc --noEmit && prettier --check  — run before calling anything done
npm run format              # prettier --write
npm test                    # tsx --test (unit tests colocated as *.test.ts)
npx quartz build             # production build → public/
```

`prebuild` npm hook already runs `install-plugins` automatically before `npx quartz build`.

## Deployment (GitHub Pages)

- `.github/workflows/deploy-pages.yaml` triggers on push to `main`: `npm ci` →
  `npx quartz plugin install` → `npx quartz build` → `actions/upload-pages-artifact` →
  `actions/deploy-pages`.
- Pages source is set to "GitHub Actions" (`build_type: workflow`), not a branch — don't look for a
  `gh-pages` branch.
- `baseUrl` in `quartz.config.yaml` (`cfuentesb30.github.io/knowledge-garden`) **must** match the
  Pages URL exactly, or CSS/asset paths break. Check this first if a deploy "succeeds" but the live
  site looks broken.
- `ci.yaml`, `deploy-v5.yaml`, `deploy-preview.yaml`, `build-preview.yaml`, `docker-build-push.yaml`
  are all gated `if: github.repository == 'jackyzha0/quartz'` — inert on this fork, ignore them.

## Content conventions (see `obsidian-content` agent for full detail)

- Frontmatter: `title`, `description` minimum; `tags`, `aliases` also supported and surfaced via
  `note-properties`.
- Wikilinks (`[[Page]]`, `[[Page|alias]]`, `[[Page#Heading]]`) resolve by shortest unambiguous
  filename match (`crawl-links` config: `markdownLinkResolution: shortest`) — verify targets exist
  before linking; a bad wikilink fails silently rather than breaking the build.
- Editorial bar per `content/index.md`: historically grounded, source-aware, explicit about
  contested scholarship and common misrepresentations. Not encyclopedia-summary tone.
- Cross-linking matters here: graph view and backlinks are only useful if notes actually link to
  each other.

## Stack notes

- Preact (not React) — `jsxImportSource: "preact"` in `tsconfig.json`.
- Node >=22 (`.node-version` pins 22.16.0), npm >=10.9.2.
- SPA navigation is enabled (`enableSPA: true`) via `spa.inline.ts` (micromorph DOM diffing) — any
  client-side script must handle re-init on SPA route change, not just first page load.
