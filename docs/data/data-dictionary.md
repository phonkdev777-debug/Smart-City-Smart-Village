# Data Dictionary

## Smart City / Smart Village — Trichirappalli

**Document:** Phase 3 — GIS Data Acquisition & Provenance

**Status:** IN PROGRESS

**Last updated:** 2026-08-17 (Phase 3B — OSM data acquired)

---

## Policy

This data dictionary documents verified field schemas only.

- If a field schema is not yet verified: `TO BE VERIFIED DURING DATA VALIDATION`
- Do not invent schemas before actual datasets are available
- Update this document as datasets are acquired and inspected

---

## DS-001: Corporation Boundary

**Status:** ACQUIRED (OSM)

Actual schema (from OpenStreetMap relation 1553009):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| id | number | OSM relation ID | YES | 1553009 |
| type | string | OSM element type | YES | "relation" |
| tags.admin_level | string | Administrative level | YES | "8" |
| tags.boundary | string | Boundary type | YES | "administrative" |
| tags.name | string | Boundary name | YES | "Trichy Corporation Limits" |
| tags.type | string | Relation type | YES | "boundary" |
| tags.website | string | Source website | YES | "https://www.trichycorporation.gov.in/" |
| tags.wikidata | string | Wikidata identifier | YES | "Q4045755" |
| members | array | Member ways (30) | YES | Outer boundary ways |

---

## DS-002: Ward Boundaries

**Status:** ACQUIRED (OSM)

Actual schema (from OpenStreetMap admin_level=10 relations):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| id | number | OSM relation ID | YES | Various IDs |
| type | string | OSM element type | YES | "relation" |
| tags.admin_level | string | Administrative level | YES | "10" |
| tags.boundary | string | Boundary type | YES | "administrative" |
| tags.name | string | Ward name | YES | "Ward 1" through "Ward 65" |
| tags.type | string | Relation type | YES | "boundary" |

---

## DS-003: Roads (OSM)

**Status:** ACQUIRED (OSM)

Actual schema (from OpenStreetMap highway ways):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| id | number | OSM way ID | YES | Unique way identifier |
| type | string | OSM element type | YES | "way" |
| tags.highway | string | Road classification | YES | primary, secondary, tertiary, residential, etc. |
| tags.name | string | Road name | NO | May be empty |
| tags.surface | string | Road surface type | NO | asphalt, concrete, etc. |
| tags.lanes | string | Number of lanes | NO | May be empty |
| tags.oneway | string | One-way flag | NO | yes/no |
| tags.width | string | Road width | NO | May be empty |
| geometry | array | Way nodes | YES | Array of {lat, lon} points |

---

## DS-004: Healthcare Facilities (OSM)

**Status:** ACQUIRED (OSM)

Actual schema (from OpenStreetMap healthcare nodes):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| id | number | OSM node ID | YES | Unique node identifier |
| type | string | OSM element type | YES | "node" |
| tags.amenity | string | Amenity type | YES | hospital, clinic, doctors, pharmacy, dentist |
| tags.healthcare | string | Healthcare type | YES | hospital, clinic, pharmacy, dentist, etc. |
| tags.name | string | Facility name | NO | May be empty |
| tags.operator | string | Operator/owner | NO | May be empty |
| tags.addr:street | string | Street address | NO | May be empty |
| tags.addr:city | string | City | NO | May be empty |
| tags.phone | string | Phone number | NO | May be empty |
| lat | number | Latitude | YES | WGS84 |
| lon | number | Longitude | YES | WGS84 |

---

## DS-005: Education Facilities (OSM)

**Status:** ACQUIRED (OSM)

Actual schema (from OpenStreetMap education nodes):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| id | number | OSM node ID | YES | Unique node identifier |
| type | string | OSM element type | YES | "node" |
| tags.amenity | string | Amenity type | YES | school, college, university, kindergarten |
| tags.name | string | Facility name | NO | May be empty |
| tags.operator | string | Operator/owner | NO | May be empty |
| tags.addr:street | string | Street address | NO | May be empty |
| tags.addr:city | string | City | NO | May be empty |
| lat | number | Latitude | YES | WGS84 |
| lon | number | Longitude | YES | WGS84 |

---

## DS-006: Water Features (OSM)

**Status:** ACQUIRED (OSM)

Actual schema (from OpenStreetMap water features):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| id | number | OSM element ID | YES | Unique element identifier |
| type | string | OSM element type | YES | "node" or "way" |
| tags.natural | string | Natural feature type | CONDITIONAL | "water" for water bodies |
| tags.waterway | string | Waterway type | CONDITIONAL | ditch, drain, canal, stream, river |
| tags.man_made | string | Man-made water feature | CONDITIONAL | pond, tank, water_tap, water_well |
| tags.name | string | Feature name | NO | May be empty |
| tags.water | string | Water body type | NO | lake, pond, reservoir, etc. |
| geometry | array/array | Nodes or way nodes | YES | Point or LineString geometry |

---

## DS-007: Civic Facilities (OSM)

**Status:** ACQUIRED (OSM)

Actual schema (from OpenStreetMap civic facility nodes):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| id | number | OSM node ID | YES | Unique node identifier |
| type | string | OSM element type | YES | "node" |
| tags.amenity | string | Amenity type | YES | police, post_office, community_centre, social_facility |
| tags.office | string | Office type | CONDITIONAL | "government" for government offices |
| tags.name | string | Facility name | NO | May be empty |
| tags.addr:street | string | Street address | NO | May be empty |
| tags.addr:city | string | City | NO | May be empty |
| tags.phone | string | Phone number | NO | May be empty |
| lat | number | Latitude | YES | WGS84 |
| lon | number | Longitude | YES | WGS84 |

---

## DS-008: Bhuvan LULC 1:50K

**Status:** NOT YET ACQUIRED

Expected schema (based on Bhuvan LULC documentation):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| TO BE VERIFIED DURING DATA VALIDATION | — | — | — | Expected: LULC class codes, class names, area attributes |

**Known LULC Classes (from Bhuvan documentation — to be verified):**

Bhuvan LULC 50K uses a classification scheme with categories including:
- Built-up land (residential, commercial, industrial, transportation)
- Water bodies (rivers, lakes, ponds, reservoirs)
- Vegetation (forest, scrub, grassland, plantations)
- Fallow land
- Agriculture

Exact class codes and names will be verified from the technical document when dataset is acquired.

---

## Shared Type Definitions (Future Web GIS)

These TypeScript interfaces will be defined in Phase 9. Listed here for reference:

### Ward

```typescript
// TO BE FINALIZED DURING PHASE 4-9
interface Ward {
  ward_id: string;
  ward_name: string;
  ward_number: number;
  geometry: MultiPolygon;
}
```

### Facility (Healthcare/Education/Civic)

```typescript
// TO BE FINALIZED DURING PHASE 4-9
interface Facility {
  facility_id: string;
  name: string;
  type: string;
  category: string;
  operator?: string;
  geometry: Point;
}
```

### Road

```typescript
// TO BE FINALIZED DURING PHASE 4-9
interface Road {
  road_id: string;
  name?: string;
  highway?: string;
  surface?: string;
  geometry: LineString;
}
```

### Water Feature

```typescript
// TO BE FINALIZED DURING PHASE 4-9
interface WaterFeature {
  feature_id: string;
  name?: string;
  type: string;
  water_body?: string;
  geometry: Point | Polygon;
}
```

---

**End of Data Dictionary**
