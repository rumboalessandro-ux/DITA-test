# DITA CI/CD Project

This repository contains a minimal DITA 1.3 documentation project with a GitHub Actions pipeline to build HTML5 and PDF output on each push to <code>main</code>.

## Struttura

- `src/maps/main.ditamap` — DITA map that references the topics
- `src/topics/introduction.dita` — Introduction topic
- `src/topics/getting-started.dita` — Getting started topic
- `themes/` — theme folder (empty placeholder)
- `.github/workflows/build-docs.yml` — GitHub Actions workflow
- `out/` — build output (ignored)

## Local build

Prerequisiti:

- Java 17+
- DITA Open Toolkit installato localmente

Esegui i comandi seguenti dalla root del repository:

```bash
dita -i src/maps/main.ditamap -f html5 -o out/html
dita -i src/maps/main.ditamap -f pdf2 -o out/pdf
```

## CI/CD

La pipeline GitHub Actions esegue:

- checkout del repository
- installazione di DITA-OT con `dita-ot/dita-ot-action@v1`
- compilazione in HTML5 e PDF
- pubblicazione dell'HTML su GitHub Pages su branch `gh-pages`
- caricamento del PDF come artefatto della run
# DITA-test
