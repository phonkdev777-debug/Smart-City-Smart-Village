# Data Provenance

## Smart City / Smart Village — Trichirappalli

**Document:** Phase 3 — GIS Data Acquisition & Provenance

**Status:** IN PROGRESS

**Last updated:** 2026-08-17 (Phase 3B — OSM data acquired)

---

## Provenance Model

Every dataset in this project follows a traceable provenance chain:

```
Source Organization
    ↓
Official Portal / Download
    ↓
Acquisition (date, method, user)
    ↓
Validation (geometry, CRS, attributes)
    ↓
Processing (cleaning, clipping, reprojection)
    ↓
Derived Dataset (processed output)
    ↓
GIS Analysis (proximity, gap, ward-level)
    ↓
Thematic Map (QGIS layout)
    ↓
Web GIS Representation (GeoJSON export)
```

Each link in this chain must be documented.

---

## Provenance Requirements

For every external dataset, the following must be recorded:

| Property | Description |
|----------|-------------|
| Dataset name | Official name of the dataset |
| Source organization | Organization that produced/publishes the data |
| Official URL | Primary access point or documentation URL |
| Access method | How the data was obtained (download, WMS, API, manual) |
| Access date | Date the data was accessed/downloaded |
| Version/cycle | Temporal version if applicable |
| License | Official license or terms of use |
| Attribution | Required attribution text |
| CRS (original) | Coordinate Reference System of the source data |
| CRS (processed) | CRS after processing (EPSG:4326 for delivery) |
| Processing steps | What was done to the data |
| Intended use | How the dataset is used in the project |
| Verification status | Whether the source and data have been verified |

---

## Source Hierarchy

When evaluating data sources, this project prioritizes:

1. **Official Indian government source** (Survey of India, Bhuvan/NRSC, state government portals)
2. **Official dataset documentation** (metadata, technical documents)
3. **Official source metadata** (CRS, licensing, methodology)
4. **Established open geospatial source** (OpenStreetMap with ODbL)
5. **Secondary documentation** (academic papers, wiki) — for discovery only

Secondary sources are NOT accepted as proof of official status.

---

## Source-Specific Provenance Notes

### OpenStreetMap (OSM)

| Property | Value |
|----------|-------|
| Source | OpenStreetMap Foundation |
| License | Open Database License (ODbL) |
| Attribution | "© OpenStreetMap contributors" |
| CRS | EPSG:4326 (native) |
| Data nature | Community-maintained, crowdsourced |
| Official status | NOT official government data |
| Completeness | NOT a complete census |
| Access method | Overpass API, bulk download, or export tools |

**OSM Provenance Rules:**
- Always attribute "© OpenStreetMap contributors"
- Always note that OSM is community-maintained, not official
- Never claim OSM data is a complete census
- Never claim missing OSM features means the feature doesn't exist
- Document the extraction date and area

### Survey of India (SoI)

| Property | Value |
|----------|-------|
| Source | Survey of India |
| Portal | https://onlinemaps.surveyofindia.gov.in/ |
| License | Government of India — free for registered government users; some datasets free for all |
| Data nature | Official government geospatial data |
| Available products | Administrative Boundary Database, Village Boundary Database, Topographical Maps |
| Administrative coverage | Up to taluk level (may not include municipal corporation boundary) |

**SoI Provenance Rules:**
- Only claim "Survey of India" if downloaded from the official SoI portal
- Document the exact product name and access date
- Note that SoI admin boundaries may stop at taluk level

### Bhuvan (ISRO/NRSC)

| Property | Value |
|----------|-------|
| Source | National Remote Sensing Centre (NRSC), ISRO |
| Portal | https://bhuvan-app1.nrsc.gov.in/ |
| Download | https://bhuvan-app3.nrsc.gov.in/data/download/ |
| License | Free for download with registration and approval |
| Data nature | Indian satellite-derived thematic data |
| Available products | LULC 1:50K, LULC 1:250K, Urban Land Use, Wastelands, etc. |
| Access method | Request-based (register, select AOI, specify purpose, email approval) |

**Bhuvan Provenance Rules:**
- Only claim "Bhuvan/ISRO/NRSC" if downloaded from the official Bhuvan portal
- Document the exact product name, temporal cycle, and access date
- Note the approval process and any restrictions
- Acknowledge ISRO/NRSC as required

### Tamil Nadu Government Portals

