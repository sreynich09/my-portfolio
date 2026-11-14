<script setup>
import { ref } from 'vue'

const siteUrl = 'https://sreynich09.github.io/my-portfolio/'

const code = {
  flow: `You push code to main ──▶ GitHub Actions builds the site (npm run build)
                     ──▶ GitHub Pages publishes the dist/ folder
                     ──▶ Site is live at https://<username>.github.io/<repo-name>/`,
  vite: `export default defineConfig({
  // Use the repo name on GitHub, "/" when running locally
  base: process.env.GITHUB_ACTIONS ? '/my-portfolio/' : '/',
  plugins: [vue()],
})`,
  workflow: `name: Deploy to GitHub Pages

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
      url: \${{ steps.deployment.outputs.page_url }}
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4`,
  imageBad: `// ❌ Breaks on GitHub Pages
image: '/images/user-directory.png'`,
  imageGood: `// ✅ Works locally and on GitHub Pages
image: \`\${import.meta.env.BASE_URL}images/user-directory.png\``,
  firstPush: `git add .
git commit -m "Add GitHub Pages deployment"
git push origin main`,
  daily: `# 1. See what you changed
git status

# 2. Save your changes
git add .
git commit -m "Describe what you changed"

# 3. Send to GitHub (this starts the deploy)
git push origin main`,
  check: `npm run build     # must finish with "✓ built"
npm run preview   # open the shown link to check the built site`,
  rename: `git remote set-url origin https://github.com/<username>/<new-repo-name>.git`,
}

const workflowParts = [
  ['on: push: branches: [main]', 'Runs every time you push to main'],
  ['npm ci', 'Installs packages from package-lock.json'],
  ['npm run build', 'Builds the site into the dist/ folder'],
  [
    'cp dist/index.html dist/404.html',
    'Makes links like /about work on refresh (needed for Vue Router)',
  ],
  ['upload-pages-artifact + deploy-pages', 'Publishes dist/ to GitHub Pages'],
]

const problems = [
  {
    problem: 'deploy job fails with "Failed to create deployment (status: 404)"',
    cause: 'GitHub Pages is not turned on',
    fix: 'Settings → Pages → Source → GitHub Actions, then re-run the jobs',
  },
  {
    problem: 'build job fails',
    cause: 'Code error or missing package',
    fix: 'Run npm run build locally, fix the error, push again',
  },
  {
    problem: 'Site is a blank white page',
    cause: 'Wrong base in vite.config.js',
    fix: "Set base to '/<exact-repo-name>/'",
  },
  {
    problem: "Images don't show",
    cause: 'Image path starts with /',
    fix: 'Use import.meta.env.BASE_URL + "images/..."',
  },
  {
    problem: "Refreshing /about shows GitHub's 404 page",
    cause: 'Missing 404.html',
    fix: 'Make sure the workflow has cp dist/index.html dist/404.html',
  },
  {
    problem: 'Site still shows the old version',
    cause: 'Browser cache',
    fix: 'Hard-refresh (Cmd/Ctrl + Shift + R) or wait a minute',
  },
  {
    problem: 'Warning: "Node.js 20 is deprecated"',
    cause: 'GitHub notice about its own tools',
    fix: 'Safe to ignore',
  },
]

const toc = [
  { id: 'overview', label: 'How it works' },
  { id: 'setup', label: 'One-time setup' },
  { id: 'daily', label: 'Updating the site' },
  { id: 'troubleshooting', label: 'Troubleshooting' },
  { id: 'rename', label: 'Renaming the repo' },
]

const copied = ref('')
async function copy(key) {
  try {
    await navigator.clipboard.writeText(code[key])
    copied.value = key
    setTimeout(() => (copied.value = ''), 1500)
  } catch {
    // clipboard not available
  }
}
</script>

