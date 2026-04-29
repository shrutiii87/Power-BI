# 📊 Student Performance Dashboard – Academic & Behavioral Insights

An interactive **Power BI Dashboard** built to analyze academic performance, attendance, and behavior of students across different grades, subjects, and terms. This project demonstrates end-to-end Power BI skills including data modeling, DAX measures, interactive visualizations, drillthrough, tooltips, bookmarks, and mobile layout.

---

## 🚀 Project Overview

The dashboard provides a multi-tab interactive report that allows educators and analysts to explore student data from both an academic and behavioral perspective — with individual student drillthrough profiles and full mobile support.

---

## 🎬 Project Demo Video

[![Watch the Project Walkthrough](https://img.shields.io/badge/▶️%20Watch%20Demo-Google%20Drive-blue?style=for-the-badge&logo=google-drive)]([https://drive.google.com/file/d/1x6efKuSzRKSjEv3kJi2alaJJ4lJl6E7Q/view?usp=sharing](https://drive.google.com/file/d/1fLobH8qLwbFO81Kp4vdha1VRxOxMBrtD/view?usp=sharing))

> 📺 Click the badge above to watch the full project walkthrough video on Google Drive.

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

<img width="383" height="253" alt="Screenshot 2026-04-27 232240" src="https://github.com/user-attachments/assets/67e8edb8-b3c1-4d10-a3b0-3bdad4609bdb" />


---

### 🔹 2️⃣ DAX Measures

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

#### 📌 Home Page

<img width="900" height="450" alt="Home Page" src="https://github.com/user-attachments/assets/878fe8e9-f4a8-45a2-9358-4cf7143e56bd" />


#### 📌 Academic View Page

<img width="900" height="500" alt="Screenshot 2026-04-28 175317" src="https://github.com/user-attachments/assets/e11987b8-5804-4118-a8d2-16eaa6d94f40" />


---

<img width="135" height="224" alt="Screenshot 2026-04-27 232938" src="https://github.com/user-attachments/assets/e98c6d0c-bd6a-4aa6-84a1-15afe7b199fd" />

---
**KPI Cards:**
- Total Students → `TOTAL Student`
- Avg Score per Subject → `Avg Score per Subject`
- Attendance % → `Attendance %`

**Bar Chart – Average Score by Subject:**
- Y-axis: `Subject` (from Scores.csv)
- X-axis: `Avg Score per Subject`
- Legend: `Class`
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

<img width="900" height="500" alt="Screenshot 2026-04-27 231859" src="https://github.com/user-attachments/assets/ac1aaca4-a9e9-400e-a7cc-4931e0f97bc3" />

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

---

<img width="900" height="500" alt="Screenshot 2026-04-27 231928" src="https://github.com/user-attachments/assets/2c8d51c4-83f3-4c7d-b9a1-a4d263792f04" />

---

<img width="350" height="254" alt="Screenshot 2026-04-27 233028" src="https://github.com/user-attachments/assets/4b1ca145-6865-471e-8837-4a2d15c190b6" />

---

<img width="615" height="349" alt="Screenshot 2026-04-27 233111" src="https://github.com/user-attachments/assets/036239cf-ca92-47f8-91dc-4b51f706a008" />


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

---

<img width="256" height="188" alt="Screenshot 2026-04-27 232804" src="https://github.com/user-attachments/assets/04c1d728-4338-4e4e-bb82-90af01103366" />

---
<img width="612" height="343" alt="Screenshot 2026-04-27 232834" src="https://github.com/user-attachments/assets/aa4fef10-0dc1-45c5-9a88-8327022f3989" />

---

A custom tooltip page configured to appear on hover over the **Average Score by Subject** visual on the Academic View page.

**Contents:**
- Clustered Bar Chart: Subject vs `% Score`
- Card: `Class Avg`

---

#### 📌 Storytelling Page

<img width="900" height="500" alt="Screenshot 2026-04-28 175448" src="https://github.com/user-attachments/assets/a735cb5d-f89b-45ed-bd88-9364ac56c948" />


---

#### 📌 Bookmarks

---

<img width="603" height="40" alt="Screenshot 2026-04-27 233244" src="https://github.com/user-attachments/assets/949e4e1e-cad1-4deb-a852-eaa72cc15758" />



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

<img width="130" height="224" alt="Screenshot 2026-04-27 233318" src="https://github.com/user-attachments/assets/a2cc80bd-fbce-4501-bbcb-bfe5ce641557" />


---
All measures are organized in a dedicated table called **Measure Management** in the Fields Pane, keeping the model clean and measures easy to find.

---

### 🔹 6️⃣ Mobile Layout *(Optional — Completed)*

---

<img width="280" height="400" alt="Mobile layout" src="https://github.com/user-attachments/assets/c0dd8344-02a6-4333-8cb8-1ea393dbee6a" />

---

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
