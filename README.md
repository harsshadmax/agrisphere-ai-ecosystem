# 🌱 AgriSphere

### AI-Powered Digital Agriculture & Farm Intelligence Platform

> **An intelligent agriculture ecosystem connecting farm monitoring, AI-driven crop intelligence, agricultural finance, digital marketplaces, and farmer decision support in one platform.**

AgriSphere is a full-stack digital agriculture platform designed to bring together the major parts of the agricultural ecosystem — **farm management, crop intelligence, financial access, digital crop trading, wallets, notifications, collaboration, and data-driven decision support**.

The platform is structured as a modular system with a **Next.js frontend**, **Node.js/Express backend**, **MongoDB data layer**, and a dedicated **FastAPI AI intelligence service**.

---

# 🎯 Vision

Agriculture involves much more than crop cultivation.

Farmers need to manage:

* 🌾 Land and crops
* 🛰️ Farm intelligence
* 📊 Production and yield
* 💰 Agricultural finance
* 🏦 Loans and credit
* 🛒 Buyers and marketplaces
* 💳 Payments and wallets
* 🤝 Collaboration
* 🔔 Notifications and alerts

AgriSphere aims to connect these workflows into a **single digital ecosystem**.

```text
                         🌱 AGRISPHERE
                              │
       ┌──────────────────────┼──────────────────────┐
       │                      │                      │
       ▼                      ▼                      ▼
  🌾 Farm Intelligence   💰 Financial Access    🛒 Digital Market
       │                      │                      │
       ▼                      ▼                      ▼
   Crop Health            Credit Score          Crop Listings
   Yield Forecast         Loan Management       Auctions
   Growth Analysis        Wallet               Buyers
       │                      │                      │
       └──────────────────────┼──────────────────────┘
                              │
                              ▼
                     🤖 AI Decision Support
                              │
                              ▼
                       👨‍🌾 Farmer Ecosystem
```

---

# ✨ Core Capabilities

## 🌾 Farm Management

AgriSphere provides a dedicated farm-management layer for organizing farmer and farm information.

The backend contains dedicated farm models, controllers, and routes for this functionality.

---

## 🤖 AI Farm Intelligence

The AI service provides multiple agricultural intelligence capabilities.

### Yield Prediction

The AI service uses a **Random Forest Regressor** for baseline yield prediction using agricultural features including:

* Soil moisture
* Temperature
* Nitrogen level
* Farm size

The current implementation trains a baseline model during service startup.

```text
Soil Moisture
      +
Temperature
      +
Nitrogen
      +
Farm Size
      │
      ▼
Random Forest
      │
      ▼
Predicted Yield
      │
      ├── Productivity Status
      ├── Estimated Value
      └── Health Status
```

---

## 🌿 Crop Health Analysis

AgriSphere includes an AI endpoint for crop-health analysis using NDVI-related inputs and soil-moisture information.

The service calculates:

* Average NDVI
* Normalized moisture stress
* Health status
* Pest-risk indication
* Agricultural recommendations

The current baseline logic classifies crop condition using NDVI thresholds and derives moisture stress from soil moisture.

```text
NDVI Values
     │
     ▼
Average NDVI
     │
     ├── High NDVI → Peak Biomass
     │
     ├── Normal    → Standard Growth
     │
     └── Low NDVI  → Chlorophyll Deficiency
```

---

## 📈 Growth Forecasting

The AI service provides an NDVI growth-forecast endpoint.

Historical NDVI values are used to estimate a trend, which is then projected over the requested forecast period.

```text
Historical NDVI
       │
       ▼
Trend Calculation
       │
       ▼
Future NDVI Projection
       │
       ├── Positive
       ├── Stagnant
       └── Declining
```

---

# 💳 Agricultural Credit Intelligence

One of AgriSphere's major components is its agriculture-focused financial layer.

The AI service calculates a credit score using:

* Annual income
* Average yearly yield value
* Previous loan defaults

The current implementation produces a score between **300 and 850**, assigns a risk category, determines loan eligibility, and calculates a recommended maximum loan amount.

