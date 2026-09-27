# ZoZo App Usage Analytics Dashboard

![Dashboard Preview](images/executive_summary_dashboard.png)

> An interactive Business Intelligence solution built with Power BI to analyse ZoZo Inc's app usage, providing data-driven insights into customer behaviour, device preference, and platform performance.

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Business Objectives](#business-objectives)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Dashboard Features](#dashboard-features)
- [Key Insights](#key-insights)
- [Tools & Technologies](#tools--technologies)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Author](#author)
- [License](#license)

---

## 📊 Project Overview

This project presents an interactive Business Intelligence solution developed using **Power BI** to analyse ZoZo Inc's app usage data. The dashboard is designed for simplicity, accuracy, and reusability, enabling stakeholders to quickly track key metrics, identify trends, and explore insights through intuitive visualisations.

**Duration:** [Project Duration]  
**Role:** Data Analyst  
**Organisation:** ZoZo Inc

---

## 🎯 Business Objectives

The dashboard addresses the following business questions:

| # | Question | Status |
|---|----------|--------|
| 1 | How many unique patrons have used the ZoZo Application? | ✅ |
| 2 | How many devices do patrons use on average? | ✅ |
| 3 | Which platform is most used (with OS version filtering)? | ✅ |
| 4 | What are the top 10 most used make/model per platform? | ✅ |
| 5 | Is there a correlation between device platform and altitude? | ✅ |
| 6 | Which is the most used version of the ZoZo application? | ✅ |
| 7 | How does platform usage trend over time? | ✅ |

---

## 📁 Dataset

### Data Dictionary

| Field Name | Definition | Data Type |
|------------|------------|-----------|
| `click_date` | Calendar date of user interaction | Date (YYYY/MM/DD) |
| `click_time` | Exact time of interaction | Time (HH:MM:SS) |
| `patron_id` | Unique user identifier | Text |
| `device_id` | Unique device identifier | Text |
| `make_model` | Device manufacturer and model | Text |
| `device_information` | Additional device data | Text |
| `device_os` | Operating system | Text |
| `app_ver` | Application version | Text |
| `gps_ver` | GPS/API version | Text |
| `gps_lat` | GPS latitude | Decimal |
| `gps_long` | GPS longitude | Decimal |
| `gps_alt` | GPS altitude (meters) | Decimal |
| `gps_accuracy` | GPS accuracy (meters) | Decimal |

### Data Quality Notes

- **Source:** Raw CSV file (pipe-delimited `|`)
- **Records:** [Insert number]
- **Date Range:** 5 days of data
- **Missing Values:** Removed nulls from `patron_id`, `gps_lat`, `gps_long`, `gps_alt`, `gps_accuracy`

---

## 🔧 Methodology

### 1. Data Preparation (Power Query)

#### Column Data Types
- Set `click_date` to **Date** type (YYYY/MM/DD)
- Created custom column `click_time_fixed` for **Time** type (HH:MM:SS)
- Corrected GPS coordinate types using **M-code** for locale handling

#### Missing Values Management
- Removed all nulls in `patron_id` → ensures valid user tracking
- Removed nulls in GPS fields → improves heat map reliability

#### Text Standardisation
- Trimmed whitespace from `make_model`, `device_name`, `device_os`
- Checked for case-sensitive duplicates in dropdowns

#### GPS Data Preparation
- Rounded lat/long to 3 decimal places
- Validated longitude range: -180 to +180
- Validated latitude range: -90 to +90
- Replaced negative altitudes with 0 (sea level)
- Created `GPS Accuracy Bands`:
  - **High:** < 10m
  - **Medium:** 10–50m
  - **Low:** 50–100m
  - **Unusable:** > 100m (filtered out)

### 2. Data Modelling

#### Star Schema Design
