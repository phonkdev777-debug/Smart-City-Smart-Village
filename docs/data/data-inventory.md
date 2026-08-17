# Data Inventory

## Smart City / Smart Village — Trichirappalli

**Document:** Phase 3 — GIS Data Acquisition & Provenance

**Status:** IN PROGRESS

**Last updated:** 2026-08-17 (Phase 3B — OSM data acquired)

---

## Inventory Summary

| Category | Datasets Identified | Datasets Verified | Datasets Acquired |
|----------|--------------------|--------------------|-------------------|
| Corporation Boundary | 2 candidates | 1 (OSM) | 1 |
| Ward Boundaries | 2 candidates | 1 (OSM) | 1 |
| Roads | 1 source | 1 (OSM) | 1 |
| Healthcare | 1 source | 1 (OSM) | 1 |
| Education | 1 source | 1 (OSM) | 1 |
| Water Features | 1 source | 1 (OSM) | 1 |
| Civic Facilities | 1 source | 1 (OSM) | 1 |
| Indian Geospatial (LULC) | 2 candidates | 1 (Bhuvan verified) | 0 (requires manual request) |

---

## Existing Project Data Status

The project specification references the following data counts. These are treated as **project-provided existing-data references**.

**OSM DATA ACQUIRED — Raw GeoJSON files in `gis/raw/osm/`**

| Category | Reference Count | Acquired Count | Status |
|----------|----------------|----------------|--------|
| Corporation Boundary | 1 | 1 (OSM relation) | ACQUIRED |
| Ward Boundaries | 65 | 65 (OSM admin_level=10) | ACQUIRED |
| Roads | 19,064 | 15,409 (bbox, not clipped) | ACQUIRED |
| Healthcare facilities | 236 | 234 | ACQUIRED |
| Education facilities | 55 | 47 | ACQUIRED |
| Water features | 563 | 528 | ACQUIRED |
| Civic facilities | 34 | 40 | ACQUIRED |

---

## Dataset Records

### DS-001: Trichirappalli Municipal Corporation Boundary

| Field | Value |
|-------|-------|
| Dataset ID | DS-001 |
| Dataset Name | Trichirappalli Municipal Corporation Boundary |
| Category | Administrative Boundary |
| Study Area | Trichirappalli Municipal Corporation |
| Source | Survey of India Administrative Boundary Database / Tamil Nadu Government |
| Official URL | https://onlinemaps.surveyofindia.gov.in/ (Admin Boundary Database — free download) |
| Source Organization | Survey of India / Tamil Nadu Government |
| Dataset Type | Vector — Administrative Boundary |
| Geometry Type | Polygon / MultiPolygon |
| CRS | TO BE VERIFIED |
| License | TO BE VERIFIED — SoI Administrative Boundary Database is free for all users |
| Attribution Requirement | TO BE VERIFIED |
| Access/Download Date | NOT YET DOWNLOADED |
| Original Filename | NOT YET DETERMINED |
| Current Repository Location | NOT PRESENT |
| Processing Status | NOT STARTED |
| Intended Project Use | Study area boundary for clipping, project context, Web GIS base layer |
| Verification Status | SOURCE VERIFIED — OSM relation 1553009 |
| Notes | Acquired via Overpass API on 2026-08-17. OSM relation 1553009, admin_level=8, 30 member ways, 359 geometry points. Coordinates: Lat 10.7273-10.8805, Lon 78.6307-78.7835. Wikidata Q4045755. Source website references trichycorporation.gov.in. This is OSM community data, NOT official government boundary. |
| Known Limitations | OSM is community-maintained, not official government data. Source tag references corporation website but data may not be current or accurate to official boundary. Official digital boundary not publicly downloadable (TNGIS requires authentication). |

### DS-002: Ward Boundaries (65 Wards)

