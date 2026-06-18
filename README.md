# automatidata-nyc-tlc-eda

**Course 2 End-of-Course Project | Google Advanced Data Analytics Certificate**  
*Go Beyond the Numbers: Translate Data into Insights*

---

## Project Overview

This project continues the fictional Automatidata workplace scenario. As a data analyst at **Automatidata**, I conducted a full **Exploratory Data Analysis (EDA)** on the 2017 NYC Yellow Taxi Trip dataset on behalf of the **New York City Taxi & Limousine Commission (TLC)**. The goal is to prepare the data for a regression model that predicts taxi fares before a ride begins.

---

## Business Goal

Build a regression model that estimates taxi fares from trip distance, time of day, and other features — enabling NYC TLC to display predicted fares to passengers before their ride starts.

---

## Dataset

**2017 Yellow Taxi Trip Data** — provided by NYC TLC

| Property | Value |
|---|---|
| Rows | 22,699 |
| Columns | 18 |
| Missing values | 0 |
| Source | NYC Taxi & Limousine Commission |

Key columns: `trip_distance`, `fare_amount` (target), `tip_amount`, `total_amount`, `tpep_pickup_datetime`, `tpep_dropoff_datetime`, `RatecodeID`, `payment_type`, `vendor_id`

> Note: This dataset was created for pedagogical purposes and may not fully reflect real NYC taxi behavior.

---

## Repository Structure

```
Course 2 - Go Beyond the Numbers Translate Data into Insights /
├── Course 2 _ Go Beyond the Numbers...project lab.py     # Main EDA script (all responses filled in)
├── Course 2 _ Go Beyond the Numbers...project lab.ipynb  # Jupyter notebook version
├── Course2_EDA_Report.docx                               # Full EDA report with all 17 visualizations
├── Course2_Executive_Summary.pptx                        # 9-slide executive presentation
├── course2_plots/                                        # All 17 generated charts (PNG, 150 DPI)
│   ├── 01_boxplot_trip_distance.png
│   ├── 02_hist_trip_distance.png
│   ├── 03_boxplot_total_amount.png
│   ├── 04_hist_total_amount.png
│   ├── 05_boxplot_tip_amount.png
│   ├── 06_hist_tip_amount.png
│   ├── 07_tip_by_vendor.png
│   ├── 08_total_amount_by_vendor.png
│   ├── 09_mean_tip_by_passenger.png
│   ├── 10_rides_by_month.png
│   ├── 11_rides_by_day.png
│   ├── 12_revenue_by_day.png
│   ├── 13_revenue_by_month.png
│   ├── 14_rides_by_hour.png
│   ├── 15_dist_vs_fare_scatter.png
│   ├── 16_correlation_heatmap.png
│   └── 17_boxplot_trip_duration.png
└── README.md
```

---

## What the Script Covers (PACE Framework)

### Plan
- Define stakeholder goals and the analytical approach
- Identify key variables: `fare_amount` (target), `trip_distance` (primary predictor), datetime features

### Analyze
- `df.head()`, `df.info()`, `df.describe()` — initial data inspection
- Distribution plots: histograms + box plots for `trip_distance`, `total_amount`, `tip_amount`
- Outlier detection: extreme values flagged for cleaning
- Vendor and payment type breakdowns

### Construct (Feature Engineering)
- `trip_duration_minutes` — from pickup/dropoff timestamps
- `pickup_hour`, `pickup_day_of_week` — temporal features
- `cost_per_mile` — derived rate metric

### Execute
- Temporal patterns: rides and revenue by day and month
- Correlation matrix: `trip_distance ↔ fare_amount` r = 0.91
- Data leakage warning: `total_amount` is derived from `fare_amount` — must not be used as a predictor
- Recommended next steps documented

---

## Key Findings

- **No missing data** — all 18 columns complete across 22,699 records
- **Primary predictor confirmed**: `trip_distance ↔ fare_amount` correlation r = 0.91
- **Data leakage risk**: `total_amount` derived from `fare_amount`; must be excluded from model features
- **Distributions are right-skewed**: most trips < 5 miles, most fares < $15, with long tails
- **Cash tip underreporting**: ~33% of trips are cash; tips recorded as $0 — tip analysis applies to credit card only
- **Temporal peaks**: Friday is highest-volume day; March and October are highest-revenue months
- **6 data quality issues** identified: negative fares, zero-distance trips, negative durations, extreme outliers, passenger count anomalies, cash tip bias

---

## Visualizations (17 Charts)

| # | Chart | Key Insight |
|---|---|---|
| 01 | Box plot — trip distance | Heavy positive skew; outliers up to 33 miles |
| 02 | Histogram — trip distance | Most trips 0–5 miles |
| 03 | Box plot — total amount | Extreme outliers (up to $1,200) |
| 04 | Histogram — total amount | Most fares $5–$20 |
| 05 | Box plot — tip amount | Concentrated near $0; long right tail |
| 06 | Histogram — tip amount | Most tips $1–$3 (credit card only) |
| 07 | Mean tip by vendor | Vendors comparable in tip behavior |
| 08 | Total amount by vendor | VeriFone slightly higher mean total |
| 09 | Mean tip by passenger count | Group rides (4–6 pax) tip marginally more |
| 10 | Rides by month | March and October peaks |
| 11 | Rides by day of week | Friday and Thursday busiest |
| 12 | Revenue by day of week | Mirrors ride volume |
| 13 | Revenue by month | March and October highest |
| 14 | Rides by pickup hour | Rush hour peaks (8am, 6–7pm) |
| 15 | trip_distance vs fare_amount scatter | Strong linear relationship; r = 0.91 |
| 16 | Correlation heatmap | Confirms trip_distance as top predictor |
| 17 | Box plot — trip duration | Outliers present; cleaning required |

---

## Recommended Next Steps

1. Clean anomalous records (negative fares, zero-distance, negative durations)
2. Investigate extreme outliers in `total_amount` (> $200)
3. Engineer `pickup_hour`, `day_of_week`, `is_weekend`, `quarter` features
4. Include `RatecodeID` — encodes airport rate codes (JFK, Newark) that explain long-distance outliers
5. Apply A/B statistical testing (per Udo Bankole's recommendation)
6. Build Tableau dashboard with NYC map of trip density by month
7. Proceed to Course 3: regression model construction

---

## Tools & Technologies

- Python 3 | pandas | numpy | matplotlib | seaborn | datetime
- Jupyter Notebook / Python script
- Microsoft Word (EDA report)
- Microsoft PowerPoint (executive summary)

---

## Author

**Walid** | Data Analyst at Automatidata (fictional scenario)  
Google Advanced Data Analytics Certificate — Course 2

---

## Related

- **Course 1 repo**: `automatidata-nyc-tlc-foundations` — initial data inspection and PACE strategy
