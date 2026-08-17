# System Architecture

## Smart City / Smart Village — Trichirappalli

**Document:** Phase 2 — System Architecture & Technical Design

**Status:** CREATED — Phase 2

**Last updated:** 2026-08-17

---

## 1. Architecture Overview

This project is a **GIS-based Spatial Decision-Support System** for Trichirappalli Municipal Corporation. The architecture follows a clear separation between desktop GIS processing and browser-based visualization, connected by well-defined data formats.

### Conceptual Pipeline

```
┌─────────────────────────────────────────────────────────────────┐
│                     LAYER 1: SOURCE DATA                        │
│                                                                 │
│  Official Indian Geospatial Data        OpenStreetMap Data      │
│  (Bhuvan, MOSDAC, VEDAS, Bhoonidhi)    (roads, landmarks,     │
│                                          contextual features)   │
│                                                                 │
│  Survey of India Data                 Other Permitted Sources   │
│  (official boundaries where required)  (as justified)           │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                     LAYER 2: GIS DATA ENGINEERING               │
│                                                                 │
│  QGIS Desktop Environment                                        │
│  ├── Data Ingestion (import from multiple sources)              │
│  ├── Validation (geometry, topology, attributes)                │
│  ├── Cleaning (removal of artifacts, repair)                    │
│  ├── CRS Handling (standardize to EPSG:4326 for delivery)       │
│  ├── Normalization (consistent attribute schemas)               │
│  ├── Attribute Validation (completeness, type correctness)      │
│  ├── Layer Organization (thematic grouping)                     │
│  └── Provenance Tracking (source, date, processing steps)       │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                     LAYER 3: SPATIAL ANALYSIS                    │
│                                                                 │
│  QGIS Processing Toolbox / Python Scripts                        │
│  ├── Facility Availability Mapping                              │
│  ├── Proximity Analysis (250m, 500m, 1000m straight-line)       │
│  ├── Gap Analysis (identifying underserved wards)               │
│  ├── Ward-Level Analysis (per-ward facility counts, coverage)   │
│  └── Satellite-Derived GIS Analysis (if data acquired)          │
│                                                                 │
│  All calculations: transparent, documented, reproducible        │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                     LAYER 4: GIS OUTPUT / DATA CONTRACT          │
│                                                                 │
│  GeoPackage (working GIS format — all layers)                   │
│  GeoJSON (browser delivery — per-layer exports)                 │
│  Shapefile (only where required by external tools)              │
│                                                                 │
│  Each export: documented CRS, attributes, provenance            │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                     LAYER 5: WEB GIS FRONTEND                    │
│                                                                 │
│  React + TypeScript + Vite                                       │
│  ├── Leaflet / React-Leaflet (map rendering)                    │
│  ├── Turf.js (client-side spatial calculations)                 │
│  ├── Layer Management (toggle, reorder, filter)                 │
│  ├── Facility Explorer (browse, search, filter facilities)      │
│  ├── Ward Analysis (select ward, view stats, proximity)         │
│  ├── Thematic Visualization (choropleth, categorized)           │
│  ├── Legends & Information Panels                               │
│  └── Evidence-Based Planning Interface                          │
│                                                                 │
│  Runs entirely in browser — no backend server                   │
└─────────────────────────────────────────────────────────────────┘
```

### Role of Each Layer

| Layer | Role | Tool |
|-------|------|------|
| Source Data | Provide authentic, verified geospatial data for Trichirappalli | Multiple Indian geospatial portals |
| GIS Data Engineering | Prepare raw data for analysis — clean, validate, normalize | QGIS |
| Spatial Analysis | Generate evidence — proximity, gaps, ward statistics | QGIS processing |
| Data Contract | Deliver processed GIS data to frontend in open formats | QGIS export |
| Web GIS Frontend | Present analysis results interactively for decision-support | React + Leaflet |

---

## 2. System Boundaries

### In Scope

