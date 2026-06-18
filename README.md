# 🇦🇪 UAE Retail & E-Commerce Executive Dashboard | Power BI

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Advanced-brightgreen?style=for-the-badge)
![Data Modeling](https://img.shields.io/badge/Data_Modeling-Star_Schema-blue?style=for-the-badge)
![Domain](https://img.shields.io/badge/Domain-UAE_Retail_%26_E--Commerce-red?style=for-the-badge)

A production-grade Power BI solution that transforms raw, multi-channel retail data into a **single source of truth** for executive decision-making. The dashboard tracks **400M+ AED in revenue** across physical flagship stores and e-commerce fulfillment hubs spanning Dubai, Abu Dhabi, and Sharjah.

---

## 📸 Dashboard Preview

> *Executive Overview Page*

![Dashboard Overview](dashboard/screenshot_overview.png)

> *Demographic & Channel Analysis Page*

![Dashboard Detail](dashboard/screenshot_detail.png)

---

## 🎯 Business Problems Solved

This dashboard was engineered to answer four questions that traditional reporting tools were leaving unanswered:

| # | Business Problem | Metric Tracked |
|---|-----------------|---------------|
| 1 | **Profitability** — Are we protecting margins despite high-cost SKUs? | Revenue vs. COGS, Gross Profit % |
| 2 | **Omnichannel Cannibalization** — Is e-commerce growing the business or stealing from stores? | Revenue by Channel, YoY growth per channel |
| 3 | **Demographic Spend** — Where should marketing allocate budget: Nationals or Expats? | Revenue segmented by customer nationality |
| 4 | **Loyalty ROI** — Does the loyalty program actually drive higher spend? | AOV by loyalty tier |

---

## 📈 Key Findings

| Insight | Result |
|--------|--------|
| Gross Profit Margin | **34.05%** — exceeds the 32.00% corporate target |
| Omnichannel Parity | Standard Retail vs. E-Commerce both at **~113M AED** in Electronics — no cannibalization |
| Expat vs. National Revenue | **351M AED** (Expats) vs. **57M AED** (Nationals) — clear signal for marketing spend |
| Overall AOV | **2.05K AED**, led by Electronics at **5.03K AED** per order |

---

## ⚙️ Technical Methodology

### Step 1 — Data Extraction & Transformation (Power Query)

- Ingested four raw `.csv` source files: transactional sales, product catalog, customer demographics, and store locations.
- Cleansed nulls, standardized date formats and AED currency types, and validated relational integrity before loading to the model.

---

### Step 2 — Data Modeling (Star Schema)

The model follows a clean star schema design, ensuring optimal query performance and unambiguous filter propagation.

```
                    ┌─────────────────┐
                    │  Dim_Customers  │
                    │  (CustomerID)   │
                    └────────┬────────┘
                             │
┌─────────────────┐          │          ┌──────────────────┐
│  Dim_Products   │          ▼          │  Dim_Locations   │
│  (ProductID)    ├──── Fact_Sales ────┤  (LocationID)    │
└─────────────────┘    (Transactions)   └──────────────────┘
                             │
                    ┌────────┴────────┐
                    │   Dim_Date      │
                    │ (Calendar Table)│
                    └─────────────────┘
```

**Modeling decisions:**
- One-to-many, unidirectional relationships on all joins for predictable cross-filter behavior.
- Custom DAX-built Calendar Table enables full Time Intelligence (MTD, YTD, MoM comparisons).
- No circular dependencies — every dimension filters the fact table only.

---

### Step 3 — DAX Measures

All business metrics are computed as explicit DAX measures. No implicit measures were used.

| Measure | Purpose | Key Functions |
|---------|---------|--------------|
| `Total Gross Revenue (AED)` | Row-context revenue calculation | `SUMX`, `RELATED` |
| `Total COGS (AED)` | Cost of goods across all transactions | `SUMX`, `RELATED` |
| `Gross Profit (AED)` | Revenue minus COGS | Arithmetic on measures |
| `Gross Profit Margin %` | Margin as percentage of revenue | `DIVIDE` (safe division) |
| `Average Order Value (AED)` | Revenue per unique transaction | `DIVIDE`, `DISTINCTCOUNT` |
| `Revenue by Channel` | Segmented by store type | `CALCULATE`, `FILTER` |
| `Revenue by Nationality` | Segmented by customer segment | `CALCULATE`, `FILTER` |

**Example — Gross Revenue (iterative row-context):**

```dax
Total Gross Revenue (AED) =
SUMX(
    Fact_Sales,
    Fact_Sales[Quantity] * RELATED(Dim_Products[Unit_Price_AED])
)
```

**Example — Safe Gross Margin:**

```dax
Gross Profit Margin % =
DIVIDE(
    [Gross Profit (AED)],
    [Total Gross Revenue (AED)],
    0
)
```

---

## 📂 Repository Structure

```
UAE-Retail-E-Commerce-Executive-Dashboard-Power-BI/
│
├── Data/
│   ├── Fact_Sales.csv           # Core transactional data
│   ├── Dim_Customers.csv        # Customer demographics & loyalty tier
│   ├── Dim_Products.csv         # Product catalog with cost & price
│   └── Dim_Locations.csv        # Store/hub locations by Emirate
│
├── dashboard/
│   ├── UAE_Retail_Dashboard.pbix   # Power BI project file
│   ├── screenshot_overview.png     # Executive overview page
│   └── screenshot_detail.png       # Channel & demographic analysis page
│
└── README.md
```

---

## 🛠️ Tools & Skills Used

| Area | Tool / Concept |
|------|---------------|
| BI Platform | Microsoft Power BI Desktop |
| Data Preparation | Power Query (M language) |
| Data Modeling | Star Schema, Relationship management |
| Calculations | DAX — `SUMX`, `CALCULATE`, `DIVIDE`, `RELATED`, `DISTINCTCOUNT`, `FILTER` |
| Time Intelligence | Custom Calendar Table, MTD / YTD measures |
| Domain Knowledge | UAE retail market, Expat/National segmentation, omnichannel dynamics |

---

## 🚀 How to Open This Project

1. Download and install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free).
2. Clone or download this repository.
3. Open `dashboard/UAE_Retail_Dashboard.pbix` in Power BI Desktop.
4. If prompted, re-point the data source to the `/Data` folder on your local machine via **Transform Data → Data Source Settings**.

---

## About

Built as a portfolio project demonstrating end-to-end Power BI development — from raw CSV files to executive-ready reporting — with a focus on the UAE retail and e-commerce market.

**Connect:** [LinkedIn]([https://www.linkedin.com/in/your-linkedin-profile](https://www.linkedin.com/in/muhammad-abdullah-a7861a3a2/) · [GitHub](https://github.com/ak786abdullah)
