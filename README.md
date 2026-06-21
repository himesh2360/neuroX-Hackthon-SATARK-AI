<p align="center">
  <img src="https://img.shields.io/badge/SATARK_AI-Phishing_Detection-DFFF00?style=for-the-badge&labelColor=000000" alt="Satark AI" />
</p>

<h1 align="center">🛡️ Satark AI — Intelligent Phishing Detection Platform</h1>

<p align="center">
  <strong>Multilingual AI-powered phishing detection for SMS, emails, URLs, and screenshots</strong><br/>
  Built for <b>NeuroX Hackathon 2026</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" />
  <img src="https://img.shields.io/badge/React_19-61DAFB?style=flat-square&logo=react&logoColor=black" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Groq_LLM-FF6B35?style=flat-square&logo=lightning&logoColor=white" />
  <img src="https://img.shields.io/badge/EasyOCR-22C55E?style=flat-square&logo=google-lens&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white" />
  <img src="https://img.shields.io/badge/SHAP-8B5CF6?style=flat-square&logo=databricks&logoColor=white" />
</p>

---

## 📋 Table of Contents

- [Problem Statement](#-problem-statement)
- [What is Satark AI?](#-what-is-satark-ai)
- [Key Features](#-key-features)
- [Architecture](#-architecture)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [API Endpoints](#-api-endpoints)
- [Detection Pipeline](#-detection-pipeline)
- [Screenshots](#-screenshots)
- [Team](#-team)
- [License](#-license)

---

## 🎯 Problem Statement

India sees **5,000+ phishing attacks daily**, targeting users via SMS, WhatsApp, and email — often in **Hindi, Hinglish, and regional languages**. Existing tools only work with English and miss culturally-specific scam patterns like fake KYC alerts, UPI QR frauds, and government impersonation. **Satark AI** bridges this gap with an AI platform purpose-built for the Indian threat landscape.

---

## 🤖 What is Satark AI?

**Satark AI** (सतर्क = "Alert" in Hindi) is a full-stack intelligent phishing detection platform that analyzes:

- 📱 **SMS / WhatsApp messages** — Paste any suspicious text
- 📧 **Emails** — Analyze email bodies for phishing indicators
- 🔗 **URLs** — Deep scan links with multi-source reputation checks
- 📸 **Screenshots** — Upload a screenshot and OCR extracts + analyzes the text

It produces an **explainable risk score (0–100)** with plain-language explanations in the user's language, powered by a combination of ML classifiers, behavioral rule engines, URL reputation APIs, and Groq LLM.

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🌐 **Trilingual Support** | Detects and analyzes English, Hindi, and Hinglish messages natively |
| 🧠 **Explainable AI (XAI)** | SHAP-based feature attribution shows *why* a message is flagged |
| 📸 **Screenshot OCR** | EasyOCR extracts text from screenshots for analysis (Hindi + English) |
| 🔗 **Deep URL Analysis** | Multi-source: PhishTank, Google Safe Browsing, VirusTotal, WHOIS, TLD analysis |
| 🎯 **Behavioral Rule Engine** | Detects urgency language, OTP extraction, brand impersonation, prize scams |
| 💬 **LLM Explanations** | Groq-powered human-readable explanations of risk verdicts |
| 🛡️ **ArmorIQ Security Layer** | Input sanitization, prompt injection detection, adversarial guardrails |
| 📊 **Drift Monitor** | Automated daily model performance checks with alerting |
| 💸 **UPI / QR Fraud Detection** | Detects fake UPI payment links and QR code scams |
| 📈 **Scan History & Dashboard** | Full history of past scans with filtering and analytics |
| 🔐 **Auth System** | JWT-based authentication with Google OAuth + email/password login |
| 🔄 **Feedback Loop** | User feedback on verdicts feeds back into model improvement |

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────────────────────┐
│                        SATARK AI PLATFORM                            │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ┌──────────────┐    HTTP/REST     ┌─────────────────────────────┐   │
│  │   Frontend    │ ◄──────────────► │        FastAPI Backend      │   │
│  │  React + TS   │                  │                             │   │
│  │  Vite + TW    │                  │  ┌───────────────────────┐  │   │
│  └──────────────┘                  │  │   ArmorIQ Middleware   │  │   │
│                                     │  │  (Input Sanitization)  │  │   │
│                                     │  └──────────┬────────────┘  │   │
│                                     │             │               │   │
│                                     │  ┌──────────▼────────────┐  │   │
│                                     │  │   Analysis Pipeline    │  │   │
│                                     │  │                       │  │   │
│                                     │  │  ┌─────────────────┐  │  │   │
│                                     │  │  │  Language Detect │  │  │   │
│                                     │  │  └────────┬────────┘  │  │   │
│                                     │  │  ┌────────▼────────┐  │  │   │
│                                     │  │  │  NLP Classifier  │  │  │   │
│                                     │  │  │ TF-IDF + MNB    │  │  │   │
│                                     │  │  └────────┬────────┘  │  │   │
│                                     │  │  ┌────────▼────────┐  │  │   │
│                                     │  │  │  SHAP Explainer │  │  │   │
│                                     │  │  └────────┬────────┘  │  │   │
│                                     │  │  ┌────────▼────────┐  │  │   │
│                                     │  │  │ Behavioral Rules│  │  │   │
│                                     │  │  └────────┬────────┘  │  │   │
│                                     │  │  ┌────────▼────────┐  │  │   │
│                                     │  │  │  URL Analyzer   │  │  │   │
│                                     │  │  └────────┬────────┘  │  │   │
│                                     │  │  ┌────────▼────────┐  │  │   │
│                                     │  │  │  Risk Engine    │  │  │   │
│                                     │  │  └────────┬────────┘  │  │   │
│                                     │  │  ┌────────▼────────┐  │  │   │
│                                     │  │  │ Groq LLM Explain│  │  │   │
│                                     │  │  └─────────────────┘  │  │   │
│                                     │  └───────────────────────┘  │   │
│                                     │                             │   │
│                                     │  ┌───────────────────────┐  │   │
│                                     │  │   EasyOCR Pipeline    │  │   │
│                                     │  │  (Hindi + English)    │  │   │
│                                     │  └───────────────────────┘  │   │
│                                     │                             │   │
│                                     │  ┌───────────────────────┐  │   │
│                                     │  │   PostgreSQL / SQLite │  │   │
│                                     │  │   (Async via SQLAlch) │  │   │
│                                     │  └───────────────────────┘  │   │
│                                     └─────────────────────────────┘   │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

### Backend
| Technology | Purpose |
|-----------|---------|
| **FastAPI** | Async REST API framework |
| **SQLAlchemy 2.0** | Async ORM with PostgreSQL/SQLite |
| **scikit-learn** | TF-IDF + Multinomial Naive Bayes phishing classifier |
| **SHAP** | Explainable AI — feature attribution for predictions |
| **EasyOCR** | Optical Character Recognition (Hindi + English) |
| **Groq API** | LLM-powered human-readable explanations |
| **httpx** | Async HTTP client for external API calls |
| **APScheduler** | Background scheduler for drift monitoring |

### Frontend
| Technology | Purpose |
|-----------|---------|
| **React 19** | UI framework |
| **TypeScript** | Type-safe development |
| **Vite** | Build tool & dev server |
| **Tailwind CSS 4** | Utility-first styling |
| **TanStack Query** | Server state management & caching |
| **Zustand** | Client state management |
| **Recharts** | Data visualization (SHAP charts) |
| **Lucide React** | Icon system |

### External APIs
| API | Purpose |
|-----|---------|
| **PhishTank** | Known phishing URL database |
| **Google Safe Browsing** | Malware/phishing URL checking |
| **VirusTotal** | Multi-engine URL reputation scan |
| **WHOIS** | Domain registration age analysis |

---

## 📁 Project Structure

```
satark-ai/
├── backend/
│   ├── ai/                         # ML & NLP modules
│   │   ├── language_detector.py    # Hindi/English/Hinglish detection
│   │   ├── model_loader.py         # Loads trained TF-IDF + MNB model
│   │   ├── model_trainer.py        # Training pipeline for classifier
│   │   └── shap_explainer.py       # SHAP feature attribution
│   ├── armoriq/                    # Security middleware
│   │   ├── middleware.py           # Request sanitization & guardrails
│   │   ├── guardrails.py           # Input validation rules
│   │   ├── prompt_guard.py         # Prompt injection detection
│   │   ├── intent_verifier.py      # Intent classification
│   │   └── audit_logger.py         # Security event logging
│   ├── models/                     # SQLAlchemy ORM models
│   │   ├── database.py             # Engine & session setup
│   │   ├── user.py                 # User model
│   │   ├── scan.py                 # Scan results model
│   │   ├── feedback.py             # User feedback model
│   │   └── ...                     # Threat reports, audit logs
│   ├── ocr/                        # OCR pipeline
│   │   ├── ocr_pipeline.py         # EasyOCR wrapper + preprocessing
│   │   ├── image_validator.py      # Image format/size validation
│   │   └── text_cleaner.py         # Post-OCR text cleaning
│   ├── routers/                    # API route handlers
│   │   ├── analyze.py              # /analyze/message, /image, /url
│   │   ├── auth.py                 # Login, register, Google OAuth
│   │   ├── history.py              # Scan history endpoints
│   │   └── feedback.py             # Feedback submission
│   ├── services/                   # Business logic
│   │   ├── risk_engine.py          # Multi-signal risk aggregation
│   │   ├── behavioral_service.py   # Rule-based behavioral scoring
│   │   ├── groq_service.py         # LLM explanation generation
│   │   ├── drift_monitor.py        # Model performance monitoring
│   │   └── ocr_service.py          # OCR orchestration service
│   ├── url_analysis/               # URL reputation engine
│   │   ├── url_analyzer.py         # Main URL analysis orchestrator
│   │   ├── reputation_sources.py   # VirusTotal, Safe Browsing clients
│   │   ├── reputation_aggregator.py# Multi-source score aggregation
│   │   ├── phishtank_checker.py    # PhishTank database lookup
│   │   ├── tld_checker.py          # Suspicious TLD detection
│   │   ├── whois_checker.py        # Domain age verification
│   │   └── redirect_follower.py    # URL redirect chain analysis
│   ├── main.py                     # FastAPI app entry point
│   ├── config.py                   # Settings via pydantic-settings
│   └── seed_db.py                  # Database seeder script
├── satark-ai-frontend/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── LoginPage.tsx       # Auth page (Google OAuth + demo)
│   │   │   └── AnalyzePage.tsx     # Main analysis dashboard
│   │   ├── components/
│   │   │   ├── analysis/           # RiskGauge, SHAPChart, VerdictBadge...
│   │   │   ├── landing/            # Feature showcase
│   │   │   └── layout/             # Header, footer
│   │   ├── api/                    # Axios client & API functions
│   │   ├── store/                  # Zustand auth store
│   │   └── App.tsx                 # Router setup
│   ├── package.json
│   └── vite.config.ts
├── data/
│   ├── model.pkl                   # Pre-trained phishing classifier
│   └── sms_spam.tsv                # Training dataset
├── .env.example                    # Environment variable template
├── requirements.txt                # Python dependencies
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- **Python 3.10+**
- **Node.js 18+** and **npm**
- **PostgreSQL** (or use SQLite for quick local dev)

### 1. Clone the Repository

```bash
git clone https://github.com/himesh2360/neuroX-Hackthon-SATARK-AI.git
cd neuroX-Hackthon-SATARK-AI
```

### 2. Set Up Environment Variables

```bash
cp .env.example .env
```

Edit `.env` and fill in your API keys (see [Environment Variables](#-environment-variables) below).

### 3. Install Backend Dependencies

```bash
# Create virtual environment (recommended)
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS/Linux

pip install -r requirements.txt
```

### 4. Initialize the Database

```bash
# Seed the database with demo user and sample scans
python -m backend.seed_db
```

> **Demo credentials:** `demo@satark.ai` / `demo123`

### 5. Start the Backend Server

```bash
python -m uvicorn backend.main:app --host 0.0.0.0 --port 8000 --reload
```

> ⚠️ **First launch:** EasyOCR will download ~300MB of model weights. This is a one-time download.

### 6. Install & Start the Frontend

```bash
cd satark-ai-frontend
npm install
npm run dev
```

### 7. Open the App

- **Frontend:** [http://localhost:5173](http://localhost:5173)
- **Backend API Docs:** [http://localhost:8000/docs](http://localhost:8000/docs)
- **ReDoc:** [http://localhost:8000/redoc](http://localhost:8000/redoc)

---

## 🔑 Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `DATABASE_URL` | ✅ | PostgreSQL/SQLite connection string |
| `SECRET_KEY` | ✅ | JWT signing key (`openssl rand -hex 32`) |
| `GROQ_API_KEY` | ✅ | Groq API key for LLM explanations |
| `GOOGLE_CLIENT_ID` | ❌ | Google OAuth client ID |
| `GOOGLE_CLIENT_SECRET` | ❌ | Google OAuth client secret |
| `PHISHTANK_API_KEY` | ❌ | PhishTank API key for URL checking |
| `GOOGLE_SAFE_BROWSING_API_KEY` | ❌ | Google Safe Browsing API key |
| `VIRUSTOTAL_API_KEY` | ❌ | VirusTotal API key for URL reputation |
| `VITE_API_BASE_URL` | ✅ | Backend API URL for frontend |

> 💡 See [`.env.example`](.env.example) for the full list with setup instructions.

---

## 📡 API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/v1/auth/register` | Register new user |
| `POST` | `/api/v1/auth/login` | Login with email/password |
| `GET` | `/api/v1/auth/google` | Initiate Google OAuth |
| `GET` | `/api/v1/auth/me` | Get current user profile |

### Analysis
| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/v1/analyze/message` | Analyze text message |
| `POST` | `/api/v1/analyze/image` | Analyze screenshot (OCR) |
| `POST` | `/api/v1/analyze/url` | Analyze URL |

### History & Feedback
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/v1/history` | Get scan history |
| `POST` | `/api/v1/feedback` | Submit verdict feedback |

### Health
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/health` | Health check |

---

## 🔍 Detection Pipeline

When a message/screenshot/URL is submitted, it flows through a **6-layer detection pipeline**:

```
Input ──► ArmorIQ Sanitization
     ──► Language Detection (EN / HI / Hinglish)
     ──► NLP Classifier (TF-IDF + MultinomialNB) + SHAP Attributions
     ──► Behavioral Rule Engine (urgency, OTP, impersonation, prizes)
     ──► URL Reputation Analysis (PhishTank + Safe Browsing + VirusTotal + WHOIS)
     ──► Risk Score Aggregation (0-100) + Verdict (SAFE / SUSPICIOUS / PHISHING)
     ──► Groq LLM Explanation Generation
     ──► Response
```

### Risk Score Weights
| Signal | Weight | Description |
|--------|--------|-------------|
| NLP Score | 40% | ML classifier probability |
| Behavioral Score | 25% | Rule-engine triggers |
| URL Score | 25% | Multi-source reputation |
| OCR Score | 10% | OCR confidence × NLP score |

### Verdict Thresholds
| Score Range | Verdict |
|-------------|---------|
| 0 – 39 | ✅ **SAFE** |
| 40 – 69 | ⚠️ **SUSPICIOUS** |
| 70 – 100 | 🚨 **PHISHING** |

---

## 🖼️ Screenshots

### Login Page
> Glassmorphism dark-mode login with Google OAuth and demo sign-in

### Analysis Dashboard
> Paste SMS, upload screenshot, or enter URL — get instant AI-powered risk analysis

### Risk Gauge & SHAP Explanation
> Visual risk score with explainable AI showing which words triggered the detection

### URL Reputation Panel
> Multi-source deep URL scan results from PhishTank, Google Safe Browsing, and VirusTotal

---

## 🔒 ArmorIQ Security Layer

Satark AI includes a built-in security middleware called **ArmorIQ** that protects the platform from adversarial attacks:

- **Input Sanitization** — Strips XSS, SQL injection, and special characters
- **Prompt Injection Detection** — Blocks attempts to manipulate LLM prompts
- **Rate Limiting** — Prevents abuse of analysis endpoints
- **Intent Verification** — Validates that inputs are genuine analysis requests
- **Audit Logging** — Logs all security events for forensics

---

## 👥 Team

Built with ❤️ for **NeuroX Hackathon 2026**

---

## 📄 License

This project is built for the NeuroX Hackathon 2026. All rights reserved.

---

<p align="center">
  <sub>🛡️ Stay Alert. Stay Safe. Stay <b>Satark</b>.</sub>
</p>
