# KillerQueen-dust.github.io

Personal academic website for Siyu Liu, built from the
[PRISM](https://github.com/xyjoey/PRISM) academic homepage template.

The repository now contains the maintainable Next.js source rather than only
the generated GitHub Pages files. Site content is stored in `content/`, static
assets in `public/`, and the generated `out/` directory is intentionally not
committed.

## Development

Node.js 22 is required.

```bash
npm ci
npm run dev
```

Open <http://localhost:3000/>. Before publishing, run:

```bash
npm run lint
npm run build
```

To preview the exact static export:

```bash
python3 -m http.server 4173 --bind 127.0.0.1 --directory out
```

Pushing `main` triggers `.github/workflows/deploy.yml`, which builds `out/`
and publishes it to GitHub Pages.

See [MAINTENANCE.md](./MAINTENANCE.md) for the content editing and deployment
guide. The template is used under its MIT license; see [LICENSE](./LICENSE).
