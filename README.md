# [✈️FlightRank 2025: Aeroclub RecSys Cup](https://www.kaggle.com/competitions/aeroclub-recsys-2025)
**Personalized Flight Recommendations for Business Travelers**

A data-driven journey into flight recommendation systems. Presented by Aeroclub for the RecSys Cup 2025, this visual blends aviation with algorithmic precision—featuring a stylized aircraft built from numerical data points, set against a sleek grid backdrop. Innovation takes flight.
---

<p align="center">
  <img src="https://raw.githubusercontent.com/Ishita95-harvad/flightrank-2025-aeroclub-recsys-cup/main/header.png" alt="FlightRank Header" width="100%">
</p>

<p align="center">
  <a href="https://www.kaggle.com/competitions/aeroclub-recsys-2025">
    <img src="https://img.shields.io/badge/Kaggle-RecSys_Cup_2025-blue?logo=kaggle" alt="Kaggle Badge">
  </a>
  <a href="https://github.com/Ishita95-harvad/flightrank-2025-aeroclub-recsys-cup/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-GPL--3.0-green" alt="License Badge">
  </a>
  <img src="https://img.shields.io/badge/Made%20with-%E2%9D%A4-GREEN" alt="Made with Love">
  <img src="https://img.shields.io/badge/Model-LightGBM-yellowgreen" alt="Model Badge">
</p>


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


## 🖼️ Project Card

![FlightRank 2025 Card](./flight_rank_linkedin_card.png)
------
### ✍️ Ending Notes from Ishita

FlightRank 2025 began as a simple question: *Can we make flight recommendations not just smarter, but fairer?* What followed was a deep dive into multimodal modeling, edge deployment, and the ethics of personalization.

This project is more than a dataset or a dashboard—it's a statement. A statement that **privacy-first AI** can be performant, that **open science** can be beautiful, and that **legal-tech principles** can guide even travel algorithms.

Whether you're a researcher, a developer, or just someone who’s tired of generic flight suggestions, I hope FlightRank sparks ideas. If it does, let’s talk. If it doesn’t, let’s improve it together.

Thanks for flying with me. ✈️  
— Ishita
-------