| Field | Value |
|-------|-------|
| Dataset ID | DS-002 |
| Dataset Name | Trichirappalli City Corporation Ward Boundaries |
| Category | Administrative Boundary |
| Study Area | Trichirappalli Municipal Corporation (65 wards) |
| Source | Trichirappalli City Corporation / Tamil Nadu Government / OSM |
| Official URL | https://www.trichycorporation.gov.in/mapwardsz4 (ward map) |
| Source Organization | Trichirappalli City Corporation |
| Dataset Type | Vector — Administrative Boundary |
| Geometry Type | Polygon / MultiPolygon |
| CRS | TO BE VERIFIED |
| License | TO BE VERIFIED |
| Attribution Requirement | TO BE VERIFIED |
| Access/Download Date | NOT YET DOWNLOADED |
| Original Filename | NOT YET DETERMINED |
| Current Repository Location | NOT PRESENT |
| Processing Status | NOT STARTED |
| Intended Project Use | Ward-level spatial analysis, ward selection, thematic mapping |
| Verification Status | SOURCE VERIFIED — 65 OSM relations (admin_level=10) |
| Notes | Acquired via Overpass API on 2026-08-17. 65 ward boundaries found in OSM (admin_level=10 within bounding box). Names: Ward 1 through Ward 65. Matches project specification count. |
| Known Limitations | OSM ward boundaries are community-maintained, not official government data. Official digital ward boundary shapefile not publicly downloadable. Corporation website has PDF ward maps only. |

### DS-003: Roads

| Field | Value |
|-------|-------|
| Dataset ID | DS-003 |
| Dataset Name | Trichirappalli Road Network |
| Category | Transportation |
| Study Area | Trichirappalli Municipal Corporation |
| Source | OpenStreetMap |
| Official URL | https://www.openstreetmap.org/relation/1819323 (Tiruchirappalli) |
| Source Organization | OpenStreetMap contributors |
| Dataset Type | Vector — Transportation |
| Geometry Type | LineString |
| CRS | EPSG:4326 (OSM native) |
| License | Open Database License (ODbL) — https://opendatacommons.org/licenses/odbl/ |
| Attribution Requirement | "© OpenStreetMap contributors" — see ODbL terms |
| Access/Download Date | NOT YET DOWNLOADED |
| Original Filename | NOT YET DETERMINED |
| Current Repository Location | NOT PRESENT |
| Processing Status | NOT STARTED |
| Intended Project Use | Road network for contextual mapping, proximity analysis reference |
| Verification Status | ACQUIRED — 15,409 elements (reference: 19,064) |
| Notes | Acquired via Overpass API on 2026-08-17. Bounding box query (10.75-10.90, 78.60-78.80). 15,409 road elements. Road types: residential (11,834), service (1,277), unclassified (677), tertiary (486), trunk (374), secondary (249), primary (170). NOT clipped to corporation boundary — some roads may be outside limits. |
| Known Limitations | Extracted from bounding box, not clipped to corporation boundary. OSM is community-maintained, not official government data. OSM is not a complete census of roads. Feature count differs from reference (expected). |

### DS-004: Healthcare Facilities

| Field | Value |
|-------|-------|
| Dataset ID | DS-004 |
| Dataset Name | Trichirappalli Healthcare Facilities |
| Category | Social Infrastructure |
| Study Area | Trichirappalli Municipal Corporation |
| Source | OpenStreetMap |
| Official URL | Overpass API query for healthcare within Trichy boundary |
| Source Organization | OpenStreetMap contributors |
| Dataset Type | Vector — Points of Interest |
| Geometry Type | Point |
| CRS | EPSG:4326 (OSM native) |
| License | Open Database License (ODbL) |
| Attribution Requirement | "© OpenStreetMap contributors" |
| Access/Download Date | NOT YET DOWNLOADED |
| Original Filename | NOT YET DETERMINED |
| Current Repository Location | NOT PRESENT |
| Processing Status | NOT STARTED |
| Intended Project Use | Healthcare facility mapping, proximity analysis, gap analysis |
| Verification Status | ACQUIRED — 234 elements (reference: 236) |
| Notes | Acquired via Overpass API on 2026-08-17. Bounding box query. 234 healthcare elements. Types: hospital (133), clinic (52), pharmacy (22), dentist (8), doctors (2), blood_bank (1). |
| Known Limitations | OSM is community-maintained, not official government data. OSM is NOT a complete census of healthcare facilities. Cannot claim "this ward has no healthcare" based on OSM absence. Feature count close to reference. |

### DS-005: Education Facilities