| Item | Description |
|------|-------------|
| Study area | Trichirappalli Municipal Corporation boundary |
| Administrative units | 65 wards |
| Road network | 19,064 roads (OSM-derived) |
| Healthcare facilities | 236 mapped facilities |
| Education facilities | 55 mapped facilities |
| Water features | 563 mapped features |
| Civic facilities | 34 mapped facilities |
| Indian satellite/geospatial data | As acquired and verified in Phase 3-5 |
| GIS preprocessing | Cleaning, CRS normalization, attribute validation |
| Spatial analysis | Proximity, gap, ward-level analysis |
| Thematic cartography | Professional maps with legend, scale, attribution |
| Web GIS | Interactive map-based decision-support interface |
| Documentation | Provenance, licensing, methodology, reproducibility |
| Ward analysis | Per-ward facility counts, coverage assessment |
| Facility exploration | Browse, search, filter mapped facilities |
| Proximity visualization | 250m / 500m / 1000m analytical radii |
| Gap analysis | Identify wards with low facility coverage |

### Out of Scope

| Item | Reason |
|------|--------|
| Native Windows/Linux/macOS applications | No requirement; Web GIS provides cross-platform access |
| Backend server | No requirement justifies it; data served statically |
| Database | GIS data served as GeoPackage/GeoJSON; no transactional needs |
| Traffic analysis | No real-time traffic data available |
| Driving-time analysis | No road-network routing capability |
| Walking-time analysis | No pedestrian routing data |
| Travel-time claims | Only straight-line proximity is supported |
| Population-weighted accessibility | No verified population spatial dataset |
| Population density analysis | No verified population spatial dataset |
| Underserved population counts | No verified population spatial dataset |
| Fabricated statistics | Project data integrity policy prohibits this |
| Fake AI scoring | No automated scoring system without verified methodology |
| Google Maps clone | Project is a decision-support system, not navigation |
| Social/login systems | No user accounts required |
| Cloud infrastructure | Zero-cost FOSS approach; static deployment sufficient |
| Paid APIs | No paid APIs without explicit approval |

---

## 3. Architecture Layers

### Layer 1 — Source Data

**Purpose:** Acquire authentic, verified geospatial data for Trichirappalli Municipal Corporation.

| Source | Data Type | Role in Project | Verification Required |
|--------|-----------|-----------------|----------------------|
| OpenStreetMap | Roads, landmarks, contextual features | Base contextual data | Yes — feature counts, completeness |
| Survey of India | Administrative boundaries | Corporation and ward boundaries | Yes — official source verification |
| Bhuvan (ISRO) | Indian remote-sensing/geospatial data | Satellite-derived analysis | Yes — dataset availability, licensing |
| MOSDAC | Meteorological data | If relevant to analysis | Yes — dataset availability, licensing |
| VEDAS | Mineral exploration/geoscience | If relevant to analysis | Yes — dataset availability, licensing |
| Bhoonidhi | Land/terrain data | If relevant to analysis | Yes — dataset availability, licensing |

**Decision:** No specific satellite dataset will be selected until Phase 3 verifies actual data availability. The architecture supports integrating one appropriate Indian satellite dataset, but does not require it.

### Layer 2 — GIS Data Engineering

**Purpose:** Prepare raw source data for spatial analysis and Web GIS delivery.

**Primary Tool:** QGIS Desktop

**Responsibilities:**

| Responsibility | Description |
|----------------|-------------|
| Ingestion | Import data from multiple sources into QGIS project |
| Validation | Verify geometry validity, topology, feature counts |
| Cleaning | Remove artifacts, repair invalid geometries |
| CRS Handling | Standardize all layers to a consistent CRS |
| Normalization | Ensure consistent attribute naming and types across layers |
| Attribute Validation | Check for missing values, type mismatches, duplicates |
| Layer Organization | Group layers thematically (healthcare, education, etc.) |
| Provenance Tracking | Record source, date, processing steps per layer |

**CRS Strategy:**

- Working CRS in QGIS: EPSG:4326 (WGS 84) — universal, compatible with web mapping
- If source data arrives in a different CRS (e.g., EPSG:4326, EPSG:32643 for UTM Zone 43N covering Tamil Nadu), reproject during ingestion
- All exported GeoJSON files: EPSG:4326 (required for Leaflet/MapLibre)
- All GeoPackage files: preserve original CRS with metadata note

### Layer 3 — Spatial Analysis

**Purpose:** Generate spatial evidence that supports planning decisions.

**Tool:** QGIS Processing Toolbox (Python scripts where needed)

