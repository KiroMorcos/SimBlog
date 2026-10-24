# SimBlog Notes (EJS edition)

A notes / blog CRUD app — **EJS templates + vanilla JavaScript + LocalStorage**.
The EJS views are rendered to plain static HTML at build time, so the site can be hosted on **GitHub Pages**.

## Structure
```
views/            EJS templates (index.ejs + partials: head, header, dialogs, footer)
public/css/       style.css
public/js/        script.js   (all CRUD / search / Markdown / drafts logic)
site.js           shared template data (title, colours, sort options, toolbar buttons)
build.js          renders views → dist/ (static site for GitHub Pages)
server.js         local preview server (Express renders the same views)
.github/workflows/deploy.yml   auto-deploy to GitHub Pages
```

## Run locally
```
npm install
npm start          # http://localhost:3000  (live-renders the EJS views)
npm run build      # writes the static site to dist/
```

## Deploy on GitHub Pages
1. Push the project to GitHub (branch `main`).
2. Repo → **Settings → Pages → Source: GitHub Actions**.
3. Every push builds and publishes the site automatically.

> If this project sits inside a sub-folder of a bigger repo, move `.github/` to the repo root and add
> `working-directory: <folder>` to the install/build steps and `path: <folder>/dist` to the upload step.

## Why no Express routes / JSON file storage?
GitHub Pages only serves static files, so server routes (`app.post('/new')`, writing `notes.json`) can't run there.
Notes are stored in the browser's LocalStorage instead — the CRUD logic runs in `public/js/script.js`.

## Features
Markdown notes · undo after delete · autosaved drafts · coloured notes · grid/list toggle · pin · tags · search · sort ·
JSON export/import · dark/light theme · shortcuts (`/` search, `n` new note) · fully responsive.
