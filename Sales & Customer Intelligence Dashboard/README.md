# 📊 Final Project – Sales & Customer Intelligence Dashboard

An advanced Power BI project covering **Data Modeling**, **DAX Measures & Calculated Columns**, **Time Intelligence**, **Filtering & Interaction**, **Navigation & UX**, **Mobile Layout**, and **Row-Level Security** — built on a normalized Star Schema with drill-through, tooltips, bookmarks, and dynamic field parameters.

---

## 🚀 Project Overview

This project demonstrates a **complete end-to-end Power BI analytics workflow**. It is organized across **8 task areas** as per the project brief:

| # | Task | Focus Area |
|---|------|-----------|
| 1️⃣ | Data Modeling | Star Schema, Relationships, Hidden Fields |
| 2️⃣ | DAX Measures & Calculated Columns | CALCULATE, FILTER, ALL, SUMX, COUNTX, AVERAGEX, SWITCH, RELATED |
| 3️⃣ | Time Intelligence | YTD, YOY, MOM — Sales & Returns |
| 4️⃣ | Dashboard Layout | Multi-page interactive report with KPIs, charts, forecasts, matrices |
| 5️⃣ | Filtering & Interaction | Slicers, Drill Up/Down, Drillthrough, Numeric Range Parameters |
| 6️⃣ | Navigation & UX | Buttons, Bookmarks, Slicer Panel, Tooltips, Conditional Formatting |
| 7️⃣ | Mobile Layout | Mobile-optimized views for KPI Cards and Top N visuals |
| 8️⃣ | Security | Row-Level Security — Roles for Region Managers |

---

## 🎯 Objectives

1. Build a robust **data model** with **star schema**
2. Use a variety of **DAX formulas and patterns** for measures and KPIs
3. Apply **Time Intelligence**, filtering, and formatting techniques
4. Create a fully interactive **multi-page Power BI report**
5. Ensure **mobile compatibility** and provide enhanced user experience

---

## 🗂️ Project Files

| File Name | Description |
|-----------|-------------|
| 📄 `PR_3_SALES_INTELLIGENCE.pbix` | Main Power BI file with all models, measures, and dashboards |
| 📘 `README.md` | Project documentation (this file) |
| 📁  `Files Used` | Files used in this project |
| 🖼️  `Project Preview` | Images of the project |

---

## 📁 Dataset Overview

The following tables were imported from Excel files and loaded into the Power BI Data Model:

- `Date_Dim`
- `Customer_Dim`
- `Product_Dim`
- `Sales_Fact`
- `Returns_Fact`
- `Region_Dim`

---

## 🧩 Tasks Breakdown

---

### 🔹 1️⃣ Data Modeling

- Created relationships between Fact and Dimension tables using **Primary & Foreign Keys**
- Hidden unnecessary fields from the Report View
- Ensured a clean **Star Schema** layout with consistent naming conventions

**Relationships defined:**

---

<img width="1000" height="500" alt="Screenshot 2026-04-30 123720" src="https://github.com/user-attachments/assets/f746af80-c001-4cad-ad20-0eb2535420bb" />


---

| From Table | To Table | Join Key | Cardinality |
|------------|----------|----------|-------------|
| Sales_Fact | Customer_Dim | CustomerID | Many → 1 |
| Sales_Fact | Product_Dim | ProductID | Many → 1 |
| Sales_Fact | Region_Dim | RegionID | Many → 1 |
| Sales_Fact | Date_Dim | DateID | Many → 1 |
| Returns_Fact | Sales_Fact | SaleID | Many → 1 |

---

### 🔹 2️⃣ DAX Measures & Calculated Columns

#### 📌 CALCULATE

```dax
Consumer Sales = 
CALCULATE(
    [Total Sales],
    Customer_Dim[Segment] = "Consumer"
)
```

#### 📌 FILTER

```dax
High Value Sales = 
CALCULATE(
    [Total Sales],
    FILTER(Sales_Fact, Sales_Fact[TotalAmount] > 1000)
)
```

#### 📌 SUMX

```dax
Revenue SUMX = 
SUMX(
    Sales_Fact,
    Sales_Fact[UnitsSold] * RELATED(Product_Dim[Price])
)
```

