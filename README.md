# 🚖 FareFlux — Taxi Fare Analysis Dashboard

> A 7-page interactive Power BI dashboard delivering end-to-end operational intelligence across **148,767 taxi booking records** (Jan–Dec 2024).

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-5-blue?style=for-the-badge)
![Records](https://img.shields.io/badge/Records-148%2C767-green?style=for-the-badge)
![Pages](https://img.shields.io/badge/Dashboard%20Pages-7-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Problem Statement](#-problem-statement)
- [Dashboard Pages](#-dashboard-pages)
- [Key Metrics & KPIs](#-key-metrics--kpis)
- [DAX Measures](#-dax-measures)
- [Dataset](#-dataset)
- [Tech Stack](#-tech-stack)
- [Key Findings](#-key-findings)
- [Future Scope](#-future-scope)
- [Project Structure](#-project-structure)
- [How to Use](#-how-to-use)
- [Author](#-author)

---

## 🔍 Overview

**FareFlux** is a production-grade Power BI analytics solution built for the urban ride-hailing industry. It transforms raw taxi booking data into actionable business intelligence — covering booking performance, vehicle-type profitability, revenue patterns, cancellation root causes, ratings, and a composite service quality gauge.

| Metric | Value |
|---|---|
| Total Bookings | 148,767 |
| Date Range | Jan 2024 – Dec 2024 |
| Vehicle Types Tracked | 7 |
| Payment Channels | 5 |
| Dashboard Pages | 7 |
| Custom DAX Measures | 5 |

---

## ❗ Problem Statement

The urban ride-hailing industry lacks integrated analytics. FareFlux addresses **5 critical operational challenges**:

1. **No booking completion visibility** — A 25% cancellation rate causing revenue loss and poor customer experience across all 7 vehicle types.
2. **Zero structured vehicle-type performance analysis** — 7 categories tracked without KPI benchmarking.
3. **Revenue leakage** — 5 payment channels (UPI, Cash, Uber Wallet, Credit Card, Debit Card) operating without per-method profitability insight.
4. **Cancellation root causes untracked** — No data to support targeted driver or customer interventions.
5. **No unified dashboard** — No way to monitor service quality, peak-hour performance, or customer retention across a full annual cycle.

---

## 📊 Dashboard Pages

### Page 1 — Homepage
Centralized navigation hub with direct links to all 6 analytical report pages.

### Page 2 — Overall Analysis
- **KPI Card:** 148.767K total bookings
- **Booking Status Pie Chart:** Completed 62% | No Driver Found 18% | Cancelled 14% | Incomplete 6%
- **Monthly Trend Line:** Peak in May (~13,000/mo), seasonal dip in December

### Page 3 — Vehicle Type Analysis
Matrix comparing all 7 vehicle types across 4 metrics: Total Revenue, Success Revenue, Avg Distance, Total Distance

| Vehicle | Total | Success | Avg Distance | Total KM |
|---|---|---|---|---|
| **Auto** ⭐ | 13M | 12M | 25.99 km | 601.79K km |
| Go Mini | 10M | 9M | 25.99 km | 482.09K km |
| Go Sedan | 9M | 9M | 25.98 km | 433.20K km |
| Bike | 8M | 7M | 26.00 km | 364.87K km |
| Premier Sedan | 6M | 6M | 25.95 km | 291.95K km |
| eBike | 4M | 3M | **26.34 km** | 172.57K km |
| Uber XL | 2M | 1M | 25.72 km | 71.59K km |

### Page 4 — Revenue Analysis
- **Payment Method Bar Chart:** UPI ~20M | Cash ~12M | Uber Wallet ~8M | Credit Card ~6M | Debit Card ~4M
- **Daily Distance Chart** with date slicer
- **Top-5 Booking IDs Table** by booking value

### Page 5 — Cancellation Analysis
- **Customer Reasons (each ~20%):** AC not working | Change of plans | Driver asked to cancel | Driver not moving | Wrong address
- **Driver Reasons (each ~25%):** Customer-related issue | Distance exceeded | Personal/car issue | Customer counted as cancelled
- **KPIs:** 92,551 successful | 37,427 driver-cancelled | **25% cancel rate**

### Page 6 — Ratings Dashboard
Customer vs Driver rating matrix broken down by vehicle type.

| Vehicle | Customer Rating | Driver Rating |
|---|---|---|
| Auto | 101.93K | 98.00K |
| Go Mini | 81.70K | 78.42K |

### Page 7 — Summary Dashboard
- **Service Quality Score Gauge:** 77.05 / 154.10
- **Retention Rate:** 30.24%
- **Revenue per KM:** 3.86M
- **Peak Hour Index:** 72.53%

---

## 📈 Key Metrics & KPIs

| KPI | Value |
|---|---|
| Total Bookings | 148,767 |
| Completion Rate | 62% |
| Cancellation Rate | 25% |
| Customer Retention Rate | 30.24% |
| Revenue per KM | 3.86M |
| Peak Hour Index | 72.53% |
| Service Quality Score | 77.05 / 154.10 |
| Top Revenue Vehicle | Auto (13M) |
| Dominant Payment Method | UPI (~20M) |

---

## 🧮 DAX Measures

```dax
-- 1. Cancellation Rate
CancelledPercentage = DIVIDE([Cancelled Bookings], [Total Bookings]) 
-- Result: 25%

-- 2. Revenue Per KM
Revenue_Per_KM = DIVIDE(SUM(rideBookings[Booking_Value]), SUM(rideBookings[Ride_Distance]))
-- Result: 3.86M

-- 3. Customer Retention Rate
Customer_Retain_Rate = DIVIDE([Returning Customers], [Total Customers])
-- Result: 30.24%

-- 4. Peak Hour Index
Premium_Peak_Hour_Index = [Peak Revenue] / [Total Revenue]
-- Result: 72.53%

-- 5. Service Quality Score (Composite KPI)
Service_Quality_Score = [Composite of Ratings, Completion & Retention]
-- Result: 77.05 / 154.10
```

---

## 🗃️ Dataset

**Source:** `rideBookings` — 148,767 rows of taxi booking records (Jan–Dec 2024)

| Column | Description |
|---|---|
| `Booking_ID` | Unique booking identifier |
| `Booking_Status` | Completed / Cancelled / No Driver / Incomplete |
| `Vehicle_Type` | Auto, Bike, eBike, Go Mini, Go Sedan, Premier Sedan, Uber XL |
| `Payment_Method` | UPI, Cash, Uber Wallet, Credit Card, Debit Card |
| `Ride_Distance` | Distance of the trip (km) |
| `Booking_Value` | Fare amount |
| `Cancellation_Reason` | Reason for cancellation (customer or driver) |
| `Customer_Rating` | Rating given by customer |
| `Driver_Rating` | Rating given to driver |
| `Date` | Booking date |

**Data Model:** Star schema with `rideBookings` as the central fact table. Date range slicer and `Vehicle_Type` filter applied globally across all pages.

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **Microsoft Power BI Desktop 2024** | Dashboard development, DAX, drill-through navigation |
| **DAX (Data Analysis Expressions)** | Custom KPI calculations |
| **Power Query (M Language)** | Data transformation & cleaning |
| **Star Schema Modeling** | Optimized data relationships |

**Visuals Used:** Pie charts · Line charts · Bar charts · Matrix tables · KPI cards · Gauge · Date slicers · Cross-filter drillthrough

---

## 💡 Key Findings

1. **Auto vehicles lead revenue** at 13M total — Uber XL is the lowest-volume segment (2M), signalling a fleet reallocation opportunity.
2. **25% cancellation rate is critical.** Equal-split reasons (customer: 5×20%, driver: 4×25%) confirm systemic process failures requiring broad intervention — not isolated fixes.
3. **UPI dominates payment adoption** (~20M) — confirming a digital-first payment strategy and enabling cashback/loyalty programmes.
4. **Evening and Morning are peak revenue windows** — prime targets for dynamic surge pricing.
5. **Customer Retention Rate of only 30.24%** — loyalty programmes and cancellation reduction are the top-priority revenue levers.
6. **Medium distance (5–15 km) generates the highest Revenue per KM** — the most profitable operational sweet spot.

---

## 🚀 Future Scope

| Enhancement | Description |
|---|---|
| 🤖 ML Fare Prediction | Embed Python/R visuals with Random Forest or XGBoost models using distance, time-of-day, vehicle type, and weather |
| 📡 Real-Time Streaming | Connect Azure Event Hubs for live booking tracking, driver availability maps, and instant cancellation alerts |
| 🗺️ Geospatial Maps | ArcGIS / Bing Maps for booking density heatmaps and high-demand pickup zone analysis |
| 👤 Driver Scorecards | Per-driver KPIs: acceptance rate, completion rate, avg rating, income/km |
| 🎯 Customer Segmentation | RFM analysis (Recency–Frequency–Monetary) for VIP / Regular / At-Risk tiers |
| 💰 Dynamic Pricing Engine | Automated surge pricing triggered by Revenue Tier and Peak Hour Index thresholds |
| 🌍 Multi-City Dashboard | Extend the framework to multi-city data with regional performance benchmarking |

---

## 📁 Project Structure

```
FareFlux/
│
├── 📊 FareFlux_Dashboard.pbix         # Main Power BI report file
├── 📂 Dataset/
│   └── rideBookings.csv               # Source dataset (148,767 records)
├── 📂 Screenshots/
│   ├── 01_Homepage.png
│   ├── 02_Overall_Analysis.png
│   ├── 03_Vehicle_Type.png
│   ├── 04_Revenue.png
│   ├── 05_Cancellation.png
│   ├── 06_Ratings.png
│   └── 07_Summary.png
├── 📂 Presentation/
│   └── FareFlux_Capstone_Presentation.pptx
└── README.md
```


---

## 👩‍💻 Author

**Stuti Shukla**  
B.Tech Computer Science  


---

## 📚 References

- [Microsoft Power BI Documentation](https://learn.microsoft.com/power-bi/)
- [Kaggle — Taxi Trip Datasets](https://www.kaggle.com)
- [Google Developers — Data Visualization Best Practices](https://developers.google.com)
- [TutorialsPoint — Power BI](https://www.tutorialspoint.com/power_bi)

---

<div align="center">
  <i>Built with 💛 using Microsoft Power BI · FareFlux Capstone Project 2024</i>
</div>
