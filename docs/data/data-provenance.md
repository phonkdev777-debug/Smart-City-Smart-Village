# Data Provenance

## Smart City / Smart Village — Trichirappalli

**Document:** Phase 3 — GIS Data Acquisition & Provenance

**Status:** IN PROGRESS

**Last updated:** 2026-08-17

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

**End of Data Provenance Document**
