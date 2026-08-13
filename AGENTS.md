# Repository guide

## Project identity

This is the source repository for `https://killerqueen-dust.github.io/`, an
academic homepage based on PRISM v1.3.3 (upstream commit
`f2748db9821e98ed487eee5104ce4cc282aa8c1e`). The repository name
`KillerQueen-dust.github.io` must remain unchanged because GitHub requires the
`<username>.github.io` name for a user Pages site.

The old committed static export was replaced with maintainable source. Do not
restore or hand-edit generated root-level HTML, `.txt`, or `_next/` files.

## Runtime and commands

- Use Node.js 22, as declared by `.nvmrc` and `package.json`.
- Install exactly from the lockfile with `npm ci`.
- Run the development server with `npm run dev` (default URL:
  `http://localhost:3000/`).
- Before handing off changes, run `npm run lint`, `npm run build`, and
  `npm audit`.
- `npm run build` creates the ignored static export in `out/`.
- Preview the production export with
  `python3 -m http.server 4173 --bind 127.0.0.1 --directory out`.

## Content ownership

User-maintained content belongs in `content/`:

- `config.toml`: site metadata, profile, social links, features, navigation.
- `about.toml`: home-page sections and research interests.
- `bio.md`: biography.
- `news.toml`: news entries.
- `publications.bib`: publications and PRISM-specific BibTeX fields.
- `teaching.toml`, `awards.toml`, `services.toml`: card pages.
- `cv.md`: CV body; `cv.toml` only configures the page.

Static assets belong in `public/`. The profile image is `public/ganyu.jpg`,
the favicon is `public/favicon.svg`, and publication previews live under
`public/papers/`. BibTeX `preview` values are filenames relative to that
papers directory.

Prefer content/config edits over React changes. Preserve valid TOML, Markdown,
and BibTeX syntax. Update `site.last_updated` in `content/config.toml` for
visible content changes.

## Framework notes

The source originated from PRISM, then received a compatibility/security
upgrade to Next.js 16.3.0 and native ESLint flat config. PRISM's unused webpack
`.bib` rule was removed because BibTeX is read with `fs`; do not reintroduce it
without a real imported-asset use case. The shared `useIsMounted` hook avoids
hydration mismatches and React 19 set-state-in-effect lint failures.

Do not commit `node_modules/`, `.next/`, or `out/`. Keep
`public/.nojekyll`, because the generated `_next/` asset directory must be
served unchanged by GitHub Pages.

## Deployment

`.github/workflows/deploy.yml` is the only deployment path. A push to `main`
or manual workflow dispatch installs with `npm ci`, lints, builds, uploads
`out/`, and deploys through GitHub Pages Actions. The repository Pages source
must be set to **GitHub Actions**, not “Deploy from a branch.”

The Git remotes should be:

- `origin`: `https://github.com/KillerQueen-dust/KillerQueen-dust.github.io.git`
- `upstream`: `https://github.com/xyjoey/PRISM.git`

When reviewing upstream changes, port them selectively; never overwrite the
personal `content/` or `public/` data wholesale.

<!-- BEGIN:nextjs-agent-rules -->

# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->
