# 🛩️ RC Telemetry Flight Analysis — July 1st, 2025  
**Aircraft**: E-flite T-28 Trojan | **Location**: Cherry Creek State Park, Colorado

---

## 🔧 PROJECT OVERVIEW

This is a personal data science project that explores real-world RC flight telemetry from a standalone GPS logger (SM Modellbau GPS Logger 3) mounted on a beginner-level aircraft. The objective was to practice data wrangling, engineering, visualization, and basic modeling using R — all with no live transmitter, no soldering, and beginner RC hardware.

The final goal: **predict flight altitude** using only basic onboard telemetry.

---

## 🛠️ HARDWARE & LOGGING SETUP

| Component          | Description |
|-------------------|-------------|
| RC Plane           | E-flite T-28 Trojan (Park Flyer) |
| Logger             | SM Modellbau GPS Logger 3 (Vario mode) |
| Power              | 1S LiPo battery (via JR-style servo adapter) |
| Transmitter        | DX6e (no telemetry) |
| Logging Mode       | Standalone (no receiver/soldering) |
| Data Storage       | microSD card (1Hz telemetry logging) |

This simple and low-cost setup let us collect real telemetry with no live feed — just plug in, fly, retrieve the SD card, and analyze.

---

## 🧪 RESEARCH GOALS

- **Q1:** How fast, far, and long was the flight?
- **Q2:** What was the flight profile (altitude, speed, and motion)?
- **Q3:** Can we **predict altitude** using basic telemetry?

---

## 📁 FILE STRUCTURE


.
├── data/
│ └── 2025-07-01-GPS3-46377-0001-Vario(GPS).csv
├── output/
│ ├── 2025-07-01_T28B_cleaned.csv
│ ├── 2025-07-01_T28B_renamed.csv
│ ├── 2025-07-01_T28B_final_25cols.csv
│ ├── altitude_lm_model.rds
│ └── predicted_vs_actual_altitude.png
├── T28B_July_1st_intro_flight.Rmd
└── README.md


---

## 🧰 R TOOLS USED

- `tidyverse`
- `lubridate`, `janitor`, `skimr`
- `ggplot2`
- `yardstick` (for model metrics)
- `geosphere` (for future mapping)
- Base R for modeling (`lm()`)

---

## 🔄 PROCESS PIPELINE (Steps 0–12)

| Step | Description |
|------|-------------|
| 0    | Project setup and logging overview |
| 1    | Load raw CSV (UTF-16, `;` delimited) |
| 2    | Drop irrelevant columns + clean names |
| 3–4  | Parse and format `flight_date` and `flight_time` |
| 5–6  | Convert telemetry and sensor columns to numeric |
| 7–8  | Feature engineering: `elapsed_time_s` and `flight_phase` (4-second bins based on vertical speed) |
| 9    | Export final tidy dataset (7630 × 26) |
| 10   | Create EDA visuals (see below) |
| 11   | Build linear regression model to predict altitude |
| 12   | Visualize model results and export model files |

---

## 📊 EDA VISUALS

- Altitude Over Time
- Vertical Speed Histogram
- Acceleration (Z-axis) Over Time
- Altitude Colored by Flight Phase
- Ground Speed vs. Altitude
- 2D Flight Path (Latitude × Longitude)
- Correlation Heatmap of Numeric Columns

---

## 🔮 MODELING RESULTS

**Target**: `relative_altitude_m`  
**Predictors**:  
- `vertical_speed_mps`  
- `ground_speed_kmh`  
- `accel_z_g`  
- `flight_phase` (factor)

**Model**: Linear Regression (`lm()`)

| Metric | Value |
|--------|-------|
| RMSE   | 0.55 m |
| MAE    | 0.46 m |
| R²     | 0.9997 ✅ |

**Interpretation**:  
This simple model accurately predicts altitude using just a few telemetry variables — a strong baseline and proof-of-concept that clean, well-logged data can yield powerful insights even with basic modeling.

---

## ✨ FUTURE IDEAS

- Compare multiple flights from different days
- Try advanced models (e.g., Random Forest, XGBoost)
- Build a Shiny app for interactive flight analysis
- Add 3D flight path and animation
- Use `geosphere` to calculate true GPS distance and bearing

---

## 📬 AUTHOR INFO

Victor King  
M.S. in Sport Analytics, Syracuse University (2025)  
✉️ victorking1492@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/victormking)  
💼 [Portfolio](https://victormking.github.io/portfolio-site)  
💻 [GitHub](https://github.com/victormking)

---

## ✅ Project Status: COMPLETE

Feature engineering ✅  
EDA ✅  
Modeling ✅  
Model export + visualization ✅  

Ready for write-up and GitHub publishing!
