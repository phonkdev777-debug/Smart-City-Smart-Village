# Architecture Decision Records

## Smart City / Smart Village — Trichirappalli

**Document:** Phase 2 — Architecture Decisions

**Status:** CREATED — Phase 2

**Last updated:** 2026-08-17

---

## ADR-001: Web GIS Instead of Native Desktop Application

**Date:** 2026-08-17

**Status:** Accepted

**Context:**

The project requires an interactive interface for exploring GIS analysis results. A decision must be made between a native desktop application and a browser-based Web GIS.

**Decision:**

Build a browser-based Web GIS application instead of native desktop applications.

**Rationale:**

- Cross-platform access without separate builds for Windows, Linux, macOS
- No installation required for end users
- Static deployment is sufficient (GitHub Pages, Netlify)
- Aligns with zero-cost approach
- Browser-based mapping libraries (Leaflet) are mature and FOSS
- GIS analysis results can be exported from QGIS to GeoJSON for browser consumption
- No requirement exists for native desktop executables

**Consequences:**

- Frontend technology (React + TypeScript) is required
- GeoJSON delivery format is required (browser-compatible)
- No direct access to local filesystem from browser (acceptable — data is pre-processed)
- Large dataset handling must consider browser memory limits

---

## ADR-002: No Backend Initially

**Date:** 2026-08-17

**Status:** Accepted

**Context:**

Web applications often include a backend server for data processing, authentication, and API endpoints. This project must decide whether a backend is needed.

**Decision:**

No backend server in the initial architecture. All GIS data is served as static files.

**Rationale:**

- GIS data is pre-processed in QGIS and exported as GeoJSON files
- No user accounts or authentication required
- No user-generated content or persistent state needed
- No real-time data ingestion required
- No transactional API operations needed
- Static frontend deployment is simpler and cheaper
- Eliminates server maintenance burden
- Aligns with zero-cost FOSS approach

**Conditions for Future Reconsideration:**

A backend may be introduced if:
- Real-time IoT sensor data ingestion is required
- User accounts with saved analyses are needed
- Collaborative annotation/editing is required
- Server-side GIS processing for large datasets is needed
- Authentication/authorization for sensitive data is required

**Consequences:**

- All data must fit in browser memory (~20K features is manageable)
- Data updates require rebuilding and redeploying the frontend
- No server-side data validation (mitigated by QGIS validation)
- Simpler deployment and maintenance

---

## ADR-003: No Database Initially

**Date:** 2026-08-17

**Status:** Accepted

**Context:**

Spatial databases like PostGIS provide powerful query capabilities. This project must decide whether a database is needed.

**Decision:**

No database in the initial architecture. GIS data is served from GeoPackage/GeoJSON files.

**Rationale:**

- Current data volume is moderate (~20K features total) — fits in browser memory
- All queries are read-only — no transactional needs
- Spatial queries are handled by Turf.js client-side
- GeoPackage serves as the working GIS format
- GeoJSON serves as the browser delivery format
- No concurrent write operations needed
- Eliminates database server setup and maintenance

**Conditions for Future Reconsideration:**

PostGIS may be introduced if:
- Dataset sizes grow beyond browser memory capacity
- Complex server-side spatial queries are needed
- Concurrent editing by multiple users is required
- Real-time data updates require server-side processing
- Authentication/authorization is needed

**Consequences:**

- Simpler architecture and deployment
- No SQL query capability (mitigated by Turf.js for client-side queries)
- Data updates require file replacement and frontend rebuild
- All spatial operations must be client-compatible or pre-computed in QGIS

---

## ADR-004: QGIS as Primary GIS Processing Environment

**Date:** 2026-08-17

**Status:** Accepted

**Context:**

GIS data processing, analysis, and cartography require a GIS tool. This project must select a processing environment.

**Decision:**

Use QGIS as the primary GIS processing environment.

**Rationale:**

- Free/Libre/Open Source Software — meets Mapathon requirement
- Industry-standard GIS tool with comprehensive processing capabilities
- Python scripting support for reproducible workflows
- Processing Toolbox for spatial analysis (buffer, intersection, etc.)
- Professional cartography with print layouts
- Supports all required data formats (GeoPackage, GeoJSON, Shapefile)
- Active community and extensive documentation
- Cross-platform (Windows, Linux, macOS)

**Consequences:**

- All GIS processing must be reproducible via QGIS
- Processing steps must be documented (Python scripts or processing history)
- QGIS project file (.qgz) is a key project artifact
- Team members must have QGIS installed for GIS work

---

## ADR-005: React + TypeScript + Leaflet for Web GIS

**Date:** 2026-08-17

**Status:** Accepted

**Context:**

The Web GIS frontend requires a technology stack for map rendering, layer management, and user interaction.

**Decision:**

Use React + TypeScript + Vite + Leaflet + React-Leaflet + Turf.js.

