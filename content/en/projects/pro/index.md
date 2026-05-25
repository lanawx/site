---
title: "Personal Website on Hugo Academic"
date: 2026-05-16
summary: "Development and deployment of a portfolio website using the Hugo static site generator and the Academic CV theme."
tags:
  - "hugo"
  - "github-pages"
  - "static-site"
  - "academic"
external_link: ""
---

## Project Objectives

Set up the Hugo environment (installation, site creation, theme integration). Connect the local repository to GitHub. Configure the social section with academic profiles (ORCID, Google Scholar, Mendeley, eLibrary). Add custom icons if necessary. Set up deployment via GitHub Pages.

## Steps Completed

### 1. Installing Hugo Extended

The following command was used in the system:

sudo apt update && sudo apt install hugo && hugo version

### 2. Creating a new site

hugo new site my-site && cd my-site

### 3. Initializing Git and adding the Academic CV theme

git init && git submodule add https://github.com/HugoBlox/hugo-blox-builder.git themes/blox-builder

### 4. Configuration setup

The following files in the config/_default/ folder were edited:

hugo.yaml (basic site parameters):
baseURL: "https://username.github.io/repo-name/"
title: "Personal Website"
enableGitInfo: true

params.yaml (theme parameters):
appearance:
  theme_day: "minimal"
  theme_night: "minimal"
  font: "minimal"
  font_size: "l"

menus.yaml (navigation menu):
main:
  - name: "Home"
    url: "/"
    weight: 10
  - name: "Projects"
    url: "/project/"
    weight: 30
  - name: "Posts"
    url: "/post/"
    weight: 40

### 5. Adding profiles to authors/admin/_index.md

The following links were added to the social section:

social:
  - icon: "orcid"
    icon_pack: "ai"
    link: "https://orcid.org/0000-0002-1832-6805"
  - icon: "google-scholar"
    icon_pack: "ai"
    link: "https://scholar.google.com/"
  - icon: "mendeley"
    icon_pack: "ai"
    link: "https://www.mendeley.com/profiles/your-profile/"
  - icon: "github"
    icon_pack: "fab"
    link: "https://github.com/username"

### 6. Setting up deployment via GitHub Pages

A file .github/workflows/hugo.yaml was created in the site root with the following content:

name: Deploy Hugo site to Pages
on:
  push:
    branches: ["main"]
  workflow_dispatch:
permissions:
  contents: read
  pages: write
  id-token: write
concurrency:
  group: "pages"
  cancel-in-progress: false
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: recursive
      - uses: actions/configure-pages@v5
      - uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: "0.124.1"
          extended: true
      - run: hugo --minify
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./public
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - uses: actions/deploy-pages@v4

### 7. Publishing

After each git push, the site is automatically built and becomes available at: https://username.github.io/repository-name/

## Result

The site is fully functional. Social network icons display correctly. Posts and project pages have been added. Automatic deployment is configured.

## Resources Used

Hugo Documentation (https://gohugo.io/documentation/), Academic CV Theme (https://hugoblox.com/templates/academic-cv/), GitHub Pages + Hugo (https://gohugo.io/hosting-and-deployment/hosting-on-github/), FontAwesome Icons (https://fontawesome.com/icons), Academic Icons (https://jpswalsh.github.io/academicons/)
