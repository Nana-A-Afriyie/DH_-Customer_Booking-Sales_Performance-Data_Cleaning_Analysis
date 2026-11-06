# 📦 DHL Customer Booking & Sales Performance Analysis

### SQL | Excel | Power BI | Data Analytics

## 📌 Project Overview

This project analyzes DHL customer booking and sales data to understand revenue performance, shipment trends, and delivery efficiency.

The dataset originally contained **10,400 records** with duplicates, missing values, and inconsistent formatting. SQL was used to clean and prepare the data for analysis.

An interactive dashboard was developed to visualize revenue, booking performance, regional sales, and delivery status.
<img width="1672" height="941" alt="DHL Logistics Analytics Dashboard 2025" src="https://github.com/user-attachments/assets/78186303-7b74-4f35-904b-f11c8dd8d3c5" />


## 🎯 Project Objectives

- Analyze revenue and booking performance.
- Identify the highest revenue-generating regions.
- Examine monthly revenue trends.
- Evaluate delivery performance and delays.
- Provide recommendations to improve business operations.

## 🛠️ Tools Used

- **SQL Server:** Data cleaning and analysis.
- **Excel:** Data inspection and preparation.
- **Power BI:** Dashboard creation and data visualization.

## 🧹 Data Cleaning Process

The dataset contained several data quality issues:

- 232 exact duplicate records.
- 400 duplicated booking IDs.
- 180 missing sales channel values.
- 120 missing shipment weight values.
- Inconsistent text formatting and decimal values.

### Cleaning Steps

1. Identified and removed duplicate records using SQL `ROW_NUMBER()` and CTEs.
2. Standardized date formats.
3. Rounded financial and weight values to two decimal places.
4. Cleaned inconsistent text using SQL string functions.
5. Handled missing values using `COALESCE()` and appropriate cleaning methods.
6. Checked data quality before analysis.

## 📊 Dashboard Overview

The dashboard summarizes **10,000 shipments across five regions** from January to December 2025.

### Key Performance Indicators

| KPI | Value |
|---|---:|
| Total Revenue | $1,503,506 |
| Base Rate | $1,305,916 |
| Surcharges | $196,591 |
| Total Bookings | 10,000 |
| Average Revenue per Booking | $150.35 |
| On-Time Delivery | 80.7% |
| Delay Rate | 7.5% |

## 🔍 Key Findings

**1. Regional Revenue**

Europe generated the highest revenue, followed by North America and Asia-Pacific. LATAM and MEA contributed smaller shares.

**2. Monthly Revenue**

Revenue fluctuated throughout 2025, with July recording one of the highest monthly performances.

**3. Delivery Performance**

- Delivered: 80.7%
- In Transit: 9.5%
- Delayed: 7.5%
- Returned: 2.3%

**4. Service Performance**

Express services generated the highest revenue among the service categories.

**5. Sales Channels**

Online bookings contributed the largest share of revenue.

## 💡 Recommendations

- **Improve Delivery Efficiency:** Investigate shipment delays and improve tracking.
- **Strengthen Key Markets:** Focus on Europe and North America to maintain revenue growth.
- **Expand Regional Opportunities:** Explore growth opportunities in LATAM and MEA.
- **Improve Revenue Planning:** Use monthly trends to forecast demand.
- **Optimize Pricing:** Review surcharges and service pricing.

## 🏁 Conclusion

This project demonstrates how SQL, Excel, and Power BI can be used to clean, analyze, and visualize logistics data.

The analysis identified key revenue drivers, regional performance trends, and opportunities to improve delivery efficiency.

It also demonstrates practical skills in **data cleaning, SQL analysis, dashboard development, and business decision-making**.


📂 Repository Structure
├── data/
│   ├── DHL_Sales_Performance_Uncleaned_10k.csv   # Raw, dirty dataset
│   └── DHL_Sales_Performance_Clean_10k.csv       # Cleaned dataset
├── sql/
│   ├── 01_data_cleaning.sql                      # Deduplication & standardization scripts
│   └── 02_sales_kpi_queries.sql                  # Analytical SQL queries
└── README.md                                     # Project documentation
