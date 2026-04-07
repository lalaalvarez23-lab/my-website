# My Professional Website

A personal website built with [Astro](https://astro.build/).

---

## Deploying to GitHub Pages

This guide walks you through publishing your website for free using **GitHub Pages** — even if you've never deployed a website before.

---

## Prerequisites

Before you start, make sure you have:

- [Git](https://git-scm.com/downloads) installed on your computer
- A free [GitHub](https://github.com) account
- [Node.js](https://nodejs.org/) (v18 or higher) installed

To verify Git and Node are installed, open a terminal and run:

```bash
git --version
node --version
```

Both commands should print a version number. If they don't, install the missing tool first.

---

## Step 1 — Configure Astro for GitHub Pages

GitHub Pages serves your site from a URL like `https://your-username.github.io/your-repo-name/`. Astro needs to know this path so internal links work correctly.

Open `astro.config.mjs` and update the `site` and `base` fields:

```js
import { defineConfig } from 'astro/config';

export default defineConfig({
  site: 'https://your-username.github.io',
  base: 'your-repo-name',
});
```

Replace `your-username` with your GitHub username and `your-repo-name` with whatever you name your repository in Step 2.

> If you plan to use a custom domain (e.g. `yourname.com`), set `site` to that domain and remove the `base` field entirely.

---

## Step 2 — Create a GitHub Repository

1. Go to [github.com](https://github.com) and sign in.
2. Click the **+** icon in the top-right corner and select **New repository**.
3. Fill in the form:
   - **Repository name**: choose a name (e.g. `my-website`). This becomes part of your URL.
   - **Visibility**: choose **Public** (GitHub Pages is free for public repos).
   - Leave everything else as-is — do **not** initialize with a README.
4. Click **Create repository**.

You'll land on a page that shows your new empty repo. Keep this tab open.

---

## Step 3 — Connect Your Local Project to GitHub

Open a terminal in your project folder (the folder containing this README) and run these commands one at a time:

```bash
# Initialize a local Git repository (skip if already done)
git init

# Tell Git your name and email (only needed once per machine)
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Stage all your project files
git add .

# Create your first commit
git commit -m "Initial commit"

# Rename the default branch to 'main'
git branch -M main

# Connect your local project to the GitHub repo you just created
# Replace the URL below with the one shown on your GitHub repo page
git remote add origin https://github.com/your-username/your-repo-name.git

# Push your code to GitHub
git push -u origin main
```

After the last command, refresh your GitHub repo page — your files should now be there.

---

## Step 4 — Set Up Automatic Deployment with GitHub Actions

GitHub Actions will automatically build and publish your site every time you push changes to `main`.

Create the following file in your project (the folder path matters):

**`.github/workflows/deploy.yml`**

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
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run build
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist

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

After creating this file, push it to GitHub:

```bash
git add .github/workflows/deploy.yml
git commit -m "Add GitHub Actions deployment workflow"
git push
```

---

## Step 5 — Enable GitHub Pages in Repository Settings

1. On your GitHub repo page, click the **Settings** tab.
2. In the left sidebar, click **Pages**.
3. Under **Build and deployment**, set the **Source** to **GitHub Actions**.
4. Click **Save**.

---

## Step 6 — Watch Your Site Go Live

1. Click the **Actions** tab on your GitHub repo page.
2. You'll see a workflow run in progress — click it to watch the logs.
3. Once it shows a green checkmark, your site is live.

Your site will be published at:

```
https://your-username.github.io/your-repo-name/
```

---

## Making Updates

Whenever you want to update your site, just make your changes locally and push:

```bash
git add .
git commit -m "Describe what you changed"
git push
```

GitHub Actions will automatically rebuild and redeploy your site. Changes usually go live within 1–2 minutes.

---

## Troubleshooting

**My site loads but all the styles/images are broken.**
Make sure the `base` field in `astro.config.mjs` matches your repository name exactly (it's case-sensitive).

**The Actions workflow failed.**
Click the failed run in the Actions tab to read the error log. Common causes: missing `npm ci` before `npm run build`, or a typo in `astro.config.mjs`.

**I get a 404 when visiting my site URL.**
Double-check that GitHub Pages is set to use **GitHub Actions** as the source (Step 5). Also confirm the workflow completed successfully (green checkmark in the Actions tab).

**I want to use a custom domain (e.g. yourname.com).**
1. In your domain registrar, add a CNAME record pointing your domain to `your-username.github.io`.
2. In GitHub repo Settings > Pages, enter your custom domain.
3. Update `site` in `astro.config.mjs` to your custom domain and remove `base`.
