# 📊 Student Performance Dashboard – Academic & Behavioral Insights

An interactive **Power BI Dashboard** built to analyze academic performance, attendance, and behavior of students across different grades, subjects, and terms. This project demonstrates end-to-end Power BI skills including data modeling, DAX measures, interactive visualizations, drillthrough, tooltips, bookmarks, and mobile layout.

---

## 🚀 Project Overview

This project was built as part of a Power BI exam assignment (2.5–3 hours, 50 marks). The dashboard provides a multi-tab interactive report that allows educators and analysts to explore student data from both an academic and behavioral perspective — with individual student drillthrough profiles and full mobile support.

---

## 📁 Project Files

| File | Description |
|------|-------------|
| 📄 `Student_Performance_Dashboard.pbix` | Main Power BI file |
| 📁 `files used/` | Source CSV datasets |
| 📷 `Project images/` | Task screenshots |
| 📘 `README.md` | Readme of the project |

---

## 📁 Data Sources

| File | Key Columns |
|------|-------------|
| 👥 `Students.csv` | StudentID, Name, Gender, Class, Section |
| 📊 `Scores.csv` | StudentID, Subject, ExamType, Score, MaxScore, Term |
| 📅 `Attendance.csv` | StudentID, Date, Status (Present/Absent), Reason |
| 🧠 `Behavior.csv` | StudentID, Date, BehaviorType, Notes |

---

## 🧩 Project Tasks Breakdown

### 🔹 1️⃣ Data Modeling & Cleaning

- Loaded all four datasets into Power BI via Power Query
- Created relationships between tables on `StudentID`
- Cleaned column names, corrected data types
- Replaced nulls/missing values where appropriate

**Relationships (Star Schema):**

| From Table | Cardinality | To Table | Join Key |
|------------|-------------|----------|----------|
| `Students csv` | 1 | `Attendance csv` (Many) | StudentID |
| `Students csv` | 1 | `Behavior csv` (Many) | StudentID |
| `Students csv` | 1 | `Scores csv` (Many) | StudentID |

> `Students csv` acts as the central dimension table. All fact tables (`Attendance csv`, `Behavior csv`, `Scores csv`) connect to it in a one-to-many relationship via `StudentID`.

**Model View:**

![Data Model](project%20images/data_model.png)

---

### 🔹 2️⃣ DAX Measures

All measures are stored in a dedicated **Measure Management** table for organized access via the Fields Pane.

```dax
% Score = DIVIDE(SUM('Scores csv'[Score]), SUM('Scores csv'[MaxScore]))
```

```dax
Avg Score per Subject = AVERAGEX(VALUES('Scores csv'[Subject]), [% Score])
```

```dax
Attendance % = 
DIVIDE(
    COUNTROWS(FILTER('Attendance csv', 'Attendance csv'[Status] = "Present")),
    COUNTROWS('Attendance csv')
)
```

```dax
Behavior Count = COUNTROWS('Behavior csv')
```

```dax
Performance Category = 
SWITCH(
    TRUE(),
    [% Score] >= 0.80, "High",
    [% Score] < 0.40, "Low",
    "Medium"
)
```

---

### 🔹 3️⃣ Visualizations

#### 📌 Academic View Page

**KPI Cards:**
- Total Students → `TOTAL Student`
- Avg Score per Subject → `Avg Score per Subject`
- Attendance % → `Attendance %`

**Bar Chart – Average Score by Subject:**
- Y-axis: `Subject` (from Scores.csv)
- X-axis: `Avg Score per Subject` + `Class Avg`
- Shows both subject-level average and class-level average side by side

**Line Chart – Performance Trend by Term:**
- X-axis: `Term`
- Y-axis: `% Score`
- Visualizes score trends across Term 1, Term 2, and Term 3

**Table – Student-wise Scores with Conditional Formatting:**
- Columns: Name, Class, Section (from Students.csv) + `% Score`, `Attendance %`, `Performance Category`
- Conditional formatting applied:
  - 🟢 Green for `% Score > 80%`
  - 🔴 Red for `% Score < 40%`

---

#### 📌 Behavioral View Page

