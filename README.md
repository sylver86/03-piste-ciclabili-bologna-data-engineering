# Bike Lanes Bologna — Geospatial Data Engineering Pipeline

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![GeoPandas](https://img.shields.io/badge/GeoPandas-0.14+-119DFF?logo=python&logoColor=white)
![Parquet](https://img.shields.io/badge/Format-Parquet-50ABF1?logo=apacheparquet&logoColor=white)
![OpenData](https://img.shields.io/badge/Data-Open%20Data%20Bologna-brightgreen)

## Overview

End-to-end **geospatial data engineering pipeline** built on open municipal data from the City of Bologna.
The pipeline ingests GeoJSON data representing the city's cycle and pedestrian lane network, converts it to Parquet for efficient columnar storage, applies structured cleaning and standardisation, and produces a production-ready dataset for spatial analytics or downstream BI tools.

This project demonstrates core data engineering practices — **modularity**, **structured logging**, **error handling**, and **layered storage** (raw → processed) — applied to real-world geospatial data.

> Relevant to infrastructure and smart-city data use cases: energy grids, mobility networks, urban planning.

---

## Pipeline Architecture

```
Open Data Bologna (GeoJSON)
        │
        ▼
  [ ingest_data.py ]
  • Load GeoJSON into GeoDataFrame
  • Validate: shape, nulls, column count
  • Serialize to raw Parquet
        │
        ▼
  data/raw/piste-ciclopedonali.parquet
        │
        ▼
  [ clean_data.py ]
  • Drop redundant columns (geo_point_2d, duso, length)
  • Merge typology fields into single 'type' column
  • Rename columns to English snake_case standard
  • Null removal on critical fields (type, year_of_data)
  • Year standardisation → integer format
  • String normalisation: lowercase, strip, special chars removal
        │
        ▼
  data/processed/piste-ciclopedonali_cleaned.parquet
```

---

## Dataset

**Source:** [Open Data Comune di Bologna](https://opendata.comune.bologna.it) — Piste Ciclopedonali
**Format:** GeoJSON (geometry: LineString, CRS: WGS84)
**Coverage:** Full municipal network of cycle and pedestrian lanes

**Final schema after cleaning:**

| Column | Type | Description |
|--------|------|-------------|
| `code` | string | Lane unique identifier |
| `year_of_data` | int | Reference year |
| `type` | string | Lane typology (e.g. "pista ciclabile - sede propria") |
| `zone_name` | string | Municipal zone |
| `neighborhood_name` | string | Neighbourhood name |
| `length_meters` | float | Lane length in metres |
| `geometry` | geometry | LineString spatial geometry |

---

## Project Structure

```
03-piste-ciclabili-bologna-data-engineering/
├── src/
│   ├── ingest_data.py       # GeoJSON ingestion & raw Parquet export
│   └── clean_data.py        # Cleaning, standardisation & processed Parquet export
├── data/
│   ├── raw/                 # Raw Parquet (post-ingestion)
│   └── processed/           # Cleaned Parquet (pipeline output)
├── requirements.txt
└── .gitignore
```

---

## Setup & Usage

```bash
git clone https://github.com/sylver86/03-piste-ciclabili-bologna-data-engineering.git
cd 03-piste-ciclabili-bologna-data-engineering
pip install -r requirements.txt

# Step 1 — Ingestion
python src/ingest_data.py

# Step 2 — Cleaning
python src/clean_data.py
```

Logs are written to `logs/pipeline.log` with timestamped entries for each pipeline phase.

---

## Engineering Highlights

- **Layered storage pattern** (raw → processed) following Medallion Architecture principles
- **Structured logging** across all pipeline phases for full observability
- **Robust error handling** with graceful exits and exception tracing at each stage
- **GeoPandas** for native geospatial data management, preserving geometry through the entire pipeline
- **Parquet** as columnar storage format — optimised for analytical workloads and downstream tools

---

## Technologies

`Python 3.10+` · `GeoPandas` · `Pandas` · `Parquet` · `Logging` · `Regex`
