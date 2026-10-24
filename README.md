# ORBIT — Operational Risk & Business Intelligence Terminal
### Global Historical Geospatial Intelligence, Multimodal Logistics & Situational Awareness Platform

ORBIT is an enterprise-grade situational awareness terminal engineered for operational risk analysts, logistics coordinators, supply chain managers, and intelligence researchers. It ingests, normalizes, deduplicates, and corroborates multi-source geospatial telemetry across global seismic hazards, natural disasters, armed violence, political instability, multimodal transport corridors (road, rail, maritime, air), structured OSINT evidence research, and ML-powered event intelligence classification.

ORBIT features a **Global Historical Geospatial Data Engine spanning October 2016 through October 2026** with over **3,980+ verified records**—providing continuous multi-year coverage with zero synthetic or fabricated placeholders.

---

## Visual Design & Architecture System

- **Visual Palette**: Strict dark operations aesthetic
  - Main Background: `#0B0F14`
  - Sidebar: `#101720`
  - Panels: `#151D27`
  - Borders: `#283341`
  - Text Primary: `#E8EDF4` | Text Secondary: `#95A3B5`
  - Accent (Cyan): `#55B8A9` | Warning (Amber): `#E8B45A` | Critical (Coral Red): `#E16B72`
- **Typography**: Inter with monospace accentuation (`JetBrains Mono` / `SFMono` / `monospace`)
- **Cartography**: MapLibre GL JS with 5 Basemap Styles and Carto Dark Matter WGS84 raster/vector projection (`EPSG:4326`)
- **Backend Architecture**: Python 3.15 FastAPI with Pydantic v2 schemas, scikit-learn ML pipeline, modular routing providers, and SQLite WAL persistence (with PostGIS migration schema)
- **Frontend Architecture**: Next.js 14 App Router, TypeScript (strict), Tailwind CSS, Lucide Icons

---

## Platform Modules & Implemented Features

### 1. Global Historical Geospatial Data Engine (2016–2026)
- **Multi-Year Archive**: Continuous 10-year coverage from October 2016 to October 2026 populated with authentic records from USGS Earthquake Hazards ($M \ge 5.8$) and NASA EONET v3.
- **Dynamic Viewport Streaming**: MapLibre `moveend` triggers query the visible bounding box with progressive detail scaling based on zoom level.
- **Point Intelligence Interrogation Drawer**: Clicking any landmass or ocean computes Haversine distance to surrounding events ($\le 25\text{km}$ immediate, $25\text{--}100\text{km}$ nearby, $100\text{--}500\text{km}$ regional) and displays ECMWF ERA5 climate reanalysis baselines.
- **Data Coverage & Audit Dashboard**: Factual record volumes by year, provider, and category with explicit disclosure of sparse corridors (Sahara, Southern Oceans, Congo Basin).

### 2. Interactive Map & Satellite Cartography
- **5 Basemaps**: Political Map, Esri Satellite Imagery, Hybrid Satellite, Terrain, and Dark Matter Streets.
- **NASA GIBS Daily TrueColor Satellite**: Direct WMTS integration with MODIS Terra true-color reflectance layers at 250m resolution.
- **10-Year Timeline Scrubber**: Interactive year scrubber (2016–2026) with event density sparklines, automated playback animation, and quick latest reset.

### 3. Historical Date Comparison & Dossier Synthesis
- **Date A vs Date B Comparison**: Computes metric deltas ($\Delta \text{Temp}$, $\Delta \text{Precip}$, $\Delta \text{Soil}$, $\Delta \text{Incidents}$) and links NASA GIBS daily satellite tiles for visual before/after analysis.
- **Location Intelligence Dossier**: Generates standardized 8-section evidence dossiers with print and PDF export formatting.

### 4. Civilian Flight Tracking & Aviation Telemetry (`/flights`)
- Real-time OpenSky Network transponder feed integration.
- Aircraft headings, barometric and geometric altitudes, ground speeds, squawk codes, airborne/ground status, and operator metadata.

### 5. Maritime AIS Tracking & Vessel Corridors (`/maritime`)
- Global AIS commercial vessel telemetry tracking container ships, crude oil tankers, bulk carriers, and tugs.
- Proximity correlation with strategic maritime chokepoints (Suez, Bab el-Mandeb, Hormuz, Malacca, Panama, Bosphorus).
- Strict separation between broadcast AIS cargo classification and verified customs manifests.

### 6. Defense Fleet Intelligence Register (`/fleet`)
- Non-tactical public defense register documenting military aircraft classes, naval combatants, carrier strike groups, and air wings.
- Source citations, commissioning history, and officially disclosed home ports. Real-time tactical tracking of combat positions is strictly prohibited.

### 7. Multimodal Logistics Intelligence (`/logistics`)
- Unified logistics monitoring across Road, Rail, Maritime, and Air transport modes.
- Open Source Routing Machine (OSRM) driving route calculations with corridor risk buffer clipping.
- Explainable Route Risk Index (RRI $\in [0, 100]$): Zero incidents returns `UNDETERMINED` (never "Safe").
- Pareto frontier trade-offs balancing Distance, Time, Corroborated Risk, and Reliability.

