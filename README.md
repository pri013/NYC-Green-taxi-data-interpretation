<h1 align="center">🚕 NYC Green Taxi Tip Prediction</h1>
<h3 align="center">Using CRISP-DM Methodology & k-NN Regression Modeling</h3>

<p align="center">
  <img src="https://img.shields.io/badge/R-4.0+-276DC3?style=for-the-badge&logo=r&logoColor=white" alt="R">
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License">
  <img src="https://img.shields.io/badge/Status-Completed-success?style=for-the-badge" alt="Status">
</p>

<p align="center">
  <i>A machine learning project that predicts tip amounts for NYC Green Taxi trips using k-Nearest Neighbors regression on 2018 trip data.</i>
</p>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Methodology](#-methodology)
- [Results](#-results)
- [Key Insights](#-key-insights)
- [Usage](#-usage)
- [References](#-references)
- [Author](#-author)

---

## 🎯 Overview

This project analyzes **NYC Green Taxi trip data from 2018** to:

1. **Predict tip amounts** using k-NN regression
2. **Understand tipping patterns** based on trip characteristics  
3. **Analyze operational efficiency** across different times and days

### Why Green Taxis?

> Green taxis (Boro Taxis) serve areas outside Manhattan's core, providing valuable insights into outer-borough transportation patterns.

---

## 📊 Dataset

| Attribute | Description |
|-----------|-------------|
| **Source** | [NYC Taxi & Limousine Commission](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) |
| **Period** | January - February 2018 |
| **Original Size** | 1,048,575 rows × 19 columns |
| **Cleaned Size** | 531,855 rows × 26 columns |

### Key Variables

| Variable | Type | Description |
|----------|------|-------------|
| `tip_amount` | Target | Tip amount in USD (credit card only) |
| `trip_distance` | Numeric | Distance traveled in miles |
| `fare_amount` | Numeric | Base fare in USD |
| `passenger_count` | Numeric | Number of passengers (1-6) |
| `overnight_surcharge` | Binary | 1 if pickup between 8PM-6AM |
| `rush_hour_surcharge` | Binary | 1 if pickup 4PM-8PM weekdays |
| `efficiency_ratio` | Engineered | Ratio of actual fare to expected fare |

---

## 📁 Project Structure

```
nyc-green-taxi-tip-prediction/
│
├── 📂 data/
│   ├── 2018_Green_Taxi_Trip_Data.csv
│   └── taxi_zone_lookup.csv
│
├── 📂 images/
│   ├── 01_actual_vs_predicted.png
│   ├── 02_avg_distance_by_hour.png
│   ├── 03_top_dropoff_5am.png
│   ├── 04_efficiency_heatmap.png
│   ├── 05_airport_trips_by_hour.png
│   ├── 06_mse_vs_k.png
│   ├── 07_short_rides_by_hour.png
│   └── 08_efficiency_weekday_weekend.png
│
├── 📄 NYC-Green-Taxi-Data-Model.Rmd
├── 📄 NYC-Green-Taxi-Data-Model.html
├── 📄 README.md
└── 📄 LICENSE
```

---

## 🛠️ Installation

### Prerequisites

- R (version 4.0 or higher)
- RStudio (recommended)

### Required Packages

```r
install.packages(c(
  "tidyverse",
  "lubridate", 
  "psych",
  "correlation",
  "caret",
  "FNN"
))
```

### Clone Repository

```bash
git clone https://github.com/yourusername/nyc-green-taxi-tip-prediction.git
cd nyc-green-taxi-tip-prediction
```

---

## 🔬 Methodology

This project follows the **CRISP-DM** (Cross-Industry Standard Process for Data Mining) framework:

### 1️⃣ Business Understanding

- Predict tip amounts to help drivers optimize earnings
- Identify factors that influence tipping behavior

### 2️⃣ Data Understanding & Exploration

**Summary Statistics for Tip Amount:**

| Statistic | Value |
|-----------|-------|
| Minimum | $0.00 |
| Median | $1.58 |
| Mean | $1.88 |
| Maximum | $50.00 |

### 3️⃣ Data Preparation

#### Data Cleaning Steps

| Step | Action | Rows Affected |
|------|--------|---------------|
| 1 | Remove missing values | ~8 rows |
| 2 | Keep credit card payments only | ~462,566 removed |
| 3 | Filter trip duration (1-180 min) | ~27,000 removed |
| 4 | Remove passenger counts > 6 | 3 removed |
| 5 | Remove incorrect dates (2009) | 9 removed |
| 6 | Remove zero-distance anomalies | ~415 removed |
| 7 | Remove tips > 35% of fare | ~21,000 removed |
| 8 | Remove tolls > $25 | 17 removed |

#### Feature Engineering

```r
# New features created
trip_duration_minutes  <- difftime(dropoff, pickup, units="mins")
speed_of_taxi          <- trip_distance / (trip_duration_minutes / 60)
efficiency_ratio       <- (fare_amount - 2.5) / (trip_distance * 2.5)
overnight_surcharge    <- ifelse(hour >= 20 | hour < 6, 1, 0)
rush_hour_surcharge    <- ifelse(hour >= 16 & hour < 20 & weekday, 1, 0)
```

#### Normalization Pipeline

1. **Log transformation** → Handle skewed distributions
2. **Min-Max scaling** → Scale all features to [0, 1]

### 4️⃣ Modeling

**Algorithm:** k-Nearest Neighbors (k-NN) Regression

**Why k-NN?**
- Non-parametric (no assumptions about data distribution)
- Intuitive interpretation
- Works well with normalized numerical features

**Selected Features:**

| Included ✅ | Excluded ❌ (Low Correlation) |
|------------|------------------------------|
| passenger_count | VendorID (-0.03) |
| log_trip_distance | PULocationID (0.01) |
| log_fare_amount | extra (0.03) |
| log_total_amount | mta_tax (-0.07) |
| efficiency_ratio | pickup_day (0.01) |
| log_speed_of_taxi | pickup_hour (0.02) |
| overnight_surcharge | tolls_amount |
| rush_hour_surcharge | - |

**Train/Test Split:** 70% Training / 30% Testing

### 5️⃣ Evaluation

<img width="458" height="289" alt="number of neighbors k " src="https://github.com/user-attachments/assets/7a15c77a-436c-4a94-a5ec-6c40463b795c" />

<p align="center"><i>Figure 1: MSE vs. Number of Neighbors (k) - Optimal k = 5</i></p>

The MSE vs. k plot demonstrates that the KNN model achieves optimal predictive performance when **k = 5**. At this point, the model balances bias and variance effectively.

---

## 📈 Results

### Model Performance

<table align="center">
  <tr>
    <td align="center"><h3>5</h3><p>Optimal k</p></td>
    <td align="center"><h3>0.000163</h3><p>MSE (normalized)</p></td>
    <td align="center"><h3>372,298</h3><p>Training Samples</p></td>
    <td align="center"><h3>159,557</h3><p>Test Samples</p></td>
  </tr>
</table>

### Actual vs Predicted Tip Amounts

<img width="469" height="289" alt="actual vs predicted amount" src="https://github.com/user-attachments/assets/7e90d045-710e-4afd-a280-247c66cbc548" />

<p align="center">
  <img src="images/01_actual_vs_predicted.png" alt="Actual vs Predicted Tip Amounts" width="700">
</p>
<p align="center"><i>Figure 2: Actual vs Predicted Tip Amounts - Points near the red dashed line indicate accurate predictions</i></p>

### Prediction Quality by Tip Range

| Tip Range | Performance | Rating |
|-----------|-------------|--------|
| $0 - $5 | Good | ⭐⭐⭐⭐ |
| $5 - $15 | Excellent | ⭐⭐⭐⭐⭐ |
| $15 - $25 | Moderate | ⭐⭐⭐ |
| > $25 | Underestimates | ⭐⭐ |

### Example Prediction

```
Test Example #5:
├── Predicted tip: $4.94
├── Actual tip:    $4.96
└── Error:         $0.02 (0.4%)
```

**Key Observations:**
- ✅ Strong performance for tips in $5–$15 range
- ✅ Dense clustering near the diagonal line shows good predictions for frequent, small tips
- ⚠️ Underestimates high tip amounts (>$20) due to rarity in training data

---

## 💡 Key Insights

### 1️⃣ Optimal Operating Hours

<img width="433" height="290" alt="heatmap" src="https://github.com/user-attachments/assets/57ef4dfc-89b2-4d19-afe6-faf2b8198c98" />

<p align="center">
  <img src="images/04_efficiency_heatmap.png" alt="Efficiency Heatmap" width="700">
</p>
<p align="center"><i>Figure 3: Average Efficiency Ratio by Pickup Hour and Day - Yellow box highlights optimal period (7AM-6PM Mon-Fri)</i></p>

> **Finding:** Best operational efficiency occurs during **7AM-6PM, Monday-Friday**

### 2️⃣ Weekday vs Weekend Efficiency

<img width="465" height="296" alt="weekday to weekend avg " src="https://github.com/user-attachments/assets/e9b7c7ec-00e3-4600-a908-17ef3f55fa89" />


<p align="center"><i>Figure 4: Average Efficiency Ratio by Hour - Weekday vs Weekend comparison</i></p>

> **Finding:** Weekday efficiency is consistently higher than weekends during business hours (6AM-6PM)

### 3️⃣ Early Morning Airport Rush

<img width="456" height="290" alt="avg distance" src="https://github.com/user-attachments/assets/94ebcaff-0bfc-471e-9c58-446fd82f82e5" />

<p align="center"><i>Figure 5: Average Trip Distance by Hour - Spike at 5AM indicates airport trips</i></p>

<img width="458" height="298" alt="drop off " src="https://github.com/user-attachments/assets/117494b6-f35c-43ea-9377-707a91496d6d" />

<p align="center"><i>Figure 6: Top Drop-off Locations at 5AM - Airports dominate early morning destinations</i></p>

> **Finding:** 5AM efficiency dip is caused by long airport trips

**Top 5AM Destinations:**

| Rank | Location | Trips |
|------|----------|-------|
| 1 | LaGuardia Airport | 223 |
| 2 | JFK Airport | 120 |
| 3 | Upper East Side North | 79 |
| 4 | Midtown Center | 72 |
| 5 | Times Square | 63 |

**5AM Passenger Profile:** 84% solo travelers (likely commuters), Average distance: 5.2 miles

### 4️⃣ Airport Trips Distribution
<img width="512" height="296" alt="long trip" src="https://github.com/user-attachments/assets/41945fc7-2f51-4980-86a5-579394f1beb0" />

<p align="center"><i>Figure 7: Airport Trips by Hour on Weekdays - Peak during afternoon rush hour</i></p>

> **Finding:** While 5AM shows airport activity, the majority of airport trips occur during afternoon rush hour (3PM-6PM)

### 5️⃣ Evening Traffic Impact

<img width="485" height="289" alt="short rides" src="https://github.com/user-attachments/assets/4d2afb30-05a8-45fa-afaa-773c3bac8f33" />

<p align="center"><i>Figure 8: Rides Under 1 Mile by Hour - Peak during evening hours (6PM-9PM)</i></p>

> **Finding:** Post-6PM efficiency drop is due to increased short/aborted rides, likely caused by passengers exiting taxis stuck in traffic

**Short Rides Peak Hours:**

| Hour | Count | Observation |
|------|-------|-------------|
| 6 PM | ~7,000 | High |
| 7 PM | ~8,300 | **Peak** |
| 8 PM | ~8,000 | High |
| 9 PM | ~6,800 | Declining |

---

## 🎯 Conclusions

1. **Model Performance:** k-NN with k=5 achieves good prediction accuracy for typical tips ($5-$15)

2. **Optimal Hours:** Drivers achieve best efficiency during weekday business hours (7AM-6PM)

3. **Morning Dip Explained:** Early morning (4-6AM) efficiency drops due to long airport trips

4. **Evening Dip Explained:** Post-6PM efficiency drops due to traffic congestion causing short/aborted rides

5. **Recommendation:** Green taxi drivers should prioritize weekday business hours for optimal earnings efficiency

---

## 🚀 Usage

### Running the Analysis

1. Open `NYC-Green-Taxi-Data-Model.Rmd` in RStudio
2. Ensure data files are in the `data/` folder
3. Click "Knit" to generate the HTML report

### Making Predictions

```r
# After running the notebook
result <- knn.predict(train_data, test_data, k = 5, return_preds = TRUE)
```

---

## 🔮 Future Improvements

| Improvement | Description | Priority |
|-------------|-------------|----------|
| 🌲 Random Forest | Try ensemble methods for better accuracy | High |
| 📍 Location Features | Encode pickup/dropoff zones | High |
| 🌧️ Weather Data | Add external weather conditions | Medium |
| 📈 Time Series | Capture seasonal patterns | Medium |
| 🌐 API Deployment | Real-time prediction service | Low |

---

## 📚 References

1. **NYC TLC Trip Data** - NYC Taxi & Limousine Commission (2018)  
   https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

2. **NYC Taxi Regulations** - NYC311  
   https://portal.311.nyc.gov/article/?kanumber=KA-01245

3. **NYC Taxi Fare Structure** - NYC TLC (2019)  
   https://web.archive.org/web/20190722151033/https://www.nyc.gov/site/tlc/passengers/taxi-fare.page

4. **NYC Traffic Study** - Corrado, K. (2021). PIX11 News  
   https://pix11.com/news/local-news/nyc-worst-traffic-in-country-study-finds/

---

## 👤 Author

**Priya Dhumal**

[![GitHub](https://github.com/pri013/NYC-Green-taxi-data-interpretation)
[![LinkedIn](www.linkedin.com/in/priya13d)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <b>⭐ If you found this project helpful, please give it a star! ⭐</b>
</p>
