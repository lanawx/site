---
title: "How I Take Notes in Obsidian"
date: 2026-05-16
summary: "Experience using Obsidian to build a personal knowledge base: notes, connections between topics, and plugins for studying."
tags:
  - "obsidian"
  - "productivity"
  - "notes"
  - "workflow"
draft: false
---

## Introduction

Obsidian is a powerful tool for creating a linked note-taking system. Unlike regular text editors, it allows you to establish connections between ideas and build a knowledge graph.

## Why Obsidian instead of Notion or Evernote?

- **Local storage:** all notes are stored on your computer as plain Markdown files.
- **Speed:** instant search and note opening.
- **Free for personal use.**
- **Links:** bidirectional links between notes.

## How I structure my notes

### 1. Atomic notes

One note — one idea or concept. For example, instead of one large "Discrete Mathematics" note, I create separate notes:

- `Graphs.md`
- `Trees.md`
- `Dijkstra's Algorithm.md`

### 2. MOC (Maps of Content)

I create maps of content — notes that collect links to other notes on a topic:

```markdown
# Discrete Mathematics

- [[Graphs]]
- [[Trees]]
- [[Dijkstra's Algorithm]]
- [[Combinatorics]]
