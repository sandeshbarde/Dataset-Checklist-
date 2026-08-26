# Upstream Oil & Gas / Geothermal Pipeline Dataset

This directory contains curated, multi-modal drilling and geologic datasets organized according to the pipeline specification.

## Directory Structure & Dataset Inventory

`
/data
├── /wcr_digital/          # (10 PDFs) Digital-native Well Completion Reports with full text layer
├── /wcr_scanned_clean/    # (6 PDFs) Scanned historical reports with clean OCR-able layouts (USGS NPRA / CA)
├── /wcr_scanned_bad/      # (6 PDFs) Degraded edge-case scans (blur, skew, noise, low-light, annotations)
├── /well_metadata/        # (2 CSVs) Well geospatial, operational, and formation index data
├── /trajectory_survey/    # (10 files) Directional surveys in CSV and CWLS LAS 2.0 format
├── /ddr_daily_reports/    # (8 files) Daily Drilling Reports (DDRs) based on Equinor Volve Field
├── /glossary/             # (3 files) Drilling terminology, abbreviations, and units (CSV, JSON, MD)
├── /mock_incidents/       # (2 files) 15 synthetic incident records (mud loss, kick, stuck pipe, H2S)
└── /geo_ner/              # (7 files) Official BGS Geo-NER dataset (training, testing, gazetteer)
`

---

### 1. Well Completion Reports (WCRs)
- **/wcr_digital/**: 10 authentic digital-native Well Completion Reports (California DWR OSWCR standard format). Complete with well header, geospatial coordinates, casing/annular seals, formation intervals, water/hydrocarbon shows, and driller certification.
- **/wcr_scanned_clean/**: 6 clean historical well reports modeled on USGS North Inigok No. 1 and Alaska NPRA exploratory tests, with typed typewriter font, official branch stamps, and signatures.
- **/wcr_scanned_bad/**: 6 edge-case degraded scans simulating real-world document challenges (heavy Gaussian blur, high-contrast fax speckle noise, 9-degree skew rotation, low-light underexposure, faded contrast, and handwritten margin notes/stains).

### 2. Well Location & Geospatial Metadata (/well_metadata/)
- wells_metadata.csv: Master metadata for 18 wells across California (Kern County / Sacramento Basin), Alaska North Slope (NPRA Inigok), and North Sea (Equinor Volve). Includes Well ID, API Number, Lat/Long, Elevation, Spud Date, Completion Date, TD, Formation, Well Type, and Status.
- ca_dwr_oswcr_index.csv: Index of California DWR OSWCR well reports linked to their respective PDF filenames.

### 3. Trajectory Surveys & Daily Drilling Reports (/trajectory_survey/ & /ddr_daily_reports/)
- Directional survey computations using minimum curvature algorithm for Volve 15/9-F-12, Volve 15/9-F-14, USGS Inigok No. 1, Elk Hills Pioneer-22B, and Kern River Horizon-01.
- Both **CSV** and standard **CWLS LAS 2.0** formats containing MD, INC, AZI, TVD, DX_EAST, DY_NORTH, TVDSS, and DLS.
- 7 Daily Drilling Reports (DDRs) capturing operational progress, BHA runs, mud properties, and formation encounters.

### 4. Domain Glossary (/glossary/)
- Structured domain dictionary (drilling_terms.csv, drilling_terms.json, bbreviations.md) covering key abbreviations and operational parameters: ROP, WOB, RPM, SPP, BOP, LCM, ECD, NPT, Kick, Stuck Pipe, TVD, MD, DLS, BHA, MWD, LWD, LOT, FIT, TOC, Mud Weight, PV, YP, PDC, KOP, H2S, etc.

### 5. Mock Incidents (/mock_incidents/)
- 15 structured synthetic drilling incident records (incidents.json and incidents.csv) covering mud loss, stuck pipe, gas kick, twist-off, H2S influx, pack-off, cement channeling, and permafrost subsidence. Tagged to specific wells, depths, timestamps, NPT hours, estimated financial impact, root cause, and mitigation actions.

### 6. Geological NER Dataset (/geo_ner/)
- Official British Geological Survey (BGS) Stratigraphic Named Entity Recognition dataset downloaded directly from the BGS repository (gs.3class.geo-all-data.txt, gs.3class.geo-training-data.txt, gs.3class.geo-testing-data.txt, ocab.gaz.txt).