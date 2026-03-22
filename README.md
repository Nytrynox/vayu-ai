# VAYU AI

India's first AI-powered hyperlocal pollution death risk predictor. VAYU AI is a comprehensive 10-page Streamlit application that fetches real-time air quality data from multiple APIs, predicts AQI 72 hours ahead, calculates personalized health risks, tracks carbon footprints, and provides hospital preparedness alerts -- all with a premium dark/light theme interface.

---

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Pages and Features](#pages-and-features)
- [Data Sources](#data-sources)
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

---

## Overview

VAYU AI was built for the **Hack For Green Bharat 2026** hackathon. The platform addresses the crisis of 16 lakh annual pollution deaths in India by providing:

- Real-time AQI monitoring with live API data (OpenAQ, WAQI)
- 72-hour AQI prediction using weather-correlated models
- Personalized health risk scoring based on age, conditions, and exposure
- NASA FIRMS fire detection with distance-based AQI impact estimation
- Hospital preparedness dashboard projecting patient loads
- Carbon footprint calculator calibrated for Indian emission factors
- AI-powered chatbot (NVIDIA Kimi K2) for pollution guidance

---

## Architecture

```
+-------------------------------------------+
|           Streamlit Dashboard             |
|  10 Pages | Dark/Light Theme | Sidebar    |
+-------------------------------------------+
         |              |            |
         v              v            v
+----------------+ +----------+ +------------------+
| data_fetcher   | | predictor| | health_calculator|
| - OpenAQ API   | | - 72h    | | - Risk scoring   |
| - WAQI API     | |   AQI    | | - Age/condition  |
| - Open-Meteo   | |   model  | |   multipliers    |
| - NASA FIRMS   | +----------+ +------------------+
| - Geocoding    |
+----------------+      |             |
         |              v             v
         |      +------------+ +------------------+
         |      | hospital   | | carbon_calculator|
         |      | _predictor | | - Transport      |
         |      | - Patient  | | - Energy         |
         |      |   load     | | - Diet factors   |
         |      +------------+ +------------------+
         v
+-------------------------------------------+
|              chatbot                      |
|  NVIDIA Kimi K2 AI responses             |
|  Context-aware pollution guidance         |
+-------------------------------------------+
```

### Data Flow

1. **Auto-location** -- User's city is detected via IP geolocation.
2. **Data Fetch** -- AQI, weather, and fire data are fetched from live APIs.
3. **Prediction** -- 72-hour AQI forecast is generated from current PM2.5 and weather data.
4. **Visualization** -- Interactive Plotly charts, Folium maps, and metric cards render results.
5. **Action** -- Health risk scores, safe windows, and hospital alerts are computed.

---

## Technology Stack

| Component          | Technology                            |
|--------------------|---------------------------------------|
| Framework          | Streamlit                             |
| Charting           | Plotly (Graph Objects + Express)       |
| Mapping            | Folium + streamlit-folium             |
| Data Processing    | pandas, NumPy                         |
| APIs               | OpenAQ, WAQI, Open-Meteo, NASA FIRMS  |
| AI Chatbot         | NVIDIA Kimi K2                        |
| Theming            | Custom CSS injection (Dark/Light)     |

---

## Project Structure

```
VAYU-AI/
|
|-- app.py                    # Main Streamlit application (760 lines, 10 pages)
|-- config.py                 # API keys and configuration
|-- requirements.txt          # Python dependencies
|
|-- data_fetcher.py           # Multi-API data acquisition module
|   |                         #   - get_best_aqi_data()
|   |                         #   - get_weather_forecast()
|   |                         #   - get_nasa_fires()
|   |                         #   - get_historical_weather()
|   |                         #   - search_locations()
|   +                         #   - get_multi_city_data()
|
|-- predictor.py              # 72-hour AQI prediction engine
|-- health_calculator.py      # Personal health risk scoring
|-- hospital_predictor.py     # Hospital patient load projection
|-- carbon_calculator.py      # Carbon footprint computation
|-- chatbot.py                # NVIDIA Kimi K2 integration
|-- gemini_explainer.py       # Gemini-based AQI explanations
|-- generate_pdf.py           # PDF report generation
+-- utils.py                  # Shared utility functions
```

---

## Pages and Features

| Page                | Description                                                   |
|---------------------|---------------------------------------------------------------|
| Home Dashboard      | Live AQI display, pollutant breakdown vs WHO limits, 72h snapshot |
| 72H Prediction      | Hourly AQI forecast chart with safe/danger windows            |
| Pollution Heatmap   | Folium map with AQI markers and NASA fire overlays            |
| Health Risk         | Age/condition-adjusted personal risk calculator               |
| City Comparison     | Multi-city AQI bar chart comparison (up to 5 cities)          |
| Hospital Alert      | Projected respiratory patient loads and medicine stocking     |
| Historical Trends   | 30-day estimated AQI from weather data, day/hour analysis     |
| Green Tracker       | Gamified eco-action logging with points and CO2 savings       |
| Carbon Calculator   | Transport, energy, and diet carbon footprint estimator        |
| AI Chatbot          | Context-aware pollution Q&A powered by NVIDIA Kimi K2        |

---

## Data Sources

| Source           | Data Provided                     | Access Method    |
|------------------|-----------------------------------|------------------|
| OpenAQ           | Real-time PM2.5, PM10, NO2, CO    | REST API         |
| WAQI             | Air Quality Index                 | REST API (token) |
| Open-Meteo       | Weather forecast and historical   | REST API (free)  |
| NASA FIRMS       | Active fire hotspots              | REST API (key)   |
| Nominatim/OSM    | Location geocoding                | REST API (free)  |

---

## Installation

```bash
git clone https://github.com/karthik-idikuda/VAYU-AI.git
cd VAYU-AI

python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### API Keys (optional)

Create `.streamlit/secrets.toml`:

```toml
NASA_FIRMS_KEY = "your_key"
WAQI_TOKEN = "your_token"
```

---

## Usage

```bash
streamlit run app.py
```

The application opens at `http://localhost:8501`. Use the sidebar to navigate between pages and search for locations.

---

## License

This project was built for the Hack For Green Bharat 2026 hackathon.
