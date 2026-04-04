# 📊 Data Leverager – Power Query Transformation Project

An end-to-end **ETL simulation project** built using Power BI's Power Query Editor to extract, clean, reshape, and combine data from multiple sources using essential data engineering techniques.

---
## 🚀 Project Overview

This project presents a complete **Power Query ETL Pipeline** built inside Microsoft Power BI Desktop. It demonstrates real-world data engineering skills including:

- 📂 **Multi-Source Extraction** — Sales files (Jan, Feb, Mar) loaded via Folder Source + Append
- 🧹 **Data Cleaning** — Removed blanks, duplicates, renamed columns, fixed data types
- 🔤 **Text Transformations** — UPPER, LOWER, TRIM, REPLACE, Split Column
- 🔢 **Numeric Transformations** — Rounding, Custom Profit Column
- 📅 **Date & Time Tools** — Day, Month, Year, Quarter, Fiscal Month, Age
- 🔀 **Pivot & Unpivot** — Region-wise reshaping of sales data
- 🔗 **Merge & Append** — Fuzzy Nested Join of employees + sales on Region
- 📊 **Group By & Aggregation** — Total Sales, Avg Order Value, Transaction Count
- 🔍 **Data Profiling** — Column Quality, Distribution, and Profile views
- ⚙️ **Dynamic Parameters** — FolderPath parameter for dynamic data source
- 🔄 **Refresh Simulation** — Auto-loaded April data via folder source


---

## 🗂️ Project Files

| File Name | Description |
|-----------|-------------|
| 📄 `PR_1_DATA_LEVERAGER.pbix` | Main Power BI file with all 13 Power Query transformations |
| 📘 `README.md` | Project documentation (this file) |
| 🔗 `Video` | explanation of project in video ( link is below) |

---

## 📁 Data Sources

| Source | Details |
|--------|---------|
| 📂 Folder Source | `Sales_Jan.xlsx`, `Sales_Feb.xlsx`, `Sales_Mar.xlsx` — loaded via Append Queries from Folder |
| 📄 Excel File | `Employees.xlsx` — EmployeeID, Name, Department, Region, BirthDate, Joining Date |
| 🌐 Web Table | Wikipedia HTML table loaded using the Web Connector |

---

## 🧩 Transformation Tasks Breakdown

### 🔹 1️⃣ Data Extraction (Task 1)
- Loaded 3 monthly sales files using **Folder Source → Append Queries from Folder**
- Loaded `Employees.xlsx` as a separate Excel connection
- Loaded an HTML table from **Wikipedia** using the Web connector

### 🔹 2️⃣ Basic Transformations (Task 2)
- Removed blank rows and columns from sales data
- Promoted first row to headers
- Renamed columns — `Product` → `Product Name`, `JoinDate` → `Joining Date`
- Changed data types of Revenue and Cost using **Change Type with Locale**
- Removed duplicate rows

### 🔹 3️⃣ Text Tools (Task 3)
Applied on CustomerName, Product Name, and Region in sales data:

| Function | Column Applied |
|----------|----------------|
| `UPPER()` | CustomerName |
| `LOWER()` | Product Name |
| `TRIM()` | Region |
| `REPLACE()` | Revenue |
| `Split Column by Delimiter` | CustomerName → `.1` & `.2` |


### 🔹 4️⃣ Numeric Tools (Task 4)
- Rounded **Revenue** column to 2 decimal places
- Created custom column: **Profit = Revenue - Cost**

### 🔹 5️⃣ Date & Time Tools (Task 5)
- Extracted **Day, Month, Year, Quarter** from `Order Date`
- Created **Fiscal Month** column via Add Column → Date → Month
- Added calculated **Age** column from `BirthDate` in employees table

### 🔹 6️⃣ Conditional Columns & Indexing (Task 6)

| Condition | Category |
|-----------|----------|
| Revenue >= 10,000 | 🟢 High |
| Revenue >= 5,000 | 🟡 Medium |
| Otherwise | 🔴 Low |

- Added **Index Column from 0** (0-based)
- Added **Index Column from 1** (1-based)

### 🔹 7️⃣ Pivot & Unpivot (Task 7)
- **Pivot:** `Region` column → Values: `Revenue` (Region rows → columns)
- **Unpivot:** Unpivoted columns back to normalized form

### 🔹 8️⃣ Merging & Appending (Task 8)
- **Append:** Jan + Feb + Mar already combined via Folder Source ✅
- **Merge:** Fuzzy Nested Join on `Region` column


### 🔹 9️⃣ Grouping & Aggregation (Task 9)
Grouped by `Source.Name` (month/file):

| File | Total Sales | Avg Order Value | Transaction Count |
|------|-------------|-----------------|-------------------|
| Sales_Jan.xlsx | 9,24,878.91 | 23,714.84 | 39 |
| Sales_Feb.xlsx | 9,37,628.91 | 24,041.76 | 39 |
| Sales_Mar.xlsx | 9,62,280.00 | 24,057.00 | 40 |

