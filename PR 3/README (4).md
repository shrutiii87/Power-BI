# 📊 DAX Depo – Advanced Calculations Using DAX in Power BI

An advanced Power BI DAX project focused on building calculated columns, measures, filter context behavior, time intelligence, quick measures, and iterator functions — all organized in a structured, multi-tab report layout.

---

## 🎬 Project Demo Video

▶ **[WATCH DEMO – GOOGLE DRIVE](#)**

🖥️ *Click the badge above to watch the full project walkthrough video on Google Drive.*

---

## 🚀 Project Overview

This project demonstrates end-to-end **DAX (Data Analysis Expressions)** implementation inside Microsoft Power BI Desktop. The focus is purely on DAX calculations across multiple categories:

- 🧮 **Calculated Columns** — Profit, ReturnFlag, Customer Full Name, Margin Category, Product Label, Category Code
- 📐 **Measures** — Total Sales, Total Cost, Total Profit, Return Rate %, Avg Sale per Transaction
- 🔍 **Filter Context & Behavior** — ALL(), FILTER(), CALCULATE() with region-level breakdowns
- ⚡ **Quick Measures** — YoY Sales Growth %, Month-over-Month Sales %
- 📅 **Time Intelligence** — Sales YTD, Sales Last Year, Running Total, Sales Last 3 Months
- 🔁 **Iterator Functions** — SUMX(), AVERAGEX() for row-by-row calculations
- 🗂️ **Measure Management** — Dedicated `_Measures` table for clean organization

---

## 🗂️ Project Files

| File Name | Description |
|-----------|-------------|
| 📄 `DAX_DEPO.pbix` | Main Power BI file with all DAX calculations and report tabs |
| 📘 `README.md` | Project documentation (this file) |
| 📁 `Source Files/` | Source Excel files used in the project |

---

## 📁 Data Sources

| File | Key Columns |
|------|-------------|
| 📊 `Sales_Fact.xlsx` | SalesID, CustomerID, ProductID, RegionID, DateKey, SalesAmount, Cost, Quantity |
| 👥 `Customer_Dim.xlsx` | CustomerID, FirstName, LastName, Segment |
| 📦 `Product_Dim.xlsx` | ProductID, ProductName, Category, Subcategory |
| 🌍 `Region_Dim.xlsx` | RegionID, RegionName |
| 📅 `Date_Dim.xlsx` | DateKey, Date, Month, Quarter, Year |
| 🔄 `Returns_Fact.xlsx` | ReturnID, SalesID, ReturnDateKey, Reason |

---

## 🖼️ Project Preview

> *(Add project preview screenshot here)*

---

## 🧩 Project Tasks Breakdown

---

### 🔹 1️⃣ Calculated Columns

Calculated columns extend existing tables with new row-by-row computed values.

#### **Profit Column** — `Sales_Fact`

```dax
Profit = 'Sales_Fact'[SalesAmount] - Sales_Fact[Cost]
```

#### **ReturnFlag Column** — `Sales_Fact`

```dax
ReturnFlag =
IF(
    COUNTROWS(
        FILTER(
            Returns_Fact,
            Returns_Fact[SalesID] = Sales_Fact[SalesID]
        )
    ) > 0,
    "Returned",
    "Not Returned"
)
```

#### **Customer Full Name Column** — `Customer_Dim`

```dax
Customer Full Name =
Customer_Dim[FirstName] & " " & Customer_Dim[LastName]
```

#### **Margin Category Column** — `Sales_Fact`

```dax
Margin Category =
SWITCH(
    TRUE(),
    (Sales_Fact[SalesAmount] - Sales_Fact[Cost]) < 100, "Low Margin",
    (Sales_Fact[SalesAmount] - Sales_Fact[Cost]) < 300, "Medium Margin",
    (Sales_Fact[SalesAmount] - Sales_Fact[Cost]) < 800, "High Margin",
    "Super Margin"
)
```

> *(Add screenshot of Margin Category column output here)*

---

### 🔹 2️⃣ Measures

Measures are dynamic aggregations that respond to filter context.

```dax
Total Sales = SUM(Sales_Fact[SalesAmount])

Total Cost = SUM(Sales_Fact[Cost])

Total Profit = [Total Sales] - [Total Cost]

Return Rate % =
DIVIDE(
    COUNTROWS(FILTER(Returns_Fact, Returns_Fact[SalesID] <> BLANK())),
    COUNTROWS(Sales_Fact),
    0
) * 100

Avg Sale per Transaction =
DIVIDE([Total Sales], COUNTROWS(Sales_Fact), 0)
```

> *(Add screenshot of Measures page output here)*

---

### 🔹 3️⃣ Filter Context & Behavior

Demonstrates how CALCULATE(), ALL(), and FILTER() manipulate filter context.

```dax
Total Sales All Regions =
CALCULATE(
    [Total Sales],
    ALL(Region_Dim)
)

Sales % of Total =
DIVIDE(
    [Total Sales],
    CALCULATE([Total Sales], ALL(Region_Dim)),
    0
) * 100

North Region Sales =
CALCULATE(
    [Total Sales],
    FILTER(Region_Dim, Region_Dim[RegionName] = "North")
)
```

> *(Add screenshot of Filter Context & Behaviour page output here)*

---

### 🔹 4️⃣ Quick Measures

Power BI's Quick Measures feature was used to auto-generate complex DAX patterns.

- **YoY Sales Growth %** — Year-over-Year comparison of SalesAmount
- **Sum of SalesAmount MoM%** — Month-over-Month percentage change

> *(Add screenshot of Quick Measure page output here)*

---

### 🔹 5️⃣ Time Intelligence

Time-based DAX functions require a properly marked Date table.

```dax
Sales YTD =
TOTALYTD(
    [Total Sales],
    Date_Dim[Date]
)

Sales Last Year =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(Date_Dim[Date])
)

Running Total Sales =
CALCULATE(
    [Total Sales],
    DATESBETWEEN(
        Date_Dim[Date],
        MIN(Date_Dim[Date]),
        MAX(Date_Dim[Date])
    )
)

Sales Last 3 Months =
CALCULATE(
    [Total Sales],
    DATESINPERIOD(
        Date_Dim[Date],
        MAX(Date_Dim[Date]),
        -3,
        MONTH
    )
)
```

> *(Add screenshot of Time Intelligence page output here)*

---

### 🔹 6️⃣ Additional Scenarios — Iterator Functions

SUMX() and AVERAGEX() iterate row by row before aggregating.

```dax
TotalRevenue =
SUMX(
    Sales_Fact,
    Sales_Fact[Quantity] * Sales_Fact[Cost]
)

AvgOrderValue =
AVERAGEX(
    Sales_Fact,
    Sales_Fact[Quantity] * Sales_Fact[Cost]
)
```

> *(Add screenshot of Additional Scenario page output here)*

---

### 🔹 7️⃣ Measure Management

All DAX measures are stored in a single dedicated **`_Measures`** table for clean organization and easy discoverability across the data model.

> *(Add screenshot of _Measures table in Fields pane here)*

---

## 📊 Report Tab Structure

| Tab | Content |
|-----|---------|
| **Measure** | Total Sales, Return Rate %, Total Profit, Total Cost, Avg Sale per Transaction |
| **Filter Context & Behaviour** | Sales by Region with ALL(), FILTER(), CALCULATE() |
| **Dax Operators** | Total Quantity Sold, Transaction Count, Max Sale, Unique Customers, Avg Quantity |
| **Quick Measure** | MoM%, YoY Growth %, Sales % of Total |
| **Time Intelligence** | Sales YTD, Sales Last Year, Sales Last 3 Months, Running Total |
| **Additional** | TotalRevenue (SUMX), AvgOrderValue (AVERAGEX) |

---

## 📌 Key Metrics at a Glance

| Metric | Value |
|--------|-------|
| 💰 Total Sales | 848K |
| 📦 Total Cost | 686K |
| 📈 Total Profit | 162K |
| 🔁 Return Rate % | 9.42% |
| 🧾 Avg Sale per Transaction | 848.40 |
| 👥 Unique Customers | 100 |
| 📦 Total Quantity Sold | 2,995 |
| 🔢 Transaction Count | 1,000 |
| 📊 Max Sale | 2,770 |
| 📉 Avg Quantity | 3.00 |

---

## 📌 Key Insights

- ✔️ **Central region** had the highest individual sales at 182,496, making up **21.51%** of total revenue
- ✔️ **East region** had the lowest share at **17.86%** (151,499)
- ✔️ **Sales YTD (848K)** matches Running Total, confirming no data outside the current year
- ✔️ **Sales Last Year is Blank** — confirms the dataset only contains a single year's data
- ✔️ **Sales Last 3 Months = 210K** — shows concentrated sales activity toward year-end
- ✔️ **MoM% = 8.89%** shows steady month-over-month growth
- ✔️ **SUMX TotalRevenue = 3M** vs SUM-based 848K — confirms Quantity × Cost aggregation behaves differently from SalesAmount SUM
- ✔️ All measures are centralized in `_Measures` table for maximum model clarity

---

## ⚠️ Challenges Faced & How I Solved Them

| Challenge | Solution |
|-----------|----------|
| ReturnFlag using row context from a different table | Used `FILTER()` inside `COUNTROWS()` to match SalesID across tables |
| Sales Last Year returning Blank | Confirmed data only spans one year — expected and correct behavior |
| SUMX result much larger than SUM-based Total Sales | Understood that SUMX iterates Quantity × Cost per row, not SalesAmount |
| Measures cluttering dimension tables | Created a blank dedicated `_Measures` table and moved all measures there |
| Quick Measure YoY returning 0.00 | Single year of data — no prior year exists for comparison |

---

## 🛠️ Tools & Technologies Used

| Tool | Features Used |
|------|---------------|
| Power BI Desktop | Report View, Table View, Model View |
| DAX | Calculated Columns, Measures, Iterator Functions, Time Intelligence |
| Power Query | Data import, type casting, blank row removal |
| Quick Measures | YoY Growth %, MoM% auto-generation |
| Fields Pane | Measure table organization, column renaming |

---

## 📈 How to Use

1. Download the repository
2. Open `DAX_DEPO.pbix` in **Microsoft Power BI Desktop**
3. Navigate across report tabs to explore each DAX category
4. Go to **Table View** to inspect calculated columns row by row
5. Open the **Fields Pane** to browse the `_Measures` table
6. Use **Matrix visuals** on Filter Context & Behaviour tab to see ALL() vs FILTER() in action

---

## 🌟 Future Enhancements

- [ ] Build an interactive **Sales Dashboard** using these measures as the backend
- [ ] Add **Row-Level Security (RLS)** by Region or Customer Segment
- [ ] Extend Time Intelligence with **PARALLELPERIOD** and **DATEADD**
- [ ] Add **Forecast measures** using statistical DAX patterns
- [ ] Connect to a **live SQL Server** data source via DirectQuery

---

## 👩‍💻 Shruti Bhawsar

📍 Ahmedabad

---

⭐ **If You Like This Project**

Give this repository a ⭐ and feel free to fork or contribute!

---

> 🗂️ *Clean DAX. Clear Context. Confident Insights.*
