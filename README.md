# Divya Warule — Portfolio

Personal portfolio site for **Divya Raosaheb Warule** — Full Stack Developer & Agentic AI Builder.

**Live portfolio:** [https://jay-07-pixel.github.io/Divya_Portfolio/](https://jay-07-pixel.github.io/Divya_Portfolio/)

---

# KALPANIK Operations AI

Agentic AI system for MSME operations — order management, workforce scheduling, inventory, and **delay risk prediction** using real-world Olist e-commerce data.

**Live:** [https://kalpanikoperations-ai-production.up.railway.app/](https://kalpanikoperations-ai-production.up.railway.app/)

**Project README:** [Agentic-AI-for-MSME-Operations](https://github.com/waruledivya1411/Agentic-AI-for-MSME-Operations/blob/main/README.md)

---

## Features

- **Shop** — Place orders (website + WhatsApp); customers see only “Your order has been placed!” and an order ID
- **Dashboard Overview** — KPIs, live orders, workforce management, stock levels
- **Agents Log** — Structured view of the last order flow, delay risk, pipeline steps, tasks & time
- **WhatsApp Log** — Terminal-style log of the WhatsApp order flow (API → agents → completion)
- **Delay / Risk Predictor** — ML model with labels: **No tension**, **A bit**, **High chances delayed** (not rule-based)
- **Manage Workforce** — Add/remove staff, update roles and shift times
- **Restock** — Add inventory quantities

---

## Live deployment (Railway)

One deployment serves both the API and the frontend (Express serves `website/` as static files).

| Page | URL |
|------|-----|
| **Shop** | [https://kalpanikoperations-ai-production.up.railway.app/](https://kalpanikoperations-ai-production.up.railway.app/) |
| **Dashboard Overview** | [https://kalpanikoperations-ai-production.up.railway.app/overview.html](https://kalpanikoperations-ai-production.up.railway.app/overview.html) |
| **Agents Log** | [https://kalpanikoperations-ai-production.up.railway.app/dashboard.html](https://kalpanikoperations-ai-production.up.railway.app/dashboard.html) |
| **WhatsApp Log** | [https://kalpanikoperations-ai-production.up.railway.app/whatsapp.html](https://kalpanikoperations-ai-production.up.railway.app/whatsapp.html) |
| **WhatsApp API** | `POST` [https://kalpanikoperations-ai-production.up.railway.app/order/whatsapp](https://kalpanikoperations-ai-production.up.railway.app/order/whatsapp) |

---

## Quick start (local)

### 1. Start the backend

```bash
cd backend
npm install
npm start
```

Server runs at [http://localhost:3000](http://localhost:3000).

### 2. Open the app

| Page | Local URL |
|------|-----------|
| **Shop** | [http://localhost:3000](http://localhost:3000) |
| **Dashboard Overview** | [http://localhost:3000/overview.html](http://localhost:3000/overview.html) |
| **Agents Log** | [http://localhost:3000/dashboard.html](http://localhost:3000/dashboard.html) |
| **WhatsApp Log** | [http://localhost:3000/whatsapp.html](http://localhost:3000/whatsapp.html) |

### 3. Test WhatsApp orders (Insomnia / Postman)

**Local:** `POST http://localhost:3000/order/whatsapp`  
**Deployed:** `POST https://kalpanikoperations-ai-production.up.railway.app/order/whatsapp`

**Headers:** `Content-Type: application/json`

**Request body (JSON):**

```json
{
  "from": "+919876543210",
  "message": "Hi, I need 2 Cotton Crew T-Shirt by tomorrow 11pm. Urgent!"
}
```

Or use `phone` instead of `from`:

```json
{
  "phone": "+919876543210",
  "message": "I need 1 Cotton Crew T-Shirt by tomorrow. Urgent!"
}
```

**Field notes:**

| Field | Required | Description |
|-------|----------|-------------|
| `from` or `phone` | Yes | Customer phone number |
| `message` or `text` | Yes | Raw WhatsApp message text |
| `name` | No | Optional customer name |

The LLM parses product, quantity, deadline, and priority from the message.

---

## Deploy (Railway)

**One deployment does everything.** The backend serves the frontend: Express serves the `website/` folder as static files, so when you deploy the repo to Railway you get both the API and the shop/dashboard at the same URL.

See **[DEPLOYMENT.md](./DEPLOYMENT.md)** for step-by-step Railway setup.

---

## Project structure

```
OPERATIONS/
├── backend/          # Node.js API (serves website/ as static)
│   ├── src/          # Agents, routes, services
│   └── ml/           # Delay predictor (train script, model, API-aligned dataset)
├── website/          # Static frontend (shop, overview, dashboard, WhatsApp log)
├── scripts/          # Utilities (e.g. technical_flowchart.py)
├── docs/             # Architecture docs
├── railway.json      # Railway config
└── DEPLOYMENT.md     # Deploy guide
```

---

## Tech stack

| Layer | Technologies |
|-------|----------------|
| **Backend** | Node.js, Express |
| **Frontend** | Vanilla JS, HTML, CSS |
| **ML** | scikit-learn (Python), logistic regression for delay prediction |
| **Data** | Olist Brazilian E-Commerce (Kaggle) |
| **Deploy** | Railway |

---

## Agent pipeline

```
Order → Inventory → Decision Engine → Workforce → Critic → Executor
```

---

## CityPulse Mumbai

Live smart-city dashboard for Mumbai, Maharashtra — air quality, traffic emissions, rainfall, and solar data on an interactive map.

Built as a portfolio project covering front-end development, geospatial visualization, and UI/UX for dashboard and app developer roles.

**GitHub:** [https://github.com/waruledivya1411/citypulse-dashboard.git](https://github.com/waruledivya1411/citypulse-dashboard.git)

### Overview

CityPulse turns public environmental APIs into a single, readable dashboard:

- 15 monitoring sites at real Mumbai landmarks
- Live metrics refreshed every 15 minutes from Open-Meteo (no API key required)
- Interactive map (Leaflet + OpenStreetMap) with filters, popups, and fly-to selection
- Charts and KPIs (Recharts) for trends, zone comparison, and alerts

### Live data (what is real)

- **Air Quality:** US AQI, PM2.5 (Open-Meteo Air Quality API / Copernicus CAMS)
- **Traffic proxy:** NO2 (ug/m3) as a practical emissions indicator
- **Flood/Rain:** Precipitation (mm) from Open-Meteo Weather API
- **Energy:** Solar radiation (W/m2) from Open-Meteo Weather API

Note: Traffic is NO2 pollution proxy, not road congestion percentage.

### Features

- KPI cards (active sites, alerts, average AQI, average NO2)
- 24-hour trend chart (AQI, NO2, solar radiation)
- Full-screen map explorer with category/status filters
- Zone-level analytics and solar irradiance time series
- Auto-generated alerts when thresholds are exceeded

### Tech stack

- **UI:** React 19, TypeScript, Tailwind CSS v4
- **Maps:** Leaflet, React-Leaflet, OpenStreetMap
- **Charts:** Recharts
- **Build:** Vite 8
- **Data:** Open-Meteo REST APIs

### Getting started

```bash
git clone <your-repo-url>
cd citypulse-mumbai
npm install
npm run dev
```

Open `http://localhost:5173` in your browser.

### How it works

1. `fetchLiveMumbaiData()` requests batch coordinates for all 15 sites.
2. Responses map into sensor objects with health status rules.
3. Alerts generate from warning/critical sensors.
4. Hourly city history powers trend charts.
5. Data auto-refreshes every 15 minutes.

---

## Smart Trip Planner India

Your intelligent travel companion for exploring Incredible India with smart itinerary planning, live data integration, and personalized recommendations.

**Live Demo:** [https://smart-tripplanner.netlify.app/](https://smart-tripplanner.netlify.app/)  
**GitHub:** [https://github.com/jay-07-pixel/Smart_Trip-_Planner-.git](https://github.com/jay-07-pixel/Smart_Trip-_Planner-.git)

### What makes this special

Smart Trip Planner India combines live API data (Google Places, OpenWeatherMap, Google Maps) with rule-based itinerary logic to build personalized travel plans by destination, budget, trip type, and travel style.  
The core planner uses real-time APIs plus template-driven planning (not a third-party LLM API).

### Key highlights

- Day-by-day itinerary generation (up to 5 days in output)
- Live hotels, restaurants, attractions via Google Places API
- Real-time weather forecasts via OpenWeatherMap
- Optional traffic analysis with best departure windows and 8-day patterns
- Budget planning with 6 category sliders and allocation tracking
- External booking and comparison links (hotels, flights, trains, buses, food delivery)
- 8 trip types and 3 travel styles (Relaxed, Balanced, Intense)
- Fully responsive design for desktop and mobile

### Trip planner features

The main interactive app is `trip-planner.html`.

- **Trip form:** destination, dates, trip type, style, budget, and optional traffic analysis
- **Live data integration:** places, weather, and route-time insights
- **Traffic analysis:** route overview, best/avoid times, and heatmap-style multi-day pattern
- **Budget management:** category-based budget splits with warnings and live tracking
- **Transport recommendations:** flights/trains/buses with budget fit hints
- **Interactive actions:** directions, details modals, booking links, and progress overlay

### Technology stack

- **Frontend:** HTML5, Tailwind CSS, JavaScript (ES6+), Font Awesome
- **Animations:** GSAP
- **Integrations:** Google Maps JavaScript API, Google Places API, Distance Matrix API, OpenWeatherMap, Browser Geolocation API
- **Deployment:** Netlify

### Getting started

```bash
git clone https://github.com/jay-07-pixel/Smart_Trip-_Planner-.git
cd Smart_Trip-_Planner-
python -m http.server 8000
```

Open `http://localhost:8000/trip-planner.html`.

### Local configuration

- Copy `js/config.example.js` to `js/config.js`
- Add API keys for Google Maps/Places and OpenWeatherMap
- Do not commit `js/config.js` (kept in `.gitignore`)

### Roadmap

- Use traveler count/interests/special requirements in generation logic
- Export itineraries (PDF/calendar) and shareable links
- Mobile app and offline support
- Multi-language support
- Future LLM-powered enhancement and direct in-app booking

---

## Medify - Healthcare Platform

A comprehensive healthcare platform that provides online pharmacy services, doctor consultations, lab test bookings, and health insurance solutions.

**GitHub:** [https://github.com/waruledivya1411/Medify.git](https://github.com/waruledivya1411/Medify.git)

### Features

- **Online Pharmacy** — browse medicines by category, search products, upload prescriptions, and manage cart
- **Doctor Consultations** — browse specialties, filter by mode/experience/fees/language, and view doctor profiles
- **Lab Tests** — doctor-created packages with pricing, discounts, categories, and carousel browsing
- **Health Insurance** — compare plans and enroll in suitable coverage options
- **User Experience** — login/signup flow, address selection, responsive UI, and localStorage-backed cart state

### Tech stack

- **Frontend:** HTML5, CSS3, Vanilla JavaScript
- **Icons:** Font Awesome 6.4.0 (CDN)
- **Data handling:** localStorage (frontend-only app)

### Project structure

```text
Dipex/
├── index.html
├── medicines.html
├── consultation.html
├── doctors.html
├── labtest.html
├── labtests-list.html
├── insurance.html
├── doctors-simple.html
├── styles.css
├── script.js
├── doctors.js
├── medicines-data.js
├── labtests-data.js
└── README.md
```

### Getting started

1. Clone or download the repository.
2. Open `index.html` in a modern browser.
3. No server/build setup is required.

### Notes

- Frontend-only architecture, no backend required for basic functionality
- For production, integrate backend services for auth, payments, booking, and order workflows

---

## Portfolio — run locally

This portfolio is a static site — no build step required.

```bash
cd Divya_Portfolio
python -m http.server 8080
```

Open [http://localhost:8080](http://localhost:8080) in your browser.

## Portfolio — deploy

| Target | How |
|--------|-----|
| **GitHub Pages** | Push to `main`; workflow in `.github/workflows/pages.yml` deploys automatically |
| **Firebase Hosting** | `firebase deploy` (config in `firebase.json`) |

---

## Contact

- **Email:** divya.warule24@sanjivani.edu.in
- **GitHub:** [waruledivya1411](https://github.com/waruledivya1411)
