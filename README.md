# Dataset-Checklist-

Upstream Oil & Gas / Geothermal Exploration & Drilling Dataset.

Organized into exact pipeline-ready structures for document processing, OCR evaluation, Named Entity Recognition (NER), trajectory survey analysis, geospatial mapping, and incident correlation.

## Directory Structure

`
/data
├── /wcr_digital/          # (10 PDFs) Digital-native Well Completion Reports (selectable text layer)
├── /wcr_scanned_clean/    # (6 PDFs)  Scanned historical reports (USGS NPRA & CA archives)
├── /wcr_scanned_bad/      # (6 PDFs)  Degraded edge-case scans (blur, skew, noise, low-light)
├── /well_metadata/        # (2 CSVs)  Master well index, lat/long coordinates, formations, TD
├── /trajectory_survey/    # (10 files) Directional surveys in CSV and CWLS LAS 2.0 format
├── /ddr_daily_reports/    # (8 files) Daily Drilling Reports (DDRs) based on Equinor Volve
├── /glossary/             # (3 files) Drilling terminology, abbreviations, and units (CSV, JSON, MD)
├── /mock_incidents/       # (2 files) 15 synthetic incident records (mud loss, kick, stuck pipe, H2S)
└── /geo_ner/              # (7 files) Official BGS Geo-NER dataset (train/test/vocab)
`

See [data/README.md](data/README.md) for detailed dataset documentation and schema details.
