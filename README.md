# Bologna CycleMap — Pipeline di Data Engineering Geospaziale

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![GeoPandas](https://img.shields.io/badge/GeoPandas-Geospatial-green)
![Parquet](https://img.shields.io/badge/Storage-Parquet-orange)
![Medallion](https://img.shields.io/badge/Architecture-Medallion-blue)

## Panoramica

Pipeline di Data Engineering per l'ingestione, validazione e trasformazione di dati geospaziali open source relativi alla rete ciclabile del Comune di Bologna. Il progetto implementa un'architettura Medallion (Raw → Processed) con storage Parquet, dimostrando la gestione end-to-end di dataset territoriali strutturati con GeoPandas.

Competenze applicabili in contesti di smart city, gestione infrastrutture fisiche, mobilità sostenibile e integrazione di dataset open geospaziali in piattaforme dati enterprise.

## Valore Enterprise

| Settore / Azienda | Rilevanza |
|-------------------|-----------|
| Utilities & Infrastrutture (Enel, Terna) | Pipeline per dati territoriali e infrastrutturali geospaziali |
| Smart City / PA | ETL per dataset open comunali e regionali |
| IT Consulting (NTT Data, Accenture) | Data Engineering geospaziale con stack Python moderno |
| Data Reply | Medallion Architecture su dati reali open source |

## Architettura Pipeline

```
GeoJSON (Comune di Bologna — Open Data)
        │
        ▼
ingest_data.py          ← validazione schema, caricamento GeoPandas, export Parquet
        │
        ▼
data/raw/               ← Bronze Layer (Parquet grezzo)
        │
        ▼
clean_data.py           ← drop colonne, snake_case, rimozione null, normalizzazione stringhe
        │
        ▼
data/processed/         ← Silver Layer (Parquet pulito)
```

## Dataset

| Campo | Tipo | Descrizione |
|-------|------|-------------|
| `geometry` | LineString | Tracciato geospaziale del percorso |
| `lunghezza` | float | Lunghezza segmento (metri) |
| `tipo_pista` | string | Tipologia infrastruttura ciclabile |
| `comune` | string | Comune di appartenenza |
| `anno_realizzazione` | int | Anno di realizzazione |

## Highlights Tecnici

- `ingest_data.py`: caricamento GeoJSON con GeoPandas, validazione schema, export Parquet tipizzato
- `clean_data.py`: drop colonne superflue, rinomina snake_case, rimozione null, normalizzazione stringhe
- Storage Parquet: compressione efficiente, tipizzazione preservata, pronto per query analitiche

## Setup

```bash
git clone https://github.com/sylver86/03-piste-ciclabili-bologna-data-engineering.git
cd 03-piste-ciclabili-bologna-data-engineering
pip install -r requirements.txt

python src/ingest_data.py    # GeoJSON → data/raw/
python src/clean_data.py     # data/raw/ → data/processed/
```

## Struttura Repository

```
03-piste-ciclabili-bologna-data-engineering/
├── src/
│   ├── ingest_data.py
│   └── clean_data.py
├── data/
│   ├── raw/
│   └── processed/
├── requirements.txt
└── README.md
```

## Stack Tecnologico

`Python 3.10+` · `GeoPandas` · `pandas` · `Parquet` · `Medallion Architecture`

---

---

# Bologna CycleMap — Geospatial Data Engineering Pipeline 🇬🇧

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![GeoPandas](https://img.shields.io/badge/GeoPandas-Geospatial-green)
![Parquet](https://img.shields.io/badge/Storage-Parquet-orange)

## Overview

Data Engineering pipeline for ingesting, validating, and transforming open-source geospatial data on Bologna's cycling network. Implements a Medallion Architecture (Raw → Processed) with Parquet storage, demonstrating end-to-end handling of structured territorial datasets with GeoPandas.

## Pipeline Architecture

```
GeoJSON (City of Bologna Open Data)
        │
        ▼
ingest_data.py      ← schema validation, GeoPandas load, Parquet export
        │
        ▼
data/raw/           ← Bronze Layer (raw Parquet)
        │
        ▼
clean_data.py       ← column pruning, snake_case rename, null removal, string normalization
        │
        ▼
data/processed/     ← Silver Layer (clean Parquet)
```

## Technical Highlights

- `ingest_data.py`: GeoJSON load via GeoPandas, schema validation, typed Parquet export
- `clean_data.py`: column pruning, snake_case normalization, null removal, string standardization
- Parquet storage: efficient compression, type preservation, optimized for analytical queries

## Setup

```bash
git clone https://github.com/sylver86/03-piste-ciclabili-bologna-data-engineering.git
cd 03-piste-ciclabili-bologna-data-engineering
pip install -r requirements.txt

python src/ingest_data.py    # GeoJSON → data/raw/
python src/clean_data.py     # data/raw/ → data/processed/
```

## Technologies

`Python 3.10+` · `GeoPandas` · `pandas` · `Parquet` · `Medallion Architecture`
