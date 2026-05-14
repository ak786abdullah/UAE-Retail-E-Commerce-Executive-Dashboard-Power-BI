# 🇦🇪 UAE Retail & E-Commerce Executive Dashboard | Power BI

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Data Modeling](https://img.shields.io/badge/Data_Modeling-Star_Schema-blue?style=for-the-badge)
![DAX](https://img.shields.io/badge/DAX-Advanced-brightgreen?style=for-the-badge)

**Interactive Dashboard Link:** [Insert your NovyPro or Power BI Service link here]

## 📌 Executive Summary
This project transforms raw, multi-channel retail data into a "Single Source of Truth" executive dashboard. Designed specifically for regional directors operating in the United Arab Emirates, this Power BI solution tracks over 400M+ AED in revenue across physical flagship stores and e-commerce fulfillment hubs in Dubai, Abu Dhabi, and Sharjah. 

The primary objective of this project was to cure business blind spots regarding **profit margins**, **omnichannel cannibalization**, and **demographic purchasing behavior**.

---

## 📸 Dashboard Preview
*[Insert a clean screenshot of your final dashboard here. On GitHub, you can just drag and drop an image file into the text editor to create a link]*

---

## 🎯 The Business Problems Solved
This dashboard was engineered to answer four critical business questions:
1. **The Profitability Problem:** Are we maintaining our target margins despite high-cost items? (Tracking Revenue vs. COGS).
2. **The Omnichannel Problem:** Is our e-commerce platform cannibalizing our physical retail stores, or are they growing concurrently?
3. **The Demographic Problem:** How does purchasing behavior differ between UAE Nationals and Expats, and where should marketing allocate their budget?
4. **The Loyalty Problem:** Does our customer loyalty program genuinely drive a higher Average Order Value (AOV)?

---

## ⚙️ Technical Execution & Methodology

### 1. Data Extraction & Transformation (Power Query)
* Extracted raw `.csv` files containing transactional data, product catalogs, customer demographics, and store locations.
* Cleansed data by handling null values, standardizing data types (e.g., Currency for AED, Dates for order history), and ensuring relational integrity.

### 2. Data Modeling
* Engineered a robust **Star Schema** data model consisting of one Fact table (`Fact_Sales`) and three Dimension tables (`Dim_Customers`, `Dim_Products`, `Dim_Locations`).
* Built a custom **Date/Calendar Table** using DAX to enable precise Time Intelligence reporting and chronological trend analysis.
* Ensured unidirectional, one-to-many filtering for optimal dashboard performance.

### 3. DAX Calculations
Developed complex, iterative DAX measures to calculate true business metrics. Key functions utilized include `SUMX`, `RELATED`, `DIVIDE`, and `DISTINCTCOUNT`.

*Example Measure - Gross Revenue:*
```dax
Total Gross Revenue (AED) = 
SUMX(
    Fact_Sales, 
    Fact_Sales[Quantity] * RELATED(Dim_Products[Unit_Price_AED])
)
# UAE Retail Performance Analysis

## 📈 Key Insights Discovered
* **Healthy Margins:** The UAE operations maintain a highly efficient **34.05% Gross Profit Margin**, successfully beating the 32.00% corporate target.
* **Omnichannel Parity:** Standard Retail (113M AED) and E-Commerce Hubs (113M AED) are performing almost identically within the Electronics sector, proving e-commerce is a primary driver, not a secondary channel.
* **Demographic Spend:** Expat customers drove **~351M AED** in revenue compared to **~57M AED** from UAE Nationals, providing concrete justification for the marketing team to skew ad spend toward the expat demographic.
* **Average Order Value:** The overall AOV sits at a healthy **2.05K AED**, heavily driven by the Electronics category (5.03K AED AOV).

## 📊 Dashboard Preview
![UAE Retail Dashboard Screenshot](https://via.placeholder.com/800x450.png?text=Insert+Your+Power+BI+Dashboard+Screenshot+Here)

---

## 📂 Repository Contents
* **Fact_Sales.csv:** Raw transactional data.
* **Dim_Customers.csv / Dim_Locations.csv / Dim_Products.csv:** Dimension lookup tables.
* **UAE_Retail_Dashboard.pbix:** The core Power BI project file.

---

### Project Note
*Transitioning analytical mathematics into data-driven business solutions.*
