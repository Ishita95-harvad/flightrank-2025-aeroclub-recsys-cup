# ✈️FlightRank 2025: Aeroclub RecSys Cup

**Personalized Flight Recommendations for Business Travelers**
---
![FlightRank Header](https://github.com/Ishita95-harvad/flightrank-2025-aeroclub-recsys-cup/blob/main/header.jpg)

A data-driven journey into flight recommendation systems. Presented by Aeroclub for the RecSys Cup 2025, this visual blends aviation with algorithmic precision—featuring a stylized aircraft built from numerical data points, set against a sleek grid backdrop. Innovation takes flight.

***

## 🧭 Challenge Overview

**Objective:**  
Predict which flight option a business traveler will select from a set of candidates in a search session (`ranker_id`).  
This is a **learning-to-rank** problem with one positive label (`selected = 1`) per group.

**Submission Format:**  
Ranked list of flight options per `ranker_id` in the test set.

---

## 📁 Dataset Components

| File | Description |
|------|-------------|
| `train.parquet` | Training data with labeled selections |
| `test.parquet` | Test data for prediction |
| `sample_submission.parquet` | Format example for submission |
| `jsons_raw.tar.kaggle` → `.gz` | Optional raw JSON data (~50GB) for feature enrichment |
| `jsons_structure.md` | Schema for JSON files |

---

## 🧩 Key Data Structures

### 🔹 Grouping
- `ranker_id`: Defines a search session (group of flight options)
- Each group has **exactly one** selected flight in training

### 🔹 User Features
- `profileId`, `sex`, `nationality`, `frequentFlyer`, `isVip`, `bySelf`, `isAccess3D`

### 🔹 Company Features
- `companyID`, `corporateTariffCode`

### 🔹 Flight Features
- Route: `searchRoute`, `requestDate`
- Price: `totalPrice`, `taxes`
- Timing: `legs0_*`, `legs1_*` (departure, arrival, duration)
- Segments: up to 4 per leg, with detailed airline, aircraft, baggage, cabin class, etc.

### 🔹 Rules & Policies
- Cancellation: `miniRules0_*`
- Exchange: `miniRules1_*`
- Corporate compliance: `pricingInfo_isAccessTP`

---

## 🛠️ Modeling Strategy Suggestions

### 1. Feature Engineering
- Normalize time features (e.g., convert to hours since request)
- Encode route types (round trip vs one-way)
- Aggregate segment-level features (e.g., total layover time, number of stops)
- Use company and user flags to model preferences (e.g., VIPs may prefer business class)

### 2. Ranking Models
- Use **pairwise** or **listwise** approaches:
  - XGBoost with group ranking
  - LightGBM with `group_id = ranker_id`
  - LambdaMART or CatBoost ranking
- Consider **deep learning** with attention over segments or transformer-based encoders

### 3. Raw JSON Enrichment (Optional)
- Extract additional metadata (e.g., fare class, booking channel)
- Use NLP on textual fields (if present) for embeddings
- Be mindful of storage and compute—preprocess into structured format

---

## 🎯 Evaluation Tips

- Focus on **intra-group ranking accuracy** (e.g., NDCG, MAP)
- Validate using **group-wise cross-validation** to avoid leakage
- Consider interpretability for business use cases (e.g., SHAP values)

---

## ✨ Visual & Narrative Ideas for Presentation

- Stylized aircraft made of data points: visualize feature importance as aircraft components (e.g., wings = price, engine = timing)
- Grid backdrop: represent search sessions as flight paths on a grid
- “Innovation takes flight”: use animated ranking trajectories or heatmaps of user preferences