| Analysis Type | Method | Output |
|---------------|--------|--------|
| Facility availability | Count features per ward | Ward-level facility counts |
| Proximity analysis | Buffer analysis at 250m, 500m, 1000m straight-line | Coverage zones per facility type |
| Gap analysis | Identify wards with zero/few facilities within radius | Gap classification per ward |
| Ward-level analysis | Aggregate statistics per ward | Ward summary GeoPackage/GeoJSON |
| Satellite-derived analysis | If satellite data acquired in Phase 5 | Derived thematic layers |

**Calculations:** All calculations occur in QGIS, NOT in the frontend. The frontend visualizes pre-computed results.

**Transparency:** Every analysis documents:
- Input datasets and their CRS
- Processing method (tool used, parameters)
- Assumptions made
- Output format and CRS
- Date of processing

### Layer 4 — GIS Output / Data Contract

**Purpose:** Define how processed GIS data moves from QGIS to the Web GIS frontend.

| Format | Role | When Used |
|--------|------|-----------|
| GeoPackage (.gpkg) | Working GIS format — all layers, full attributes | QGIS processing, archival |
| GeoJSON (.json) | Browser delivery format — per-layer exports | Web GIS frontend consumption |
| Shapefile (.shp) | Legacy compatibility only | Only where external tool requires it |

**Why GeoPackage as working format:**
- Single-file container for multiple layers
- Open standard (OGC)
- Supports complex attribute schemas
- Preserves CRS metadata
- Better than Shapefile (no 2GB limit, no field name truncation)

**Why GeoJSON for browser delivery:**
- Native JSON — no parsing library needed
- Directly consumable by Leaflet/MapLibre
- Lightweight for web传输
- Well-understood by all web mapping libraries

**Data Contract per Layer:**

| Layer | Geometry Type | Key Attributes | Identifier | CRS (Delivery) |
|-------|--------------|----------------|------------|-----------------|
| Corporation Boundary | Polygon | name, area | `corp_boundary` | EPSG:4326 |
| Ward Boundaries | Polygon | ward_name, ward_id, ward_number | `wards` | EPSG:4326 |
| Roads | LineString | name, highway, surface | `roads` | EPSG:4326 |
| Healthcare | Point | name, type, category, operator | `healthcare` | EPSG:4326 |
| Education | Point | name, type, category, operator | `education` | EPSG:4326 |
| Water Features | Point/Polygon | name, type, water_body | `water` | EPSG:4326 |
| Civic Facilities | Point | name, type, category | `civic` | EPSG:4326 |
| Satellite-Derived | Raster/Vector | TO BE VERIFIED DURING PHASE 5 | TBD | EPSG:4326 |

**Note:** Exact attribute schemas will be verified and finalized during Phase 4 (GIS Data Engineering) after actual datasets are acquired.

### Layer 5 — Web GIS Frontend

**Purpose:** Present GIS analysis results interactively for evidence-based planning decisions.

**Technology:** React + TypeScript + Vite + Leaflet + React-Leaflet + Turf.js

**Responsibilities:**

| Module | Responsibility |
|--------|---------------|
| Application Shell | Layout, navigation, header, sidebar structure |
| Map Module | Leaflet map initialization, base layers, controls |
| Layer Management | Toggle layers on/off, reorder, opacity control |
| Facility Explorer | Browse facilities by category, search, filter |
| Ward Analysis | Select ward, display ward-level statistics |
| Spatial Analysis Presentation | Visualize proximity buffers, gap results |
| Thematic Layer Visualization | Render choropleth/categorized ward maps |
| Legends | Display map legends for active thematic layers |
| Information Panels | Show facility details, ward summaries |
| Data Access Layer | Load GeoJSON files, manage data state |
| Utilities | Shared functions (formatting, color scales) |
| Shared Types | TypeScript interfaces for all data structures |

---

## 4. Backend Decision

### Decision: No Backend Initially

**Rationale:**

| Factor | Assessment |
|--------|-----------|
| Data delivery | Pre-processed GIS data can be served as static GeoJSON files |
| User accounts | Not required — no login, no user-generated content |
| Persistent state | Not required — all analysis is pre-computed |
| Live transactional APIs | Not required — no real-time data writes |
| Complexity reduction | Eliminating backend reduces development and deployment burden |
| Cost | Zero-cost approach — static deployment (GitHub Pages, Netlify) |
| FOSS alignment | Static frontend + QGIS = fully FOSS stack |

**Future conditions for backend introduction:**

