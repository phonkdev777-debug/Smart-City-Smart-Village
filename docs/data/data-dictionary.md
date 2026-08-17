# Data Dictionary

## Smart City / Smart Village — Trichirappalli

**Document:** Phase 3 — GIS Data Acquisition & Provenance

**Status:** IN PROGRESS

**Last updated:** 2026-08-17

---

## Policy

This data dictionary documents verified field schemas only.

- If a field schema is not yet verified: `TO BE VERIFIED DURING DATA VALIDATION`
- Do not invent schemas before actual datasets are available
- Update this document as datasets are acquired and inspected

---

## DS-001: Corporation Boundary

**Status:** NOT YET ACQUIRED

Expected schema (based on SoI Administrative Boundary Database):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| TO BE VERIFIED DURING DATA VALIDATION | — | — | — | — |

---

## DS-002: Ward Boundaries

**Status:** NOT YET ACQUIRED

Expected schema (based on project requirements):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| TO BE VERIFIED DURING DATA VALIDATION | — | — | — | Expected fields: ward_name, ward_id, ward_number |

---

## DS-003: Roads (OSM)

**Status:** NOT YET ACQUIRED

Expected schema (based on OSM data model):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| TO BE VERIFIED DURING DATA VALIDATION | — | — | — | Expected OSM tags: name, highway, surface, oneway, lanes |

---

## DS-004: Healthcare Facilities (OSM)

**Status:** NOT YET ACQUIRED

Expected schema (based on OSM tagging):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| TO BE VERIFIED DURING DATA VALIDATION | — | — | — | Expected OSM tags: name, amenity, healthcare, operator, addr:* |

---

## DS-005: Education Facilities (OSM)

**Status:** NOT YET ACQUIRED

Expected schema (based on OSM tagging):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| TO BE VERIFIED DURING DATA VALIDATION | — | — | — | Expected OSM tags: name, amenity, education, operator, addr:* |

---

## DS-006: Water Features (OSM)

**Status:** NOT YET ACQUIRED

Expected schema (based on OSM tagging):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| TO BE VERIFIED DURING DATA VALIDATION | — | — | — | Expected OSM tags: name, natural, water, waterway, man_made |

---

## DS-007: Civic Facilities (OSM)

**Status:** NOT YET ACQUIRED

Expected schema (based on OSM tagging):

| Field | Type | Meaning | Required | Notes |
|-------|------|---------|----------|-------|
| TO BE VERIFIED DURING DATA VALIDATION | — | — | — | Expected OSM tags: name, amenity, office, government |

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
