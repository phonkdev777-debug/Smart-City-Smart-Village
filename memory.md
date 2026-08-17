# Smart Trichy — Project Memory

> This file is the project's living state document.
> A future AI model or developer must be able to read this file and understand the current project state without relying on chat history.

**Last updated:** 2026-08-17

---

## Project Identity

| Field | Value |
|-------|-------|
| Project Name | Smart Trichy |
| Full Title | GIS-based Spatial Decision-Support System for Smart City / Smart Village Planning in Trichirappalli |
| Competition | FOSSEE Geospatial Mapathon 2026 |
| Registered Topic | Smart City / Smart Village |
| Study Area | Trichirappalli Municipal Corporation, Tamil Nadu, India |

---

## Competition

FOSSEE Geospatial Mapathon 2026

## Registered Topic

Smart City / Smart Village

## Study Area

Trichirappalli Municipal Corporation, Tamil Nadu, India

## Project Objective

Build a GIS-based Spatial Decision-Support System that demonstrates how GIS supports real-world urban planning decisions in Trichirappalli Municipal Corporation. The system must map facilities, perform spatial analysis, identify gaps, generate evidence, and support planning decisions.

## Primary SDG

**SDG 11 — Sustainable Cities and Communities**

---

## Current Phase

**Phase 3 — GIS Data Acquisition & Provenance**

## Current Status

**IN PROGRESS**

---

## Completed Work

### Phase 1 — COMPLETE
- [x] Project identity established.
- [x] FOSSEE Mapathon project requirements documented (`docs/requirements/project-requirements.md`).
- [x] Study area confirmed as Trichirappalli Municipal Corporation.
- [x] Ten-phase development lifecycle established and documented.
- [x] Initial technology direction established (React + TypeScript + Vite + Leaflet + QGIS).
- [x] Backend deferred from initial architecture (no unnecessary infrastructure).
- [x] Web GIS identified as an additional interface, not a replacement for GIS analysis.
- [x] Professional anti-vibe-coding workflow established.
- [x] Project memory/state mechanism established (this file).
- [x] `.gitignore` created.
- [x] `LICENSE` created (GNU GPL v3.0).
- [x] `README.md` created.
- [x] `opencode.json` created.
- [x] `docs/requirements/project-requirements.md` created.
- [x] All 27 Phase 1 requirements verified satisfied.

### Phase 2 — COMPLETE
- [x] System architecture document created (`docs/architecture/system-architecture.md`).
- [x] Architecture decision records created (`docs/decisions/architecture-decisions.md` — 8 ADRs).
- [x] System boundaries documented (in-scope and out-of-scope).
- [x] 5-layer architecture defined (Source Data, GIS Engineering, Spatial Analysis, Data Contract, Web GIS Frontend).
- [x] Backend decision formally documented (ADR-002).
- [x] Database decision formally documented (ADR-003).
- [x] Data flow designed (QGIS → GeoJSON → React/Leaflet).
- [x] Frontend module architecture defined (12 logical modules).
- [x] GIS data contract defined per layer (7 layers + satellite).
- [x] Provenance architecture designed.
- [x] Reproducibility architecture designed.
- [x] Testing architecture designed (GIS + Frontend + Integration).
- [x] Security & data integrity safeguards defined.
- [x] Dependency policy established.
- [x] Performance considerations documented.
- [x] Cartography architecture defined.
- [x] README.md updated.
- [x] Consistency review completed — no contradictions found.
- [x] All 16 Phase 2 acceptance criteria verified.

### Phase 3 — IN PROGRESS
- [x] Data inventory created (`docs/data/data-inventory.md` — 9 dataset records).
- [x] Data provenance model established (`docs/data/data-provenance.md`).
- [x] Data dictionary initialized (`docs/data/data-dictionary.md` — schemas pending verification).
- [x] Data quality report initialized (`docs/data/data-quality-report.md`).
- [x] Repository inspected — no GIS data files present.
- [x] Indian geospatial dataset candidates researched (Bhuvan LULC 50K primary, 250K alternative).
- [x] Survey of India portal documented (Admin Boundary Database — free access).
- [x] OpenStreetMap sources identified for roads, healthcare, education, water, civic.
- [x] Trichy Corporation website documented (ward map, city map).
- [ ] Actual data acquisition — NOT YET STARTED.
- [ ] Data validation — NOT YET STARTED.

## Pending Work

- [ ] Acquire actual GIS datasets (corporation boundary, wards, roads, facilities, water, civic).
- [ ] Validate acquired datasets (geometry, CRS, attributes, counts).
- [ ] Verify Indian geospatial dataset (Bhuvan LULC 50K) availability and access.
- [ ] Complete data provenance documentation for all acquired datasets.
- [ ] Begin Phase 4 — GIS Data Engineering (only after Phase 3 complete).

## Active Decisions

