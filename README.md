[![Страница приложения](https://img.shields.io/badge/Страница_приложения-green?style=for-the-badge)](%GITHUB_PAGE%)
[![Установить плагин](https://img.shields.io/badge/Установить_плагин-blue?style=for-the-badge&logo=data:image/svg%2bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAtOTYwIDk2MCA5NjAiIHdpZHRoPSIyNHB4IiBmaWxsPSIjZThlYWVkIj48cGF0aCBkPSJtNzIwLTgwIDEyMC0xMjAtMjgtMjgtNzIgNzJ2LTE2NGgtNDB2MTY0bC03Mi03Mi0yOCAyOEw3MjAtODBaTTQ4MC04MDAgMjQzLTY2M2wyMzcgMTM3IDIzNy0xMzctMjM3LTEzN1pNMTIwLTMyMXYtMzE4cTAtMjIgMTAuNS00MHQyOS41LTI5bDI4MC0xNjFxMTAtNSAxOS41LTh0MjAuNS0zcTExIDAgMjEgM3QxOSA4bDI4MCAxNjFxMTkgMTEgMjkuNSAyOXQxMC41IDQwdjE1OWgtODB2LTExNkw0NzktNDM0IDIwMC01OTZ2Mjc0bDI0MCAxMzl2OTJMMTYwLTI1MnEtMTktMTEtMjkuNS0yOVQxMjAtMzIxWk03MjAgMHEtODMgMC0xNDEuNS01OC41VDUyMC0yMDBxMC04MyA1OC41LTE0MS41VDcyMC00MDBxODMgMCAxNDEuNSA1OC41VDkyMC0yMDBxMCA4My01OC41IDE0MS41VDcyMCAwWk00ODAtNDkxWiIvPjwvc3ZnPg==)](https://360.topomatic.ru?extensionInstallPath=%GITHUB_PAGE_ENCODED%)

# Установка зависимостей

```sh
npm install
```

# Сборка

```sh
npm run build
```

# Отладка

```sh
npm run serve
```

# Развертывание GitHub Pages

.github/workflows/jekyll-gh-pages.yml
```yaml
name: Deploy Jekyll with GitHub Pages dependencies preinstalled

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Pages
        uses: actions/configure-pages@v5
      - name: Copy site
        run: |
          mkdir site
          cp ./README.md ./site/README.md
          cp ./_config.yml ./site/_config.yml
          cp -r ./docs ./site/docs
      - name: Build with Jekyll
        uses: actions/jekyll-build-pages@v1
        with:
          source: ./site
          destination: ./jekyll
      - name: Build plugin
        run: |
          mkdir dist
          cp ./package.json ./dist/package.json
          cp -r ./src ./dist/src
          cp -r ./icons ./dist/icons
          cp -r ./locales ./dist/locales
          cp -a ./jekyll/. ./dist/
      - name: Upload Artifact Site
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy Site to GitHub Pages
        id: deployment-site
        uses: actions/deploy-pages@v4
```

# Установка

```typescript
const extensionPath = '%GITHUB_PAGE%'
const href = `https://360.topomatic.ru?extensionInstallPath=${encodeURIComponent(extensionPath)}`;
```