```text
Farmer Financial Data
          │
          ▼
    Credit Algorithm
          │
          ▼
     Credit Score
          │
    ┌─────┼─────┐
    ▼     ▼     ▼
   Low   Medium High
   Risk   Risk  Risk
          │
          ▼
   Loan Eligibility
```

### Current Credit Tiers

|   Score | Risk   |
| ------: | ------ |
| 720–850 | Low    |
| 600–719 | Medium |
| 300–599 | High   |

The service also categorizes qualifying users into a Gold or Standard tier.

> **Note:** The current credit model is an application-level algorithmic baseline, not a production banking credit bureau model.

---

# 🏦 Loan Management

The backend contains a dedicated loan module with:

* Loan model
* Loan controller
* Loan routes

This allows the platform architecture to support farmer financing workflows alongside the AI credit layer.

---

# 🛒 Digital Agricultural Marketplace

AgriSphere includes a marketplace layer connecting agricultural producers and buyers.

The backend contains dedicated marketplace and crop-listing components.

### Marketplace Concepts

```text
Farmer
   │
   ▼
Crop Listing
   │
   ▼
Marketplace
   │
   ├── Buyer Discovery
   ├── Crop Transactions
   └── Auction
          │
          ▼
       Buyer
```

---

# 🔨 Auction System

The platform contains dedicated auction models, controllers, and routes for agricultural trading.

This allows crop listings to support competitive buyer participation rather than relying only on fixed-price transactions.

---

# 💰 Digital Wallet

AgriSphere includes a wallet and transaction layer.

The backend contains:

* Wallet model
* Transaction model
* Wallet routes
* Wallet controller

The frontend also includes Razorpay integration support through `react-razorpay`, while the backend includes the Razorpay SDK.

---

# 🔔 Notifications

The platform includes a dedicated notification system for communicating important platform events to users.

The backend contains notification models, controllers, and routes.

---

# 🤝 Action Room

AgriSphere includes an **Action Room** architecture designed around actionable tasks and decisions.

The backend contains:

```text
ActionRoom
ActionTask
ActionDecision
```

models along with dedicated controllers and routes.

This provides a foundation for converting agricultural intelligence into structured actions rather than only displaying analytics.

---

# 📅 Meetings & Collaboration

The platform contains meeting-related models and routes, including:

* Meetings
* Meeting tasks
* Meeting controllers
* Meeting routes

This provides a collaboration layer for coordinating agricultural activities and decisions.

---

# 🏗️ System Architecture

AgriSphere follows a modular three-service architecture:

```text
                         ┌───────────────────────┐
                         │       USER            │
                         │ Farmer / Buyer /      │
                         │ Finance / Admin       │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │       FRONTEND        │
                         │ Next.js + React       │
                         │ TypeScript             │
                         └───────────┬───────────┘
                                     │
                              REST / Socket.IO
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │        BACKEND        │
                         │ Node.js + Express     │
                         │ MongoDB + Mongoose    │
                         └───────┬────────┬──────┘
                                 │        │
                       API / Data │        │ AI Requests
                                 │        │
                                 │        ▼
                                 │ ┌──────────────────┐
                                 │ │   AI SERVICE     │
                                 │ │ FastAPI           │
                                 │ │ Scikit-learn      │
                                 │ │ NumPy / Pandas    │
                                 │ └──────────────────┘
                                 │
                                 ▼
                         ┌───────────────────────┐
                         │     MongoDB           │
                         │ Users / Farms / Loans │
                         │ Auctions / Wallets    │
                         │ Transactions / etc.   │
                         └───────────────────────┘
```

---

# 🧩 Technology Stack

## Frontend

The frontend is built with:

* **Next.js 16**
* **React 19**
* **TypeScript**
* **Tailwind CSS**
* **Axios**
* **Framer Motion**
* **Leaflet**
* **Mapbox GL**
* **Recharts**
* **Socket.IO Client**
* **Razorpay**
* **Lucide React**

These dependencies are defined in the current frontend package configuration.

