# How to Host This Project on GitHub Pages

This guide explains how this portfolio is published to **GitHub Pages** for free, and how to do the same for another Vue + Vite project.

🌐 Live site: **https://sreynich09.github.io/my-portfolio/**

---

## How it works (big picture)

```
You push code to main ──▶ GitHub Actions builds the site (npm run build)
                     ──▶ GitHub Pages publishes the dist/ folder
                     ──▶ Site is live at https://<username>.github.io/<repo-name>/
```

You don't upload files by hand. Every push to `main` updates the site automatically in about 1 minute.

---

## Part 1: One-time setup

These are already done for this repo. Follow them when you set up a **new** project.

### Step 1: Set the base path in `vite.config.js`

GitHub Pages serves a project site from a sub-folder (`/<repo-name>/`), so Vite needs to know that name.

```js
export default defineConfig({
  // Use the repo name on GitHub, "/" when running locally
  base: process.env.GITHUB_ACTIONS ? '/my-portfolio/' : '/',
  plugins: [vue()],
})
```

> ⚠️ Replace `my-portfolio` with **your repo name**. If it's wrong, the site shows a **blank page**.

### Step 2: Add the deploy workflow

Create the file `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: npm
      - run: npm ci
      - run: npm run build
      # Vue Router uses history mode: serve index.html for unknown paths
      - run: cp dist/index.html dist/404.html
      - uses: actions/upload-pages-artifact@v3
        with:
          path: dist

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

What each part does:

| Part | What it does |
| --- | --- |
| `on: push: branches: [main]` | Runs every time you push to `main` |
| `npm ci` | Installs packages from `package-lock.json` |
| `npm run build` | Builds the site into the `dist/` folder |
| `cp dist/index.html dist/404.html` | Makes links like `/about` work on refresh (needed for Vue Router) |
| `upload-pages-artifact` + `deploy-pages` | Publishes `dist/` to GitHub Pages |

### Step 3: Use correct paths for images in `public/`

Files in `public/` must use `import.meta.env.BASE_URL`, not a path starting with `/`:

```js
// ❌ Breaks on GitHub Pages
image: '/images/user-directory.png'

// ✅ Works locally and on GitHub Pages
image: `${import.meta.env.BASE_URL}images/user-directory.png`
```

> 💡 Don't name a folder in `public/` the same as a page route (e.g. `public/projects/` and the `/projects` page). GitHub will redirect the page to the folder.

### Step 4: Push the code to GitHub

```bash
git add .
git commit -m "Add GitHub Pages deployment"
git push origin main
```

### Step 5: Turn on GitHub Pages

1. Open your repo on GitHub → **Settings** → **Pages** (left menu).
2. Under **Build and deployment → Source**, choose **GitHub Actions**.
3. **Don't** click "Configure" on the Jekyll or Static HTML cards. We already have our own workflow.

### Step 6: Run the deploy

If the first run failed (because Pages wasn't turned on yet):

1. Go to the **Actions** tab.
2. Click the failed run.
3. Click **Re-run jobs** → **Re-run all jobs** → **Re-run jobs**.
   (Leave "Enable debug logging" unchecked.)

When both **build** and **deploy** are green ✅, open:
`https://<your-username>.github.io/<repo-name>/`

---

## Part 2: Updating the site (every day)

After the setup, updating is just three commands:

```bash
# 1. See what you changed
git status

# 2. Save your changes
git add .
git commit -m "Describe what you changed"

# 3. Send to GitHub (this starts the deploy)
git push origin main
```

Then:

1. Open the **Actions** tab on GitHub.
2. Wait about 1 minute for the run to turn green ✅.
3. Refresh your live site. If you still see the old version, hard-refresh with **Cmd + Shift + R** (Mac) or **Ctrl + Shift + R** (Windows).

### Check before you push

It's a good habit to test the build on your computer first:

```bash
npm run build     # must finish with "✓ built"
npm run preview   # open the shown link to check the built site
```

If `npm run build` fails on your computer, it will also fail on GitHub.

---

## Troubleshooting

| Problem | Cause | Fix |
| --- | --- | --- |
| **deploy** job fails with `Failed to create deployment (status: 404)` | GitHub Pages is not turned on | Settings → Pages → Source → **GitHub Actions**, then re-run the jobs |
| **build** job fails | Code error or missing package | Run `npm run build` locally, fix the error, push again |
| Site is a **blank white page** | Wrong `base` in `vite.config.js` | Set `base` to `'/<exact-repo-name>/'` |
| Images don't show | Image path starts with `/` | Use `` `${import.meta.env.BASE_URL}images/...` `` |
| Refreshing `/about` shows GitHub's 404 page | Missing `404.html` | Make sure the workflow has `cp dist/index.html dist/404.html` |
| Site still shows the old version | Browser cache | Hard-refresh (Cmd/Ctrl + Shift + R) or wait a minute |
| Warning: "Node.js 20 is deprecated" | GitHub notice about its own tools | Safe to ignore |

---

## If you rename the repo

1. Update `base` in `vite.config.js` to the new name.
2. Update your local remote:
   ```bash
   git remote set-url origin https://github.com/<username>/<new-repo-name>.git
   ```
3. Push. The new address will be `https://<username>.github.io/<new-repo-name>/`.