A backend could become justified if:
- Real-time data ingestion from IoT sensors is required
- User accounts and saved analyses are needed
- Collaborative annotation or editing is required
- Server-side GIS processing is needed for large datasets
- Authentication/authorization is needed for sensitive data

**If a backend is introduced in the future:**
1. Stop implementation
2. Document the specific requirement that cannot be met statically
3. Create an architecture decision record (ADR)
4. Choose appropriate technology (likely Python/FastAPI given FOSS constraint)
5. Document API contracts
6. Maintain separation of concerns

### Documented as: ADR-002

---

## 5. Database Decision

### Decision: No Database Initially

**Rationale:**

| Factor | Assessment |
|--------|-----------|
| Data characteristics | GIS data is read-heavy, write-rare |
| Data volume | Moderate (65 wards, ~20K features total) — fits in browser memory |
| Data format | GeoPackage/GeoJSON serves the current need |
| Query needs | Spatial queries handled by Turf.js client-side |
| Transaction needs | No concurrent writes, no transactions |
| Complexity | Database adds deployment complexity without clear benefit |

**Future conditions for database introduction:**

PostGIS could become justified if:
- Dataset sizes grow beyond what browsers can efficiently handle
- Complex spatial queries are needed server-side
- Concurrent editing by multiple users is required
- Real-time data updates require server-side processing
- Authentication/authorization is needed

**If PostGIS is introduced:**
1. Document the specific limitation being addressed
2. Create an ADR
3. Migrate data from GeoPackage to PostGIS
4. Update the data flow accordingly

### Documented as: ADR-003

---

## 6. Data Flow

### End-to-End Data Flow

```
Source Data (Bhuvan, OSM, SoI, etc.)
│
│  [Phase 3: Acquisition]
│  Download/extract from official sources
│  Record provenance, license, date
│
▼
Raw GIS Files (.shp, .tif, .gpkg, etc.)
│
│  [Phase 4: Data Engineering]
│  QGIS: import, validate, clean, CRS normalize
│  QGIS: attribute normalization, layer organization
│
▼
Processed GeoPackage (master working file)
│
│  [Phase 6: Spatial Analysis]
│  QGIS: proximity buffers, gap analysis, ward stats
│  All calculations in QGIS — NOT in frontend
│
▼
Analysis Results (GeoPackage layers)
│
│  [Phase 7/8: Export]
│  QGIS: export per-layer as GeoJSON
│  EPSG:4326 for all browser-delivered files
│
▼
GeoJSON Files (per-layer, browser-ready)
│
│  [Phase 9: Web GIS]
│  React: load GeoJSON via fetch/static import
│  Leaflet: render on map
│  Turf.js: optional client-side proximity visualization
│
▼
Interactive Web GIS (browser)
│
│  User: explore layers, select wards, view analysis
│  No server round-trips — all data client-side
```

### Where Calculations Occur

| Calculation | Location | Tool |
|-------------|----------|------|
| Data cleaning | Desktop | QGIS |
| CRS reprojection | Desktop | QGIS |
| Proximity buffers | Desktop | QGIS Processing |
| Gap analysis | Desktop | QGIS Processing |
| Ward statistics | Desktop | QGIS Processing |
| Thematic classification | Desktop | QGIS |
| Buffer visualization (user) | Browser | Turf.js |
| Distance measurement (user) | Browser | Turf.js / Leaflet |
| Layer rendering | Browser | Leaflet |

**Principle:** Heavy GIS processing occurs in QGIS. The frontend visualizes pre-computed results and provides interactive exploration.

---

## 7. Frontend Architecture

### Logical Modules