**KPI Cards:**
- Total Incidents
- Disruptive Count
- Helpful Count
- Participative Count

**Clustered Bar Chart – Behavior Count by BehaviorType:**
- Y-axis: `BehaviorType`
- X-axis: `Behavior Count`

**Donut Chart – Behavior Distribution:**
- Legend: `BehaviorType`
- Values: `Behavior Count`

**Slicer:**
- BehaviorType slicer (Tile style)

---

#### 📌 Student Profile (Drillthrough) Page

**KPI Cards:**
- `% Score`
- `Attendance %`
- `First Name` (from Students.csv)
- `Performance Category`
- `Section`

**Clustered Bar Chart – % Score by Subject:**
- X-axis: `Subject`
- Y-axis: `% Score`

> **How to use Drillthrough:** In the Academic View table, right-click any student name → Drillthrough → Student Profile. The page will load all metrics specific to that selected student.

---

#### 📌 Tooltip Page

A custom tooltip page configured to appear on hover over the **Average Score by Subject** visual on the Academic View page.

**Contents:**
- Clustered Bar Chart: Subject vs `% Score`
- Card: `Class Avg`

---

### 🔹 4️⃣ Interactivity

| Feature | Details |
|---------|---------|
| **Slicers** | Class (Between/Range), Section (Tiles), Subject (Tiles), Term (Tiles) |
| **Bookmarks** | Two bookmarks created for Academic View and Behavioral View — used with buttons for seamless page switching |
| **Drillthrough** | Student Profile page configured as a drillthrough destination from the Academic View table |
| **Tooltip** | Custom tooltip page hovers on the Average Score by Subject bar chart |
| **Conditional Formatting** | Applied on % Score column in table (Green > 80%, Red < 40%) |

---

### 🔹 5️⃣ Measure Management

All measures are organized in a dedicated table called **Measure Management** in the Fields Pane, keeping the model clean and measures easy to find.

---

### 🔹 6️⃣ Mobile Layout *(Optional — Completed)*

A mobile-optimized layout was created for the Academic View page, rearranging visuals vertically for the Power BI mobile app. KPI cards, bar chart, and line chart are all visible in a scrollable single-column layout.

---

## 📊 Report Tab Structure

| Tab | Content |
|-----|---------|
| **Academic View** | KPI Cards (Total Students, Avg Score, Attendance %), Bar Chart, Line Chart, Table with Conditional Formatting, Slicers |
| **Behavioral View** | KPI Cards (Incidents, Disruptive, Helpful, Participative), Bar Chart, Donut Chart, Slicer |
| **Student Profile** | Drillthrough page with individual student KPIs and subject-wise bar chart |
| **Tooltip** | Custom hover tooltip with mini bar chart and Class Avg card |

---

## 📈 How to Use

1. Download or clone the repository
2. Open `Student_Performance_Dashboard.pbix` in **Microsoft Power BI Desktop**
3. Navigate across the report tabs using the **Academic View** and **Behavioral View** bookmark buttons
4. Use slicers to filter by Class, Section, Subject, or Term
5. Right-click any student in the table → **Drillthrough → Student Profile** to view individual metrics
6. Hover over bars in the Average Score chart to see the custom **Tooltip**
7. Go to **Table View** to inspect DAX measures
8. Open the **Fields Pane** to browse the `Measure Management` table

---

## 🛠️ Tools & Technologies Used

| Tool | Features Used |
|------|--------------|
| **Power BI Desktop** | Report View, Table View, Model View, Mobile Layout |
| **DAX** | Measures, SWITCH, DIVIDE, AVERAGEX, CALCULATE, FILTER, COUNTROWS |
| **Power Query** | Data import, type casting, null handling, column renaming |
| **Bookmarks** | Page navigation between Academic and Behavioral views |
| **Drillthrough** | Individual student profile page |
| **Tooltips** | Custom hover tooltip with mini visuals |
| **Fields Pane** | Measure table organization |

---

## 👩‍💻 Shruti Bhawsar

📍 Ahmedabad

⭐ If you like this project — give this repository a ⭐ and feel free to fork or contribute!

🎓 Clean DAX. Clear Insights. Complete Dashboard.
