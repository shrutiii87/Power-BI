### 🔹 7️⃣ Verification – Matrix Tables

Used Matrix visuals to verify all relationship flows:

| Matrix | Rows | Columns | Values |
|--------|------|---------|--------|
| Matrix 1 | Product Category | Region (Germany / India / USA) | Sum of Revenue |
| Matrix 2 | Fiscal Year | Return Reason (Damaged / Not Needed / Wrong Item) | Return Count |
| Matrix 3 | Customer Segment | — | Sum of Revenue |

**Matrix Results:**

### 🔹 1️⃣ Sales Group by Product Category and Region

| Category | Germany | India | USA | Total |
|----------|---------|-------|-----|-------|
| Clothing | ₹26,521 | ₹27,725 | ₹38,015 | ₹92,261 |
| Electronics | ₹26,489 | ₹31,692 | ₹44,712 | ₹1,02,893 |
| Furniture | ₹23,990 | ₹26,347 | ₹41,435 | ₹91,772 |
| **Total** | **₹77,000** | **₹85,764** | **₹1,24,162** | **₹2,86,926** |

### 🔹 2️⃣ Return Reason by Fiscal Year

| Fiscal Year | Damaged | Not Needed | Wrong Item | Total |
|-------------|---------|------------|------------|-------|
| FY2022 | 15 | 17 | 15 | 47 |
| FY2023 | 19 | 18 | 16 | 53 |
| **Total** | **34** | **35** | **31** | **100** |

### 🔹3️⃣ Revenue By Customer Segment 

| Segment | Sum of Revenue |
|---------|---------------|
| Gold | ₹95,597 |
| Platinum | ₹93,893 |
| Silver | ₹97,436 |
| **Total** | **₹2,86,926** |

---

## 🎬 Project Demo Video

[![▶ WATCH DEMO – GOOGLE DRIVE](https://img.shields.io/badge/▶%20WATCH%20DEMO-GOOGLE%20DRIVE-4285F4?style=for-the-badge&logo=googledrive&logoColor=white)](https://drive.google.com/file/d/1Ax2q81JJfqHjOYBV_VfqNsYL90CqvuoO/view?usp=sharing)

> 🖥️ Click the badge above to watch the full project walkthrough video on Google Drive.

---

## 🖼️ Project Preview 

![Project Preview](https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO_NAME/main/project_preview.png)

---

## 📌 Key Insights from the Model

✔️ Electronics was the highest revenue category at ₹1,02,893 across all regions

✔️ USA contributed the most revenue (₹1,24,162) among all regions

✔️ Return volume increased from FY2022 (47) to FY2023 (53), with "Not Needed" being the top reason

✔️ All 3 customer segments (Gold, Platinum, Silver) had nearly equal revenue distribution

✔️ The inactive relationship on `ReturnDateKey` successfully resolved filter ambiguity

✔️ Hierarchies enabled drill-down from Country → State → City and Year → Quarter → Month → Date

---

## ⚠️ Challenges Faced & How I Solved Them

| Challenge | How It Was Solved |
|-----------|------------------|
| Filter ambiguity between `Return_fact` and `Date_dim` | Set `ReturnDateKey` relationship as inactive to eliminate ambiguity |
| Incorrect data category on `ProductName` | Manually reassigned category in Column Tools tab |
| Blank rows appearing after Power Query load | Added `FilterNullAndWhitespace` step + `Removed Blank Rows` in Applied Steps |
| Relationship direction confusion | Set all relationships to single cross-filter; enabled bidirectional only where verified |
| Snowflake layout looked same as Star | Reorganized tables in a separate Model View tab named "snowflake Schema" |

---

## 🛠️ Tools & Technologies Used

| Tool | Features Used |
|------|--------------|
| Power BI Desktop | Model View, Power Query Editor, Matrix Visual |
| Power Query | Data type changes, blank row removal, header promotion |
| Power BI Model View | Relationships, cardinality settings, inactive relationships |
| Column Tools | Data categories, data formats, summarization settings |
| Data Pane (Fields) | Hierarchies, column renaming, sort by column |

---

## 📈 How to Use

1. Download the repository
2. Open `PR_2_DATA_MODELER.pbix` in Microsoft Power BI Desktop
3. Go to **Model View** to explore the Star Schema and Snowflake Schema layouts
4. Navigate to **Table View** to inspect individual tables and their data types
5. Open the **Report View** to see the Matrix verification tables
6. Use the **Fields Pane** to explore hierarchies and data categories

---

## 🌟 Future Enhancements

- [ ] Add DAX Measures (Total Revenue, Return Rate %, Avg Revenue per Customer)
- [ ] Build an interactive Sales & Returns Dashboard on top of this data model
- [ ] Add Row-Level Security (RLS) by Region or Segment
- [ ] Connect to a live SQL Server data source
- [ ] Enable incremental refresh for large datasets via Power BI Service

---

## 👩‍💻 Shruti Bhawsar
📍 Ahmedabad

---

⭐ **If You Like This Project**

Give this repository a ⭐ and feel free to fork or contribute!

> 🗂️ *Clean Models, Clear Relationships, Confident Insights*