**Rationale:**

- **React:** Component-based UI, large ecosystem, well-maintained
- **TypeScript:** Type safety improves maintainability and catches errors early
- **Vite:** Fast build tool, modern, FOSS
- **Leaflet:** Mature, lightweight, FOSS interactive mapping library
- **React-Leaflet:** Official React integration for Leaflet
- **Turf.js:** Client-side spatial analysis (buffer, distance, area calculations)

**Alternatives Considered:**

| Alternative | Reason for Rejection |
|-------------|---------------------|
| MapLibre GL JS | Heavier, WebGL-based — Leaflet is lighter for this use case |
| OpenLayers | Heavier than Leaflet; Leaflet sufficient for project scope |
| Vue.js | React chosen for broader ecosystem and team familiarity |
| Angular | Heavier than React for this project scope |
| Plain JavaScript | TypeScript provides type safety needed for GIS data contracts |

**Consequences:**

- Frontend bundle will include React, Leaflet, Turf.js
- TypeScript interfaces must be defined for all GIS data structures
- Component architecture must be planned (see system-architecture.md)

---

## ADR-006: GeoPackage as Working Format, GeoJSON for Browser Delivery

**Date:** 2026-08-17

**Status:** Accepted

**Context:**

GIS data must flow from QGIS processing to the Web GIS frontend. A data format strategy is needed.

**Decision:**

- **GeoPackage (.gpkg):** Primary working format for all GIS layers in QGIS
- **GeoJSON (.json):** Delivery format for browser consumption in the Web GIS

**Rationale:**

**GeoPackage as working format:**
- OGC open standard
- Single-file container for multiple layers
- Supports complex attribute schemas and metadata
- No Shapefile limitations (2GB size limit, 10-char field names)
- Native format in QGIS
- Preserves CRS metadata

**GeoJSON for browser delivery:**
- Native JSON — parseable without libraries
- Directly consumable by Leaflet/MapLibre
- Lightweight for web传输
- Well-supported by all web mapping libraries
- Easy to inspect and debug

**Consequences:**

- QGIS exports GeoJSON per-layer (not monolithic)
- GeoJSON files are EPSG:4326 (required for Leaflet)
- GeoPackage files may use other CRS (metadata notes required)
- Shapefile only used where external tool specifically requires it

---

## ADR-007: GNU GPL v3.0 License

**Date:** 2026-08-17

**Status:** Accepted

**Context:**

The project requires a FOSS license compatible with the Mapathon requirements.

**Decision:**

Use GNU General Public License v3.0.

**Rationale:**

- Strong copyleft license — ensures derivative works remain FOSS
- Compatible with all chosen technology licenses (MIT, Apache-2.0, BSD)
- Meets Mapathon FOSS requirement
- Well-understood, widely used

**Consequences:**

- All project code must be released under GPL v3.0
- Derivative works must also be GPL v3.0
- Attribution requirements must be maintained

---

## ADR-008: No Fabricated Data — Strict Data Integrity Policy

**Date:** 2026-08-17

**Status:** Accepted

**Context:**

AI-assisted development can lead to fabricated data, statistics, or analysis results. The project must maintain strict data integrity.

**Decision:**

All data, statistics, and analysis results must originate from verified sources or documented calculations. Fabrication is strictly prohibited.

**Rationale:**

- Mapathon requires real, genuine, verifiable datasets
- Fabricated data undermines project credibility
- GIS analysis must be reproducible
- Professional engineering standards require data integrity
- AI-generated content must be verified against real sources

**What Is Prohibited:**

- Invented facility counts or statistics
- Fabricated population values
- Fake GIS analysis results
- Invented API responses
- Fake accessibility scores
- Invented satellite statistics
- Made-up ward data

**What Is Required:**

- Documented source for every dataset
- Verified feature counts and attributes
- Transparent calculation methodology
- Clear distinction between verified data and estimates

**Consequences:**

- All data must be acquired from real sources
- Processing steps must be documented
- Any uncertainty must be explicitly stated
- Missing data must be reported as missing, not invented

---

## Summary of Decisions

| ADR | Decision | Status | Date |
|-----|----------|--------|------|
| 001 | Web GIS instead of native desktop | Accepted | 2026-08-17 |
| 002 | No backend initially | Accepted | 2026-08-17 |
| 003 | No database initially | Accepted | 2026-08-17 |
| 004 | QGIS as primary GIS tool | Accepted | 2026-08-17 |
| 005 | React + TypeScript + Leaflet | Accepted | 2026-08-17 |
| 006 | GeoPackage working, GeoJSON delivery | Accepted | 2026-08-17 |
| 007 | GNU GPL v3.0 | Accepted | 2026-08-17 |
| 008 | No fabricated data — strict integrity | Accepted | 2026-08-17 |

---

**End of Architecture Decision Records**
