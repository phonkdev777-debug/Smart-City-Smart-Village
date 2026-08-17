# Project Requirements

## Smart City / Smart Village — Trichirappalli

**Source:** FOSSEE Geospatial Mapathon 2026 Project Specification

**Document status:** Phase 1 baseline — extracted from competition specification

---

## 1. Competition Identity

| Field | Value |
|-------|-------|
| Competition | FOSSEE Geospatial Mapathon 2026 |
| Registered Topic | Smart City / Smart Village |
| Study Area | Trichirappalli Municipal Corporation, Tamil Nadu, India |

---

## 2. Study Area Constraints

- The study area is **Trichirappalli Municipal Corporation** only.
- NOT the entire Trichy district.
- NOT surrounding rural blocks unless explicitly part of the municipal boundary.
- Boundary must be sourced from an authoritative administrative boundary dataset.

---

## 3. Data Requirements

### 3.1 Data Authenticity

- All datasets must be **real, genuine, and verifiable**.
- No fabricated data, statistics, GIS results, accessibility scores, population values, satellite statistics, API responses, or fake GIS layers.
- Dataset provenance **must** be documented.
- Licensing and attribution **must** be documented.

### 3.2 Permitted Data Sources

| Source | Type |
|--------|------|
| Bhuvan (ISRO) | Indian geospatial/remote-sensing |
| MOSDAC | Meteorological and oceanographic |
| VEDAS | Mineral exploration and geoscience |
| Bhoonidhi | Land/terrain data |
| Survey of India | Official Survey of India data (from required official source) |
| OpenStreetMap | Contextual base data |
| Other permitted Indian geospatial sources | As justified |

### 3.3 Data Prohibition

- No random GIS datasets without provenance.
- No random boundary shapefiles presented as official.
- No invented facility counts, ward statistics, population values, satellite statistics, accessibility scores, gap counts, or GIS analysis results.

---

## 4. Technology Requirements

### 4.1 Mandatory

- **Free/Libre/Open Source Software** and technologies.

### 4.2 Projected Stack

| Layer | Technology |
|-------|------------|
| GIS | QGIS |
| Frontend | React, TypeScript, Vite |
| Interactive Mapping | Leaflet, React-Leaflet |
| Spatial Utility | Turf.js (where appropriate) |
| Data Formats | GeoPackage, GeoJSON, Shapefile (where required) |

### 4.3 Explicit Exclusions (Initial)

- No backend framework (Node.js/Express/FastAPI/Django).
- No database (PostgreSQL/PostGIS).
- No native desktop applications (Windows EXE, Linux, macOS).
- No paid APIs/services without explicit approval.

---

## 5. GIS Analysis Requirements

### 5.1 Core Workflow

```
Map → Spatial Analysis → Identify Problem → Generate Evidence → Support Planning Decisions
```

### 5.2 Analytical Radii

| Radius | Classification |
|--------|---------------|
| 250 m | Analytical choice |
| 500 m | Analytical choice |
| 1000 m | Analytical choice |

These are **analytical choices**, NOT government standards or official accessibility standards.

### 5.3 Proximity Methodology

- Distances are **straight-line proximity** unless a future verified routing methodology is introduced.
- Straight-line distance must NOT be called "walking time", "driving time", "travel time", or "traffic accessibility".

### 5.4 Analysis Categories

- Facility availability analysis
- Proximity analysis
- Gap analysis
- Ward-level analysis
- Transparent calculations
- Documented assumptions

---

## 6. Cartographic Requirements

### 6.1 Thematic Maps (Core Deliverables)

Every thematic map must include:

- Meaningful title
- Legend
- Scale
- North arrow (where appropriate)
- CRS/context (where appropriate)
- Source attribution
- Methodology/reference information (where appropriate)

### 6.2 Possible Map Categories

- Healthcare accessibility/proximity
- Education facility gaps
- Civic facility availability/gaps
- Water distribution
- Indian satellite-derived thematic analysis
- Other justified GIS findings

---

## 7. Web GIS Requirements

- The Web GIS is an **additional demonstration/interface**, NOT a replacement for GIS analysis.
- Must NOT become a Google Maps clone.
- Must NOT be a navigation application or generic map viewer.
- Must present the actual GIS analysis.
- Must support: spatial analysis, thematic visualization, facility exploration, ward analysis, evidence-based planning.

---

## 8. Policy Constraints

### 8.1 National Geospatial Policy 2022
- Project must align with the National Geospatial Policy 2022.

### 8.2 Indian Space Policy 2023
- Project must align with the Indian Space Policy 2023.

### 8.3 SDG Alignment
- At least one SDG alignment required.
- **SDG 11** (Sustainable Cities and Communities) is the primary alignment.

### 8.4 Zero-Cost
- The project should remain zero-cost where possible.

### 8.5 Reproducibility
- GIS methodology must be reproducible.

---

## 9. What the Project Is NOT

- NOT a Google Maps clone
- NOT a navigation application
- NOT a generic map viewer
- NOT a street-view application
- NOT a social application
- NOT a generic dashboard with random statistics
- NOT an AI-generated scoring system
- NOT a collection of unrelated map layers

---

## 10. Current Data Context

The following figures are treated as source-provided project data (not to be manually altered):

| Category | Count |
|----------|-------|
| Wards | 65 |
| Roads | 19,064 |
| Healthcare facilities | 236 |
| Education facilities | 55 |
| Water features | 563 |
| Civic facilities | 34 |

---

## 11. Known Limitations

- No verified population spatial dataset available.
- Therefore: no population-weighted accessibility, no population density analysis, no underserved population counts, no population-based service equity claims.
- Road routing / travel-time analysis is outside current scope.

---

## 12. Documentation Requirements

- Dataset provenance must be documented.
- Licensing and attribution must be documented.
- GIS methodology must be reproducible.
- GitHub documentation must be maintained.
- Final project packaging must include reproducibility documentation.
