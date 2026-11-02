# 🌤️ Weather Sentiment Analyzer

An intelligent, full-stack web application that combines real-time meteorological data with Natural Language Processing (NLP) sentiment analysis to assess the psychological and environmental impact of current weather conditions. The system provides actionable wellness tips, productivity scores, comfort ratings, and eco-friendly climate recommendations.

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Tech Stack](#-tech-stack)
- [System Architecture](#-system-architecture)
- [Workflow](#-workflow)
- [Repository Structure](#-repository-structure)
- [Prerequisites](#-prerequisites)
- [How to Run](#-how-to-run)
  - [1. Backend Setup (Flask API)](#1-backend-setup-flask-api)
  - [2. Frontend Setup (React Application)](#2-frontend-setup-react-application)
- [API Reference](#-api-reference)
- [Configuration](#-configuration)
- [License](#-license)

---

## 🌟 Overview

The **Weather Sentiment Analyzer** bridges environmental monitoring with natural language perception. Users can query current weather for any city or enter custom weather impressions. The platform processes this text alongside live atmospheric readings (temperature, humidity, wind velocity, sky conditions) to determine:

1. **Sentiment & Emotion**: Analyzes tone, polarity, and subjectivity of weather descriptions.
2. **Weather Dimensions**: Classifies texts into categories like temperature, precipitation, wind, and sky condition.
3. **Daily Impact Scores**: Computes scores for productivity, comfort level, and outdoor activity feasibility.
4. **Context-Aware Recommendations**: Offers lifestyle recommendations, wellness tips, and climate action guidance tailored to the prevailing weather.

---

## ✨ Key Features

- **Real-Time Weather Integration**: Queries live weather conditions, temperature, humidity, and wind speed via the WeatherAPI.
- **NLP Sentiment Analysis**: Employs TextBlob to quantify sentiment polarity (negative to positive) and subjectivity (objective vs. subjective perception).
- **Automated Weather Summarization**: Synthesizes live weather telemetry into human-readable descriptive text ready for immediate analysis.
- **Quick-Select Weather Presets**: Pre-populated phrases for rapid testing and demonstrations.
- **Rule-Based Weather Categorization**: Uses regular expressions to parse descriptions into meteorological categories (temperature, precipitation, wind, sky condition).
- **Holistic Impact Assessment**:
  - 🎯 **Productivity Index**: Evaluates optimal conditions for focus and work.
  - 🌡️ **Comfort Level**: Balances thermal sensation and relative humidity.
  - 🏃 **Activity Feasibility**: Assesses safety and enjoyment for outdoor exercises.
- **Personalized Recommendations Engine**:
  - **Activities & Wellness**: Tailored suggestions for running, nature walks, home workouts, or mindfulness.
  - **Climate Action & Sustainability**: Immediate actions (energy conservation, green transit), resilience adaptation (rainwater collection, solar utilization), and climate awareness tracking.

---

## 💻 Tech Stack

### Frontend
| Technology | Description |
| :--- | :--- |
| **React 18** | Component-driven UI development and state management (`useState`, `useEffect`) |
| **CSS3** | Modern responsive grid and flexbox layouts, visual meters, and animations |
| **HTML5 / JavaScript (ES6+)** | Modern asynchronous client logic with Fetch API |
| **WeatherAPI** | Third-party REST API for live meteorological data |

### Backend
| Technology | Description |
| :--- | :--- |
| **Python 3.8+** | Core runtime environment |
| **Flask** | Lightweight WSGI web application framework and RESTful routing |
| **Flask-CORS** | Cross-Origin Resource Sharing handling for React frontend communication |
| **TextBlob** | Natural language processing library for sentiment polarity and subjectivity |
| **Regular Expressions (`re`)** | Regex pattern matching for meteorological text categorization |

---

## 🏗️ System Architecture

The application adopts a decoupled client-server architecture:

```mermaid
flowchart TD
    subgraph Client ["Frontend (React.js - Port 3000)"]
        UI["User Interface (App.js)"]
        ImpactCalc["Client-side Impact Calculations (Productivity, Comfort, Activity)"]
        Visuals["Visualization Meters & Recommendation Cards"]
    end

    subgraph External ["External Services"]
        WAPI["WeatherAPI (current.json)"]
    end

    subgraph Server ["Backend (Flask REST API - Port 5000)"]
        APIEndpoint["Flask Route: POST /analyze"]
        NLP["TextBlob Sentiment Engine (Polarity & Subjectivity)"]
        CatEngine["Regex Weather Categorizer"]
        RecEngine["Rule-based Recommendation Generator"]
    end

    UI -->|"1. Query City Weather"| WAPI
    WAPI -->|"2. Return Weather Metrics"| UI
    UI -->|"3. Auto-generate / Input Text + Weather Data"| APIEndpoint
    APIEndpoint --> NLP
    APIEndpoint --> CatEngine
    APIEndpoint --> RecEngine
    NLP --> APIEndpoint
    CatEngine --> APIEndpoint
    RecEngine --> APIEndpoint
    APIEndpoint -->|"4. JSON Response (Sentiment, Categories, Recs)"| ImpactCalc
    ImpactCalc --> Visuals
```

---

## 🔄 Workflow

```mermaid
sequenceDiagram
    autonumber
    actor User
    participant Frontend as React Client (Port 3000)
    participant WeatherAPI as WeatherAPI
    participant Backend as Flask API (Port 5000)

    User->>Frontend: Enters city name (e.g., "Mumbai") & clicks "Get Weather"
    Frontend->>WeatherAPI: GET /v1/current.json?q={city}
    WeatherAPI-->>Frontend: Weather telemetry (temperature, condition, humidity, wind)
    Frontend->>Frontend: Generates weather description & populates text area

    User->>Frontend: Edits text or selects quick phrase, then clicks "Analyze Weather"
    Frontend->>Backend: POST /analyze with { text, weather_data }
    Note over Backend: 1. TextBlob evaluates polarity & subjectivity<br/>2. Regex categorizes weather keywords<br/>3. Recommender generates lifestyle & sustainability tips
    Backend-->>Frontend: Returns JSON with sentiment, categories & recommendations
    Frontend->>Frontend: Computes Productivity, Comfort, and Activity indices
    Frontend-->>User: Displays sentiment meter, impact scores, and recommendation cards
```

---

## 📁 Repository Structure

```text
Weather_analysis-main/
├── backend/
│   ├── app.py                 # Flask server, NLP analysis & recommendation logic
│   └── requirements.txt       # Python dependencies (Flask, Flask-CORS, TextBlob)
├── public/
│   ├── index.html             # HTML entry point
│   └── manifest.json          # Web app manifest
├── src/
│   ├── App.css                # Application styles, meters, cards & animations
│   ├── App.js                 # Primary React component (UI, state, API calls)
│   ├── index.css              # Global styles
│   ├── index.js               # React DOM entry point
│   └── reportWebVitals.js     # Web performance measuring utility
├── package.json               # Node.js project manifest & scripts
├── package-lock.json          # Node dependency lockfile
└── README.md                  # Project documentation
```

---

## ⚙️ Prerequisites

Ensure you have the following installed on your machine:
- **Node.js**: `v16.x` or higher ([Download Node.js](https://nodejs.org/))
- **npm**: `v8.x` or higher (bundled with Node.js)
- **Python**: `3.8` or higher ([Download Python](https://www.python.org/))
- **pip**: Python package manager

---

## 🚀 How to Run

### 1. Backend Setup (Flask API)

1. Open a terminal and navigate to the `backend` directory:
   ```bash
   cd backend
   ```

2. (Optional but recommended) Create and activate a virtual environment:
   - **Windows**:
     ```bash
     python -m venv venv
     .\venv\Scripts\activate
     ```
   - **macOS / Linux**:
     ```bash
     python3 -m venv venv
     source venv/bin/activate
     ```

3. Install the required Python packages:
   ```bash
   pip install -r requirements.txt
   ```
   *(Alternatively: `pip install flask flask-cors textblob`)*

4. Download TextBlob corpora (if prompted on first run):
   ```bash
   python -m textblob.download_corpora
   ```

5. Start the Flask server:
   ```bash
   python app.py
   ```
   *The backend will run on `http://localhost:5000`.*

---

### 2. Frontend Setup (React Application)

1. Open a new terminal window and navigate to the project root directory:
   ```bash
   cd Weather_analysis-main
   ```

2. Install Node.js dependencies:
   ```bash
   npm install
   ```

3. Start the React development server:
   ```bash
   npm start
   ```

4. The application will automatically launch in your default browser at:
   ```
   http://localhost:3000
   ```

---

## 📡 API Reference

### Analyze Weather & Sentiment

- **Endpoint**: `/analyze`
- **Method**: `POST`
- **Content-Type**: `application/json`

#### Request Body
```json
{
  "text": "The current weather in Mumbai is sunny with a temperature of 28°C.",
  "weather_data": {
    "temp_c": 28,
    "condition": "Sunny"
  }
}
```

#### Response Body
```json
{
  "sentiment": {
    "sentiment": "positive",
    "polarity": 0.5,
    "subjectivity": 0.4
  },
  "categories": {
    "temperature": true,
    "sky_condition": true
  },
  "recommendations": [
    {
      "icon": "🏃‍♂️",
      "title": "Perfect for Exercise",
      "description": "Ideal conditions for running, cycling, or outdoor workout."
    },
    {
      "icon": "🌱",
      "title": "Energy Conservation",
      "description": "Use natural ventilation when possible, minimize AC usage during peak hours."
    }
  ]
}
```

---

## 🔧 Configuration

### WeatherAPI Key
The live weather search uses [WeatherAPI](https://www.weatherapi.com/).
- The API call is configured in [src/App.js](file:///d:/Weather_analysis-main/src/App.js#L143).
- To supply your own API key:
  1. Sign up for a free key at [WeatherAPI.com](https://www.weatherapi.com/).
  2. Replace the `key` query parameter in the `fetch` URL in `src/App.js`:
     ```javascript
     const response = await fetch(`https://api.weatherapi.com/v1/current.json?key=YOUR_API_KEY&q=${encodeURIComponent(location)}&aqi=no`);
     ```

---

## 📄 License

This project is licensed under the MIT License - feel free to adapt and build upon it!
