<img width="934" height="519" alt="Screenshot 2026-09-16 223939" src="https://github.com/user-attachments/assets/4e966466-f980-4ea6-b020-d467038bfdaf" />
<img width="920" height="367" alt="Screenshot 2026-09-16 224010" src="https://github.com/user-attachments/assets/bc75fc60-03c2-4ff5-8333-f704a9b79084" />
<img width="941" height="469" alt="Screenshot 2026-09-16 224040" src="https://github.com/user-attachments/assets/428cfc07-371a-4056-87de-f653a0e6d436" />
<img width="939" height="470" alt="Screenshot 2026-09-16 224135" src="https://github.com/user-attachments/assets/8941c8cc-df65-4e07-85dd-b5ab7d1f4611" />
<img width="938" height="288" alt="Screenshot 2026-09-16 224216" src="https://github.com/user-attachments/assets/cc158742-c7f7-4b06-8f9b-f46c4a0708cb" />
# DH_-Customer_Booking-Sales_Performance-Data_Cleaning_Analysis
This project analyzes DHL customer booking sales performance to uncover revenue drivers, regional trade patterns, and service line trends. Using SQL, a 10,000+ row dataset was cleaned by resolving duplicate entries, missing values, and formatting errors to ensure accurate financial reporting and operational insights

## 📌 Project Overview
This project focuses on analyzing sales performance, revenue drivers, and operational metrics for DHL customer bookings. To simulate real-world data engineering and analytics workflows, the project utilizes a dataset containing 10,000+ booking records that underwent comprehensive data cleaning and transformation using SQL prior to analysis.

The objective is to identify revenue trends across customer segments, evaluate high-performing delivery services, and track shipping performance metrics.

---

## 🗃️ Dataset Architecture & Data Quality Issues
The raw dataset (`DHL_Sales_Performance_Uncleaned.csv`) contains **10,400 raw records** across 12 operational, financial, and customer dimensions. 

Prior to analysis, the dataset contained intentional data quality issues to test SQL cleaning procedures:
* **Exact Duplicate Rows:** 232 full-row duplicate records.
* **Primary Key Duplicates:** 400 instances of duplicated `Booking_ID` values resulting from system re-entries or status updates.
* **Missing Data:** 180 missing records in `Sales_Channel` and 120 missing values in `Weight_KG`.
* **Formatting Inconsistencies:** Mixed case formatting (`b2b` vs `B2C`) and leading/trailing whitespace in text columns.
* **Precision Errors:** Unrounded decimal figures across weight and financial columns.

---

## 🧹 Data Cleaning & Transformation (SQL Pipeline)

The data cleaning pipeline was executed in SQL to enforce data integrity and structure:

### 1. Removing Duplicates (Deduplication)
Used CTEs and `ROW_NUMBER()` window functions to filter out exact duplicate rows and retain only the most recent booking status per `Booking_ID`:

