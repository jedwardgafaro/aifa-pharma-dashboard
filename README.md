# 💊 AIFA Pharma Dashboard – Analisi Consumi Farmaceutici Italia 2024

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?logo=powerbi)
![DAX](https://img.shields.io/badge/DAX-Data%20Modeling-orange)
![Data](https://img.shields.io/badge/Fonte-AIFA%20Ufficiale-blue)
![Status](https://img.shields.io/badge/Status-Completato-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

## 📌 Descrizione del Progetto

Dashboard interattiva sviluppata con **Power BI** per l'analisi dei consumi farmaceutici in Italia nel 2024, basata su dati ufficiali dell'**AIFA (Agenzia Italiana del Farmaco)**.

Il progetto nasce dall'obiettivo di trasformare dati grezzi del sistema sanitario italiano in insight chiari e azionabili, utili a supportare decisioni strategiche in ambito farmaceutico e healthcare.

---

## 🎯 Obiettivi

- Analizzare la spesa farmaceutica totale per canale di distribuzione (convenzionata vs tracciabilità)
- Identificare le categorie terapeutiche con maggiore impatto sulla spesa pubblica
- Visualizzare la distribuzione geografica dei consumi per regione
- Costruire un modello dati scalabile e misure DAX riutilizzabili

---

## 📊 Dataset

| Attributo | Dettaglio |
|-----------|-----------|
| Fonte | [AIFA – Agenzia Italiana del Farmaco](https://www.aifa.gov.it) |
| Periodo | Anno 2024 |
| Righe | ~999+ record |
| Colonne | 17 variabili |
| Aggiornamento | Annuale (OsMed) |

**Variabili principali:**

| Colonna | Descrizione |
|---------|-------------|
| `anno` / `mese` | Dimensione temporale |
| `codreg` / `regione` | Dimensione geografica (20 regioni) |
| `classe` | Classe di rimborsabilità (A, C, H) |
| `atc1` → `atc4` | Gerarchia terapeutica ATC a 4 livelli |
| `descrizione_atc1` → `atc4` | Descrizioni delle categorie |
| `numero_confezioni_traccia` | Volumi canale ospedaliero |
| `spesa_flusso_tracciabilita` | Spesa canale ospedaliero |
| `numero_confezioni_convenzionata` | Volumi farmacia convenzionata SSN |
| `spesa_convenzionata` | Spesa farmacia convenzionata SSN |

---

## 🛠️ Tecnologie e Strumenti

```
Power BI Desktop
├── Power Query     → pulizia, trasformazione e imputazione valori nulli
├── DAX             → misure calcolate e KPI dinamici
├── Data Modeling   → relazioni e gerarchia ATC
└── Visual Design   → mappa, treemap, drill-down, slicer interattivi
```

---

## 📐 Misure DAX Principali

```DAX
Spesa Totale =
SUMX('AIFA', 'AIFA'[spesa_flusso_tracciabilita] + 'AIFA'[spesa_convenzionata])

Confezioni Totali =
SUMX('AIFA', 'AIFA'[numero_confezioni_traccia] + 'AIFA'[numero_confezioni_convenzionata])

Spesa per Confezione =
DIVIDE([Spesa Totale], [Confezioni Totali], 0)

Spesa Convenzionata % =
DIVIDE(SUM('AIFA'[spesa_convenzionata]), [Spesa Totale], 0) * 100

Spesa Ospedaliera % =
DIVIDE(SUM('AIFA'[spesa_flusso_tracciabilita]), [Spesa Totale], 0) * 100
```

---

## 📋 Struttura del Report

### 📈 Pagina 1 – Overview
- 4 Card KPI: Spesa Totale, Confezioni Totali, Spesa Ospedaliera %, Spesa Convenzionata %
- Istogramma: Spesa Totale per Mese
- Grafico a torta: Distribuzione Spesa per Canale
- Tabella: Top 10 Categorie Terapeutiche per Spesa
- Slicer: filtro per Mese

### 🗺️ Pagina 2 – Analisi Regionale
- Mappa coropletica: Spesa Totale per Regione
- Grafico a barre orizzontali: Ranking Regioni per Spesa
- Card: Confezioni Totali e Spesa per Confezione
- Slicer: filtro per Regione

### 💊 Pagina 3 – Categorie Terapeutiche
- Grafico a barre con Drill-down: Top 10 Categorie ATC1 → ATC2
- Grafico a torta: Distribuzione per Classe di Rimborsabilità
- Card: Spesa Totale e Confezioni Totali
- Slicer: filtro per Categoria ATC1

---

## 💼 Valore per il Business

| Beneficio | Descrizione |
|-----------|-------------|
| 🏥 Visione sanitaria | Panoramica completa della spesa farmaceutica pubblica italiana |
| 📍 Analisi geografica | Identifica regioni con maggiore o minore consumo |
| 💊 Focus terapeutico | Evidenzia categorie ad alto impatto sulla spesa SSN |
| 🔍 Drill-down interattivo | Navigazione dalla macro alla micro categoria ATC |
| ⚡ Decisioni data-driven | Strumento concreto per analisti e manager del settore pharma |

---

## 📁 Struttura del Repository

```
aifa-pharma-dashboard/
│
├── report/
│   └── AIFA_Pharma_Dashboard.pbix      # File Power BI principale
│
├── screenshots/
│   └── dashboard_overview.png          # Screenshot pagina Overview
│   └── dashboard_regionale.png         # Screenshot pagina Regionale
│   └── dashboard_categorie.png         # Screenshot pagina Categorie
│
└── README.md                           # Questo file
```

> ⚠️ **Nota:** Il dataset `.csv` non è incluso nel repository per limiti di dimensione.
> Per aggiornare i dati, scarica il file aggiornato da [AIFA – OsMed](https://www.aifa.gov.it/dati-consumo-farmaci) e collegalo al file `.pbix`.

---

## ⚙️ Come Aprire il Report

1. Scarica e installa **[Power BI Desktop](https://powerbi.microsoft.com/desktop/)** (gratuito)
2. Clona o scarica questo repository
3. Apri il file `report/AIFA_Pharma_Dashboard.pbix`
4. Se richiesto, aggiorna il percorso del dataset scaricandolo da [AIFA – OsMed](https://www.aifa.gov.it/dati-consumo-farmaci)
5. Esplora le 3 pagine del report tramite i tab in basso

---

## 🚀 Possibili Sviluppi Futuri

- Integrazione con dati storici AIFA (2020–2024) per analisi trend pluriennale
- Previsioni di spesa con modelli statistici in Python
- Confronto spesa Italia vs benchmark europei
- Dashboard ottimizzata per dispositivi mobile

---

## 👤 Autore

**Jhon Edward Gafaro Nieto**
📍 Modena, Italia
🔗 [LinkedIn](https://www.linkedin.com/in/edwardgafaro)
🐙 [GitHub](https://github.com/edwardgafaro)

---

## 📄 Licenza

Questo progetto è distribuito sotto licenza MIT. Vedi il file `LICENSE` per i dettagli.
