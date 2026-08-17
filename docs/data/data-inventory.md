# Data Inventory

## Smart City / Smart Village — Trichirappalli

**Document:** Phase 3 — GIS Data Acquisition & Provenance

**Status:** IN PROGRESS

**Last updated:** 2026-08-17

---

## Inventory Summary

| Category | Datasets Identified | Datasets Verified | Datasets Acquired |
|----------|--------------------|--------------------|-------------------|
| Corporation Boundary | 2 candidates | 0 | 0 |
| Ward Boundaries | 2 candidates | 0 | 0 |
| Roads | 1 source | 0 | 0 |
| Healthcare | 1 source | 0 | 0 |
| Education | 1 source | 0 | 0 |
| Water Features | 1 source | 0 | 0 |
| Civic Facilities | 1 source | 0 | 0 |
| Indian Geospatial (LULC) | 2 candidates | 0 | 0 |

---

## Existing Project Data Status

The project specification references the following data counts. These are treated as **project-provided existing-data references**.

**SOURCE DATA NOT YET PRESENT IN REPOSITORY.**

No GIS data files (.shp, .gpkg, .geojson, .tif) exist in the repository.

| Category | Reference Count | Files in Repository | Status |
|----------|----------------|---------------------|--------|
| Corporation Boundary | 1 | None | NOT PRESENT |
| Ward Boundaries | 65 | None | NOT PRESENT |
| Roads | 19,064 | None | NOT PRESENT |
| Healthcare facilities | 236 | None | NOT PRESENT |
| Education facilities | 55 | None | NOT PRESENT |
| Water features | 563 | None | NOT PRESENT |
| Civic facilities | 34 | None | NOT PRESENT |

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
| Verification Status | NOT VERIFIED — candidates identified, actual availability pending |
| Notes | SoI provides admin boundaries up to taluk level. Municipal corporation boundary may need to be sourced from Tamil Nadu Government / Trichy Corporation official sources. Trichy Corporation website has city map PDF with ward boundaries. |
| Known Limitations | SoI admin boundary database may not have municipal corporation level — may stop at taluk. Corporation boundary may need to be derived from ward boundaries or sourced from state government. |

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
| Verification Status | NOT VERIFIED — ward count confirmed as 65 (5 zones × 13 wards) |
| Notes | Corporation website confirms 65 wards in 5 zones. Ward map PDF available. OSM may have ward boundaries as admin_level 8. TN Urban Tree portal also has ward data. |
| Known Limitations | Digital ward boundary shapefile/GeoJSON source not yet identified. May need to extract from OSM or request from corporation. |

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
| Verification Status | NOT VERIFIED — OSM relation exists, feature count not yet verified against 19,064 reference |
| Notes | Roads can be extracted via Overpass API or download tools (osmium, etc.). Need to clip to municipal corporation boundary. OSM data is community-maintained — not official government data. |
| Known Limitations | OSM is not a complete census of roads. Missing OSM roads do not necessarily mean they don't exist. Cannot be claimed as official road data. |

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
| Verification Status | NOT VERIFIED — reference count 236 not yet verified |
| Notes | OSM healthcare features tagged with amenity=hospital, amenity=clinic, amenity=doctors, healthcare=* |
| Known Limitations | OSM is not a complete census of healthcare facilities. Cannot claim "this ward has no healthcare" based on OSM absence. |

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
| Verification Status | NOT VERIFIED — reference count 55 not yet verified |
| Notes | OSM education features tagged with amenity=school, amenity=college, amenity=university, education=* |
| Known Limitations | OSM is not a complete census of education facilities. |

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
| Verification Status | NOT VERIFIED — reference count 563 not yet verified |
| Notes | OSM water features tagged with natural=water, waterway=*, man_made=water_tap, etc. |
| Known Limitations | OSM water features may not be complete. |

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
| Verification Status | NOT VERIFIED — reference count 34 not yet verified |
| Notes | OSM civic features may include community centres, town halls, post offices, fire stations, police stations, etc. Exact category definition needs clarification. |
| Known Limitations | "Civic facilities" is a broad category — exact definition needs alignment with project specification. |

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
| Verification Status | NOT VERIFIED — dataset exists on Bhuvan, availability for Trichy district pending confirmation |
| Notes | Available temporal cycles: 2005-06, 2011-12, 2015-16. Latest available is 2015-16. Download requires user registration, AOI selection, purpose specification, and email approval. LULC classes include built-up, water, vegetation, fallow land, etc. |
| Known Limitations | Latest LULC 50K is 2015-16 — not current. Download process is manual (request-based). Data may not cover exact corporation boundary — will need clipping. Classification scheme needs verification. |

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
| Study area boundary | DS-001 (Corporation Boundary) | NOT VERIFIED |
| Ward boundaries (65) | DS-002 (Ward Boundaries) | NOT VERIFIED |
| Road network (19,064) | DS-003 (Roads — OSM) | NOT VERIFIED |
| Healthcare (236) | DS-004 (Healthcare — OSM) | NOT VERIFIED |
| Education (55) | DS-005 (Education — OSM) | NOT VERIFIED |
| Water features (563) | DS-006 (Water — OSM) | NOT VERIFIED |
| Civic facilities (34) | DS-007 (Civic — OSM) | NOT VERIFIED |
| Indian satellite/geospatial data | DS-008 (Bhuvan LULC 50K) | NOT VERIFIED |
| Population spatial data | N/A — Not available | NOT APPLICABLE |

---

**End of Data Inventory**
