# Product Requirements Document (PRD)

## Project: GeoDrill-AI (Upstream Drilling & Subsurface Intelligence Platform)

### 1. Executive Summary & Objective
**GeoDrill-AI** is an AI-powered subsurface intelligence and drilling safety platform. It addresses the massive challenges of unstructured legacy drilling reports, multi-modal sensor/survey data, and critical drilling hazards (Non-Productive Time, lost circulation, kicks, stuck pipe) by establishing a robust **5-Layer AI Pipeline**.

---

### 2. User Personas
1. **Drilling Engineer**: Needs real-time 3D well trajectory verification, dogleg severity (DLS) calculations, and predictive incident mitigation plans while drilling.
2. **Geologist / Geoscientist**: Analyzes stratigraphic formations, lithology layers, and correlates geological entity extraction from historical completion reports.
3. **Drilling Superintendent / Asset Manager**: Requires automated NPT and financial risk assessment reports across multi-well drilling campaigns.
4. **Data Engineer / ML Engineer**: Manages pipeline ingestion, OCR benchmarking on degraded scans, and hybrid RAG vector database synchronization.

---

### 3. Five-Layer AI Pipeline Specifications

#### **Layer 1: Multi-Modal Document Ingestion & OCR Engine**
* **Inputs**: Digital native PDFs (`wcr_digital`), clean historical scans (`wcr_scanned_clean`), and degraded scans (`wcr_scanned_bad`).
* **Requirements**:
  * Auto-classify document type (digital vs scanned).
  * CV2 pre-processing: deskewing (+/- 15 deg), adaptive thresholding, Gaussian deblurring.
  * Extract tabular data (casing profiles, formation depths, perforation intervals).
  * Target Metric: >85% Character Recognition Accuracy on degraded scans, <5s per page processing.

#### **Layer 2: Stratigraphic & Domain NER Extraction Layer**
* **Inputs**: OCR text output and Daily Drilling Report narratives.
* **Requirements**:
  * Train and fine-tune models on the British Geological Survey (BGS) 3-class dataset (`LEXICON`, `ROCK`, `TIME`).
  * Extract drilling-specific parameters: WOB (Weight on Bit), ROP (Rate of Penetration), RPM, Mud Weight, ECD, BOP ratings.
  * Target Metric: Geo-NER F1-score >= 88%.

#### **Layer 3: 3D Trajectory & Spatial Calculation Engine**
* **Inputs**: CWLS LAS 2.0 files and directional survey CSVs (MD, INC, AZI).
* **Requirements**:
  * Implement industry-standard **Minimum Curvature Algorithm** (MCM) to compute TVD (True Vertical Depth), North-South ($dX$), East-West ($dY$), and Dogleg Severity (DLS in deg/30m or deg/100ft).
  * Compute 3D wellbore spatial coordinates and geo-spatial bounding envelopes.
  * Target Metric: Computation time < 100ms for 1,000 survey stations.

#### **Layer 4: Domain Knowledge Graph & Semantic Enrichment Layer**
* **Inputs**: Extracted entities, Master Well Metadata, and Drilling Glossary (`drilling_terms.json`, `abbreviations.md`).
* **Requirements**:
  * Normalize domain acronyms (e.g., KOP, BHA, LCM, NPT, LOT, FIT).
  * Construct a property graph linking Wells $\leftrightarrow$ Formations $\leftrightarrow$ Incidents $\leftrightarrow$ Trajectory Zones.
  * Index unstructured text into hybrid vector stores (Dense Embeddings + BM25 Sparse Search).

#### **Layer 5 (Last New Section): Real-time Incident Correlation & AI Decision Copilot**
* **Inputs**: Historical Incident Database (`mock_incidents/incidents.json`), DDRs, Formation tops, and active trajectory coordinates.
* **Requirements**:
  * **Hazard Pattern Matching**: Correlate real-time depth & lithology against historical incidents (e.g., mud loss in Monterey Shale at 7,800 ft MD).
  * **NPT & Financial Risk Scoring**: Estimate probability of stuck pipe, kick, or lost circulation with estimated downtime hours and cost impact.
  * **Agentic Decision Support**: AI Copilot generates actionable mitigation workflows (e.g., pumping LCM pills, adjusting mud weight to 1.25 SG, monitoring shaker screens).

---

### 4. Non-Functional Requirements (NFR)
* **High Availability & Low Latency**: API response times < 250ms for query endpoints.
* **Scalability**: Capable of ingesting and indexing 10,000+ well completion reports.
* **Security & Compliance**: Role-based access control (RBAC), end-to-end encryption for operational data.
* **Explainability**: AI recommendations must cite specific source pages, survey stations, or historical incident logs.

---

### 5. Success Metrics & KPIs
* **NPT Hazard Reduction**: >30% earlier hazard identification compared to manual report review.
* **Extraction Automation**: >90% reduction in manual data entry time for historical completion records.
* **Trajectory Accuracy**: 100% compliance with standard CWLS and API directional survey equations.
