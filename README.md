# PRAGYAN-AICTE

AI-powered application validation, document authentication, discrepancy detection, and regulatory compliance decision support for technical institution applications.

> **Important:** This is a prototype and decision-support tool. Automated findings and sample records are illustrative only. They are not official AICTE verification or regulatory decisions. Statutory scrutiny, inspections, and final decisions remain with authorized officials and committees.

## Project information

- **Organization:** All India Council for Technical Education (AICTE)
- **Department:** Regulation Bureau
- **SIH problem statement:** 26261 — AI-Powered Application Validation, Document Authentication and Regulatory Compliance Verification
- **Theme:** Smart Automation

## Features

- Overview dashboard with application, document, deficiency, and audit summaries.
- Application queue with search, status filters, and scrutiny detail views.
- Document upload and preliminary PDF scrutiny, including metadata checks and extracted facts.
- Illustrative issuing-authority verification statuses and regulatory compliance rules.
- Alerts, deficiencies, reviewer actions, and audit-trail views.
- Configurable sample rules and evaluation benchmark endpoints.
- 3D, scroll-driven document verification experience with a 2D fallback.
- Local demo data fallback for frontend browsing when the API is not configured or available.

The application includes sample/demo records. Authority statuses, rules, benchmarks, and findings must not be represented as live official determinations.

## Technology

### Frontend

- React
- Vite
- React Three Fiber and Three.js
- GSAP
- React Router

### Backend

- Python
- FastAPI and Uvicorn
- PyMuPDF and Pillow for PDF/image analysis
- ReportLab for PDF dossier generation

## Repository layout and branches

The repository currently keeps the frontend and backend in separate Git branches:

- `Frontend` branch: frontend application under `Frontend/`.
- `Backend` branch: FastAPI application under `Backend/`.

Each deployment should use its corresponding branch and root directory. In each branch, the root directory for the service is the folder containing its app files.

Frontend branch:

```text
Frontend/
  package.json
  package-lock.json
  index.html
  vite.config.js
  public/
  src/
```

Backend branch:

```text
Backend/
  main.py
  forensic.py
  rules.py
  dossier_generator.py
  uploads/
  requirements.txt
```

Ensure `Backend/requirements.txt` is committed to the `Backend` branch before deploying the API.

## Run locally

### Frontend

Prerequisites: Node.js and npm.

From the repository root:

```bash
cd Frontend
npm install
npm run dev
```

Open the local URL printed by Vite (normally `http://localhost:5173`).

To build and preview the production frontend:

```bash
npm run build
npm run preview
```

### Backend

Prerequisites: Python 3.10 or newer and pip.

From the repository root:

```bash
cd Backend
python -m venv .venv
```

Activate the virtual environment:

```powershell
# Windows PowerShell
.\.venv\Scripts\Activate.ps1
```

```bash
# macOS/Linux
source .venv/bin/activate
```

Install dependencies and start the API:

```bash
pip install -r requirements.txt
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

Useful local URLs:

- Health check: `http://127.0.0.1:8000/api/v1/health`
- Interactive API docs: `http://127.0.0.1:8000/docs`

The frontend uses `http://127.0.0.1:8000` by default during local development.

## Deploy the backend to Render

Create a **Web Service** connected to this GitHub repository and configure:

| Setting | Value |
|---|---|
| Branch | `Backend` |
| Root Directory | `Backend` |
| Runtime | Python |
| Build Command | `pip install -r requirements.txt` |
| Start Command | `uvicorn main:app --host 0.0.0.0 --port $PORT` |

No environment variable is required for the current demo backend. After deployment, verify:

```text
https://YOUR-RENDER-SERVICE.onrender.com/api/v1/health
https://YOUR-RENDER-SERVICE.onrender.com/docs
```

Render free services may sleep when idle, so the first request after inactivity may take longer.

## Deploy the frontend to Vercel

Import the GitHub repository into Vercel and configure:

| Setting | Value |
|---|---|
| Production Branch | `Frontend` |
| Root Directory | `Frontend` |
| Framework Preset | Vite |
| Install Command | `npm install` |
| Build Command | `npm run build` |
| Output Directory | `dist` |

To connect the frontend to the deployed backend, add this Vercel environment variable for **Production** (and Preview if needed):

```text
VITE_API_BASE_URL=https://YOUR-RENDER-SERVICE.onrender.com
```

Use the Render service's base URL only—do not add `/api/v1/health` or a trailing slash. Redeploy the frontend after adding or changing the variable.

The frontend source must read this variable when constructing its API base URL. For example, in `Frontend/src/services/api.js`:

```js
const BACKEND_BASE_URL = (
  import.meta.env.VITE_API_BASE_URL ||
  (import.meta.env.DEV ? 'http://127.0.0.1:8000' : '')
).replace(/\/$/, '');
```

Commit and push this frontend code change to the `Frontend` branch before expecting Vercel to use the environment variable. If no production API URL is configured, the frontend is intended to show demo data where supported; backend-only actions will not be available.

## API overview

The API is prefixed with `/api/v1`. Main endpoint groups include:

- `GET /health`
- `GET /applications` and `GET /applications/{app_id}`
- `GET /rules` and `PUT /rules/{rule_id}`
- `POST /scrutiny/verify-files`
- `POST /scrutiny/record-action`
- `GET /scrutiny/export-dossier/{app_id}`
- `GET /audit-trail`
- `GET /metrics/evaluation-benchmarks`
- Faculty registry, ghost-alert, notification, and demo authentication routes

For the complete current request/response schemas, use the deployed `/docs` page.

## Demo and deployment limitations

- Application records, rule changes, and audit events are held in process memory. They can reset when the service restarts and are not shared across multiple service instances.
- Uploaded files and generated artifacts use local filesystem storage. Local disk may be ephemeral on hosted services; files can be lost on redeploy/restart unless persistent storage is configured.
- Use durable database/object storage and appropriate access controls before using this prototype with real institutional or personal information.
- Configure backend CORS to allow only the deployed frontend origin for production. Do not treat broad development CORS settings as a production security policy.
- Protect upload and reviewer endpoints with authentication and authorization before exposing the service for real use.
- Do not upload sensitive, confidential, or personal documents to this demonstration deployment.

## Tests

The backend includes a basic API verification script. From the `Backend` directory, install the runtime dependencies plus the test client if needed, then run:

```bash
python test_backend.py
```

## License

No license is specified in this repository. Unless a license is added, reuse and redistribution are not granted by this README.