---

## Backend

The backend uses:

* **Node.js**
* **Express 5**
* **MongoDB**
* **Mongoose**
* **JWT**
* **bcrypt**
* **Socket.IO**
* **Nodemailer**
* **Razorpay**
* **Telegram Bot API**
* **dotenv**

These dependencies are defined in the backend package configuration.

---

## AI Service

The AI service uses:

* **Python**
* **FastAPI**
* **Uvicorn**
* **Pydantic**
* **Scikit-learn**
* **NumPy**
* **Pandas**

---

# 📂 Project Structure

```text
agrisphere/
│
├── ai-service/
│   ├── models/
│   ├── predictors/
│   ├── main.py
│   ├── schemas.py
│   └── requirements.txt
│
├── backend/
│   ├── config/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── scripts/
│   ├── services/
│   ├── .env.template
│   ├── package.json
│   ├── server.js
│   └── diag.js
│
├── frontend/
│   ├── public/
│   ├── src/
│   ├── .gitignore
│   ├── eslint.config.mjs
│   ├── next.config.ts
│   ├── package.json
│   ├── postcss.config.mjs
│   └── tsconfig.json
│
├── .gitignore
└── README.md
```

The current repository structure contains the three major application layers shown above.

---

# 🔄 End-to-End Workflow

```text
                 👨‍🌾 Farmer
                     │
                     ▼
              ┌──────────────┐
              │   Frontend   │
              └──────┬───────┘
                     │
                     ▼
              ┌──────────────┐
              │   Backend    │
              └──────┬───────┘
                     │
       ┌─────────────┼──────────────┐
       │             │              │
       ▼             ▼              ▼
     Farms         Finance       Marketplace
       │             │              │
       │             ▼              ▼
       │          Credit          Auction
       │          / Loans          / Sales
       │
       ▼
   AI Service
       │
   ┌───┼───────────────┐
   │   │               │
   ▼   ▼               ▼
Yield Crop Health   Growth
     Analysis       Forecast
       │
       └───────────────┐
                       ▼
                Farmer Insights
                       │
                       ▼
                 Action Room
```

---

# 🧠 AI Intelligence Layer

The current AI service exposes the following core endpoints:

| Endpoint                     | Purpose                       |
| ---------------------------- | ----------------------------- |
| `GET /`                      | AI service health/status      |
| `POST /predict-yield`        | Predict agricultural yield    |
| `POST /crop-health-analysis` | Analyze crop health           |
| `POST /growth-forecast`      | Forecast NDVI growth          |
| `POST /credit-score`         | Calculate farmer credit score |

These endpoints are implemented in the current FastAPI service.

---

# 📊 Yield Prediction

The baseline yield model uses a Random Forest Regressor with four features:

```text
┌─────────────────┐
│ Soil Moisture   │
├─────────────────┤
│ Temperature     │
├─────────────────┤
│ Nitrogen Level  │
├─────────────────┤
│ Farm Size       │
└────────┬────────┘
         │
         ▼
   Random Forest
         │
         ▼
  Predicted Yield
```

The current implementation trains the baseline model from a small in-code historical dataset during startup.

This makes the current AI service a **functional prototype/baseline**, rather than a production-trained agricultural model.

---

# 🛰️ Crop Intelligence

The crop-health service accepts NDVI values and soil-moisture information.

It produces:

```text
NDVI
 │
 ├── Average NDVI
 │
 ├── Health Status
 │
 ├── Moisture Stress
 │
 ├── Pest Risk
 │
 └── Recommendations
```

---

# 💳 Farmer Credit Intelligence

AgriSphere connects agricultural performance and financial information into a credit-scoring workflow.

```text
Annual Income
     +
Average Yield Value
     +
Loan Default History
     │
     ▼
Credit Score
     │
     ├── Risk Category
     ├── Eligibility
     ├── Recommended Loan
     └── Farmer Tier
```

The current algorithm uses income, yield value, and previous defaults with fixed weights/penalties.

---

# 🛍️ Agricultural Digital Market

