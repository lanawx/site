---
title: "Персональный сайт на Hugo Academic"
date: 2026-05-16
summary: "Разработка и развёртывание сайта-портфолио с использованием генератора статических сайтов Hugo и темы Academic CV."
tags:
  - "hugo"
  - "github-pages"
  - "static-site"
  - "academic"
external_link: ""
---

## Задачи проекта

Настроить окружение Hugo (установка, создание сайта, подключение темы). Связать локальный репозиторий с GitHub. Настроить секцию social с академическими профилями (ORCID, Google Scholar, Mendeley, eLibrary). Добавить кастомные иконки при необходимости. Настроить деплой через GitHub Pages.

## Выполненные шаги

### 1. Установка Hugo Extended

В системе использовалась команда:

sudo apt update && sudo apt install hugo && hugo version

### 2. Создание нового сайта

hugo new site my-site && cd my-site

### 3. Инициализация Git и подключение темы Academic CV

git init && git submodule add https://github.com/HugoBlox/hugo-blox-builder.git themes/blox-builder

### 4. Настройка конфигурации

Были отредактированы следующие файлы в папке config/_default/:

hugo.yaml (базовые параметры сайта):
baseURL: "https://username.github.io/repo-name/"
title: "Персональный сайт"
enableGitInfo: true

params.yaml (параметры темы):
appearance:
  theme_day: "minimal"
  theme_night: "minimal"
  font: "minimal"
  font_size: "l"

menus.yaml (меню навигации):
main:
  - name: "Главная"
    url: "/"
    weight: 10
  - name: "Проекты"
    url: "/project/"
    weight: 30
  - name: "Посты"
    url: "/post/"
    weight: 40

### 5. Добавление профилей в authors/admin/_index.md

В секцию social были добавлены следующие ссылки:

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

### 6. Настройка деплоя через GitHub Pages

В корне сайта создан файл .github/workflows/hugo.yaml со следующим содержимым:

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

### 7. Публикация

После каждого git push сайт автоматически собирается и становится доступен по адресу: https://username.github.io/repository-name/

## Результат

Сайт полностью функционирует. Иконки социальных сетей отображаются корректно. Добавлены посты и страницы проектов. Настроен автоматический деплой.

## Использованные ресурсы

Документация Hugo (https://gohugo.io/documentation/), Тема Academic CV (https://hugoblox.com/templates/academic-cv/), GitHub Pages + Hugo (https://gohugo.io/hosting-and-deployment/hosting-on-github/), FontAwesome иконки (https://fontawesome.com/icons), Academic Icons (https://jpswalsh.github.io/academicons/)
