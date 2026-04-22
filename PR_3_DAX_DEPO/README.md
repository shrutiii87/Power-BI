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

## 🧩 Project Tasks Breakdown

---

### 🔹 1️⃣ Calculated Columns

![Calculated Column Output](https://github.com/shrutiii87/Power-BI/blob/main/PR_3_DAX_DEPO/Project%20images/Calculated%20Coloumnn%20(1).png)

### 🔹 2️⃣ Measures 

![Measures](https://github.com/shrutiii87/Power-BI/blob/main/PR_3_DAX_DEPO/Project%20images/Measures%20(2).png)

### 🔹 3️⃣ Quick Measures 

![Quick Measures](https://github.com/shrutiii87/Power-BI/blob/main/PR_3_DAX_DEPO/Project%20images/Quick%20Measures%20(3).png)

### 🔹 4️⃣ Measures Managment

![Measures Table](https://github.com/shrutiii87/Power-BI/blob/main/PR_3_DAX_DEPO/Project%20images/Measures%20Table%20(4).png)

### 🔹 5️⃣ Filter Context & Behavior

![Filter Context & Behavior](https://github.com/shrutiii87/Power-BI/blob/main/PR_3_DAX_DEPO/Project%20images/Filter%20Context%20%26%20Behavior%20(5).png)

### 🔹 6️⃣  DAX Operators and Functions

![DAX Operators and Functions](https://github.com/shrutiii87/Power-BI/blob/main/PR_3_DAX_DEPO/Project%20images/DAX%20Operators%20and%20Functions%20(6).png)

### 🔹 7️⃣  Joining and Relationships

![Joining and Relationships](https://github.com/shrutiii87/Power-BI/blob/main/PR_3_DAX_DEPO/Project%20images/Joining%20and%20Relationships%20(7).png)

### 🔹 8️⃣  Time Intelligence (Matrix-based Analysis)

![Time Intelligence (Matrix-based Analysis)](https://github.com/shrutiii87/Power-BI/blob/main/PR_3_DAX_DEPO/Project%20images/Time%20Intelligence%20(Matrix-based%20Analysis)%20(8).png)

### 🔹 9️⃣  Additional Scenarios

![SWITCH](https://github.com/shrutiii87/Power-BI/blob/main/PR_3_DAX_DEPO/Project%20images/Additional%20Scenarios%20(9).png)

☝️ i have not done sales ranges beacuse i have taken out margin category using SWITCH .  in task DAX operators & functions . in that there was already switch so i did the sales range one there . 

![SUMX() , AVERAGEX()](https://github.com/shrutiii87/Power-BI/blob/main/PR_3_DAX_DEPO/Project%20images/Add%20Scenarios(9).png)

---

### 🔹 🔟 Output Requirement

![output requirement](https://github.com/shrutiii87/Power-BI/blob/main/PR_3_DAX_DEPO/Project%20images/Output%20Requirement%20(10).png)

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
