# British Airways — Data Science Job Simulation
### Forage Data Science Virtual Experience Programme

---

## Project Overview

This project was completed as part of the **British Airways Data Science Job Simulation** on Forage. It consists of two tasks that tackle real-world data challenges faced by BA's teams:

- **Task 1** — Building a lounge eligibility demand model for Heathrow Terminal 3
- **Task 2** — Predicting customer booking behaviour using machine learning

---

## File Structure

```
BA-Data-Science-Simulation/
│
├── README.md                          # Project overview (this file)
├── Lounge_Eligibility_Lookup.xlsx     # Task 1 Excel workbook
│   ├── Sheet 1 - Raw Data             # Flight schedule sample (1st May 2025)
│   ├── Sheet 2 - Calculations         # Pivot table with averaged tier percentages
│   ├── Sheet 3 - Lookup Table         # Final reusable lookup table with notes
│   └── Sheet 4 - Worked Example       # 13 sample flights with categories applied
├── Task_2.ipynb                       # Task 2 Jupyter notebook (full ML pipeline)
└── British_Airways_Task_2.pptx        # Task 2 summary slide for stakeholders
```

---

---

# Task 1 — Lounge Eligibility Demand Model

## Problem Statement

British Airways needs to anticipate how many passengers will be eligible to use each lounge on a typical day at Heathrow T3. Since future schedules can change, the planning team needed a model based on flight groupings rather than specific flight numbers or aircraft types.

## Tools Used
- **Microsoft Excel** — data filtering, formula calculations, pivot tables

## Methodology

### 1. Data Sample
A sample of **58 flights** from **1st May 2025** was extracted from the full BA flight schedule as a representative single-day dataset.

### 2. Flight Groupings
Flights were grouped using three dimensions:
- **Arrival Region** — Asia, Europe, Middle East, North America
- **Haul Type** — Short-haul or Long-haul
- **Time of Day** — Morning, Lunchtime, Afternoon, Evening

These were combined into category labels such as `Long-haul Morning - Middle East` or `Short-haul Morning - Europe`.

### 3. Eligibility Calculation
For each flight, tier eligibility percentages were calculated using actual passenger data:

```
Tier 1 % = TIER1_ELIGIBLE_PAX ÷ Total Seats × 100
Tier 2 % = TIER2_ELIGIBLE_PAX ÷ Total Seats × 100
Tier 3 % = TIER3_ELIGIBLE_PAX ÷ Total Seats × 100
```

### 4. Lookup Table
A pivot table was used to average the percentages within each category grouping, producing a clean, reusable lookup table.

## Lounge Tiers

| Tier | Lounge | Eligibility |
|------|--------|-------------|
| Tier 1 | Concorde Room *(hypothetical at T3)* | First class cabin + Gold Executive Club |
| Tier 2 | First Lounge | Business class + oneworld Emerald |
| Tier 3 | Club Lounge | Silver Executive Club + oneworld Sapphire |

> **Note:** There is currently no Concorde Room at Terminal 3. Tier 1 estimates reflect passengers who would qualify for that level of service and are intended to inform whether a Tier 1 lounge may be needed in the future.

## Key Findings

- **Middle East Morning flights** had the highest Tier 3 eligibility at **26%**, suggesting a strong frequent flyer base on these routes
- **Europe Short-haul** flights had **0–1% Tier 1 eligibility** as BA does not operate a First cabin on short-haul services
- **Morning departures** consistently showed higher eligibility across all tiers, reflecting the higher proportion of business travellers on early flights
- **Asia and North America** long-haul routes showed moderate but consistent eligibility, driven by corporate travel patterns
- **Evening flights** across all regions showed the lowest eligibility, indicating a more leisure-focused passenger mix

## How to Use the Lookup Table

1. Identify the **arrival region** of the flight (Asia, Europe, Middle East, North America)
2. Identify the **haul type** (short-haul or long-haul)
3. Identify the **time of day** (morning, lunchtime, afternoon, evening)
4. Find the matching row in the lookup table
5. Multiply the tier percentages by the expected passenger count to estimate lounge demand

---

---

# Task 2 — Predicting Customer Booking Behaviour

## Problem Statement

British Airways wanted to understand what drives customers to complete a booking. With an **85/15 class imbalance** (most customers don't complete bookings), the challenge was to build a model that could reliably identify customers likely to book.

## Tools Used
- **Python** — pandas, scikit-learn, matplotlib
- **Jupyter Notebook** — full analysis and modelling pipeline
- **PowerPoint** — stakeholder summary slide

## Methodology

### 1. Exploratory Data Analysis
- Examined 50,000 customer booking records across 14 features
- Identified significant class imbalance: 85% did not complete bookings, 15% did
- Converted `flight_day` from text to numeric values

### 2. Feature Engineering
New features created to improve model performance:
- `is_weekend` — whether the flight falls on a weekend
- `total_add_ons` — sum of extra baggage, in-flight meals and preferred seat requests
- `route_freq` — frequency encoding of routes (busier routes assigned higher values)
- `booking_region` — countries mapped to 10 world regions using one-hot encoding

### 3. Encoding Strategy
- **Label Encoding** used for `sales_channel` and `trip_type` — safe for Random Forest as it splits on thresholds, not order
- **Frequency Encoding** used for `route` — avoids the problem of 800+ dummy variables
- **One-Hot Encoding** used for `booking_region` — captures regional booking patterns meaningfully

### 4. Model Training
```
Random Forest Classifier
- n_estimators = 200
- max_depth = 15
- class_weight = balanced
- train/test split = 80/20
```
`class_weight='balanced'` was used to handle the class imbalance without discarding data.

### 5. Model Evaluation

| Metric | Score |
|--------|-------|
| Accuracy | 78.55% |
| ROC-AUC | 77.23% |
| Recall (bookers) | 52% |
| Precision (bookers) | 35% |

## Key Findings

- **Route frequency** was the strongest predictor — busier routes have more committed bookers
- **Purchase lead time** was the second strongest — customers who book earlier are more likely to complete
- **Length of stay** reflects customer planning behaviour and correlates with booking completion
- **Southeast Asia and Oceania** were strong regional predictors of booking completion
- **Middle East, South America and Central Asia** had near-zero importance
- **Add-on preferences** (extra baggage, meals, seat) had low predictive importance — they don't reliably indicate whether someone will complete a booking

## Model Limitations

- Precision of 35% means the model generates false alarms — 65 out of every 100 predicted bookers don't actually book
- Recall of 52% means roughly half of real bookers are missed
- ROC-AUC of 77.23% confirms the model is genuinely useful but has room for improvement

---

## About This Simulation

This project was completed as part of the **British Airways Data Science Virtual Experience Programme** hosted on [Forage](https://www.theforage.com). The simulation provides hands-on experience with real-world data challenges faced by BA's data science and airport planning teams.
## Connect With Me
[LinkedIn](https://www.linkedin.com/in/gayatri-londhe-/)
