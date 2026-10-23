<div align="center">

# ⚙️ PRAGYAN-AICTE · Backend

### FastAPI service for document scrutiny, rule checks and dossier generation

*Powering preliminary PDF analysis, reviewer actions and audit trails for technical institution applications.*



<p align="center">
  <a href="https://aictepragyan.vercel.app" target="_blank">
    <img
      src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=21&pause=1000&color=36BCF7&center=true&vCenter=true&width=650&lines=Click+Me;AICTE+Pragyan+Platform"
      alt="Visit Pragyan - AICTE Pragyan Platform"
    />
  </a>
</p>

<br/>

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Uvicorn](https://img.shields.io/badge/Uvicorn-499848?style=for-the-badge&logo=gunicorn&logoColor=white)
![PyMuPDF](https://img.shields.io/badge/PyMuPDF-PDF%20Analysis-red?style=for-the-badge)
![Render](https://img.shields.io/badge/Deploy-Render-46E3B7?style=for-the-badge&logo=render&logoColor=black)

</div>

---

> [!IMPORTANT]
> **Prototype notice.** This service is a demonstration and decision-support prototype. Automated findings and sample records are **not** official AICTE verification or regulatory decisions. Authorized officials remain responsible for scrutiny and final decisions.

## 📑 Table of Contents

- [Overview](#-overview)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Run Locally](#-run-locally)
- [Deploy to Render](#-deploy-to-render)
- [Connect the Frontend](#-connect-the-frontend)
- [API Overview](#-api-overview)
- [Tests](#-tests)
- [Deployment & Security Limitations](#-deployment--security-limitations)

---

## 🎯 Overview

The backend of **PRAGYAN-AICTE** provides:

- 📋 Demo application and regulatory-rule APIs
- 📄 Document-upload scrutiny with preliminary PDF analysis
- 👩‍⚖️ Reviewer actions and audit-trail responses
- 🧾 PDF dossier generation

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **Python 3.10+** | Runtime |
| **FastAPI** | API framework |
| **Uvicorn** | ASGI server |
| **PyMuPDF + Pillow** | PDF and image analysis |
| **ReportLab** | PDF dossier generation |

## 📂 Project Structure

```text
Backend/
├── main.py                # FastAPI app and routes
├── forensic.py            # Preliminary PDF analysis
├── rules.py               # Regulatory rules
├── mock_data.py           # Demo records
├── dossier_generator.py   # PDF dossier generation
├── requirements.txt
├── test_backend.py
└── uploads/
```

## 🚀 Run Locally

**Prerequisites:** Python 3.10 or newer and pip.

From this directory (the one containing `main.py`):

```bash
python -m venv .venv
```

Activate the virtual environment:

```powershell
# Windows PowerShell
.\.venv\Scripts\Activate.ps1
```

```bash
# macOS / Linux
source .venv/bin/activate
```

Install dependencies and start the API:

```bash
pip install -r requirements.txt
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

| Local URL | Purpose |
|---|---|
| <http://127.0.0.1:8000/api/v1/health> | Health check |
| <http://127.0.0.1:8000/docs> | Interactive API documentation |

## ☁️ Deploy to Render

Create a **Web Service** connected to the GitHub repository and set:

| Setting | Value |
|---|---|
| Branch | `Backend` |
| Root Directory | `Backend` |
| Runtime | Python |
| Build Command | `pip install -r requirements.txt` |
| Start Command | `uvicorn main:app --host 0.0.0.0 --port $PORT` |

No environment variables are required by the current demo backend. After deployment, test:

```text
https://YOUR-RENDER-SERVICE.onrender.com/api/v1/health
https://YOUR-RENDER-SERVICE.onrender.com/docs
```

> [!NOTE]
> Make sure `Backend/requirements.txt` is committed to the `Backend` branch before deploying.

> [!TIP]
> Render's free service may spin down during inactivity, so the first request after a quiet period can be delayed.

## 🔗 Connect the Frontend

In your frontend host (for example, Vercel), set:

```text
VITE_API_BASE_URL=https://YOUR-RENDER-SERVICE.onrender.com
```

Use the Render **base URL only**. The frontend must read this variable at build time and be redeployed after it is set. For production, configure CORS to allow only the frontend's origin.

## 🔌 API Overview

All routes use the `/api/v1` prefix.

| Method | Endpoint | Purpose |
|---|---|---|
| `GET` | `/api/v1/health` | Health check |
| `GET` | `/api/v1/applications` | List applications |
| `GET` | `/api/v1/applications/{app_id}` | Application details |
| `GET` | `/api/v1/rules` | List rules |
| `PUT` | `/api/v1/rules/{rule_id}` | Update a rule |
| `POST` | `/api/v1/scrutiny/verify-files` | Upload and scrutinize files |
| `POST` | `/api/v1/scrutiny/record-action` | Record a reviewer action |
| `GET` | `/api/v1/scrutiny/export-dossier/{app_id}` | Export PDF dossier |
| `GET` | `/api/v1/audit-trail` | View audit trail |
| `GET` | `/api/v1/metrics/evaluation-benchmarks` | Evaluation benchmarks |

Use `/docs` for the complete interactive reference and request/response schemas.

## 🧪 Tests

From this directory, install the runtime dependencies and any test dependencies required by `test_backend.py`, then run:

```bash
python test_backend.py
```

## ⚠️ Deployment & Security Limitations

- **In-memory state:** application records, rule updates and audit data live in process memory. They can reset on restart and are not shared between multiple service instances.
- **Ephemeral storage:** uploaded PDFs and generated files are stored on local disk, which may be ephemeral on hosted services. Use persistent/object storage if files must survive restarts or redeploys.
- **CORS and auth:** configure production CORS narrowly, and add authentication and authorization before exposing reviewer or upload endpoints to real users.
- **Data privacy:** do not use this demo service to process confidential, sensitive or personal documents.
- **Not official:** automated analyses and sample records are illustrative and must not be treated as official decisions.

---

<div align="center">

**PRAGYAN-AICTE · Smart India Hackathon · Problem Statement 26261**

*Decision support for officials, not a replacement for them.*

</div>
