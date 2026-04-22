# 📊 DAX Depo – Advanced Calculations Using DAX in Power BI

An advanced Power BI DAX project focused on building calculated columns, measures, filter context behavior, time intelligence, quick measures, and iterator functions — all organized in a structured, multi-tab report layout.

---

## 🚀 Project Overview

This project demonstrates end-to-end **DAX (Data Analysis Expressions)** inside Microsoft Power BI Desktop. The focus is purely on DAX calculations across multiple categories — no complex visuals, just clean logic verified through Matrix tables and Card visuals.

---

## 📁 Project files 

| File | Description |
|------|-------------|
| 📄 `Sales_Fact` | Main Power BI file  |
| 📁 `files used` | Files used in project |
| 📷 `Project images` | task screenshots |
| 📘 `README>md` | Readme of the project |

---

## 📁 Data Sources

| File | Key Columns |
|------|-------------|
| 📊 `Sales_Fact` | SalesID, CustomerID, ProductID, RegionID, DateKey, SalesAmount, Cost, Quantity |
| 👥 `Customer_Dim` | CustomerID, FirstName, LastName, Segment |
| 📦 `Product_Dim` | ProductID, ProductName, Category, Subcategory |
| 🌍 `Region_Dim` | RegionID, RegionName |
| 📅 `Date_Dim` | DateKey, Date, Month, Quarter, Year |
| 🔄 `Returns_Fact` | ReturnID, SalesID, ReturnDateKey, Reason |

---

## 🔗 Relationships & Data Model

![Relationships](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Relationships.png)

![Joining and Relationships](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/joining%20and%20relationships.png)

---

## 🧩 Project Tasks Breakdown

---

### 🔹 1️⃣ Calculated Columns

Calculated columns extend existing tables with new row-by-row computed values.

#### Profit & ReturnFlag — `Sales_Fact`

```dax
Profit = 'Sales_Fact'[SalesAmount] - Sales_Fact[Cost]
```

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

![Calculated Column - Profit & ReturnFlag](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Calculated%20column%20(2).png)

![Calculated Column 2](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Calculated%20Coloumn%20(2).png)

---

#### Customer Full Name — `Customer_Dim` (CONCATENATE)

```dax
Customer Full Name =
Customer_Dim[FirstName] & " " & Customer_Dim[LastName]
```

![Concat](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Concat.png)

---

#### UPPER & LEFT

![UPPER and LEFT](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/UPPER%20%2C%20LEFT.png)

---

#### IF, AND, OR, SWITCH

![IF AND OR SWITCH](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/IF%20%2C%20AND%20%2C%20OR%20%2C%20SWITCH.png)

---

#### YEAR, EOMONTH

![YEAR EOMONTH](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/YEAR%20%2C%20EOMONTH%20%2C%20YEAR.png)

---

### 🔹 2️⃣ Measures

```dax
Total Sales = SUM(Sales_Fact[SalesAmount])
```

![Measures](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Measures.png)

---

### 🔹 3️⃣ Measure Management

All DAX measures are stored in a dedicated **`_Measures`** table for clean organization.

![Measure Management](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Measure%20Managment.png)

---

### 🔹 4️⃣ Filter Context & Behavior

```dax
North Region Sales =
CALCULATE(
    [Total Sales],
    FILTER(Region_Dim, Region_Dim[RegionName] = "North")
)
```

```dax
Sales % of Total =
DIVIDE(
    [Total Sales],
    CALCULATE([Total Sales], ALL(Region_Dim)),
    0
) * 100
```

```dax
Total Sales All Regions =
CALCULATE(
    [Total Sales],
    ALL(Region_Dim)
)
```

![Filter Context and Behaviour](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Filter%20context%20and%20behaviour.png)

---

### 🔹 5️⃣ DAX Operators

![DAX Operators](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Dax%20Operators.png)

---

### 🔹 6️⃣ Quick Measures

![Quick Measures](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Quick%20Measures.png)

---

### 🔹 7️⃣ Time Intelligence

```dax
Sales YTD =
TOTALYTD(
    [Total Sales],
    Date_Dim[Date]
)
```

```dax
Sales Last Year =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(Date_Dim[Date])
)
```

```dax
Running Total Sales =
CALCULATE(
    [Total Sales],
    DATESBETWEEN(
        Date_Dim[Date],
        MIN(Date_Dim[Date]),
        MAX(Date_Dim[Date])
    )
)
```

```dax
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

![Time Intelligence](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/time%20intelligence.png)

---

### 🔹 8️⃣ Additional Scenarios — Iterator Functions

```dax
TotalRevenue =
SUMX(
    Sales_Fact,
    Sales_Fact[Quantity] * Sales_Fact[Cost]
)
```

```dax
AvgOrderValue =
AVERAGEX(
    Sales_Fact,
    Sales_Fact[Quantity] * Sales_Fact[Cost]
)
```

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

![Additional Scenario](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Additional%20Scenario.png)

![Additional Scenario 2](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Additional%20Scenario%20(2).png)

---

### 🔹 9️⃣ Output Requirement

![Output Requirement](https://raw.githubusercontent.com/shrutiii87/Power-BI/main/PR_3_DAX_DEPO/project%20images/Output%20Requirement.png)

---

## 🛠️ Tools & Technologies Used

| Tool | Features Used |
|------|---------------|
| Power BI Desktop | Report View, Table View, Model View |
| DAX | Calculated Columns, Measures, Iterator Functions, Time Intelligence |
| Power Query | Data import, type casting, blank row removal |
| Quick Measures | YoY Growth %, MoM% auto-generation |
| Fields Pane | Measure table organization |

---

## 📈 How to Use

1. Download the repository
2. Open `DAX_DEPO.pbix` in **Microsoft Power BI Desktop**
3. Navigate across report tabs to explore each DAX category
4. Go to **Table View** to inspect calculated columns row by row
5. Open the **Fields Pane** to browse the `_Measures` table

---

## 👩‍💻 Shruti Bhawsar

📍 Ahmedabad

---

⭐ **If You Like This Project** — give this repository a ⭐ and feel free to fork or contribute!

> 🗂️ *Clean DAX. Clear Context. Confident Insights.*