```
src/
├── app/                    # Application shell
│   ├── App.tsx             # Root component
│   ├── Layout.tsx          # Page layout (header, sidebar, map area)
│   └── Router.tsx          # Route definitions (if multi-page)
│
├── map/                    # Map module
│   ├── MapContainer.tsx    # Leaflet map initialization
│   ├── BaseLayers.tsx      # Base layer options (OSM, etc.)
│   └── MapControls.tsx     # Zoom, scale, fullscreen controls
│
├── layers/                 # Layer management
│   ├── LayerPanel.tsx      # Layer toggle/control panel
│   ├── LayerRenderer.tsx   # Render layers on map
│   └── LayerFilters.tsx    # Filter layer visibility
│
├── facilities/             # Facility explorer
│   ├── FacilityList.tsx    # Browse facilities by category
│   ├── FacilitySearch.tsx  # Search facilities by name/type
│   ├── FacilityDetail.tsx  # Show facility details on click
│   └── FacilityFilter.tsx  # Filter by type, category
│
├── analysis/               # Spatial analysis presentation
│   ├── ProximityPanel.tsx  # Proximity analysis controls
│   ├── GapPanel.tsx        # Gap analysis results
│   └── AnalysisLegend.tsx  # Analysis legends
│
├── wards/                  # Ward analysis
│   ├── WardSelector.tsx    # Ward selection (click/dropdown)
│   ├── WardStats.tsx       # Ward-level statistics display
│   └── WardHighlight.tsx   # Highlight selected ward
│
├── thematic/               # Thematic layer visualization
│   ├── ChoroplethLayer.tsx # Choropleth rendering
│   ├── CategorizedLayer.tsx# Categorized rendering
│   └── ThematicLegend.tsx  # Thematic legends
│
├── ui/                     # Shared UI components
│   ├── InfoPanel.tsx       # Information/detail panels
│   ├── Legend.tsx           # Map legend component
│   ├── Sidebar.tsx         # Sidebar container
│   └── Header.tsx          # Application header
│
├── data/                   # Data access layer
│   ├── loadGeoJSON.ts      # Load and parse GeoJSON files
│   ├── datasets.ts         # Dataset registry (file paths, metadata)
│   └── types.ts            # TypeScript interfaces for data
│
├── utils/                  # Utilities
│   ├── colors.ts           # Color scales and palettes
│   ├── format.ts           # Number/date formatting
│   └── spatial.ts          # Spatial helper functions
│
└── types/                  # Shared types
    ├── ward.ts             # Ward data interfaces
    ├── facility.ts         # Facility data interfaces
    ├── layer.ts            # Layer configuration interfaces
    └── analysis.ts         # Analysis result interfaces
```

### Module Responsibilities

| Module | Responsibility | Dependencies |
|--------|---------------|-------------|
| app/ | Application structure, routing, layout | — |
| map/ | Map initialization, base layers, controls | Leaflet, React-Leaflet |
| layers/ | Layer toggling, rendering, filtering | map/, data/ |
| facilities/ | Facility browsing, search, filtering | layers/, data/ |
| analysis/ | Proximity/gap visualization | layers/, data/ |
| wards/ | Ward selection and statistics | layers/, data/ |
| thematic/ | Thematic map rendering | layers/, data/ |
| ui/ | Shared presentation components | — |
| data/ | Data loading, type definitions | — |
| utils/ | Formatting, colors, spatial helpers | — |
| types/ | TypeScript interfaces | — |

---

## 8. GIS Data Contract

### Data Contract Definition

Every dataset consumed by the Web GIS must conform to a documented contract:

| Property | Description |
|----------|-------------|
| Geometry type | Point, LineString, Polygon, MultiPolygon |
| Key attributes | Schema definition per layer type |
| Identifier | Unique field name for each feature |
| Source | Dataset name and source organization |
| CRS | Coordinate Reference System (EPSG:4326 for delivery) |
| Provenance | Source URL, access date, license, processing steps |
| Update process | How the layer is regenerated from source data |

### Layer Contracts

#### Corporation Boundary

| Property | Value |
|----------|-------|
| Geometry | MultiPolygon |
| Key attributes | `name` (string), `area_sqkm` (float) |
| Identifier | `corp_boundary` |
| Source | Survey of India / State Government boundary data |
| CRS | EPSG:4326 |
| Provenance | TO BE VERIFIED DURING PHASE 3 |

#### Ward Boundaries

| Property | Value |
|----------|-------|
| Geometry | MultiPolygon |
| Key attributes | `ward_name` (string), `ward_id` (string), `ward_number` (int) |
| Identifier | `wards` |
| Source | Trichirappalli Municipal Corporation / Census |
| CRS | EPSG:4326 |
| Provenance | TO BE VERIFIED DURING PHASE 3 |

#### Roads

| Property | Value |
|----------|-------|
| Geometry | LineString |
| Key attributes | `name` (string), `highway` (string), `surface` (string) |
| Identifier | `roads` |
| Source | OpenStreetMap |
| CRS | EPSG:4326 |
| Provenance | TO BE VERIFIED DURING PHASE 3 |

#### Healthcare Facilities