| Decision | Rationale | ADR | Date |
|----------|-----------|-----|------|
| Web GIS instead of native desktop | Cross-platform, no installation, static deployment sufficient | ADR-001 | 2026-08-17 |
| No backend initially | No requirement justifies it; static GeoJSON delivery sufficient | ADR-002 | 2026-08-17 |
| No database initially | Data volume fits browser memory; no transactional needs | ADR-003 | 2026-08-17 |
| QGIS as primary GIS tool | Industry-standard FOSS GIS, processing, analysis, cartography | ADR-004 | 2026-08-17 |
| React + TypeScript + Leaflet | Typed, component-based, mature FOSS mapping stack | ADR-005 | 2026-08-17 |
| GeoPackage working, GeoJSON delivery | GeoPackage for QGIS; GeoJSON for browser (EPSG:4326) | ADR-006 | 2026-08-17 |
| GNU GPL v3.0 | Strong copyleft FOSS license, Mapathon compliant | ADR-007 | 2026-08-17 |
| No fabricated data — strict integrity | All data from verified sources; fabrication prohibited | ADR-008 | 2026-08-17 |
| Proximity radii (250m, 500m, 1000m) | Analytical choices, NOT government standards | — | 2026-08-17 |

---

## Technology Stack

| Layer | Technology | Status |
|-------|-----------|--------|
| GIS Desktop | QGIS | Planned |
| Frontend | React, TypeScript, Vite | Planned |
| Interactive Mapping | Leaflet, React-Leaflet | Planned |
| Spatial Utility | Turf.js | Planned |
| Data Formats | GeoPackage, GeoJSON, Shapefile | Planned |
| Backend | NONE | Deferred |
| Database | NONE | Deferred |

---

## Architecture Summary