#### 📌 ALL

```dax
Sales % of Total = 
DIVIDE(
    [Total Sales],
    CALCULATE([Total Sales], ALL(Customer_Dim[Segment])),
    0
) * 100
```

#### 📌 AVERAGEX

```dax
Avg Margin % = AVERAGEX(Sales_Fact, Sales_Fact[Profit Margin %])
```

#### 📌 SWITCH for KPI Classification

```dax
Sales KPI Label = 
SWITCH(
    TRUE(),
    [Total Sales] >= 50000, "Excellent",
    [Total Sales] >= 30000, "Good",
    [Total Sales] >= 10000, "Average",
    "Poor"
)
```

#### 📌 COUNTX

```dax
Customer Count = COUNTX(Sales_Fact, Sales_Fact[CustomerID])
```

#### 📌 Calculated Columns

**Profit Margin Classification (on Sales_Fact):**

```dax
Margin Category = 
SWITCH(
    TRUE(),
    [Profit Margin %] < 0.20, "Low Margin",
    [Profit Margin %] < 0.40, "Medium Margin",
    [Profit Margin %] < 0.60, "High Margin",
    "Super Margin"
)
```

**Customer Full Name (on Customer_Dim):**

```dax
FullName = Customer_Dim[FirstName] & " " & Customer_Dim[LastName]
```

**Year-Month Formatting (on Date_Dim):**

```dax
YearMonth = FORMAT(Date_Dim[Date], "YYYY-MM")
```

---

### 🔹 3️⃣ Time Intelligence

Applied YOY, MOM, and YTD measures to identify seasonal trends in Sales and Returns.

**YOY Growth %:**

```dax
YOY Growth % = 
DIVIDE([Total Sales] - [Sales Last Year], [Sales Last Year], 0)
```

**MOM Growth %:**

```dax
MOM Growth % = 
DIVIDE([Total Sales] - [Prev Month Sales], [Prev Month Sales], 0) * 100
```

**YTD Sales:**

```dax
YTD Sales = TOTALYTD([Total Sales], Date_Dim[Date])
```

**YTD Returns:**

```dax
YTD Returns = TOTALYTD([Total Returns], Returns_Fact[ReturnDate])
```

---

### 🔹 4️⃣ Dashboard Layout

The report is structured across **6 pages** — 1 Main Overview, 2 Detail Pages, 1 Drillthrough Page, 1 Tooltip Page, and 1 Parameters Page:

#### 📄 Home Page  — (Sales & Customer Intelligence Dashboard)

<img width="1200" height="700" alt="Screenshot 2026-04-30 112343" src="https://github.com/user-attachments/assets/6711e707-4ffd-465c-95ab-f406cd8d56a9" />

---

#### 📄 Page 1 — Overview (Sales & Customer Intelligence Dashboard)

<img width="1200" height="700" alt="Screenshot 2026-04-30 113130" src="https://github.com/user-attachments/assets/ec4e16c1-f47d-45db-85b2-0184e3a7f947" />

---

- **KPI Cards:** Total Sales (844.02K) · Total Profit (457.80K) · Total Returns (50) · YOY Growth % (2026.8%)
- **Line Chart:** Total Sales vs YTD Sales by Month 
- **Donut Chart:** Total Sales by Category (Technology · Furniture · Office Supplies)
- **Bar Chart:** Total Sales by Region
- **Matrix Table:**  with conditional formatting
- **Slicers:** Quarter · Region · Year

---

#### 📄 Page 2 — Products Analysis

---
<img width="1200" height="700" alt="Screenshot 2026-04-30 113300" src="https://github.com/user-attachments/assets/e5db8167-704f-4fce-a22d-3eebce30adfd" />

---

TREND LINE AND FORECAST

---

<img width="313" height="98" alt="Screenshot 2026-04-30 123006" src="https://github.com/user-attachments/assets/2f7fef52-faa9-43ca-968b-3bf6f3e7a0a3" />

---

- **KPI Cards:** Total Products (100) · Avg Margin % (0.54) · Top Category (Office Supplies)
- **Summary Table:** Category-wise Total Sales · Total Profit · sum of Profit Margin
- **Bar Chart:** Top N Products by Total Sales (TOP N DONE HERE)
- **Line Chart:** Total Sales by Day ( TREND LINE AND FORECAST )
- **Slicers:** Year · Category

