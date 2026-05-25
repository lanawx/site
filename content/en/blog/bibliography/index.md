---
title: "Working with Bibliography: Tools and Best Practices"
date: 2026-05-01
summary: "Overview of bibliography management systems: Zotero, Mendeley, EndNote. How to automate citation import in Hugo Academic."
draft: false
---

## Introduction

Proper bibliography formatting is the foundation of academic work. Modern tools make it possible to automate the collection, storage, and citation of sources.

## Bibliography Management Systems

| Tool | Platforms | Import from DOI/BibTeX | Free | Integration with Word/Google Docs |
|---|---|---|---|---|
| **Zotero** | Windows, Mac, Linux, Web | Yes | Yes (up to 300 MB cloud storage) | Yes |
| **Mendeley** | Windows, Mac, Linux, Web | Yes | Yes (2 GB cloud storage) | Yes |
| **EndNote** | Windows, Mac, Web | Yes | No (paid) | Yes |
| **JabRef** | Java (cross-platform) | Yes | Yes | Limited |

## Integration with Hugo Academic

The `wowchemy/starter-hugo-academic` theme supports automatic import of publications from a `.bib` (BibTeX) file.

### Step-by-Step Instructions

1. **Export publications** from Zotero/Mendeley in BibTeX format (`.bib`).

2. **Place the file** `publications.bib` in the `assets/` or `data/` folder.

3. **Run the Hugo command** to generate publication pages:
   ```bash
   hugo