| Property | Value |
|----------|-------|
| Geometry | Point |
| Key attributes | `name` (string), `type` (string), `category` (string), `operator` (string) |
| Identifier | `healthcare` |
| Source | OpenStreetMap / Official healthcare directory |
| CRS | EPSG:4326 |
| Provenance | TO BE VERIFIED DURING PHASE 3 |

#### Education Facilities

| Property | Value |
|----------|-------|
| Geometry | Point |
| Key attributes | `name` (string), `type` (string), `category` (string), `operator` (string) |
| Identifier | `education` |
| Source | OpenStreetMap / Official education directory |
| CRS | EPSG:4326 |
| Provenance | TO BE VERIFIED DURING PHASE 3 |

#### Water Features

| Property | Value |
|----------|-------|
| Geometry | Point / Polygon |
| Key attributes | `name` (string), `type` (string), `water_body` (string) |
| Identifier | `water` |
| Source | OpenStreetMap / Survey of India |
| CRS | EPSG:4326 |
| Provenance | TO BE VERIFIED DURING PHASE 3 |

#### Civic Facilities

| Property | Value |
|----------|-------|
| Geometry | Point |
| Key attributes | `name` (string), `type` (string), `category` (string) |
| Identifier | `civic` |
| Source | OpenStreetMap / Municipal records |
| CRS | EPSG:4326 |
| Provenance | TO BE VERIFIED DURING PHASE 3 |

---

## 9. Provenance Architecture

### Per-Dataset Provenance Record

Every external dataset will have a provenance record:

```yaml
dataset:
  name: "Dataset name"
  source: "Source organization"
  url: "Download URL or portal reference"
  access_date: "YYYY-MM-DD"
  license: "License name and version"
  attribution: "Required attribution text"
  crs_original: "EPSG:XXXX"
  crs_delivery: "EPSG:4326"
  processing_steps:
    - "Step 1: Import into QGIS"
    - "Step 2: Reproject to EPSG:4326"
    - "Step 3: ..."
  intended_use: "How this dataset is used in the project"
  verification_status: "verified / pending"
```

### Provenance Storage

- Individual dataset provenance: stored in `docs/data/` (created in Phase 3)
- Aggregate provenance summary: included in reproducibility package (Phase 8)
- Per-layer metadata: embedded in GeoPackage metadata fields

---

## 10. Reproducibility Architecture

### Reproducibility Requirements

Another GIS analyst must be able to reproduce the analysis by:

1. Acquiring the same source datasets (or equivalent from same source)
2. Following the documented processing steps in QGIS
3. Running the same analysis with the same parameters
4. Obtaining equivalent results

### Reproducibility Components

| Component | How It Is Maintained |
|-----------|---------------------|
| Source data | Documented download URLs, access dates, versions |
| Processing steps | Documented per-layer in QGIS processing history |
| CRS handling | Documented per-layer (original CRS → EPSG:4326) |
| Analysis parameters | Documented (radii: 250m, 500m, 1000m) |
| Derived outputs | GeoPackage/GeoJSON with metadata |
| Map generation | QGIS project file (.qgz) with layout templates |
| Web GIS export | GeoJSON files per-layer, CRS standardized |

### Future Processing Scripts

Processing scripts (Python for QGIS, or shell scripts) may be introduced in later phases where they improve reproducibility. They will be documented with:
- Purpose
- Input requirements
- Expected output
- How to run

---

## 11. Testing Architecture

### GIS Testing Strategy

| Test Type | What Is Tested | Method |
|-----------|---------------|--------|
| Geometry validity | No invalid geometries, no self-intersections | QGIS geometry validator |
| CRS consistency | All layers in expected CRS | QGIS CRS check |
| Feature counts | Counts match expected values | Count features per layer |
| Missing attributes | No null values in required fields | Attribute table inspection |
| Duplicate features | No duplicate geometries or IDs | Spatial/attribute deduplication |
| Spatial relationships | Ward containment, facility locations correct | Visual + spatial query |
| Proximity calculations | Buffer distances correct | Manual verification against known distances |

### Frontend Testing Strategy