The marketplace layer is designed to connect:

```text
                 AGRISPHERE MARKET
                       │
       ┌───────────────┼───────────────┐
       ▼               ▼               ▼
    Farmer           Buyer           Trader
       │               │               │
       └───────────────┼───────────────┘
                       ▼
                 Crop Listings
                       │
                       ▼
                    Auctions
```

The backend contains dedicated crop-listing, marketplace, and auction models/controllers/routes.

---

# 🔐 Authentication & Security

The backend stack includes:

* JWT authentication
* Password hashing with bcrypt
* Environment-variable configuration
* CORS
* Role-oriented application architecture

The backend dependencies include `jsonwebtoken`, `bcryptjs`, `cors`, and `dotenv`.

> Never commit production credentials, database passwords, payment keys, Telegram tokens, or other secrets to GitHub.

---

# 💬 Communication & Integrations

The backend currently includes dependencies for:

### 📧 Email

Nodemailer is included for email-based communication.

### 🤖 Telegram

The Node Telegram Bot API package is included for Telegram-based communication.

### 💳 Payments

Razorpay support is included in both the backend and frontend.

### ⚡ Real-Time Communication

Socket.IO is included on both the backend and frontend for real-time application communication.

---

# 🚀 Getting Started

## Prerequisites

Install:

* Node.js
* npm
* Python 3.x
* MongoDB
* Git

---

## 1. Clone the Repository

```bash
git clone https://github.com/Devadharshan619/agrisphere.git
cd agrisphere
```

---

# 2. Backend Setup

```bash
cd backend
npm install
```

Create your environment file from the provided template:

```bash
cp .env.template .env
```

On Windows PowerShell:

```powershell
Copy-Item .env.template .env
```

Configure the required database, authentication, payment, email, and external-service variables.

### Start Backend

Development:

```bash
npm run dev
```

Production-style start:

```bash
npm start
```

The current backend package defines both `dev` and `start` scripts, plus a database seeding script.

---

# 3. AI Service Setup

Open another terminal:

```bash
cd ai-service
```

Create a Python environment:

```bash
python -m venv venv
```

### Windows

```powershell
venv\Scripts\activate
```

### Linux / macOS

```bash
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Start the FastAPI service:

```bash
uvicorn main:app --reload
```

The AI service is implemented with FastAPI and exposes the agricultural intelligence endpoints described above.

---

# 4. Frontend Setup

Open another terminal:

```bash
cd frontend
npm install
```

Start development mode:

```bash
npm run dev
```

The current frontend is a Next.js application and its package configuration defines `dev`, `build`, `start`, and `lint` scripts.

Open:

```text
http://localhost:3000
```

---

# 🏃 Running the Full Platform

For local development, run the three services separately:

```text
Terminal 1
──────────
Backend
npm run dev

        │
        ▼

Terminal 2
──────────
AI Service
uvicorn main:app --reload

        │
        ▼

Terminal 3
──────────
Frontend
npm run dev
```

Architecture:

```text
Browser
   │
   ▼
Next.js :3000
   │
   ▼
Node.js / Express
   │
   ├──────────► MongoDB
   │
   └──────────► FastAPI AI Service
                       │
                       ├── Yield
                       ├── Crop Health
                       ├── Growth Forecast
                       └── Credit Score
