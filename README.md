# Sentri Backend

Backend services for Sentri’s recovery-support platform and PRC collaboration track.

## Project Status

Sentri backend APIs are implemented and actively used for authentication, data operations, and service integration. A **deployed backend UI is not yet implemented**. We currently rely on API-first workflows and limited admin/developer-facing pages.

We do, however, have a concrete roadmap for the production backend UI and database operations surface (see [Backend UI Roadmap](#backend-ui--database-roadmap)).

## What This Repository Contains

- Flask application entry points and server runtime (`main.py`, `app.py`, `host.py`)
- REST APIs under `api/` (auth, users, posts, microblog, feedback, AI endpoints, data tooling)
- SQLAlchemy-style data models under `model/`
- Database initialization and migration scripts under `scripts/`
- Templates/static assets for existing minimal UI and operational pages
- Docker and deployment support (`Dockerfile`, `docker-compose.yml`, nginx config files)

## Core Architecture

- **Backend framework:** Python + Flask
- **Data layer:** SQLite for local/dev and production-oriented migration scripts for external DB targets
- **Auth:** JWT/cookie-backed auth flows and role-aware endpoints
- **Integration points:** AI service APIs, social/microblog APIs, data export/import endpoints

## Quick Start

### 1) Clone and enter the repo

```bash
git clone <your-fork-or-origin-url>
cd Sentri_backend
```

### 2) Create environment and install dependencies

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 3) Configure environment variables

Create a `.env` file in the repository root with required values (examples include admin/test users, API keys, and DB configuration).

### 4) Initialize database

```bash
./scripts/db_init.py
```

### 5) Run backend

```bash
python main.py
```

## Existing API Capability (High Level)

- User authentication and identity endpoints
- User CRUD and account lifecycle operations
- Social posts and microblog endpoints
- Reply/reaction interactions for community content
- AI endpoints (Gemini/Groq integration wrappers)
- Data export/import and operational utility endpoints

## Backend UI & Database Roadmap

The deployed backend UI is intentionally deferred while core API and privacy architecture are stabilized. Based on the **Technical Handoff & Development Roadmap**, the backend UI for data and moderation will be implemented in phases:

### Phase 1: Privacy-Centric Data Management UI

- Build a staff-facing data console backed by persistent storage (Node.js/PostgreSQL-aligned integration path in broader system architecture)
- Decouple identity from activity logs using UUID mapping patterns
- Provide explicit CRUD controls for sobriety-garden and journal datasets
- Add an auditable **Account Purge** operation to permanently remove a user’s stored entries

### Phase 2: Admin Moderation Dashboard (RBAC)

- Introduce role-based admin views for PRC staff
- Moderation queue for flagged community interactions
- Real-time update tools for community bulletin content
- Soft/hard delete controls for unsafe or inappropriate posts/interactions

### Phase 3: Public-to-Authenticated Access Bridge

- Add “before-login” backend support for anonymous feature access (e.g., program-finder usage prior to account creation)
- Ensure routing and API partitioning between anonymous and authenticated contexts
- Preserve trust-first data collection: only require account linkage when necessary

### Phase 4: UX-Supportive Backend Surfaces

- Ship API-backed UI contracts optimized for mobile-first clients (320px–480px)
- Support calmer crisis-oriented UX direction (serene/neutral palette goals on frontend)
- Harden observability and operational metrics for staff workflows

## Planned Partnership Execution Notes

As Sentri moves from prototype to service-learning deployment with Poway Recovery Center:

- Requirements-gathering sessions will drive schema alignment with center operations
- SQL schema evolution will be tied to concrete staff workflows (moderation, journals, bulletin, accountability logs)
- Backend UI rollout will follow governance and privacy validation milestones

## Repository Layout (Selected)

```text
api/                  # API endpoints
model/                # Data models
machinelearning/      # ML-related services/scripts
scripts/              # DB and ops scripts
templates/            # Existing minimal Flask/Jinja UI
static/               # Frontend assets for existing pages
instance/             # Runtime data (db/uploads/backups)
socket/               # Socket server and related deploy files
```

## Deployment Notes

- Includes Docker and docker-compose assets for containerized deployment
- Includes nginx config artifacts for reverse-proxy setups
- Intended to run in local, cloud VM, or container orchestration contexts

## Contributing

1. Create a feature branch
2. Implement and test changes
3. Open a PR with:
   - Summary of backend/API changes
   - Migration notes (if DB affected)
   - Security/privacy impact notes

## License

Copyright (c) Microsoft Corporation. All rights reserved.
Licensed under the MIT License. See https://go.microsoft.com/fwlink/?linkid=2090316 for license information.