| Test Type | What Is Tested | Method |
|-----------|---------------|--------|
| Component behavior | Components render correctly | Unit tests (Vitest) |
| Map rendering | Leaflet initializes, layers display | Integration tests |
| Layer toggling | Layers show/hide correctly | Integration tests |
| Filtering | Facility filter produces correct subset | Unit tests |
| Ward selection | Ward click selects correct ward | Integration tests |
| Data loading | GeoJSON files load without errors | Unit tests |
| Error states | Graceful handling of missing data | Unit tests |

### Integration Testing

| Test Type | What Is Tested | Method |
|-----------|---------------|--------|
| GIS → Frontend | GeoJSON valid, coordinates correct | Automated GeoJSON schema validation |
| Attribute consistency | Frontend types match GeoJSON attributes | TypeScript type checking |
| Coordinate correctness | Features render in correct locations | Visual verification against reference |

### Test Data Policy

- No fabricated test data unless explicitly needed for controlled fixtures
- Use actual project GeoJSON files for integration tests
- If fixtures are needed, derive them from actual data (subsets), not invented data

---

## 12. Security & Data Integrity

### Data Integrity Safeguards

| Safeguard | Description |
|-----------|-------------|
| No fabricated data | All numbers, statistics, and results from verified sources |
| Source verification | Every dataset checked against official source before use |
| License verification | Every dataset license verified before incorporation |
| Deterministic processing | Same inputs → same outputs (no random components) |
| Attribute validation | Check for nulls, type mismatches, duplicates |

### Dependency Security

| Safeguard | Description |
|-----------|-------------|
| Controlled dependencies | Only approved FOSS libraries added |
| No secret keys | No API keys, tokens, or secrets in code |
| No unnecessary external APIs | Static data delivery, no external service calls |
| License compatibility | All dependencies checked for GPL-compatible licenses |

### File Handling

| Safeguard | Description |
|-----------|-------------|
| Safe GIS file handling | GeoPackage/GeoJSON read-only in frontend |
| No local file writes | Frontend does not write to filesystem |
| Input validation | Validate GeoJSON structure before rendering |

---

## 13. Dependency Policy

### Policy

Before adding any library:

1. **Identify why it is needed** — what specific requirement does it fulfill?
2. **Check if the requirement can be met without it** — can existing tools handle it?
3. **Check maintenance/activity** — is the library actively maintained?
4. **Check license compatibility** — is it GPL-compatible?
5. **Check bundle/runtime impact** — how much does it add to bundle size?
6. **Document the reason** — record in ADR if significant

### Current Approved Dependencies

| Dependency | Purpose | License | Justification |
|------------|---------|---------|---------------|
| React | UI framework | MIT | Standard, well-maintained |
| TypeScript | Type safety | Apache-2.0 | Required for maintainability |
| Vite | Build tool | MIT | Fast, modern, FOSS |
| Leaflet | Interactive mapping | BSD-2-Clause | Mature, lightweight, FOSS |
| React-Leaflet | React wrapper for Leaflet | Apache-2.0 | Official React integration |
| Turf.js | Client-side spatial analysis | MIT | FOSS spatial utility |

### Dependency Review Checklist

- [ ] License is FOSS-compatible
- [ ] Library is actively maintained (recent commits, responsive maintainer)
- [ ] Bundle size is justified by functionality
- [ ] No transitive dependency conflicts
- [ ] Documented in this architecture document

---

## 14. Performance Architecture

### Performance Considerations

| Concern | Mitigation |
|---------|-----------|
| GeoJSON file size | Per-layer export (not single monolithic file); simplification where safe |
| Layer loading | Lazy-load layers on demand, not all at once |
| Rendering | Avoid re-rendering unchanged layers; use React.memo where appropriate |
| Large datasets | Roads (19K features) — may need simplification for web display |
| Client memory | ~20K features total — manageable for modern browsers |
| Initial load | Load base map + corporation boundary first; other layers on demand |

### Performance Constraints

- Do NOT simplify GIS data in a way that changes analytical correctness
- Do NOT optimize prematurely — document concerns for later
- Prioritize analytical accuracy over visual smoothness

---

## 15. Cartography Architecture

### Thematic Map Standards

Every thematic map must include:

| Element | Description |
|---------|-------------|
| Title | Clear, descriptive, indicating subject and area |
| Legend | Classification scheme, color mapping, units |
| Scale | Scale bar or representative fraction |
| North arrow | Where appropriate for orientation |
| CRS information | Coordinate system used |
| Source attribution | Data source for each layer |
| Methodology note | Analysis method, assumptions, date |