<template>
  <section class="mx-auto max-w-4xl px-4 py-16 sm:px-6 sm:py-24">
    <!-- Header -->
    <div class="mb-12 text-center">
      <p
        class="mb-2 text-sm font-semibold tracking-widest text-indigo-600 uppercase dark:text-indigo-400"
      >
        Guide
      </p>
      <h1 class="mb-4 text-4xl font-extrabold tracking-tight sm:text-5xl">
        Host a Vue site on <span class="text-gradient">GitHub Pages</span>
      </h1>
      <p class="mx-auto max-w-2xl text-lg text-slate-500 dark:text-slate-400">
        How this portfolio is published for free, and how to do the same for your own Vue + Vite
        project.
      </p>
      <a
        :href="siteUrl"
        class="mt-6 inline-flex items-center gap-2 rounded-full bg-indigo-50 px-4 py-2 text-sm font-medium text-indigo-700 transition hover:bg-indigo-100 dark:bg-indigo-500/15 dark:text-indigo-300 dark:hover:bg-indigo-500/25"
      >
        🌐 {{ siteUrl }}
      </a>
    </div>

    <!-- Table of contents -->
    <nav
      class="mb-14 flex flex-wrap justify-center gap-2 rounded-2xl border border-slate-200 bg-white p-4 dark:border-slate-800 dark:bg-slate-900"
    >
      <a
        v-for="item in toc"
        :key="item.id"
        :href="`#${item.id}`"
        class="rounded-full px-4 py-1.5 text-sm font-medium text-slate-600 transition hover:bg-slate-100 hover:text-indigo-600 dark:text-slate-300 dark:hover:bg-slate-800 dark:hover:text-indigo-300"
        >{{ item.label }}</a
      >
    </nav>

    <div class="guide space-y-16">
      <!-- Overview -->
      <article id="overview">
        <h2>How it works</h2>
        <div class="codeblock">
          <button class="copy" @click="copy('flow')">
            {{ copied === 'flow' ? 'Copied!' : 'Copy' }}
          </button>
          <pre><code>{{ code.flow }}</code></pre>
        </div>
        <p>
          You don't upload files by hand. Every push to <code>main</code> updates the site
          automatically in about 1 minute.
        </p>
      </article>

      <!-- Setup -->
      <article id="setup">
        <h2>Part 1 · One-time setup</h2>
        <p class="muted">
          These are already done for this portfolio. Follow them when you set up a new project.
        </p>

        <div class="step">
          <span class="num">1</span>
          <div class="min-w-0 flex-1">
            <h3>Set the base path in <code>vite.config.js</code></h3>
            <p>
              GitHub Pages serves a project site from a sub-folder
              (<code>/&lt;repo-name&gt;/</code>), so Vite needs to know that name.
            </p>
            <div class="codeblock">
              <button class="copy" @click="copy('vite')">
                {{ copied === 'vite' ? 'Copied!' : 'Copy' }}
              </button>
              <pre><code>{{ code.vite }}</code></pre>
            </div>
            <p class="callout warn">
              ⚠️ Replace <code>my-portfolio</code> with <strong>your repo name</strong>. If it's
              wrong, the site shows a <strong>blank page</strong>.
            </p>
          </div>
        </div>

        <div class="step">
          <span class="num">2</span>
          <div class="min-w-0 flex-1">
            <h3>Add the deploy workflow</h3>
            <p>Create the file <code>.github/workflows/deploy.yml</code>:</p>
            <div class="codeblock">
              <button class="copy" @click="copy('workflow')">
                {{ copied === 'workflow' ? 'Copied!' : 'Copy' }}
              </button>
              <pre><code>{{ code.workflow }}</code></pre>
            </div>
            <p>What each part does:</p>
            <div class="table-wrap">
              <table>
                <thead>
                  <tr>
                    <th>Part</th>
                    <th>What it does</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="[part, desc] in workflowParts" :key="part">
                    <td>
                      <code>{{ part }}</code>
                    </td>
                    <td>{{ desc }}</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <div class="step">
          <span class="num">3</span>
          <div class="min-w-0 flex-1">
            <h3>Use correct paths for images in <code>public/</code></h3>
            <p>
              Files in <code>public/</code> must use <code>import.meta.env.BASE_URL</code>, not a
              path starting with <code>/</code>:
            </p>
            <div class="codeblock">
              <pre><code>{{ code.imageBad }}</code></pre>
            </div>
            <div class="codeblock">
              <button class="copy" @click="copy('imageGood')">
                {{ copied === 'imageGood' ? 'Copied!' : 'Copy' }}
              </button>
              <pre><code>{{ code.imageGood }}</code></pre>
            </div>
            <p class="callout">
              💡 Don't name a folder in <code>public/</code> the same as a page route (e.g.
              <code>public/projects/</code> and the <code>/projects</code> page). GitHub will
              redirect the page to the folder.
            </p>
          </div>
        </div>

        <div class="step">
          <span class="num">4</span>
          <div class="min-w-0 flex-1">
            <h3>Push the code to GitHub</h3>
            <div class="codeblock">
              <button class="copy" @click="copy('firstPush')">
                {{ copied === 'firstPush' ? 'Copied!' : 'Copy' }}
              </button>
              <pre><code>{{ code.firstPush }}</code></pre>
            </div>
          </div>
        </div>

        <div class="step">
          <span class="num">5</span>
          <div class="min-w-0 flex-1">
            <h3>Turn on GitHub Pages</h3>
            <ol>
              <li>
                Open your repo on GitHub → <strong>Settings</strong> → <strong>Pages</strong> (left
                menu).
              </li>
              <li>
                Under <strong>Build and deployment → Source</strong>, choose
                <strong>GitHub Actions</strong>.
              </li>
              <li>
                <strong>Don't</strong> click "Configure" on the Jekyll or Static HTML cards. We
                already have our own workflow.
              </li>
            </ol>
          </div>
        </div>

        <div class="step">
          <span class="num">6</span>
          <div class="min-w-0 flex-1">
            <h3>Run the deploy</h3>
            <p>If the first run failed (because Pages wasn't turned on yet):</p>
            <ol>
              <li>Go to the <strong>Actions</strong> tab.</li>
              <li>Click the failed run.</li>
              <li>
                Click <strong>Re-run jobs</strong> → <strong>Re-run all jobs</strong> →
                <strong>Re-run jobs</strong> (leave "Enable debug logging" unchecked).
              </li>
            </ol>
            <p class="callout success">
              ✅ When both <strong>build</strong> and <strong>deploy</strong> are green, open
              <code>https://&lt;your-username&gt;.github.io/&lt;repo-name&gt;/</code>
            </p>
          </div>
        </div>
      </article>

      <!-- Daily -->
      <article id="daily">
        <h2>Part 2 · Updating the site</h2>
        <p>After the setup, updating is just three commands:</p>
        <div class="codeblock">
          <button class="copy" @click="copy('daily')">
            {{ copied === 'daily' ? 'Copied!' : 'Copy' }}
          </button>
          <pre><code>{{ code.daily }}</code></pre>
        </div>
        <p>Then:</p>
        <ol>
          <li>Open the <strong>Actions</strong> tab on GitHub.</li>
          <li>Wait about 1 minute for the run to turn green ✅.</li>
          <li>
            Refresh your live site. If you still see the old version, hard-refresh with
            <strong>Cmd + Shift + R</strong> (Mac) or <strong>Ctrl + Shift + R</strong> (Windows).
          </li>
        </ol>

        <h3 class="mt-8">Check before you push</h3>
        <p>It's a good habit to test the build on your computer first:</p>
        <div class="codeblock">
          <button class="copy" @click="copy('check')">
            {{ copied === 'check' ? 'Copied!' : 'Copy' }}
          </button>
          <pre><code>{{ code.check }}</code></pre>
        </div>
        <p>If <code>npm run build</code> fails on your computer, it will also fail on GitHub.</p>
      </article>

      <!-- Troubleshooting -->
      <article id="troubleshooting">
        <h2>Troubleshooting</h2>
        <div class="grid gap-4">
          <div
            v-for="p in problems"
            :key="p.problem"
            class="rounded-2xl border border-slate-200 bg-white p-5 dark:border-slate-800 dark:bg-slate-900"
          >
            <p class="!mb-2 font-semibold text-slate-800 dark:text-slate-100">{{ p.problem }}</p>
            <p class="!mb-1 text-sm"><span class="label">Cause</span>{{ p.cause }}</p>
            <p class="!mb-0 text-sm"><span class="label fix">Fix</span>{{ p.fix }}</p>
          </div>
        </div>
      </article>

      <!-- Rename -->
      <article id="rename">
        <h2>If you rename the repo</h2>
        <ol>
          <li>Update <code>base</code> in <code>vite.config.js</code> to the new name.</li>
          <li>Update your local remote:</li>
        </ol>
        <div class="codeblock">
          <button class="copy" @click="copy('rename')">
            {{ copied === 'rename' ? 'Copied!' : 'Copy' }}
          </button>
          <pre><code>{{ code.rename }}</code></pre>
        </div>
        <p>
          Push. The new address will be
          <code>https://&lt;username&gt;.github.io/&lt;new-repo-name&gt;/</code>.
        </p>
      </article>
    </div>
  </section>
</template>

<style scoped>
@reference "../assets/styles.css";

article {
  scroll-margin-top: 6rem;
}
.guide h2 {
  @apply mb-6 text-2xl font-bold sm:text-3xl;
}
.guide h3 {
  @apply mb-3 text-lg font-semibold;
}
.guide p {
  @apply mb-4 leading-relaxed text-slate-600 dark:text-slate-300;
}
.guide .muted {
  @apply text-slate-500 dark:text-slate-400;
}
.guide ol {
  @apply mb-4 list-decimal space-y-2 pl-6 text-slate-600 marker:text-indigo-500 dark:text-slate-300;
}
.guide :not(pre) > code {
  @apply rounded-md bg-slate-100 px-1.5 py-0.5 font-mono text-[0.85em] text-indigo-700 dark:bg-slate-800 dark:text-indigo-300;
}

.step {
  @apply mb-6 flex gap-4 rounded-2xl border border-slate-200 bg-white p-5 sm:p-6 dark:border-slate-800 dark:bg-slate-900;
}
.step .num {
  @apply grid h-9 w-9 shrink-0 place-items-center rounded-xl bg-gradient-to-br from-indigo-500 to-fuchsia-500 font-bold text-white;
}

.codeblock {
  @apply relative mb-4 overflow-hidden rounded-xl bg-slate-900 dark:bg-black/60 dark:ring-1 dark:ring-slate-800;
}
.codeblock pre {
  @apply overflow-x-auto p-4 pt-11 text-sm leading-relaxed text-slate-100 sm:pt-4 sm:pr-20;
}
.codeblock .copy {
  @apply absolute top-2 right-2 rounded-md bg-white/10 px-2.5 py-1 text-xs font-medium text-slate-200 transition hover:bg-white/20;
}

.callout {
  @apply rounded-xl border-l-4 border-indigo-400 bg-indigo-50 p-4 dark:bg-indigo-500/10;
}
.callout.warn {
  @apply border-amber-400 bg-amber-50 dark:bg-amber-500/10;
}
.callout.success {
  @apply border-emerald-400 bg-emerald-50 dark:bg-emerald-500/10;
}

.table-wrap {
  @apply mb-4 overflow-x-auto rounded-xl border border-slate-200 dark:border-slate-800;
}
table {
  @apply w-full text-left text-sm;
}
th {
  @apply bg-slate-50 px-4 py-2 font-semibold dark:bg-slate-800/60;
}
td {
  @apply border-t border-slate-200 px-4 py-2 text-slate-600 dark:border-slate-800 dark:text-slate-300;
}

.label {
  @apply mr-2 inline-block rounded-full bg-amber-100 px-2 py-0.5 text-xs font-semibold text-amber-700 dark:bg-amber-500/15 dark:text-amber-300;
}
.label.fix {
  @apply bg-emerald-100 text-emerald-700 dark:bg-emerald-500/15 dark:text-emerald-300;
}
</style>