| Property | Value |
|----------|-------|
| Sources | TNGIS (tngis.tn.gov.in), TN Urban Tree (tnurbantree.tn.gov.in), Trichy Corporation (trichycorporation.gov.in) |
| License | Government of Tamil Nadu — terms TBD |
| Data nature | State/city government administrative data |
| Available products | Ward maps, city maps, administrative boundaries |

**TN Government Provenance Rules:**
- Document the exact portal and page where data was found
- Note if data is available for download or only for viewing
- Verify licensing before incorporating

---

## Provenance Template

Use this template for each acquired dataset:

```yaml
dataset_id: "DS-XXX"
dataset_name: ""
source_organization: ""
official_url: ""
access_method: "download / WMS / API / manual"
access_date: "YYYY-MM-DD"
version_cycle: ""
license: ""
attribution: ""
crs_original: ""
crs_processed: "EPSG:4326"
processing_steps:
  - ""
intended_use: ""
verification_status: "verified / not verified"
notes: ""
```

---

## Provenance Storage Locations

| Location | Content |
|----------|---------|
| `docs/data/data-inventory.md` | Dataset-level provenance summary |
| `docs/data/data-quality-report.md` | Validation results per dataset |
| `docs/data/data-dictionary.md` | Attribute schemas per dataset |
| QGIS project file (.qgz) | Processing history, layer styles |
| GeoPackage metadata | Embedded per-layer metadata |
| `docs/reproducibility/` (Phase 8) | Final reproducibility package |

---

## Acquired Dataset Provenance

### DS-001: Corporation Boundary (OSM)

```yaml
dataset_id: "DS-001"
dataset_name: "Trichy Corporation Limits"
source_organization: "OpenStreetMap contributors"
official_url: "https://www.openstreetmap.org/relation/1553009"
access_method: "Overpass API query"
access_date: "2026-08-17"
version_cycle: "OSM current"
license: "Open Database License (ODbL)"
attribution: "© OpenStreetMap contributors"
crs_original: "EPSG:4326 (WGS84)"
crs_processed: "EPSG:4326"
processing_steps:
  - "Query relation 1553009 via Overpass API"
  - "Retrieve with member way geometry"
intended_use: "Study area boundary for clipping, project context, Web GIS base layer"
verification_status: "source verified"
notes: "OSM relation 1553009, admin_level=8, 30 member ways, 359 geometry points. Wikidata Q4045755. Source references trichycorporation.gov.in. This is community data, not official government boundary."
```

### DS-002: Ward Boundaries (OSM)

```yaml
dataset_id: "DS-002"
dataset_name: "Trichy Corporation Ward Boundaries"
source_organization: "OpenStreetMap contributors"
official_url: "https://www.openstreetmap.org (admin_level=10 relations)"
access_method: "Overpass API query (bounding box)"
access_date: "2026-08-17"
version_cycle: "OSM current"
license: "Open Database License (ODbL)"
attribution: "© OpenStreetMap contributors"
crs_original: "EPSG:4326 (WGS84)"
crs_processed: "EPSG:4326"
processing_steps:
  - "Query admin_level=10 relations in bounding box (10.75,78.60,10.90,78.80)"
intended_use: "Ward-level spatial analysis, ward selection, thematic mapping"
verification_status: "source verified"
notes: "65 ward boundaries found. Names: Ward 1 through Ward 65. Matches project specification count. Community-maintained, not official."
```

### DS-003: Roads (OSM)

```yaml
dataset_id: "DS-003"
dataset_name: "Trichy Road Network"
source_organization: "OpenStreetMap contributors"
official_url: "https://www.openstreetmap.org"
access_method: "Overpass API query (bounding box)"
access_date: "2026-08-17"
version_cycle: "OSM current"
license: "Open Database License (ODbL)"
attribution: "© OpenStreetMap contributors"
crs_original: "EPSG:4326 (WGS84)"
crs_processed: "EPSG:4326"
processing_steps:
  - "Query highway=* ways in bounding box (10.75,78.60,10.90,78.80)"
intended_use: "Road network for contextual mapping, proximity analysis reference"
verification_status: "acquired"
notes: "15,409 road elements. Extracted from bounding box, NOT clipped to corporation boundary. Residential (11,834), service (1,277), unclassified (677), tertiary (486), trunk (374)."
```

### DS-004: Healthcare Facilities (OSM)