```sql
WITH RankedBookings AS (
    SELECT 
        *,
        ROW_NUMBER() OVER (
            PARTITION BY Booking_ID 
            ORDER BY Booking_Date DESC, Total_Revenue_USD DESC
        ) AS row_num
    FROM DHL_Sales_Performance_Uncleaned
)
DELETE FROM RankedBookings 
WHERE row_num > 1;

Standardizing Dates & Numeric Precision
Converted timestamp fields into short date formats (YYYY-MM-DD).

Rounded all numeric columns (Weight_KG, Base_Rate_USD, Surcharges_USD, Total_Revenue_USD) to 2 decimal places using ROUND() and CAST().

SQLUPDATE DHL_Sales_Performance_Uncleaned
SET 
    Booking_Date = CAST(Booking_Date AS DATE),
    Weight_KG = ROUND(CAST(Weight_KG AS numeric), 2),
    Base_Rate_USD = ROUND(CAST(Base_Rate_USD AS numeric), 2),
    Surcharges_USD = ROUND(CAST(Surcharges_USD AS numeric), 2),
    Total_Revenue_USD = ROUND(CAST(Total_Revenue_USD AS numeric), 2);
. Text Standardization & Missing Value Imputation
Applied TRIM() and UPPER() / INITCAP() to standardize Customer_Type, Service_Type, and Sales_Channel.

Handled missing values using COALESCE() or targeted imputation logic.

📊 Key Insights & Analytics Focus Areas
Once cleaned, the dataset was analyzed across three main domains:

Sales Performance by Service Line: Revenue breakdown across Express Worldwide, Express Envelope, eCommerce Parcel, and Freight.

Regional Trade Routes: Identification of high-volume origin and destination shipping corridors (North America, Europe, APAC, LATAM, MEA).

Delivery Exceptions & Reliability: Analyzing delay rates and returned package percentages across sales channels (Online Portal, Account Manager, API Integration).

** DASHBOARD EXPLAINED AND RECCOMENDATION**
This visual is a DHL Bookings Dashboard for 2025 that summarizes performance metrics across 10,000 shipments. It breaks down logistics analytics into high-level KPIs and detailed charts covering revenue distributions, trends, and shipment delivery statuses.   
Key Performance Indicators (KPI Cards)
Total Revenue: $1,503,506 (averaging $150.35 per booking).   
Base Rate: $1,305,916 (represents 86.9% of total revenue).   
Surcharges: $196,591 (represents 13.1% of total revenue).   
Total Bookings: 10,000 total shipments handled between January and December 2025.   
On-Time Delivery: 80.7% (translating to 8,065 delivered shipments on time).   
Delay Rate: 7.5% (752 delayed orders).   
Visual Data Breakdowns
Total Revenue (USD) by Origin Region (Bar Chart):
Shows revenue contribution across five regions.   
Europe leads as the highest revenue-generating origin, followed closely by N. America and APAC.   
LATAM and MEA represent significantly smaller shares of origin revenue.   
Monthly Revenue (USD) Jan – Dec 2025 (Line Chart):
Tracks monthly performance fluctuated between $110K and $150K+ throughout the year. 
Peak revenue occurred around July, with noticeable dips around February and September/October.   
Delivery Status Breakdown (Donut Chart):
Delivered (Green): Represents the vast majority of shipments.   
In Transit (Blue): A moderate portion of active shipments currently moving.   
Delayed (Orange): Accounts for 7.5% of shipments.   
Returned (Red): A small fraction of shipments that failed delivery and were returned.

**RECCOMENDATIONS AND CONCLUSIONS**
Improve On-Time Delivery & Reduce Delays
Root-Cause Analysis on Delays: With a 7.5% delay rate (752 shipments) and an 80.7% on-time delivery rate, analyze underlying causes (e.g., custom hold-ups, carrier bottlenecks, or warehouse fulfillment lags) to move closer to an industry-standard 90%+ target.   
**Real-time Delay Mitigation**: Implement proactive transit tracking for shipments flagged as "In Transit" to resolve exceptions before they convert into full delays or returns.   
*** Capitalize on High-Performing & Emerging Regions***
Double Down on Core Markets: Europe and North America generate the vast majority of revenue. Focus marketing and capacity allocation here to protect high-margin trade lanes.   
**Expand Regional Penetration**: LATAM and MEA show lower revenue volume. Evaluate whether this is due to limited carrier routes or untapped market demand and consider targeted pricing or route expansion to grow regional market share.   
** Smooth Out Monthly Revenue Volatility**
Demand Forecasting & Seasonal Promotions: Monthly revenue swings between $110K and $150K+, with a peak in July followed by mid-to-late year dips. Introduce off-peak volume incentives or contract guarantees during slow months (e.g., February and autumn) to stabilize cash flow year-round.   
** Optimize Revenue & Ancillary Surcharges**
Review Surcharge Structure: Surcharges currently account for 13.1% ($196,591) of total revenue. Audit these line items (fuel fees, address corrections, oversize handling) to ensure rates accurately cover operational costs without alienating customers.   
🛠️ Tools & Technologies Used
SQL (PostgreSQL / SQL Server Management Studio): Data extraction, CTE deduplication, data cleaning, and aggregation queries.[DHL_Sales_Performance_Uncleaned_10k.csv](https://github.com/user-attachments/files/32316806/DHL_Sales_Performance_Uncleaned_10k.csv)



Power BI / Figma: Dashboard visual reporting and KPI tracking.

📂 Repository Structure
├── data/
│   ├── DHL_Sales_Performance_Uncleaned_10k.csv   # Raw, dirty dataset
│   └── DHL_Sales_Performance_Clean_10k.csv       # Cleaned dataset
├── sql/
│   ├── 01_data_cleaning.sql                      # Deduplication & standardization scripts
│   └── 02_sales_kpi_queries.sql                  # Analytical SQL queries
└── README.md                                     # Project documentation