---

#### 📄 Page 3 — Customer Analysis

<img width="1200" height="700" alt="Screenshot 2026-04-30 113728" src="https://github.com/user-attachments/assets/0a0a7ab4-0046-4456-943e-c4f2af02ba7a" />

---

- **KPI Cards:** Total Customers (198) · Avg Sales per Customer (4.26K) · Return Rate % (0.05)
- **Donut Chart:** Total Customers by Segment
- **Bar Chart:** Top N Customers by Profit ( TOP N DONE HERE )
- **Detail Table:** FullName · Total Sales · Total Returns · Total Profit ( DONE DRILLTHROUGH FROM THESE TABLE )
- **Slicers:** Segment · Region · Year

---

#### 📄 Page 4 — Drillthrough

<img width="1200" height="700" alt="Screenshot 2026-04-30 114028" src="https://github.com/user-attachments/assets/74b211d4-e465-4b2d-8462-2cf7009a0df5" />

---

<img width="488" height="286" alt="Screenshot 2026-04-30 114718" src="https://github.com/user-attachments/assets/5bb526c4-1228-4eb9-ba49-069457d40a2b" />

---

- **KPI Cards:** Total Returns · Return Rate % · YTD Returns
- **Bar Chart:** Total Returns by ReturnReason
- **Detail Table:** ReturnID · FullName · ProductName · Retrun Reason

---

#### 📄 Page 5 — Tooltip

<img width="145" height="109" alt="Screenshot 2026-04-30 114844" src="https://github.com/user-attachments/assets/647c9964-b4e3-4ec6-86da-106943fca076" />

---

<img width="490" height="275" alt="Screenshot 2026-04-30 115005" src="https://github.com/user-attachments/assets/f0ff71a6-1aac-43ff-a96d-6b8d82b5c7a0" />

---

- Compact card visual showing **Total Sales** and **Total Profit**
- Assigned as a hover Tooltip on main dashboard visuals

#### 📄 Page 6 — Manage Parameters

<img width="303" height="225" alt="Screenshot 2026-04-30 114913" src="https://github.com/user-attachments/assets/9cb39027-58d5-40d1-99a4-8e8a7fd185f5" />

---


- **Field Parameter** (`Chosen Measure`) for dynamic switching between Total Sales · Total Profit · Total Returns
- **Period Slicer:** Month / Quarter / Year
- **Year Slicer:** 2024 · 2025
- **Matrix Table:** Selected measure values per customer × year

---

### 🔹 5️⃣ Filtering & Interaction

- Added **Slicers** for Product, Customer Segment, Region, and Date
- Used **Drill Up/Down** and **Drillthrough filters** across pages
- Implemented **Numeric Range Parameters** for custom filtering on sales values

---

### 🔹 6️⃣ Navigation & UX

---
###  Bookmarks and buttons 

<img width="230" height="31" alt="Screenshot 2026-04-30 115105" src="https://github.com/user-attachments/assets/8bbce53b-c1b6-4042-a8e2-6c4c8ffe71ee" />

---

### Condiional Formatting 

<img width="152" height="92" alt="Screenshot 2026-04-30 115137" src="https://github.com/user-attachments/assets/13c52dc1-106f-423f-8b0a-d674e0795de1" />

---

- Added **Custom Buttons & Bookmarks** for smooth page navigation (Overview → Products → Customer → Drillthrough)
- Built a  **Slicer Panel** for a cleaner report canvas
- Enabled **Tooltips** with mini visual summaries on hover
- Used **Advanced Conditional Formatting** in Matrix and Table views (color-coded by performance)

---

### 🔹 7️⃣ Mobile Layout

---

<img width="1200" height="700" alt="Screenshot 2026-04-30 122026" src="https://github.com/user-attachments/assets/62cba0b1-9c57-40fd-a692-05f333a53c50" />

---

- Optimized key pages for **mobile viewing**
- Prioritized **KPI Cards** and **Top N visuals** in the mobile layout view

---

### 🔹 8️⃣ Security

