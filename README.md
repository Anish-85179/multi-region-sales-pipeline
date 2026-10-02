# Multi-Region Retail Sales Consolidation & Analytics Pipeline

## 📌 Project Overview
Engineered an end-to-end automated data consolidation pipeline and executive dashboard in Google Sheets for a multi-regional retail network (North, South, East, West). Standardized individual branch transactional feeds and built a live central data engine to power real-time executive decision-making.

## 🔗 Live Interactive Links & Proof
* **Live Google Sheets Workbook**: [View Interactive Dashboard](https://docs.google.com/spreadsheets/d/1CzIQ0rwuGOhl3HoiZ9K5CB2y1_vng_mZdFVeKxEKEik/edit?usp=sharing)
* **Downloaded Backup**: `Multi_Region_Retail_Sales_Pipeline.xlsx` (available in repository)

## 📊 Live Dashboard & Architecture
![Executive Dashboard](dashboard.png)

### Central Master Console ETL
![Master Console Query](master_console.png)


## 🏗️ Technical Architecture & Data Flow
1. **Branch Streams**: 4 regional tabs enforcing a standardized 8-column schema (`Date`, `Store_ID`, `Product_Category`, `Quantity`, `Unit_Price`, `Total_Revenue`, `Payment_Method`, `Region`).
2. **Calculated Fields**: Applied `=ARRAYFORMULA()` for automated line-item revenue computations (`Quantity * Unit_Price`).
3. **Master Console Engine**: Leveraged native array stacking (`{}`) and SQL-style `QUERY()` logic to merge distributed datasets into a single real-time ledger without external permissions or `#REF!` latency.
4. **Executive Layer**: Built aggregate KPI tables and visual charts summarizing revenue across regions, categories, and payment methods.

## 🛠️ Key Formula Implementation
```excel
=QUERY(
  {
    'Branch-North-Sales'!A1:H;
    'Branch-South-Sales'!A2:H;
    'Branch-East-Sales'!A2:H;
    'Branch-West-Sales'!A2:H
  },
  "SELECT * WHERE Col1 IS NOT NULL ORDER BY Col1 ASC",
  1
)
