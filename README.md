# ConstructIQ AI

> **Next-Generation Multimodal Construction Intelligence & Structural Engineering Platform**

ConstructIQ AI is a full-stack, enterprise-grade civil engineering intelligence system designed to streamline construction workflows. It integrates computer vision and multimodal large language models to automate hazard inspections, structural crack diagnostics, project scheduling, property valuation, climate advisories, and daily field reporting.

---

## Key Capabilities

| Module | AI Modality | Description |
|---|---|---|
| **Site Safety & PPE** | Multimodal Vision | Analyzes site photos for OSHA hazard compliance, scaffolding security, and PPE enforcement. |
| **Crack Diagnostics** | Structural Vision | Detects and categorizes surface vs. structural cracks, assessing risk severity and remediation procedures. |
| **Project Planner** | Reasoning LLM | Generates detailed phase timelines, critical path dependencies, material schedules, and cost estimates. |
| **Property Valuation** | Predictive AI | Calculates real estate valuations, price-per-sqft estimates, and comparable market analysis trends. |
| **Weather Risk Advisory** | Environmental AI | Assesses environmental forecasts to provide work-safety windows and activity-specific mitigation advisories. |
| **Daily Site Reporting** | Multimodal LLM | Converts raw site notes and optional inspection photos into standardized daily progress reports. |
| **Engineering Assistant** | Knowledge Assistant | Interactive AI consultation on structural codes, building standards, materials, and troubleshooting. |

---

## Architecture & Dual-Provider Support

ConstructIQ AI supports two operational runtime modes configured seamlessly via environment variables:

1. **Local Edge Inference (Offline / Private)**:
   - Uses [Ollama](https://ollama.com) running locally.
   - **Text & Reasoning**: `llama3.2` (3.2B parameters)
   - **Vision & Diagnostics**: `llava:7b` (7B parameters)
   - Zero external API costs, 100% data privacy on-premise.

2. **Cloud Production Deployment**:
   - Uses Google Gemini API (`gemini-3.5-flash-lite` / `gemini-2.0-flash-lite`)
   - Scalable, low-latency, and serverless-friendly for platforms like Render and Vercel.

---

## Repository Structure

```
constructiq-ai/
├── backend/
│   ├── main.py              # FastAPI application & unified AI routing engine
│   ├── requirements.txt     # Backend Python dependencies
│   ├── render.yaml          # Render web service deployment configuration
│   └── .env                 # Backend runtime environment configuration
└── frontend/
    ├── src/
    │   ├── App.jsx           # Master navigation & workspace dashboard
    │   ├── App.css           # Workspace & component styling
    │   ├── index.css         # Global design tokens & styling
    │   ├── main.jsx          # React 19 entry point
    │   ├── features/         # Feature modules
    │   │   ├── SafetyMonitoring.jsx
    │   │   ├── CrackDetection.jsx
    │   │   ├── ProjectPlanner.jsx
    │   │   ├── PropertyValuation.jsx
    │   │   ├── WeatherAdvisory.jsx
    │   │   ├── DailySiteReport.jsx
    │   │   └── AIAssistant.jsx
    │   ├── components/       # Shared UI components
    │   │   ├── ImageUploader.jsx
    │   │   ├── ResultCard.jsx
    │   │   └── Spinner.jsx
    │   └── services/
    │       └── api.js        # Typed HTTP client service
    ├── vercel.json          # Vercel SPA routing configuration
    ├── vite.config.js       # Vite build & proxy settings
    └── package.json         # Frontend dependencies & scripts
```

---

## Local Setup & Development

### 1. Prerequisites
- **Python**: 3.11 or higher
- **Node.js**: 18+ and **npm**: 9+
- *(Optional for local AI)*: [Ollama](https://ollama.com)

### 2. Clone Repository
```bash
git clone https://github.com/shivamojha23/constructiq-ai.git
cd constructiq-ai
```

### 3. Backend Setup
```bash
cd backend
python -m venv .venv

# Activate virtual environment
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

Create `backend/.env`:
```env
APP_HOST=0.0.0.0
APP_PORT=8000
ALLOWED_ORIGINS=http://localhost:5173,http://127.0.0.1:5173

# Choose AI Provider:
# Option A: Local Ollama
USE_OLLAMA=true
OLLAMA_BASE_URL=http://localhost:11434

# Option B: Cloud Gemini
# USE_OLLAMA=false
# GEMINI_API_KEY=your_gemini_api_key_here
```

Start backend:
```bash
uvicorn main:app --reload --host 127.0.0.1 --port 8000
```

### 4. Frontend Setup
```bash
cd frontend
npm install
npm run dev
```

Visit `http://localhost:5173` to access the ConstructIQ AI workspace.

---

## Production Deployment Guide

### Deploying Frontend to Vercel (Free & Instant)
1. Push your repository to your GitHub account (`https://github.com/shivamojha23/constructiq-ai`).
2. Log into [vercel.com](https://vercel.com) using your GitHub account.
3. Click **Add New** > **Project** and select your `constructiq-ai` repository.
4. Set **Root Directory** to `frontend`.
5. Under Environment Variables, set:
   - `VITE_API_URL` = Your backend URL (e.g., `https://your-backend.onrender.com`)
6. Click **Deploy**. Vercel will generate your personal live link (e.g. `https://constructiq-ai.vercel.app`).

### Deploying Backend to Render (Free)
1. Log into [render.com](https://render.com).
2. Click **New** > **Web Service** and link your `constructiq-ai` repository.
3. Set **Root Directory** to `backend`.
4. Build Command: `pip install -r requirements.txt`
5. Start Command: `uvicorn main:app --host 0.0.0.0 --port $PORT`
6. Add Environment Variables:
   - `USE_OLLAMA`: `false`
   - `GEMINI_API_KEY`: `<Your Gemini API Key>`
   - `ALLOWED_ORIGINS`: `<Your Vercel Frontend URL>`

---

## Author & License

Developed and maintained by **Shivam Ojha** ([@shivamojha23](https://github.com/shivamojha23)).
Licensed under the MIT License.