### 8. Surplus Inventory Marketplace (`/marketplace`)
- Verified marketplace for surplus, damaged, returned, and rejected delivery inventories.
- 5-tier condition grading (`GRADE_A` through `GRADE_SALVAGE`) with inspection notes.
- Atomic inventory reservation to prevent overselling.
- Grounded AI assistant answering inventory queries with mandatory system citation IDs.

### 9. ML Intelligence Event Classifier (`/reports`, `/api/ml`)
- **Engine**: Scikit-Learn TF-IDF feature extraction coupled with Multinomial Logistic Regression ($C=5.0$, L2 penalty).
- **Taxonomy**: 6 operational categories (`CONFLICT_AND_SECURITY`, `CIVIL_UNREST_AND_POLITICAL`, `NATURAL_HAZARD`, `WEATHER_AND_ENVIRONMENT`, `INFRASTRUCTURE_AND_TRANSPORT`, `OTHER_OR_UNCERTAIN`).
- **Baseline Concordance**: Evaluated side-by-side with a deterministic `KeywordRuleClassifier` to measure lift (+30.68% accuracy lift).
- **Uncertainty Quantification**: Calibrated probability posteriors with 3-tier states (`CONFIDENT`, `REVIEW_REQUIRED`, `ABSTAIN`).

### 10. Evidence Intelligence & OSINT Workspace (`/evidence`)
- SSRF-hardened source ingestion with loopback, link-local, and cloud metadata blocking (`169.254.169.254`).
- Multi-source claims analysis (`FACTUAL`, `TEMPORAL`, `CAUSAL`, `ATTRIBUTION`, `POLICY`, `GEOGRAPHIC`).
- Entity-relationship intelligence network with explicit `[ALLEGED]` and `[INFERRED]` markers.

### 11. Security, RBAC & Cryptographic Audit Ledger
- Argon2id and PBKDF2-SHA256 password hashing with constant-time verification.
- Enforced session tokens with secure cookie attributes (`HttpOnly`, `SameSite=Lax`, `Secure`).
- Sub-resource IDOR protection on all evidence cases, claims, and entity relationships.
- Append-only, SHA-256 hash-chained cryptographic audit ledger (`orbit_audit_log`).

---

## Technology Stack

| Layer | Technologies Used |
| :--- | :--- |
| **Frontend Framework** | Next.js 14 (App Router), React 18, TypeScript (Strict Mode) |
| **Styling & UI** | Tailwind CSS, Lucide Icons, Canvas API |
| **Cartography & GIS** | MapLibre GL JS, Carto Basemaps, Esri World Imagery, NASA GIBS WMTS |
| **Backend API** | Python 3.15, FastAPI, Starlette, Pydantic v2, Uvicorn |
| **Machine Learning** | Scikit-Learn (TF-IDF, Logistic Regression), NumPy, Joblib |
| **Database & Storage** | SQLite 3 (WAL mode, composite spatial-temporal indexes), PostGIS schema |
| **Data Ingestion** | HTTPX (Async), USGS FDSNWS, NASA EONET v3, Open-Meteo ERA5, GDELT 2.0 |
| **Testing & Quality** | Pytest, Pytest-Asyncio, Node.js Native Test Runner (`node:test`), ESLint |

---

## Project Structure

