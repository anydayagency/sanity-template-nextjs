# Customization Checklist

Concrete things to swap when starting a new client project. Work top-to-bottom — each item names the file or env var to change.

## Project metadata

- [ ] `package.json` — `name`, `description`, `keywords`, `homepage`, `bugs.url`
- [ ] `frontend/package.json` — `name` if you want it more specific than `frontend`
- [ ] `studio/package.json` — `name`, `version`, `keywords`, `license`
- [ ] Root `README.md` — replace the upstream Sanity template intro with the client project intro
- [ ] `vercel-installation-instructions.md` — update the `[vercel-deploy]` URL at the bottom (currently points at `sanity-io/sanity-template-nextjs-clean`) or delete the file if not using Vercel one-click

## Sanity project wiring

- [ ] `frontend/.env.local` — `NEXT_PUBLIC_SANITY_PROJECT_ID`, `NEXT_PUBLIC_SANITY_DATASET`, `SANITY_API_READ_TOKEN`, `NEXT_PUBLIC_SANITY_STUDIO_URL`
- [ ] `studio/.env.local` — `SANITY_STUDIO_PROJECT_ID`, `SANITY_STUDIO_DATASET`, `SANITY_STUDIO_PREVIEW_URL`
- [ ] `studio/sanity.config.ts` — `projectId`, `dataset`, `name`, `title`
- [ ] `studio/sanity.cli.ts` — `projectId`, `dataset`
- [ ] `frontend/sanity.cli.ts` — `projectId`, `dataset`
- [ ] `frontend/sanity/lib/api.ts` — verify defaults match the new project

## Branding & assets

- [ ] `frontend/app/layout.tsx` — `metadata` (title, description, OG tags), root font, theme colors
- [ ] `frontend/app/favicon.ico`
- [ ] `frontend/public/images/` — replace `tile-1-*.png` and `tile-grid-*.png` or remove if unused
- [ ] `frontend/app/components/Header.tsx` — logo, nav, brand name
- [ ] `frontend/app/components/Footer.tsx` — links, copyright
- [ ] `frontend/app/globals.css` — design tokens (colors, fonts, spacing)
- [ ] `frontend/tailwind.config.ts` — theme extensions (palette, fonts, breakpoints)
- [ ] `sanity-next-preview.png` — replace the template screenshot or delete

## Content schema

- [ ] `studio/src/schemaTypes/documents/` — keep / extend / remove `page`, `post`, `person`
- [ ] `studio/src/schemaTypes/singletons/settings.tsx` — site settings (nav, footer, social)
- [ ] `studio/src/schemaTypes/objects/` — `blockContent`, `button`, `callToAction`, `infoSection`, `link` — adapt to the design system
- [ ] `studio/src/schemaTypes/index.ts` — register new types, drop unused ones
- [ ] `studio/src/structure/index.ts` — desk structure / singletons / grouping
- [ ] After changes: regenerate types — `npm run sanity:typegen --workspace=studio` (auto-runs via `predev`)

## Frontend rendering

- [ ] `frontend/app/page.tsx`, `frontend/app/[slug]/page.tsx`, `frontend/app/posts/[slug]/page.tsx` — adjust queries and layout
- [ ] `frontend/sanity/lib/queries.ts` — GROQ queries for new/changed schema
- [ ] `frontend/app/components/PageBuilder.tsx` and `BlockRenderer.tsx` — wire up new block types
- [ ] `frontend/app/components/Onboarding.tsx`, `GetStartedCode.tsx` — delete the upstream onboarding components once the client site has real content
- [ ] `frontend/app/sitemap.ts` — verify base URL and routes

## Sample data

- [ ] `studio/sample-data.tar.gz` — regenerate (`cd studio && sanity dataset export`) once you have real seed content, or remove if unused
- [ ] `package.json` `import-sample-data` script — remove if you removed the file

## Repo conventions (usually keep, occasionally tune)

- [ ] `.github/pull_request_template.md` — adjust sections for the client's review workflow
- [ ] `.github/workflows/pr-lint.yml` — semantic PR title check (allowed types match `commitlint.config.js`)
- [ ] `commitlint.config.js` — add scopes if you want a `scope-enum` rule
- [ ] `.husky/pre-commit` — currently runs `npm run lint`; add `type-check` here if the team wants it on every commit

## Agent / AI tooling (optional)

- [ ] `.agents/skills/` and `.claude/skills/` — keep the skill packs that apply to this project, prune the rest

## Repo housekeeping

- [ ] Add a `LICENSE` at the root (the studio is currently `UNLICENSED`)
- [ ] Update GitHub repo description and topics
- [ ] Set up GitHub branch protection on `main` (require PR, require `PR Lint` to pass)
- [ ] Configure Vercel project (Root Directory: `frontend`, env vars from `frontend/.env.local`)

## Final pass

- [ ] `git grep -i "sanity-template-nextjs"` — find any remaining upstream references
- [ ] `git grep -i "anydayagency"` — replace org references where the project should not advertise the agency
- [ ] `npm run lint && npm run type-check` — both green
- [ ] `npm run dev` — frontend and studio both load with real content