```

---

# 🧪 Current Prototype Status

AgriSphere is currently structured as a **full-stack prototype** with several functional modules and an AI intelligence layer.

Some AI functionality is intentionally implemented as baseline/simulation logic. For example, the current yield model trains on a small hard-coded dataset, the growth forecast introduces simulated noise, and crop-health outputs use rule-based thresholds.

This architecture provides a foundation for replacing the prototype logic with:

* Real agricultural datasets
* Satellite-derived features
* Historical farm records
* Calibrated yield models
* Production credit models
* Real crop-health models

without redesigning the entire platform.

---

# 🔮 Future Roadmap

## 🛰️ Advanced Satellite Intelligence

Integrate satellite data pipelines such as:

* Sentinel-2
* Landsat
* NDVI
* NDWI
* NDBI
* EVI
* SAVI

for deeper spatial and temporal farm analytics.

---

## 🤖 Production AI Models

Replace baseline models with trained agricultural models using:

* Historical yield datasets
* Weather data
* Soil data
* Satellite features
* Crop-specific models
* Regional agricultural datasets

---

## 📈 Advanced Forecasting

Future versions can incorporate:

* Time-series forecasting
* Weather prediction
* Seasonal trends
* Crop growth curves
* Drought indicators
* Water-stress prediction

---

## 🏦 Financial Intelligence

Potential enhancements:

* Explainable credit scoring
* Alternative credit signals
* Repayment prediction
* Loan-risk forecasting
* Financial institution dashboards
* Automated document verification

---

## 🌾 Agricultural Marketplace

Future versions can introduce:

* Real-time commodity pricing
* Demand prediction
* Buyer recommendations
* Crop price forecasting
* Smart auctions
* Supply-chain tracking

---

## 🌍 Scalable Agriculture Ecosystem

The long-term architecture can evolve toward:

```text
Satellite Data
      +
Weather Data
      +
Soil Data
      +
Farm Data
      +
Market Data
      +
Financial Data
      │
      ▼
┌──────────────────────┐
│   AGRISPHERE AI      │
│ Intelligence Layer   │
└──────────┬───────────┘
           │
     ┌─────┼─────┐
     ▼     ▼     ▼
  Farmer Buyer Finance
     │     │     │
     └─────┼─────┘
           ▼
   Intelligent Agriculture
       Ecosystem
```

---

# 🎯 Key Project Objectives

### 🌱 1. Digitize Farm Management

Bring farm-related information into a structured digital platform.

### 🤖 2. Apply AI to Agriculture

Convert agricultural data into predictions, health indicators, and recommendations.

### 💳 3. Improve Financial Access

Use agricultural and financial information to support data-driven credit decisions.

### 🛒 4. Connect Farmers to Markets

Enable digital crop listings, buyer interaction, and auctions.

### 🤝 5. Convert Insights into Actions

Use the Action Room architecture to move from analytics toward structured decision-making.

---

# 📌 Project Highlights

```text
                    🌱 AGRISPHERE
                         │
       ┌─────────────────┼─────────────────┐
       │                 │                 │
       ▼                 ▼                 ▼
  Farm Intelligence   Finance          Marketplace
       │                 │                 │
       ▼                 ▼                 ▼
 Crop Health         Credit Score       Listings
 Yield Prediction    Loans              Auctions
 Growth Forecast     Wallet             Buyers
       │                 │                 │
       └─────────────────┼─────────────────┘
                         │
                         ▼
                  🤖 AI Intelligence
                         │
                         ▼
                  👨‍🌾 Farmer
                  Decision Support
```

---

# 📚 Learning & Technical Scope

This project demonstrates practical integration of:

* Full-stack web development
* Next.js
* React
* TypeScript
* Node.js
* Express
* MongoDB
* Mongoose
* REST APIs
* Socket.IO
* FastAPI
* Machine Learning
* Random Forest
* NDVI-based analysis
* Agricultural analytics
* Credit scoring
* Digital payments
* Email automation
* Telegram integration
* Marketplace architecture
* Modular backend design

---

# 👨‍💻 Author

## Devadharshan

Computer Science Engineering — Artificial Intelligence & Machine Learning

GitHub:

https://github.com/Devadharshan619

---

# ⭐ Support

If you find AgriSphere interesting:

⭐ Star the repository
🍴 Fork the project
🐛 Report issues
💡 Suggest improvements
🤝 Contribute to the project

---

# 📜 License

This project currently does not specify a dedicated open-source license in the repository.

If you intend to make AgriSphere openly reusable, consider adding an appropriate license.

---

# 🌱 AgriSphere

> **From farm data to intelligent decisions.**

**Monitor. Predict. Finance. Trade. Act.**

AgriSphere brings agricultural intelligence, financial access, and digital markets together into one connected ecosystem.