```yaml
dataset_id: "DS-004"
dataset_name: "Trichy Healthcare Facilities"
source_organization: "OpenStreetMap contributors"
official_url: "https://www.openstreetmap.org"
access_method: "Overpass API query (bounding box)"
access_date: "2026-08-17"
version_cycle: "OSM current"
license: "Open Database License (ODbL)"
attribution: "© OpenStreetMap contributors"
crs_original: "EPSG:4326 (WGS84)"
crs_processed: "EPSG:4326"
processing_steps:
  - "Query amenity=hospital|clinic|doctors and healthcare=* in bounding box"
intended_use: "Healthcare facility mapping, proximity analysis, gap analysis"
verification_status: "acquired"
notes: "234 elements. Hospital (133), clinic (52), pharmacy (22), dentist (8), doctors (2), blood_bank (1). NOT a complete census."
```

### DS-005: Education Facilities (OSM)

```yaml
dataset_id: "DS-005"
dataset_name: "Trichy Education Facilities"
source_organization: "OpenStreetMap contributors"
official_url: "https://www.openstreetmap.org"
access_method: "Overpass API query (bounding box)"
access_date: "2026-08-17"
version_cycle: "OSM current"
license: "Open Database License (ODbL)"
attribution: "© OpenStreetMap contributors"
crs_original: "EPSG:4326 (WGS84)"
crs_processed: "EPSG:4326"
processing_steps:
  - "Query amenity=school|college|university|kindergarten in bounding box"
intended_use: "Education facility mapping, gap analysis"
verification_status: "acquired"
notes: "47 elements. School (39), university (5), college (3). NOT a complete census."
```

### DS-006: Water Features (OSM)

```yaml
dataset_id: "DS-006"
dataset_name: "Trichy Water Features"
source_organization: "OpenStreetMap contributors"
official_url: "https://www.openstreetmap.org"
access_method: "Overpass API query (bounding box)"
access_date: "2026-08-17"
version_cycle: "OSM current"
license: "Open Database License (ODbL)"
attribution: "© OpenStreetMap contributors"
crs_original: "EPSG:4326 (WGS84)"
crs_processed: "EPSG:4326"
processing_steps:
  - "Query natural=water, waterway=*, man_made=water_tap|water_well in bounding box"
intended_use: "Water feature mapping, distribution analysis"
verification_status: "acquired"
notes: "528 elements. Mixed geometry (Point/Polygon/LineString). Ditch (319), drain (50), canal (50), water (47), stream (36), river (22). May not be complete."
```

### DS-007: Civic Facilities (OSM)

```yaml
dataset_id: "DS-007"
dataset_name: "Trichy Civic Facilities"
source_organization: "OpenStreetMap contributors"
official_url: "https://www.openstreetmap.org"
access_method: "Overpass API query (bounding box)"
access_date: "2026-08-17"
version_cycle: "OSM current"
license: "Open Database License (ODbL)"
attribution: "© OpenStreetMap contributors"
crs_original: "EPSG:4326 (WGS84)"
crs_processed: "EPSG:4326"
processing_steps:
  - "Query amenity=community_centre|town_hall|post_office|fire_station|police|library and office=government in bounding box"
intended_use: "Civic facility mapping, availability analysis"
verification_status: "acquired"
notes: "40 elements. Police (12), post_office (11), community_centre (8), government (7), social_facility (2)."
```

### DS-008: Bhuvan LULC 1:50K

```yaml
dataset_id: "DS-008"
dataset_name: "Land Use Land Cover 1:50,000 — Tamil Nadu"
source_organization: "National Remote Sensing Centre (NRSC), ISRO"
official_url: "https://bhuvan-app3.nrsc.gov.in/data/download/"
access_method: "Manual request (register, AOI, purpose, email approval)"
access_date: "2026-08-17 (verified, not downloaded)"
version_cycle: "2005-06, 2011-12, 2015-16"
license: "Free for download with registration"
attribution: "ISRO/NRSC acknowledgement expected"
crs_original: "TO BE VERIFIED"
crs_processed: "TO BE VERIFIED"
processing_steps: []
intended_use: "Thematic analysis — LULC distribution, urban expansion, green space, built-up area"
verification_status: "source verified — requires manual download request"
notes: "Available via Bhuvan portal. Shapefile format. Process: Register → Select districts → Draw AOI → Specify purpose → Email approval. Latest cycle: 2015-16."
```

---

**End of Data Provenance Document**
