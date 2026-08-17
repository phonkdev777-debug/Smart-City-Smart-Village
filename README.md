# Smart Trichy

**GIS-based Spatial Decision-Support System for Smart City / Smart Village Planning in Trichirappalli**

---

## Competition

**FOSSEE Geospatial Mapathon 2026**

| Field | Value |
|-------|-------|
| Competition | FOSSEE Geospatial Mapathon 2026 |
| Registered Topic | Smart City / Smart Village |
| Study Area | Trichirappalli Municipal Corporation, Tamil Nadu, India |

---

## Problem Statement

Urban and village planning in Indian municipal corporations requires evidence-based spatial decision-making. Trichirappalli Municipal Corporation, like many Indian cities, faces challenges in equitable distribution of civic facilities, healthcare, education, and water infrastructure across its 65 wards. Without spatial analysis, gaps in service availability remain hidden, and planning decisions lack quantitative geographic evidence.

This project builds a GIS-based Spatial Decision-Support System that maps existing infrastructure, performs proximity and gap analysis, and generates evidence to support informed planning decisions for Trichirappalli.

---

## Objectives

1. Map and verify civic infrastructure (healthcare, education, water, civic facilities) across Trichirappalli Municipal Corporation.
2. Perform proximity analysis using analytically justified radii (250m, 500m, 1000m).
3. Identify infrastructure gaps at the ward level.
4. Generate professional thematic maps as core deliverables.
5. Provide an interactive Web GIS interface for exploring analysis results.
6. Maintain full data provenance, licensing, and reproducibility documentation.
7. Align with SDG 11 — Sustainable Cities and Communities.

---

## Project Positioning

This is a **GIS-based Spatial Decision-Support System**, NOT:

- A Google Maps clone
- A navigation application
- A generic map viewer
- A street-view application
- A social application
- A generic dashboard with random statistics
- An AI-generated scoring system
- A collection of unrelated map layers

### Core GIS Workflow

```
Map → Spatial Analysis → Identify Problem → Generate Evidence → Support Planning Decisions
```

---

## Technology Stack

| Layer | Technology |
|-------|-----------|
| GIS Desktop | QGIS |
| Frontend | React, TypeScript, Vite |
| Interactive Mapping | Leaflet, React-Leaflet |
| Spatial Utility | Turf.js |
| Data Formats | GeoPackage, GeoJSON, Shapefile |
| Backend | None (initially) |
| Database | None (initially) |
| License | GNU GPL v3.0 |

---

## Architecture Overview

```
┌─────────────────────────────────────────────┐
│              Browser (Web GIS)              │
│  React + TypeScript + Vite + Leaflet        │
│  Turf.js (client-side spatial analysis)     │
├─────────────────────────────────────────────┤
│         Static GeoPackage / GeoJSON         │
│         (no backend, no database)           │
├─────────────────────────────────────────────┤
│              QGIS (Desktop)                 │
│  Data processing, analysis, cartography     │
│  Export to GeoPackage/GeoJSON for Web GIS   │
└─────────────────────────────────────────────┘
```

---

## Data Source Policy

All datasets must be:

- Real, genuine, and verifiable
- From recognized Indian geospatial sources (Bhuvan, MOSDAC, VEDAS, Bhoonidhi, Survey of India, OpenStreetMap)
- Documented with provenance, licensing, and attribution
- Processed reproducibly using FOSS tools

**No fabricated data, statistics, or GIS results are permitted.**

---

## GIS Analysis Overview

### Spatial Analysis Types

- Facility availability mapping
- Proximity analysis (250m, 500m, 1000m straight-line)
- Gap analysis (identifying underserved areas)
- Ward-level analysis

### Analytical Radii

The proximity radii (250m, 500m, 1000m) are **analytical choices**, NOT government standards or official accessibility mandates.

### Proximity Methodology

All distances are **straight-line proximity**. They are NOT walking time, driving time, travel time, or traffic analysis.

---

## Thematic Maps

Professional thematic maps are core deliverables and will include:

- Healthcare accessibility/proximity
- Education facility gaps
- Civic facility availability/gaps
- Water distribution
- Indian satellite-derived thematic analysis

Each map includes: title, legend, scale, north arrow, CRS context, source attribution, and methodology.

---

## Web GIS Overview

The Web GIS is an **additional demonstration interface** — not a replacement for GIS analysis. It presents analysis results through:

- Trichy Corporation boundary visualization
- Ward layer rendering
- Facility layers (healthcare, education, civic, water)
- Layer control and toggling
- Facility explorer and search
- Ward selection and analysis panels
- Proximity analysis visualization
- Gap analysis results

---

## Development Phases

| Phase | Name | Status |
|-------|------|--------|
| 1 | Project Governance & Requirements | COMPLETE |
| 2 | System Architecture & Technical Design | COMPLETE |
| 3 | GIS Data Acquisition & Provenance | IN PROGRESS |
| 4 | GIS Data Engineering | NOT STARTED |
| 5 | Indian Geospatial Data Integration | NOT STARTED |
| 6 | Spatial Analysis | NOT STARTED |
| 7 | Thematic Cartography | NOT STARTED |
| 8 | Dataset & Reproducibility Package | NOT STARTED |
| 9 | Web GIS Application | NOT STARTED |
| 10 | Verification, Documentation & Submission | NOT STARTED |

---

## Current Project Status

**Phase 1 — COMPLETE**

Project governance and requirements have been fully verified. All 27 Phase 1 requirements confirmed satisfied.

**Phase 2 — COMPLETE**

System architecture and technical design have been documented and verified:

- `docs/architecture/system-architecture.md` — Complete system architecture
- `docs/decisions/architecture-decisions.md` — 8 architecture decision records

Consistency review completed — no contradictions found. No application code, GIS data, or analysis has been implemented yet.

**Phase 3 — IN PROGRESS**

GIS data acquisition and provenance documentation in progress:

- `docs/data/data-inventory.md` — 9 dataset records identified
- `docs/data/data-provenance.md` — Provenance model established
- `docs/data/data-dictionary.md` — Schemas pending verification
- `docs/data/data-quality-report.md` — Quality report template ready

No datasets have been acquired yet. Data acquisition is the critical next step.

---

## Reproducibility

This project is committed to reproducible GIS methodology:

- All processing steps documented
- All data sources and provenance recorded
- All tools are FOSS
- All analysis assumptions transparent
- All datasets include metadata and licensing

---

## Data Attribution

All datasets used in this project will carry appropriate attribution and licensing information as documented in `docs/requirements/project-requirements.md` and the final reproducibility package.

---

## License

This project is licensed under the **GNU General Public License v3.0** — see the [LICENSE](LICENSE) file for details.

---

## Development Principles

- **Correctness** over quantity
- **Reproducibility** over convenience
- **Data authenticity** over fabrication
- **GIS methodology** over visual effects
- **Maintainability** over complexity
- **Traceability** over assumption
- **Documentation** over undocumented changes
- **Validation** over claimed completion
- **Rule compliance** over convenience

---

## FOSSEE Mapathon Alignment

This project is developed for the FOSSEE Geospatial Mapathon 2026 under the following alignment:

- **National Geospatial Policy 2022** — aligned
- **Indian Space Policy 2023** — aligned
- **SDG 11 — Sustainable Cities and Communities** — primary alignment
- **Free/Libre/Open Source Software** — mandatory
- **India-specific study area** — Trichirappalli Municipal Corporation