### 🔹 🔟 Data Profiling & Quality (Task 10)
- Enabled **Column Quality**, **Column Distribution**, **Column Profile** from View tab

| Column | Distinct Values | Valid | Errors | Empty |
|--------|-----------------|-------|--------|-------|
| CustomerName | 114 | 100% | 0% | 0% |
| Region | 4 | 100% | 0% | 0% |
| Product | 5 | 100% | 0% | 0% |

### 🔹 1️⃣1️⃣ Source Settings & Parameters (Task 11)
- Created Parameter `FolderPath` (Type: Text) with current folder path as default
- Used parameter to make folder source **dynamic**
- Changed data source credentials for `Employees.xlsx` via **Data Source Settings** ✅

### 🔹 1️⃣2️⃣ Refresh Simulation (Task 12)
- Copied an existing file → renamed `Sales_Apr.xlsx` → placed in same folder
- Clicked **Refresh** in Power BI → April data loaded automatically ✅
- All previous transformations carried over successfully ✅

---

## 🎬 Project Demo Video

> ▶️ **[Click here to watch the project walkthrough video](https://drive.google.com/file/d/1mmttqSvp1TvZw6htoes8afExkHGAepTX/view?usp=sharing)**

---

## 🗃️ Query Summary

**Total Queries: 13**

| Query Name | Description |
|------------|-------------|
| `sales data` | Main cleaned & transformed sales table (Tasks 2–6) |
| `employees` | Employee dataset with age, date parts, renamed columns |
| `web table` | Wikipedia HTML table via Web connector |
| `Merge1` | Fuzzy join of employees + sales data on Region |
| `Group by` | Sales aggregated by source file (Total, Avg, Count) |
| `Data Profiling` | Column quality and distribution profiling view |
| `Pivot & unpivot` | Region-pivoted and unpivoted sales data |
| `april_sales` | Refresh simulation with Sales_Apr.xlsx |
| `folder path ("C...")` | Parameter-driven dynamic folder path query |
| `Parameter1` | FolderPath parameter (Helper Queries folder) |
| `Sample File` | Helper query for folder source |
| `Transform File` | Custom function for file transformation |
| `Transform Sa...` | Transform Sample file query |

---

## ⚠️ Challenges Faced & How I Solved Them

| Challenge | How It Was Solved |
|-----------|-------------------|
| Web connector not loading table | Used a stable Wikipedia URL and selected the correct table from Navigator |
| Change Type with Locale errors | Selected **English (India)** as locale for Revenue and Cost columns |
| Data Source Settings path error after moving files | Re-entered correct path in Data Source Settings and refreshed |

---

## 🛠️ Tools & Technologies Used

| Tool | Features Used |
|------|---------------|
| Power BI Desktop | Power Query Editor, M Language, Data Source Settings |
| Power Query | Folder Source, Web Connector, Append, Merge, Group By, Pivot/Unpivot |
| M Query Language | Custom columns, Split, FuzzyNestedJoin, Change Type with Locale |
| Excel | Source files — Sales_Jan/Feb/Mar.xlsx, Employees.xlsx |

---

## 📌 Key Insights Derived

✔️ March had the **highest total sales** at ₹9,62,280 across 40 transactions

✔️ All 3 months had nearly **equal average order values** (~₹24,000)

✔️ **Fuzzy join** successfully matched Region values despite case/space inconsistencies

✔️ Data profiling confirmed **100% data quality** — no errors, nulls, or duplicates

✔️ Dynamic parameter setup makes the pipeline **reusable across any folder path**

✔️ Refresh simulation proved the **ETL pipeline is fully automated** for new monthly data

---

## 📈 How to Use

1. Download the repository
2. Open `PR_1_DATA_LEVERAGER.pbix` in **Microsoft Power BI Desktop**
3. Go to **Transform Data** to open Power Query Editor
4. Navigate through the **13 queries** in the Queries pane on the left
5. Update the `FolderPath` parameter if your sales files are in a different location
6. Click **Close & Apply** to load transformations into the data model

---

## 🌟 Future Enhancements

- [ ] Add DAX Measures & KPI Cards in Power BI Report View
- [ ] Connect to a live SQL Server or SharePoint data source
- [ ] Automate refresh via Power BI Service + Scheduled Refresh
- [ ] Build an interactive Sales Dashboard on top of this ETL layer
- [ ] Add incremental refresh for large monthly datasets

---

## 👩‍💻 Shruti Bhawsar

📍 Ahmedabad

---

⭐ **If You Like This Project**

Give this repository a ⭐ and feel free to fork or contribute!

📊 *Turning Raw Data into Clean, Structured, Actionable Pipelines*