---
<img width="1200" height="700" alt="Screenshot 2026-04-30 122625" src="https://github.com/user-attachments/assets/ba956ec1-152f-44f5-9d93-712f8c7c2620" />

---

- Added **Roles for Region Managers** using Row-Level Security (RLS)
- Simulated **row-level security** so each Region Manager can only view data for their assigned region

---

## 📌 Key Insights from the Dashboard

✔️ **Office Supplies** was the top-selling category with the highest total sales volume

✔️ **YOY Growth reached 2026.8%** — reflecting strong year-on-year expansion

✔️ **Anthony Mendoza** ranked as the highest profit-generating customer

✔️ **Return Rate is only 0.05%** — indicating strong product and delivery quality

✔️ **All 3 customer segments** (Consumer · Corporate · Home Office) had a balanced distribution

✔️ The **Drillthrough page** enables seamless investigation of individual return records

✔️ **Field Parameters** make the dashboard fully dynamic — viewers switch between KPIs without navigating to separate pages

✔️ **RLS roles** ensure each Region Manager sees only their regional data

---

## ⚠️ Challenges Faced & How I Solved Them

| Challenge | How It Was Solved |
|-----------|-------------------|
| YOY measure returning blanks for the first year | Used `DIVIDE` with 0 as alternate result to handle blank denominator |
| `Margin Category` column showing incorrect buckets | Verified `Profit Margin %` was stored as a ratio (0–1) and adjusted thresholds |
| Field Parameter not appearing in slicer | Added `Chosen Measure Fields` to slicer and set `Chosen Measure Order` for sorting |
| Drillthrough page not activating on right-click | Placed the drillthrough field in the **Drillthrough** well on Page 4 |
| Tooltip appearing on wrong visuals | Set page type to **Tooltip** and assigned it per visual in the Format pane |
| RLS roles not filtering correctly | Verified DAX filter on `Region_Dim[RegionName]` matched exact values in the dataset |
| Slicer panel overlapping visuals | Used Bookmarks to toggle panel visibility — hidden by default, shown on button click |

---

## 🛠️ Tools & Technologies Used

| Tool | Features Used |
|------|--------------|
| Power BI Desktop | Model View, Report View, Field Parameters, Drillthrough, Tooltips, Bookmarks, RLS |
| Power Query (M Language) | Data type enforcement, column cleanup, header promotion |
| DAX | CALCULATE, FILTER, ALL, SUMX, AVERAGEX, SWITCH, COUNTX, RELATED, Time Intelligence |
| Power BI Model View | Star Schema layout, relationship cardinality, hidden fields |
| Matrix & Table Visuals | Conditional formatting, measure verification |

---

## 📈 How to Use

1. Download or clone this repository
2. Open `PR_3_SALES_INTELLIGENCE.pbix` in **Microsoft Power BI Desktop**
3. Go to **Model View** to explore the Star Schema and all table relationships
4. Navigate to **Report View** and switch pages using the **custom navigation buttons**
5. Use the **Slicers** (Year · Region · Segment · Category) to filter the dashboard interactively
6. **Right-click** any customer or product data point → **Drillthrough** to see detailed return records
7. **Hover** over visuals to activate the **Tooltip** page for quick Sales & Profit summary
8. Open **Manage Parameters** page and use the `Chosen Measure` slicer to switch KPIs dynamically
9. To test **RLS**, go to Modeling tab → View As → select a Region Manager role

---

## 🌟 Future Enhancements

- [ ] Connect to a **live SQL Server** data source for scheduled refresh
- [ ] Build a **What-If Parameter** for discount impact scenario analysis
- [ ] Publish to **Power BI Service** with automatic data refresh
- [ ] Add **AI Visuals** — Key Influencers & Decomposition Tree for deeper insight discovery
- [ ] Expand **RLS** to cover Customer Segment-level access control

---

## 👩‍💻 Shruti Bhawsar

📍 Ahmedabad | 

[![GitHub](https://img.shields.io/badge/GitHub-shrutiii87-181717?style=flat&logo=github)](https://github.com/shrutiii87)

---

⭐ **If You Like This Project**

Give this repository a ⭐ and feel free to fork or contribute!

📊 *Clean Models · Sharp DAX · Confident Insights*
