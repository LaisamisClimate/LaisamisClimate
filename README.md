# LCLI Carbon Exchange

**Community-First Carbon Brokerage Platform for Northern Kenya**

LCLI connects verified community land projects in northern Kenya to global climate buyers — with indigenous consent at the center of every deal.

---

## 📋 Overview

This repository contains:

- **`exchange.html`** — Full-stack React SPA with integrated UI for carbon project marketplace
- **`server.js`** — Secure Node.js/Express backend for AI-powered carbon estimation
- **`package.json`** — Dependencies & scripts for backend

### Key Features

✅ **Live Project Marketplace** — Filterable listings with real Verra registry data  
✅ **AI Carbon Estimator** — Claude-powered analysis of land potential  
✅ **Market Intelligence Dashboard** — Price trends, supply, and buyer analysis  
✅ **Community Consent First** — FPIC verification built into every workflow  
✅ **Secure Backend** — Rate limiting, error handling, environment-based secrets  

---

## 🚀 Quick Start

### Prerequisites

- **Node.js** ≥ 18.0.0  
- **Anthropic API Key** (get one: https://console.anthropic.com/account/keys)

### 1. Setup Backend

```bash
# Install dependencies
npm install

# Create .env file from template
cp .env.example .env

# Edit .env and add your Anthropic API key
nano .env
# ANTHROPIC_API_KEY=sk-ant-your-key-here
# FRONTEND_URL=http://localhost:5000

# Start development server
npm run dev
# Server runs on http://localhost:3000
```

### 2. Serve Frontend

**Option A: Static HTTP Server**
```bash
# Using Python
python -m http.server 5000

# Or using Node (install: npm install -g http-server)
http-server exchange.html -p 5000

# Then open: http://localhost:5000
```

**Option B: VS Code Live Server**
- Right-click `exchange.html` → "Open with Live Server"
- Frontend will run on http://localhost:5500

---

## 📁 File Structure

```
LaisamisClimate/
├── exchange.html          # React SPA (frontend)
├── server.js              # Express backend API
├── package.json           # Node dependencies
├── .env.example           # Environment template
├── .gitignore             # Git ignore rules
└── README.md              # This file
```

---

## 🔌 API Reference

### `POST /api/estimate`

Generates AI-powered carbon credit analysis.

**Request:**
```json
{
  "message": "Land: 5000 hectares of Savanna Grassland. Current use: Open Grazing. Duration: 20 years. Nearest town: Laisamis, Marsabit County. Consent status: Full FPIC documented."
}
```

**Response (Success):**
```json
{
  "text": "## Annual Emissions Reduction\n\n**Estimated: 2,500 tCO₂e/year**\n..."
}
```

**Response (Error):**
```json
{
  "error": "Missing or invalid \"message\" field"
}
```

**Rate Limits:**
- 10 requests per 15 minutes per IP
- Max message length: 5,000 characters

---

## 🔐 Security

### Best Practices Implemented

✅ **API Key Management** — Secrets stored in `.env` (never in code)  
✅ **CORS** — Restricted to whitelisted frontend URL  
✅ **Rate Limiting** — Prevents abuse; 10 reqs/15min per IP  
✅ **Input Validation** — Message length & type checks  
✅ **Error Handling** — Safe error messages (no stack traces exposed)  
✅ **Timeout** — 30-second request timeout on frontend  

### Environment Variables

Create `.env` file (copy from `.env.example`):

```bash
ANTHROPIC_API_KEY=sk-ant-...          # Your Anthropic API key
PORT=3000                              # Server port (default: 3000)
NODE_ENV=development                   # Environment: development/production
FRONTEND_URL=http://localhost:5000     # Frontend URL for CORS
```

**Never commit `.env` to Git** (it's in `.gitignore`)

---

## 🌐 Deployment

### Deploy Backend to Heroku

```bash
# Install Heroku CLI: https://devcenter.heroku.com/articles/heroku-cli

# Create app
heroku create lcli-carbon-api

# Set environment variables
heroku config:set ANTHROPIC_API_KEY=sk-ant-your-key-here
heroku config:set FRONTEND_URL=https://your-frontend-url.com

# Deploy
git push heroku main

# View logs
heroku logs --tail
```

### Deploy Frontend to GitHub Pages

```bash
# Push exchange.html to docs/ folder
mkdir -p docs
cp exchange.html docs/index.html
git add docs/
git commit -m "Deploy frontend to GitHub Pages"
git push origin main
```

Then enable GitHub Pages in repo settings: `Settings` → `Pages` → `Deploy from branch` → `main /docs`

---

## 🛠️ Development

### Run in Development Mode

```bash
# Backend with hot reload
npm run dev

# Frontend (separate terminal)
python -m http.server 5000
```

### Testing the API

```bash
# Test /health endpoint
curl http://localhost:3000/health

# Test /api/estimate
curl -X POST http://localhost:3000/api/estimate \ 
  -H "Content-Type: application/json" \ 
  -d '{"message": "Land: 5000 hectares of Savanna Grassland. Duration: 20 years. Consent: Full FPIC documented."}'
```

---

## 📊 Project Data

### Live Projects (4 listed)

1. **Northern Kenya Rangelands Carbon Project** (SUSPENDED)
   - Type: Grassland/Soil Carbon
   - Area: 1,900,000 ha
   - Status: Under Verra Review

2. **Kasigau Corridor REDD+ Phase II** (ACTIVE)
   - Type: REDD+ / Avoided Deforestation
   - Price: $14–$18/tonne
   - Annual: 1,428,835 tCO₂e/year

3. **Acorn Agroforestry** (ACTIVE)
   - Type: Agroforestry / CRUs
   - Price: €20–€31/tonne (~$22–$34)
   - Area: ~40,000 ha (4,000+ farms)

4. **Kenya Agricultural Carbon Project** (ACTIVE)
   - Type: SALM / Soil Carbon
   - Price: $9–$13/tonne
   - Area: 22,000 ha

---

## 🤝 Community & Consent

LCLI's core principle: **Indigenous consent at the center of every deal.**

- ✅ FPIC (Free, Prior, Informed Consent) required for all listed projects
- ✅ Community benefit verification (% of revenue)
- ✅ Transparent pricing & commissions
- ✅ No upfront costs for landowners

---

## 📝 License

MIT License — See LICENSE file for details

---

## 📧 Support

**LCLI Team**  
Laisamis, Marsabit County, Kenya  
Email: contact@laisamisclimate.org  

**Repository:** https://github.com/LaisamisClimate/LaisamisClimate

---

## 🔄 Recent Fixes & Changes

### v1.0.0 (Current)

✅ **Fixed Critical Issues:**
- Moved Anthropic API calls to secure backend
- Added proper API key management via `.env`
- Implemented error handling & timeout protection
- Added rate limiting (10 reqs/15min)
- Fixed radio button naming bug in Contact form
- Added CORS support for frontend-backend communication

✅ **Security Improvements:**
- No sensitive keys in client-side code
- Input validation on all endpoints
- Graceful error messages
- Environment-based configuration

✅ **Backend Features:**
- Express.js server on port 3000
- Health check endpoint (`/health`)
- Request logging & monitoring
- Rate limiting per IP
- Comprehensive error handling