```
orbit/
├── backend/
│   ├── app/
│   │   ├── api/
│   │   │   ├── endpoints/
│   │   │   │   ├── events.py        # /api/events (filtering, search, bbox, pagination)
│   │   │   │   ├── geospatial.py    # /api/geospatial (viewport, location intel, coverage, dossier)
│   │   │   │   ├── stats.py         # /api/stats (metrics, category counts, regional distribution)
│   │   │   │   ├── sync.py          # /api/sync (trigger sync, data freshness status)
│   │   │   │   ├── health.py        # /api/health (service & database health probe)
│   │   │   │   ├── logistics.py     # /api/logistics (multimodal routing & RRI)
│   │   │   │   ├── marketplace.py   # /api/marketplace (listings, orders, assistant)
│   │   │   │   ├── conflict.py      # /api/conflict (conflict events & statistics)
│   │   │   │   ├── flights.py       # /api/flights (ADS-B telemetry)
│   │   │   │   ├── maritime.py      # /api/maritime (AIS vessel tracking)
│   │   │   │   ├── fleet.py         # /api/fleet (defense registry)
│   │   │   │   ├── evidence.py      # /api/evidence (cases, claims, entities, dossiers)
│   │   │   │   ├── auth.py          # /api/auth (login, logout, session, audit ledger)
│   │   │   │   └── ml.py            # /api/ml (status, classify, correct, evaluation)
│   │   │   └── router.py            # Master API router
│   │   ├── db/                      # Repository interfaces & SQLite persistent engine
│   │   ├── ml/                      # Pre-trained classifier artifacts & training datasets
│   │   ├── models/                  # Pydantic data models & schemas
│   │   ├── services/
│   │   │   ├── historical/          # Historical data pipeline, anomaly detector, service
│   │   │   ├── ml/                  # ML training, preprocessing, baseline, inference
│   │   │   ├── routing/             # OSRM highway engine & risk scoring
│   │   │   ├── sources/             # USGS, NASA EONET, EMSC, GDELT ingestors
│   │   │   ├── ingestor.py          # Multi-source concurrent ingestion orchestrator
│   │   │   └── deduplicator.py      # Spatial/temporal deduplication engine
│   │   ├── config.py                # Environment configuration settings
│   │   └── main.py                  # FastAPI application entrypoint
│   ├── tests/                       # 107 passing backend unit & integration tests
│   ├── requirements.txt             # Backend dependencies
│   ├── run.py                       # Backend startup script
│   └── schema_postgis.sql           # Enterprise PostGIS migration schema
├── frontend/
│   ├── src/
│   │   ├── app/                     # Next.js App Router pages (14 routes)
│   │   ├── components/
│   │   │   ├── drawer/              # Location intelligence & event detail drawers
│   │   │   ├── geospatial/          # Comparison, dossier, and coverage audit modals
│   │   │   ├── map/                 # MapContainer (MapLibre GL) & HistoricalTimelineSlider
│   │   │   ├── logistics/           # Multimodal corridor planner & risk gauges
│   │   │   └── marketplace/         # Surplus inventory catalog, grading, assistant
│   │   ├── lib/api.ts               # Typed client API SDK
│   │   └── types/                   # TypeScript interfaces
│   ├── tests/                       # 57 passing frontend unit tests
│   └── package.json                 # Frontend dependencies & scripts
├── docs/                            # Architecture specifications & operational reports
├── docker-compose.yml               # Container deployment specification
├── .env.example                     # Environment template (secrets omitted)
├── .gitignore                       # Root ignore rules (no secrets/databases/builds)
└── README.md                        # Documentation
```

---

## Installation & Local Setup

### Prerequisites
- **Python:** 3.11+ (Python 3.15 tested)
- **Node.js:** 18+ (Node.js 22 tested) & npm
- **Git**

### 1. Clone the Repository
```bash
git clone https://github.com/<your-username>/ORBIT.git
cd ORBIT
```

### 2. Backend Setup
```bash
cd backend

# Create and activate virtual environment
python -m venv venv
# On Windows:
.\venv\Scripts\activate
# On Linux/macOS:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Run the backend server
python run.py
```
*Backend runs on:* `http://127.0.0.1:8000`  
*Swagger Documentation:* `http://127.0.0.1:8000/docs`

### 3. Frontend Setup
In a new terminal:
```bash
cd frontend

# Install dependencies
npm install

# Start the development server
npm run dev
# OR build and start production server:
npm run build
npm run start
```
*Frontend runs on:* `http://localhost:3000`

---

## Environment Variables

Copy `.env.example` to create your local environment:
```bash
cp .env.example .env
```

| Variable | Default | Purpose |
| :--- | :--- | :--- |
| `ORBIT_ENVIRONMENT` | `development` | Deployment environment (`development` / `production`) |
| `ORBIT_AUTH_ENFORCE` | `False` | Enforce session authentication on protected endpoints |
| `SQLITE_DB_PATH` | `./orbit.db` | Persistent SQLite database path |
| `DATABASE_URL` | `sqlite:///./orbit.db` | Database connection string (SQLite or PostgreSQL) |
| `ORBIT_ROUTING_OSRM_URL` | `https://router.project-osrm.org` | OSRM routing engine service |
| `NEXT_PUBLIC_API_URL` | `http://127.0.0.1:8000/api` | Frontend API base URL |
| `ENABLE_USGS` | `True` | Enable USGS Earthquake Hazards ingestion |
| `ENABLE_NASA_EONET` | `True` | Enable NASA EONET natural hazards ingestion |
| `ENABLE_GDELT` | `True` | Enable GDELT conflict monitoring feed |

---

## Verification & Testing

### Backend Unit Tests (107 Tests)
```powershell
cd backend
$env:PYTHONPATH = "."
pytest tests -v
```

### Frontend Unit Tests (57 Tests across 19 Suites)
```powershell
cd frontend
node --test tests/*.test.js
```

### Production Build & Type Checking
```powershell
cd frontend
npm run build
```

---

## License & Data Attribution
- **Codebase License**: MIT License
- **Seismic Telemetry**: USGS Earthquake Hazards Program (ComCat) & EMSC
- **Natural Hazards**: NASA Earth Observatory Natural Event Tracker (EONET v3)
- **Atmospheric Physics**: Open-Meteo ERA5 Reanalysis (ECMWF)
- **Satellite TrueColor**: NASA GIBS / EOSDIS (MODIS Terra)
- **Cartography**: OpenStreetMap contributors, CARTO Positron & Dark Matter
