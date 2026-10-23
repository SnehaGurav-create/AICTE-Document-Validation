<div align="center">

# 🖥️ PRAGYAN-AICTE · Frontend

### The React experience behind AI-powered application validation for technical institutions

*Dashboards, scrutiny workflows and an immersive 3D document-verification journey.*

<br/>

![React](https://img.shields.io/badge/React-19-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![Three.js](https://img.shields.io/badge/Three.js-000000?style=for-the-badge&logo=three.js&logoColor=white)
![GSAP](https://img.shields.io/badge/GSAP-88CE02?style=for-the-badge&logo=greensock&logoColor=black)
![React Router](https://img.shields.io/badge/React_Router-CA4245?style=for-the-badge&logo=reactrouter&logoColor=white)
![Vercel](https://img.shields.io/badge/Deploy-Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)

</div>

---

> [!IMPORTANT]
> **Prototype notice.** This project uses demonstration data. Automated findings are preliminary indicators, not official verification or regulatory decisions. Authorized officials remain responsible for scrutiny and final decisions.

## 📑 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Run Locally](#-run-locally)
- [Connect to the Backend](#-connect-to-the-backend)
- [Deploy to Vercel](#-deploy-to-vercel)
- [Important Limitations](#-important-limitations)

---

## 🎯 Overview

This is the **frontend** of **PRAGYAN-AICTE**, a prototype decision-support platform for the preliminary review of technical institution applications and their supporting documents. It talks to a separate FastAPI backend and gracefully falls back to demo data when that backend isn't available.

## ✨ Features

| | Feature | Description |
|---|---|---|
| 📊 | **Overview & Queue** | Application overview and review queue |
| 📄 | **Document Validation** | Document-validation and preliminary scrutiny workflows |
| ⚖️ | **Compliance Views** | Compliance, deficiencies, reviewer actions and audit-trail screens |
| 🧊 | **3D Experience** | Scroll-driven 3D document experience with a **2D fallback** |
| 🔌 | **Demo Fallback** | Demo data for supported views when the backend is unavailable |

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **React 19** | UI library |
| **Vite** | Dev server and build tool |
| **React Three Fiber + Three.js** | 3D rendering |
| **GSAP** | Scroll-driven animation |
| **React Router** | Client-side routing |

## 📂 Project Structure

```text
Frontend/
├── package.json
├── package-lock.json
├── index.html
├── vite.config.js
├── public/
└── src/
    ├── components/
    ├── context/
    ├── data/
    └── services/
```

## 🚀 Run Locally

**Prerequisites:** Node.js and npm.

From this directory (the one containing `package.json`):

```bash
npm install
npm run dev
```

Open the local URL printed by Vite, usually <http://localhost:5173>.

<details>
<summary><b>Build, preview and lint</b></summary>

<br/>

Build and preview the production version:

```bash
npm run build
npm run preview
```

Run lint checks:

```bash
npm run lint
```

</details>

## 🔗 Connect to the Backend

For local development, the frontend API service defaults to `http://127.0.0.1:8000`.

For a deployed backend, set this environment variable in your hosting provider:

```text
VITE_API_BASE_URL=https://YOUR-RENDER-SERVICE.onrender.com
```

> [!TIP]
> Use only the backend base URL. Do **not** include `/api/v1/health` or a trailing slash. Vite embeds `VITE_` variables at build time, so **redeploy the frontend after changing the value**.

> [!WARNING]
> The frontend API code must read `import.meta.env.VITE_API_BASE_URL`. If the deployed branch still hard-codes `http://127.0.0.1:8000`, update and push that code first. Otherwise the deployed frontend will ignore the variable.

## ☁️ Deploy to Vercel

Import this repository into Vercel and configure:

| Setting | Value |
|---|---|
| Production Branch | `Frontend` |
| Root Directory | `Frontend` |
| Framework Preset | Vite |
| Install Command | `npm install` |
| Build Command | `npm run build` |
| Output Directory | `dist` |

When connecting to the deployed backend, add `VITE_API_BASE_URL` under Vercel's **Environment Variables**, then redeploy.

## ⚠️ Important Limitations

- Some screens and verification information are illustrative demo content.
- Backend-dependent functions require a separately deployed and reachable API.
- Do not submit real, confidential or personal documents to an unreviewed demo deployment.
- See the backend README for API deployment, storage limitations and security notes.

---

<div align="center">

**PRAGYAN-AICTE · Smart India Hackathon · Problem Statement 26261**

*Decision support for officials, not a replacement for them.*

</div>
