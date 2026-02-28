# 📊 Power BI Survey Report Dashboard

## Preface

This project presents a comprehensive data professional survey analysis built entirely in **Microsoft Power BI**. The dataset contains responses from **630 survey participants** across various data-related roles worldwide. The goal is to transform raw survey data into an interactive, visually compelling dashboard that surfaces key insights about salaries, programming language preferences, job satisfaction, and the perceived difficulty of breaking into the data industry.

The workflow covers the full pipeline — from raw Excel ingestion and Power Query data transformation, through calculated columns and custom measures, to final dashboard design and layout. Each step below is documented with a screenshot for reproducibility.

---

## 🔧 Process Logs

### Step 1 — Load and Transform Data from Excel

Load the raw survey Excel file into Power BI via **Get Data → Excel Workbook**, then open **Power Query Editor** to begin transformation.

![Step 1](assets/images/1.load_transform_data.png)

---

### Step 2 — Remove Useless Columns

Identify and remove columns that carry no analytical value (e.g., metadata, timestamps, or empty fields) to keep the data model clean and performant.

![Step 2](assets/images/2.remove_useless_column.png)

---

### Step 3 — Split Q1 Column by Delimiter `(` and Remove Split Remainder

Split the **Q1 – Job Title** column using `(` as the delimiter to isolate the clean job title text, then delete the resulting right-side split column containing trailing parenthetical content.

![Step 3](assets/images/3.split_q1_column.png)

---

### Step 4 — Split Q5 Column by Delimiter `:` and Remove Split Remainder

Split the **Q5 – Favorite Programming Language** column using `:` as the delimiter to extract only the language name, then remove the resulting right-side split column.

![Step 4](assets/images/4.split_q5_column.png)

---

### Step 5 — Duplicate Q3 Column and Split Copy by Digit-to-Non-Digit

Duplicate the **Q3 – Current Yearly Salary (in USD)** column, then split the copy using a **digit-to-non-digit** boundary to separate the lower and upper salary range values. Remove any extraneous split columns that are not needed.

![Step 5](5.split_q3_column.png)

---

### Step 6 — Replace Values in Q3 Split Copy and Change Data Type

On the Q3 split copy columns:
- Replace `k` → *(blank)*
- Replace `-` → *(blank)*
- Replace `+` → `225`

Then change the data type of both split columns to **Whole Number** to enable numeric calculations.

![Step 6](assets/images/6.remove_and_replace_values.png)

---

### Step 7 — Add Custom Column: Average Salary

Create a new custom column named **Average Salary** using the formula:

```
= ([#"Q3 - Current Yearly Salary (in USD) - Copy.1"] + [#"Q3 - Current Yearly Salary (in USD) - Copy.2"]) / 2
```

Set the data type to **Decimal Number**.

![Step 7](assets/images/7.costumn_column_formula.png)

---

### Step 8 — Remove Q3 Split Copy Columns

After the Average Salary column has been successfully created, remove the two Q3 split copy columns (`Copy.1` and `Copy.2`) to declutter the model.

![Step 8](assets/images/8.remove_split_copy.png)

---

### Step 9 — Split Q4 & Q11 Columns by Delimiter `(`, Remove Remainders, Close & Apply

Split both **Q4** and **Q11 – Country** columns using `(` as the delimiter to extract clean values, remove the right-side split remainders for each, then click **Close & Apply** to load the transformed data into the Power BI report view.

![Step 9](assets/images/9.remove_split_column.png)

---

### Step 10 — Create Dashboard Title with Text Box

Insert a **Text Box** at the top of the report canvas and type the dashboard title (e.g., *"Data Professional Survey Breakdown"*). Apply appropriate font size, color, and alignment to establish a clear visual hierarchy.

![Step 10](assets/images/10.create_dashboard_title.png)

---

### Step 11 — Create Cards: Count of Survey Takers & Average Age

Add two **Card** visuals:
- **Card 1:** `Unique ID` → Count → *Count of Survey Takers*
- **Card 2:** `Q10 – Current Age` → Average → *Average Age of Survey Takers*

![Step 11](assets/images/11.create_card_dashboard.png)

---

### Step 12 — Create Stacked Bar Chart: Average Salary by Job Title

Insert a **Stacked Bar Chart** with:
- **Y-Axis:** Q1 – Job Title
- **X-Axis:** Average Salary (Average)
- **Legend:** Q1 – Job Title

Title: *Average Salary by Job Title*

![Step 12](assets/images/12.stacked_bar_chart.png)

---

### Step 13 — Create Stacked Column Chart: Favorite Programming Language

Insert a **Stacked Column Chart** with:
- **X-Axis:** Q5 – Favorite Programming Language
- **Y-Axis:** Unique ID (Count)
- **Legend:** Q1 – Job Title

Title: *Favorite Programming Language*

![Step 13](assets/images/13.stacked_column_chart.png)

---

### Step 14 — Create Tree Map: Country of Survey Takers

Insert a **Tree Map** with:
- **Category:** Q11 – Country
- **Values:** Q11 – Country

Title: *Country of Survey Takers*

![Step 14](assets/images/14.create_tree_map.png)

---

### Step 15 — Create Gauge: Happiness with Work/Life Balance

Insert a **Gauge** visual with:
- **Value:** Q6 – Work/Life Balance (Average)
- **Minimum Value:** Min
- **Maximum Value:** Max

Title: *Happiness with Work/Life Balance*

![Step 15](assets/images/15.create_gauge_wlb.png)

---

### Step 16 — Create Gauge: Happiness with Salary

Insert a second **Gauge** visual with:
- **Value:** Q6 – Salary (Average)
- **Minimum Value:** Min
- **Maximum Value:** Max

Title: *Happiness with Salary*

![Step 16](assets/images/16.create_gauge_salary.png)

---

### Step 17 — Create Doughnut Chart: Difficulty to Break into Data

Insert a **Doughnut Chart** with:
- **Legend:** Q7 – Difficulty
- **Values:** Q7 – Difficulty

Title: *Difficulty to Break into Data*

![Step 17](assets/images/17.create_doughnut_chart.png)

---

### Step 18 — Arrange Dashboard

Resize, align, and reposition all visuals on the canvas for a clean, balanced layout. Apply a consistent color theme, adjust padding/spacing, and verify that all chart titles and labels are readable.

![Step 18](assets/images/18.dashboard.png)

---

## 💡 Insights

| # | Insight |
|---|---------|
| 🌍 | Survey takers are **mostly from the United States** |
| 💰 | **Data Scientists** have the **highest average salary** among all job titles |
| 👥 | There are **630 survey takers** with an **average age of 30** |
| ⚖️ | Happiness with **Work/Life Balance** is **slightly above average** |
| 💵 | Happiness with **Salary** is **slightly below average** |
| 🚪 | Most respondents say breaking into data is **neither easy nor difficult** |
| 🐍 | **Python** is the most popular programming language among survey takers |

---

## 🛠️ Tools Used

- **Microsoft Power BI Desktop** — Data transformation, modeling & visualization
- **Microsoft Excel** — Raw survey data source
- **Power Query Editor** — ETL pipeline (steps 1–9)

---

## 📁 Project Structure

```
powerbi-survey-report/
│
├── README.md
├── Survey_Dashboard.pbix        # Power BI project file
├── data/
│   └── survey_raw.xlsx          # Raw Excel survey data
└── images/
    ├── step_01.png
    ├── step_02.png
    ├── ...
    └── step_18.png
```
