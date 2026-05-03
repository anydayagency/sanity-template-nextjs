# Template Conversion Summary

What this repo adds on top of the upstream [`sanity-io/sanity-template-nextjs-clean`](https://github.com/sanity-io/sanity-template-nextjs-clean). Read this if you're wondering "why is X here, was it already in the Sanity template or did we add it?"

## Commit & PR conventions

Conventional Commits are enforced locally and in CI.

- **`commitlint.config.js`** — extends `@commitlint/config-conventional`; restricts `type-enum` to `feat | fix | docs | style | refactor | perf | test | build | ci | chore`; enforces lowercase, no trailing period, 100-char header limit.
- **`.husky/commit-msg`** — runs `commitlint --edit` on every commit message.
- **`.husky/pre-commit`** — runs `npm run lint` before each commit.
- **`.github/workflows/pr-lint.yml`** — `amannn/action-semantic-pull-request@v5` validates PR titles against the same type list, lowercase subject required.
- **`.github/pull_request_template.md`** — Summary / Type of Change / What's Included / Breaking Changes / Notes / Test Plan structure.
- **`.github/copilot-commit-message-instructions.md`** — Conventional Commits v1.0.0 reference for AI assistants.

Dependencies added to root `package.json`:

- `@commitlint/cli`, `@commitlint/config-conventional`, `husky`
- `prepare` script: `husky || true` (no-op when husky isn't installed, e.g. CI without dev deps)

## Agent / AI tooling

Skill packs for AI assistants — not part of the upstream template, not required at runtime.

- **`.agents/skills/`**
  - `sanity-best-practices/` — framework-specific guidance (Next.js, Astro, Svelte, Hydrogen, Remix, Nuxt, Angular), GROQ, schema, page builder, portable text, visual editing, migrations, typegen, SEO, localization
  - `content-modeling-best-practices/` — taxonomy, separation of concerns, reference vs embedding, content reuse
  - `content-experimentation-best-practices/` — experiment design, statistical foundations, CMS integration, common pitfalls
  - `frontend-design/`, `web-design-guidelines/`
  - `executing-plans/`, `find-skills/`
- **`.claude/skills/`** — Claude-Code-specific subset (`find-skills`, `frontend-design`, `web-design-guidelines`)

Prune to what the client project actually needs.

## Documentation

- **`README.md`** — upstream content kept; **Template documentation** section added pointing at this file, the setup guide, and the customization checklist.
- **`TEMPLATE_SETUP.md`** — agency-side workflow for spinning up a new client project from this repo.
- **`CUSTOMIZATION_CHECKLIST.md`** — file-by-file list of what to change per project.
- **`vercel-installation-instructions.md`** — inherited from upstream; the `[vercel-deploy]` URL still points at `sanity-io/sanity-template-nextjs-clean` and needs to be re-pointed per client.

## Unchanged from upstream

The application itself — `frontend/` (Next.js 16 App Router, Tailwind 4, `next-sanity`, Sanity Live Content, Presentation/Visual Editing) and `studio/` (Sanity v5, Assist, Unsplash plugin, page builder schema) — is the upstream Sanity template. Treat changes there as deliberate divergence and document them in this file when they happen.

## Keeping in sync with upstream

The upstream template still gets occasional updates (Next.js version bumps, schema improvements). Approach:

1. Add upstream as a remote: `git remote add upstream https://github.com/sanity-io/sanity-template-nextjs-clean.git`
2. Fetch and diff: `git fetch upstream && git log --oneline HEAD..upstream/main`
3. Cherry-pick or merge selectively — most agency additions are in root configs, `.github/`, `.husky/`, `.agents/`, `.claude/`, so conflicts should be rare.
