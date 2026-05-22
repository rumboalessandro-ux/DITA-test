# DITA CI/CD Project — Specifica per Claude Code

## Obiettivo

Crea un progetto DITA minimale con pipeline CI/CD per compilare automaticamente la documentazione ad ogni push.

## Stack

| Componente | Strumento |
|---|---|
| Processore DITA | DITA-OT (Java 17+) |
| CI/CD | GitHub Actions |
| Output | HTML5 + PDF (Apache FOP) |
| Pubblicazione | GitHub Pages (branch `gh-pages`) |

## Struttura directory

```
dita-project/
├── .github/
│   └── workflows/
│       └── build-docs.yml
├── src/
│   ├── maps/
│   │   └── main.ditamap
│   └── topics/
│       ├── introduction.dita
│       └── getting-started.dita
├── themes/
├── out/
├── .gitignore
└── README.md
```

## Dettaglio file

### `src/maps/main.ditamap`
- Mappa DITA 1.3 valida
- Titolo: "My Documentation"
- Referenzia entrambi i topic in `../topics/`

### `src/topics/introduction.dita`
- Struttura `<topic>` DITA 1.3 valida
- Contenuto placeholder realistico (non lorem ipsum)
- Titolo: "Introduction"

### `src/topics/getting-started.dita`
- Struttura `<topic>` DITA 1.3 valida
- Contenuto placeholder realistico
- Titolo: "Getting Started"

### `.github/workflows/build-docs.yml`
- Trigger: push su branch `main`
- Step 1: checkout repo
- Step 2: installa DITA-OT usando l'action ufficiale `dita-ot/dita-ot-action@v1`
- Step 3: compila in HTML5 → `out/html/`
- Step 4: compila in PDF → `out/pdf/`
- Step 5: pubblica `out/html/` su GitHub Pages (branch `gh-pages`)
- Step 6: carica il PDF come artefatto scaricabile dalla run

### `.gitignore`
- Escludi `out/`
- Escludi `*.log`
- Escludi cartelle temporanee Java (`.dita-ot-*/`)

### `README.md`
- Breve descrizione del progetto
- Istruzioni per compilare localmente:
  ```bash
  dita -i src/maps/main.ditamap -f html5 -o out/html
  dita -i src/maps/main.ditamap -f pdf2 -o out/pdf
  ```
- Prerequisiti: Java 17+, DITA-OT installato localmente

## Vincoli

- Versione DITA target: **1.3**
- Usare `dita-ot/dita-ot-action@v1` nel workflow (non installazione manuale di DITA-OT)
- Il plugin PDF è `org.dita.pdf2`, già incluso in DITA-OT — nessun plugin aggiuntivo
- La cartella `themes/` va creata ma può restare vuota