| Field | Value |
|-------|-------|
| Dataset ID | DS-005 |
| Dataset Name | Trichirappalli Education Facilities |
| Category | Social Infrastructure |
| Study Area | Trichirappalli Municipal Corporation |
| Source | OpenStreetMap |
| Official URL | Overpass API query for education within Trichy boundary |
| Source Organization | OpenStreetMap contributors |
| Dataset Type | Vector — Points of Interest |
| Geometry Type | Point |
| CRS | EPSG:4326 (OSM native) |
| License | Open Database License (ODbL) |
| Attribution Requirement | "© OpenStreetMap contributors" |
| Access/Download Date | NOT YET DOWNLOADED |
| Original Filename | NOT YET DETERMINED |
| Current Repository Location | NOT PRESENT |
| Processing Status | NOT STARTED |
| Intended Project Use | Education facility mapping, gap analysis |
| Verification Status | ACQUIRED — 47 elements (reference: 55) |
| Notes | Acquired via Overpass API on 2026-08-17. Bounding box query. 47 education elements. Types: school (39), university (5), college (3). |
| Known Limitations | OSM is community-maintained, not official government data. OSM is NOT a complete census of education facilities. Feature count differs from reference (expected). |

### DS-006: Water Features

| Field | Value |
|-------|-------|
| Dataset ID | DS-006 |
| Dataset Name | Trichirappalli Water Features |
| Category | Hydrology |
| Study Area | Trichirappalli Municipal Corporation |
| Source | OpenStreetMap |
| Official URL | Overpass API query for water within Trichy boundary |
| Source Organization | OpenStreetMap contributors |
| Dataset Type | Vector — Hydrology |
| Geometry Type | Point / Polygon / LineString |
| CRS | EPSG:4326 (OSM native) |
| License | Open Database License (ODbL) |
| Attribution Requirement | "© OpenStreetMap contributors" |
| Access/Download Date | NOT YET DOWNLOADED |
| Original Filename | NOT YET DETERMINED |
| Current Repository Location | NOT PRESENT |
| Processing Status | NOT STARTED |
| Intended Project Use | Water feature mapping, distribution analysis |
| Verification Status | ACQUIRED — 528 elements (reference: 563) |
| Notes | Acquired via Overpass API on 2026-08-17. Bounding box query. 528 water elements. Types: waterway=ditch (319), waterway=drain (50), waterway=canal (50), natural=water (47), waterway=stream (36), waterway=river (22). Mixed geometry: Point/Polygon/LineString. |
| Known Limitations | OSM is community-maintained, not official government data. OSM water features may not be complete. Feature count close to reference. |

### DS-007: Civic Facilities

| Field | Value |
|-------|-------|
| Dataset ID | DS-007 |
| Dataset Name | Trichirappalli Civic Facilities |
| Category | Civic Infrastructure |
| Study Area | Trichirappalli Municipal Corporation |
| Source | OpenStreetMap |
| Official URL | Overpass API query for civic amenities within Trichy boundary |
| Source Organization | OpenStreetMap contributors |
| Dataset Type | Vector — Points of Interest |
| Geometry Type | Point |
| CRS | EPSG:4326 (OSM native) |
| License | Open Database License (ODbL) |
| Attribution Requirement | "© OpenStreetMap contributors" |
| Access/Download Date | NOT YET DOWNLOADED |
| Original Filename | NOT YET DETERMINED |
| Current Repository Location | NOT PRESENT |
| Processing Status | NOT STARTED |
| Intended Project Use | Civic facility mapping, availability analysis |
| Verification Status | ACQUIRED — 40 elements (reference: 34) |
| Notes | Acquired via Overpass API on 2026-08-17. Bounding box query. 40 civic elements. Types: police (12), post_office (11), community_centre (8), office=government (7), social_facility (2). |
| Known Limitations | OSM is community-maintained, not official government data. "Civic facilities" is a broad category. Feature count differs from reference (expected). |

### DS-008: Bhuvan LULC 1:50K (Indian Geospatial Dataset — Primary Candidate)