```
┌─────────────────────────────────────────────────────────────────┐
│                     LAYER 1: SOURCE DATA                        │
│  Bhuvan, MOSDAC, VEDAS, Bhoonidhi, Survey of India, OSM       │
└──────────────────────────┬──────────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                     LAYER 2: GIS DATA ENGINEERING               │
│  QGIS: Ingest → Validate → Clean → CRS Normalize → Organize   │
└──────────────────────────┬──────────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                     LAYER 3: SPATIAL ANALYSIS                    │
│  QGIS: Proximity (250m/500m/1000m), Gap, Ward-Level Analysis   │
└──────────────────────────┬──────────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                     LAYER 4: DATA CONTRACT                       │
│  GeoPackage (working) → GeoJSON (EPSG:4326 per layer)         │
└──────────────────────────┬──────────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                     LAYER 5: WEB GIS FRONTEND                    │
│  React + TypeScript + Vite + Leaflet + Turf.js                 │
│  Layer Control | Facility Explorer | Ward Analysis | Thematic  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Data Sources

| Source | Purpose | Status |
|--------|---------|--------|
| OpenStreetMap | Roads, healthcare, education, water, civic facilities (contextual) | Identified — extraction pending |
| Survey of India | Administrative boundary database (up to taluk level) | Identified — corporation boundary may need state source |
| Bhuvan (ISRO/NRSC) | LULC 1:50K (primary Indian geospatial candidate) | Identified — download request pending |
| Tamil Nadu Government | Ward boundaries, corporation boundary | Identified — portal documented |
| VEDAS | Geoscience data | Not yet evaluated for relevance |
| MOSDAC | Meteorological data | Not yet evaluated for relevance |
| Bhoonidhi | Land/terrain data | Not yet evaluated for relevance |

## Data Provenance

Provenance model established in `docs/data/data-provenance.md`. Per-dataset provenance will be documented as datasets are acquired. Key sources identified:

- **OSM:** ODbL license, "© OpenStreetMap contributors", community-maintained (not official)
- **Survey of India:** Free admin boundary database, up to taluk level
- **Bhuvan:** Free with registration, LULC 50K available for Tamil Nadu
- **TN Government:** Ward/corporation data via official portals

## Dataset Status

| Dataset | Source | Acquired | Processed | Verified |
|---------|--------|----------|-----------|----------|
| Trichy Corporation Boundary | SoI / TN Govt | No | No | No |
| Ward Boundaries (65 wards) | TN Govt / OSM | No | No | No |
| Roads (19,064) | OpenStreetMap | No | No | No |
| Healthcare facilities (236) | OpenStreetMap | No | No | No |
| Education facilities (55) | OpenStreetMap | No | No | No |
| Water features (563) | OpenStreetMap | No | No | No |
| Civic facilities (34) | OpenStreetMap | No | No | No |
| Population spatial data | N/A | Not available | N/A | N/A |
| Bhuvan LULC 1:50K | ISRO/NRSC | No | No | No |

---

## GIS Analysis Status

| Analysis Type | Status |
|---------------|--------|
| Facility availability | NOT STARTED |
| Proximity analysis (250m) | NOT STARTED |
| Proximity analysis (500m) | NOT STARTED |
| Proximity analysis (1000m) | NOT STARTED |
| Gap analysis | NOT STARTED |
| Ward-level analysis | NOT STARTED |
| Satellite-derived analysis | NOT STARTED |

## Thematic Map Status

| Map | Status |
|-----|--------|
| Healthcare accessibility | NOT STARTED |
| Education facility gaps | NOT STARTED |
| Civic facility availability | NOT STARTED |
| Water distribution | NOT STARTED |
| Satellite-derived thematic | NOT STARTED |

## Web GIS Status

| Component | Status |
|-----------|--------|
| React project scaffold | NOT STARTED |
| Leaflet map integration | NOT STARTED |
| Ward layer rendering | NOT STARTED |
| Facility layers | NOT STARTED |
| Layer control | NOT STARTED |
| Facility explorer | NOT STARTED |
| Ward analysis panel | NOT STARTED |
| Proximity analysis UI | NOT STARTED |

## Testing Status

NOT STARTED

---

## Known Issues

None at initialization.

## Known Limitations

1. **No verified population spatial dataset** — population-weighted accessibility, density analysis, and underserved population claims cannot be made.
2. **Straight-line proximity only** — no road-network routing or travel-time analysis.
3. **No backend** — all data is served client-side; large datasets may need optimization.
4. **Analytical radii are choices, not standards** — 250m/500m/1000m must never be presented as government standards.

---

## Important Rules

1. No fabricated data, statistics, or GIS results.
2. No Google Maps clone behavior.
3. No straight-line distance presented as travel/driving/walking time.
4. No population-weighted claims without verified spatial population data.
5. No government-standard claims for analytical radii.
6. No paid APIs/services without explicit approval.
7. All data must have documented provenance.
8. All maps must have title, legend, scale, and source attribution.
9. Professional engineering workflow: INSPECT → PLAN → IMPLEMENT → VERIFY → DOCUMENT → CHECKPOINT.
10. Anti-vibe-coding: no uncontrolled generation, no fake data, no unnecessary complexity.

---

## Phase History

### Phase 1 — Project Governance & Requirements

| Field | Value |
|-------|-------|
| Status | **COMPLETE** |
| Started | 2026-08-17 |
| Completed | 2026-08-17 |
| Completed work | Project identity, requirements doc, .gitignore, LICENSE, README.md, opencode.json, memory.md |
| Files created | `memory.md`, `README.md`, `opencode.json`, `.gitignore`, `LICENSE`, `docs/requirements/project-requirements.md` |
| Decisions made | No backend, no database, React+TS+Vite+Leaflet, GNU GPL v3.0, proximity radii are analytical choices |
| Validation | All Phase 1 files verified to exist; all 27 Phase 1 requirements verified satisfied |
| Known issues | None |
| Remaining work | None — phase complete |
| Next action | Phase 2 — System Architecture & Technical Design |

### Phase 2 — System Architecture & Technical Design

| Field | Value |
|-------|-------|
| Status | **COMPLETE** |
| Started | 2026-08-17 |
| Completed | 2026-08-17 |
| Completed work | System architecture doc, 8 ADRs, system boundaries, 5-layer architecture, data flow, frontend module design, GIS data contract, provenance architecture, reproducibility architecture, testing architecture, security/integrity, dependency policy, performance architecture, cartography architecture |
| Files created | `docs/architecture/system-architecture.md`, `docs/decisions/architecture-decisions.md` |
| Files modified | `README.md`, `memory.md` |
| Decisions made | ADR-001 through ADR-008 recorded |
| Validation | All Phase 2 files verified; consistency review completed — no contradictions |
| Known issues | None |
| Remaining work | None — phase complete |
| Next action | Phase 3 — GIS Data Acquisition & Provenance |

### Phase 3 — GIS Data Acquisition & Provenance

| Field | Value |
|-------|-------|
| Status | **IN PROGRESS** |
| Started | 2026-08-17 |
| Completed work | Data inventory (9 datasets), provenance model, data dictionary (schemas pending), quality report template, Indian geospatial candidate research |
| Files created | `docs/data/data-inventory.md`, `docs/data/data-provenance.md`, `docs/data/data-dictionary.md`, `docs/data/data-quality-report.md` |
| Decisions made | Bhuvan LULC 50K as primary Indian dataset candidate; OSM as contextual/facility data source |
| Validation | Repository inspected — no GIS data files present |
| Known issues | No datasets acquired yet; data acquisition is the critical next step |
| Remaining work | Acquire datasets, validate, complete provenance, verify Indian dataset |
| Next action | Acquire GIS datasets and validate them |

### Phase 4 — GIS Data Engineering

Status: **NOT STARTED**

### Phase 5 — Indian Geospatial Data Integration

Status: **NOT STARTED**

### Phase 6 — Spatial Analysis

Status: **NOT STARTED**

### Phase 7 — Thematic Cartography

Status: **NOT STARTED**

### Phase 8 — Dataset & Reproducibility Package

Status: **NOT STARTED**

### Phase 9 — Web GIS Application

Status: **NOT STARTED**

### Phase 10 — Verification, Documentation & Submission

Status: **NOT STARTED**
