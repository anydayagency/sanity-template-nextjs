# Template Setup

How to spin up a new client project from this template. For end-user installation of the upstream Sanity template see [README.md](README.md). For converting a Vercel one-click deploy to local dev see [vercel-installation-instructions.md](vercel-installation-instructions.md).

## 1. Create the new repo

Use this repo as a GitHub template (**Use this template → Create a new repository**) or clone and re-init:

```shell
git clone --depth=1 https://github.com/anydayagency/sanity-template-nextjs.git <client-project>
cd <client-project>
rm -rf .git
git init -b main
```

Set the new GitHub remote:

```shell
git remote add origin <new-repo-url>
```

## 2. Install dependencies

```shell
npm install
```

This installs the root, `frontend/`, and `studio/` workspaces and runs `husky` to register the commit hooks.

## 3. Create the Sanity project

Either use [sanity.io/manage](https://www.sanity.io/manage) → **Create new project**, or run from `studio/`:

```shell
cd studio && npx sanity init --env
```

Note the **project ID** and **dataset name** — you need both for the env files below.

## 4. Configure environment variables

Copy the example env files in both workspaces:

```shell
cp frontend/.env.example frontend/.env.local
cp studio/.env.example studio/.env.local
```

Fill in:

- `frontend/.env.local` — `NEXT_PUBLIC_SANITY_PROJECT_ID`, `NEXT_PUBLIC_SANITY_DATASET`, `SANITY_API_READ_TOKEN` (create the token at [sanity.io/manage](https://www.sanity.io/manage) → API → Tokens, **Viewer** role).
- `studio/.env.local` — `SANITY_STUDIO_PROJECT_ID`, `SANITY_STUDIO_DATASET`.

## 5. Run the customization pass

Walk through [CUSTOMIZATION_CHECKLIST.md](CUSTOMIZATION_CHECKLIST.md) — package metadata, branding, schema, demo content, etc. Do this before importing sample data so the schema matches the project.

## 6. (Optional) Import sample data

Useful while iterating on the schema and frontend:

```shell
npm run import-sample-data
```

It targets the `production` dataset and uses `--replace`, so don't run it against a dataset that already has real content.

## 7. Run locally

From the project root:

```shell
npm run dev
```

- Next.js — [http://localhost:3000](http://localhost:3000)
- Studio — [http://localhost:3333](http://localhost:3333)

## 8. Deploy

- **Studio:** `cd studio && npx sanity deploy` — pick a hostname (`<client>.sanity.studio`).
- **Frontend:** create a Vercel project, set **Root Directory** to `frontend`, and add the same env vars from `frontend/.env.local`. Set `NEXT_PUBLIC_SANITY_STUDIO_URL` to the deployed Studio URL.

## What you get from this template

See [TEMPLATE_CONVERSION_SUMMARY.md](TEMPLATE_CONVERSION_SUMMARY.md) for what was added on top of the upstream Sanity template (commit hooks, PR conventions, agent skills, etc.) so you know what's intentional and what to tune.