| Field | Value |
|-------|-------|
| Dataset ID | DS-008 |
| Dataset Name | Land Use Land Cover 1:50,000 — Tamil Nadu |
| Category | Indian Geospatial / Remote Sensing |
| Study Area | Trichirappalli district (will be clipped to corporation boundary) |
| Source | Bhuvan (ISRO/NRSC) |
| Official URL | https://bhuvan-app1.nrsc.gov.in/thematic/ and https://bhuvan-app3.nrsc.gov.in/data/download/ |
| Source Organization | National Remote Sensing Centre (NRSC), ISRO |
| Dataset Type | Vector — Thematic (Land Use Land Cover) |
| Geometry Type | Polygon |
| CRS | EPSG:4326 (Bhuvan WMS default) |
| License | TO BE VERIFIED — Bhuvan data is free for download but requires request and approval |
| Attribution Requirement | TO BE VERIFIED — acknowledgement expected from users |
| Access/Download Date | NOT YET DOWNLOADED |
| Original Filename | NOT YET DETERMINED |
| Current Repository Location | NOT PRESENT |
| Processing Status | NOT STARTED |
| Intended Project Use | Thematic analysis — land use/land cover distribution within Trichy corporation, urban expansion analysis, green space identification, built-up area analysis |
| Verification Status | SOURCE VERIFIED — download requires manual request |
| Notes | Verified from Bhuvan portal on 2026-08-17. Available temporal cycles: 2005-06, 2011-12, 2015-16. Format: Shapefile. Download process: Register → Select up to 5 districts → Draw AOI → Specify purpose → Email approval → Download link. LULC classes include built-up, water, vegetation, fallow land, etc. WMS service also available for visualization. |
| Known Limitations | Latest LULC 50K is 2015-16 — not current. Download is request-based (manual process, cannot be automated). Data may not cover exact corporation boundary — will need clipping. Classification scheme needs verification from technical document. |

### DS-009: Bhuvan LULC 1:250K (Indian Geospatial Dataset — Alternative Candidate)

| Field | Value |
|-------|-------|
| Dataset ID | DS-009 |
| Dataset Name | Land Use Land Cover 1:250,000 — India |
| Category | Indian Geospatial / Remote Sensing |
| Study Area | All India (will be clipped to Trichy corporation) |
| Source | Bhuvan (ISRO/NRSC) |
| Official URL | https://bhuvan-app1.nrsc.gov.in/2dresources/bhuvanstore2.php |
| Source Organization | National Remote Sensing Centre (NRSC), ISRO |
| Dataset Type | Raster/Vector — Thematic |
| Geometry Type | Polygon (vectorized) or Raster |
| CRS | TO BE VERIFIED |
| License | TO BE VERIFIED |
| Attribution Requirement | TO BE VERIFIED |
| Access/Download Date | NOT YET DOWNLOADED |
| Original Filename | NOT YET DETERMINED |
| Current Repository Location | NOT PRESENT |
| Processing Status | NOT STARTED |
| Intended Project Use | Broader land use context if 50K is unavailable |
| Verification Status | NOT VERIFIED |
| Notes | Available for multiple years (2004-05 through 2022-23). Lower resolution than 50K. Direct data download available. |
| Known Limitations | Lower resolution (1:250K) — less detailed than 50K. May not be suitable for ward-level analysis. |

---

## Dataset Relationship to Project Requirements

| Requirement | Dataset(s) | Status |
|-------------|-----------|--------|
| Study area boundary | DS-001 (Corporation Boundary — OSM) | ACQUIRED |
| Ward boundaries (65) | DS-002 (Ward Boundaries — OSM, 65 found) | ACQUIRED |
| Road network (19,064) | DS-003 (Roads — OSM, 15,409 found) | ACQUIRED |
| Healthcare (236) | DS-004 (Healthcare — OSM, 234 found) | ACQUIRED |
| Education (55) | DS-005 (Education — OSM, 47 found) | ACQUIRED |
| Water features (563) | DS-006 (Water — OSM, 528 found) | ACQUIRED |
| Civic facilities (34) | DS-007 (Civic — OSM, 40 found) | ACQUIRED |
| Indian satellite/geospatial data | DS-008 (Bhuvan LULC 50K) | VERIFIED — requires manual request |
| Population spatial data | N/A — Not available | NOT APPLICABLE |

---

**End of Data Inventory**