### Classification Approach

Classification methods will be determined by the actual data distribution during Phase 7. No arbitrary color schemes or classification breaks will be designed before data is analyzed.

### Visual Hierarchy

- Base layer: muted, non-distracting
- Thematic layers: clear color differentiation
- Selected/highlighted features: visually distinct
- Text labels: readable at map scale
- Legends: positioned to not obscure map content

---

## 16. Directory Structure (Future Implementation)

The following structure will be created during implementation phases:

```
smart-trichy/
├── memory.md
├── README.md
├── opencode.json
├── .gitignore
├── LICENSE
│
├── docs/
│   ├── requirements/
│   │   └── project-requirements.md      # Phase 1
│   ├── architecture/
│   │   └── system-architecture.md       # Phase 2 (this file)
│   ├── decisions/
│   │   └── architecture-decisions.md    # Phase 2 (ADRs)
│   ├── data/                            # Phase 3 (provenance records)
│   ├── gis/                             # Phase 4 (processing notes)
│   └── reproducibility/                 # Phase 8 (final docs)
│
├── data/                                # Phase 3-4 (GIS data)
│   ├── raw/                             # Downloaded source data
│   ├── processed/                       # Cleaned, CRS-normalized data
│   └── interim/                         # Intermediate processing outputs
│
├── analysis/                            # Phase 6 (analysis outputs)
│   ├── proximity/                       # Buffer analysis results
│   ├── gap/                             # Gap analysis results
│   └── wards/                           # Ward-level statistics
│
├── maps/                                # Phase 7 (QGIS project + exports)
│   ├── project.qgz                      # QGIS project file
│   └── exports/                         # Exported thematic maps
│
├── web-gis/                             # Phase 9 (React application)
│   ├── src/
│   │   ├── app/
│   │   ├── map/
│   │   ├── layers/
│   │   ├── facilities/
│   │   ├── analysis/
│   │   ├── wards/
│   │   ├── thematic/
│   │   ├── ui/
│   │   ├── data/
│   │   ├── utils/
│   │   └── types/
│   ├── public/
│   │   └── data/                        # GeoJSON files for browser
│   ├── package.json
│   ├── tsconfig.json
│   ├── vite.config.ts
│   └── index.html
│
└── submission/                          # Phase 10 (final packaging)
```

---

## 17. Unresolved Design Decisions

The following design decisions are intentionally deferred:

| Decision | Reason Deferred | When to Resolve |
|----------|----------------|-----------------|
| Specific satellite dataset | Not yet verified in Phase 3 | Phase 5 |
| Exact attribute schemas | Not yet verified with actual data | Phase 4 |
| Thematic classification breaks | Depends on actual data distribution | Phase 7 |
| Color schemes for maps | Depends on data and accessibility review | Phase 7 |
| Frontend state management | Depends on complexity assessment during Phase 9 | Phase 9 |
| Simplification thresholds for roads | Depends on performance testing | Phase 9 |

---

## 18. Architecture Diagram — Simplified

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│    QGIS DESKTOP                                                    │
│    ┌──────────────────────────────────────────────┐                 │
│    │  Source Data → Clean → Normalize → Analyze   │                 │
│    │  → Export GeoJSON (EPSG:4326 per layer)      │                 │
│    └──────────────────────────────────────────────┘                 │
│                          │                                          │
│                          ▼                                          │
│    ┌──────────────────────────────────────────────┐                 │
│    │  GeoJSON Files (public/data/*.json)          │                 │
│    │  wards.json, healthcare.json, education.json │                 │
│    │  roads.json, water.json, civic.json          │                 │
│    └──────────────────────────────────────────────┘                 │
│                          │                                          │
│                          ▼                                          │
│    BROWSER                                                          │
│    ┌──────────────────────────────────────────────┐                 │
│    │  React + TypeScript + Vite                   │                 │
│    │  ├── Leaflet Map (render layers)             │                 │
│    │  ├── Layer Control (toggle/filter)           │                 │
│    │  ├── Facility Explorer (browse/search)       │                 │
│    │  ├── Ward Analysis (select/analyze)          │                 │
│    │  ├── Thematic Maps (choropleth/categorized)  │                 │
│    │  └── Turf.js (client-side proximity viz)     │                 │
│    └──────────────────────────────────────────────┘                 │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

**End of System Architecture Document**
