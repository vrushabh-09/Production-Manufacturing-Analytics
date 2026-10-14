<div align="center">

# 🏭 Production-Manufacturing-Analytics

### End-to-end production, quality, downtime and workforce analytics built in **Power BI**

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-39%20Measures-5F7A8C?style=for-the-badge)
![Data Model](https://img.shields.io/badge/Star%20Schema-1%20Fact%20%2B%205%20Dims-2B3340?style=for-the-badge)
![Pages](https://img.shields.io/badge/Report%20Pages-5-EDC373?style=for-the-badge)
![Records](https://img.shields.io/badge/Fact%20Records-500%2B-4C8C7A?style=for-the-badge)

</div>

## 🎥 Dashboard Demo

<div align="center">

[![Watch the demo](Executive%20overview%20Dashboard%20Report1.png)](https://drive.google.com/file/d/1KwGHzLhLYLvRKkvRh99fTwHj5V2tTKKN/view?usp=sharing)

▶️ *Click the image to watch the dashboard demo*

</div>

---

## 📑 Table of Contents

1. [Project Overview](#-project-overview)
2. [Business Problem & Objectives](#-business-problem--objectives)
3. [Key Features](#-key-features)
4. [Tech Stack](#-tech-stack)
5. [Data Model](#-data-model)
6. [Dashboard Walkthrough](#-dashboard-walkthrough)
   - [1. Executive Overview](#1-executive-overview-dashboard)
   - [2. Production Analysis](#2-production-analysis-dashboard)
   - [3. Quality & Defects](#3-quality--defects-dashboard)
   - [4. Machine & Downtime Analysis](#4-machine--downtime-analysis-dashboard)
   - [5. Employee & Shift Performance](#5-employee--shift-performance-dashboard)
7. [KPI & DAX Measure Catalogue](#-kpi--dax-measure-catalogue)
8. [Key Insights](#-key-insights)
9. [Repository Structure](#-repository-structure)
10. [Getting Started](#-getting-started)
11. [Author](#-author)

---

## 📊 Project Overview

This project is a **🏭 Production-Manufacturing-Analytics** built in Power BI. It turns raw manufacturing production records into an interactive, five-page report that lets plant managers, quality engineers, maintenance leads and HR/shift supervisors monitor performance from a single place.

The solution is powered by a clean **star schema** (1 fact table + 5 dimension tables), a library of **39 DAX measures** (OEE, MTBF, Defect Rate, First Pass Yield, Cost of Poor Quality and more), and a consistent navigation and slicer experience across every page.

| | |
|---|---|
| **Domain** | Manufacturing / Operations Analytics |
| **Tool** | Microsoft Power BI Desktop |
| **Modelling** | Star schema, one-to-many relationships |
| **Data period** | January 2023 – December 2024 |
| **Volume** | 500+ production fact records · ~174K units produced |
| **Report pages** | 5 pages · 25+ interactive visuals |

---

## 🎯 Business Problem & Objectives

Manufacturing teams often track output, quality and downtime in disconnected spreadsheets, which makes it hard to see *why* performance moves. This dashboard answers the questions that matter on the shop floor:

- 📈 **How much are we producing**, and is the trend improving?
- ⚙️ **How effective is our equipment** (OEE) against target?
- 🔍 **Where do defects come from**, and what do they cost us?
- ⏱️ **Which machines and downtime categories** hurt availability the most?
- 👷 **Which shifts and employees** drive output and quality?

---

## ✨ Key Features

- ✅ **Star schema design**: 1 fact table + 5 dimension tables for fast, simple DAX
- ✅ **5 report pages** with 25+ interactive visuals and cross-filtering
- ✅ **39 DAX measures** including OEE, MTBF, MTTR, Defect Rate, First Pass Yield
- ✅ **Global slicers** on every page: Shift, Role, Machine, Product Category
- ✅ **Button-based side navigation** with active-page highlighting
- ✅ **Dynamic card colours** driven by KPI performance
- ✅ **Pareto, waterfall, treemap, donut, scatter and trend visuals** for varied analysis

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Visualisation & reporting | Power BI Desktop |
| Data modelling | Star schema (Power BI Model view) |
| Calculation language | DAX |
| Data source | CSV files generated with Python (`Generate data.ipynb`) |
| Data generation | Python (Jupyter Notebook) |
| Version control | Git / GitHub |

---

## 🧩 Data Model

The model follows a classic **star schema**: a central `Production` fact table surrounded by five dimension tables. All relationships are **one-to-many (1 → \*)** from dimension to fact.

![Data Model](Data%20Model.png)

```text
                    Product ──┐
                    Machine ──┤
                    Employee ─┼──<  Production  >── Date
                    Shift ────┘
```

### Tables

| Table | Type | Grain | Key Columns |
|---|---|---|---|
| **Production** | Fact | One production record | `ProductionID`, `DateKey`, `MachineKey`, `ProductKey`, `EmployeeKey`, `ShiftKey`, `CycleTime_Min`, `DefectCount`, `Downtime_Min`, `Downtime Reason`\*, `Hour of Day`\* |
| **Product** | Dimension | One product | `ProductKey`, `ProductCode`, `ProductName`, `ProductCategory`, `SellingPrice`, `StandardCost` |
| **Machine** | Dimension | One machine | `MachineKey`, `MachineName`, `Line`, `Manufacturer`, `Age_Years`, `Capacity_PerHour` |
| **Employee** | Dimension | One employee | `EmployeeKey`, `EmployeeName`, `Role`, `Experience_Years`, `HourlyRate` |
| **Shift** | Dimension | One shift | `ShiftKey`, `ShiftName`, `ShiftType`, `StartTime`, `EndTime` |
| **Date** | Dimension | One calendar day | `DateKey`, `Date`, `Month`, `MonthName`, `IsWeekend`, … |

<sub>\* Calculated columns.</sub>

### Relationships

| From (1) | To (\*) | Key |
|---|---|---|
| `Product` | `Production` | `ProductKey` |
| `Machine` | `Production` | `MachineKey` |
| `Employee` | `Production` | `EmployeeKey` |
| `Shift` | `Production` | `ShiftKey` |
| `Date` | `Production` | `DateKey` |

---

## 🖥️ Dashboard Walkthrough

Every page shares the same layout: a **navigation panel** on the left, **four global slicers** (Shift, Role, Machine, Product Category) at the top, a **KPI card row**, and **four analytical visuals**.

### 1. Executive Overview Dashboard

![Executive Overview Dashboard](Executive%20overview%20Dashboard%20Report1.png)

**Purpose:** a one-glance health check of the whole plant for leadership.

| KPI Card | Description |
|---|---|
| **Total Produced** | Total units produced (~174K) |
| **OEE %** | Overall Equipment Effectiveness |
| **Total Downtime (Hrs)** | Cumulative downtime hours (186) |
| **Revenue Lost to Defects** | Selling-price value of defective units (~$665K) |
| **MTBF (Min)** | Mean time between failures |

**Visuals:** Total Produced by Date (area/line trend) · Defect Rate by Product (bar) · Total Produced by Shift (donut) · OEE % vs OEE Target % by Month (column)

---

### 2. Production Analysis Dashboard

![Production Analysis Dashboard](Production%20analysis%20Dashboard%20Report2.png)

**Purpose:** understand output volume, cycle time and machine utilisation across products and shifts.

| KPI Card | Description |
|---|---|
| **Total Quantity** | Total units produced |
| **Avg Cycle Time (Min)** | Average minutes per production cycle |
| **Total Setup Time (Min)** | Cumulative setup time |
| **Utilization %** | Share of capacity used |
| **MTBF (Min)** | Mean time between failures |

**Visuals:** Total Produced by Date · Total Produced by Product Category (treemap) · Total Produced by Shift and Product Category (stacked bar) · Avg Cycle Time and Total Produced by Month (bubble)

---

### 3. Quality & Defects Dashboard

![Quality and Defects Dashboard](Quality%20and%20defects%20Dashboard%20Report3.png)

**Purpose:** quantify defects, find the biggest contributors and measure the cost of poor quality.

| KPI Card | Description |
|---|---|
| **Total Defects** | Defective units (5,359) |
| **Defect Rate** | Defects ÷ units produced (3.1%) |
| **First Pass Yield** | Share of units right the first time (96.9%) |
| **Cost of Poor Quality** | Financial impact of defects (~$692K) |
| **Rework Estimate** | Estimated units needing rework (~27K) |

**Visuals:** Total Defects & Defect Pareto % by Product (combo) · Total Defects by Month (waterfall) · Product-level quality table · Machine × Product defect table

---

### 4. Machine & Downtime Analysis Dashboard

![Machine and Downtime Analysis Dashboard](Machine%20and%20downtime%20analysis%20Dashboard%20Report4.png)

**Purpose:** pinpoint which machines and downtime categories reduce availability.

| KPI Card | Description |
|---|---|
| **Total Downtime (Hrs)** | Total hours of stoppage (186) |
| **Avg Downtime / Event** | Average minutes per downtime event |
| **Machine Availability %** | Uptime share of scheduled time |
| **OEE by Machine** | OEE at machine level |
| **Top Underperformer** | Machine flagged with the weakest performance |

**Visuals:** Total Downtime (Hrs) by Machine (bar) · Total Downtime (Hrs) by Month (area/column) · Average Downtime Min by Downtime Reason (donut: Major / Medium / Minor) · OEE and OEE Target by Line (column)

---

### 5. Employee & Shift Performance Dashboard

![Employee and Shift Performance Dashboard](Employee%20and%20shift%20performance%20Dashboard%20Report5.png)

**Purpose:** compare productivity and quality across shifts, roles and individual operators.

| KPI Card | Description |
|---|---|
| **Total Operators** | Headcount in scope (20) |
| **Overtime Hours** | Downtime hours on the overtime (Night) shift |
| **Best Shift Name** | Shift with the highest total output (Night) |
| **Experience–Defect Correlation** | Correlation between experience and defect rate |
| **Defect Rate** | Overall defect rate (3.1%) |

**Visuals:** Total Produced by Year / Quarter / Month / Day (drill-down trend) · Total Produced by Employee (bar) · Total Produced and Defect Rate by Hourly Rate (scatter) · Employee detail table (role, output, defect rate, efficiency, hourly rate)

---

## 🔧 KPI & DAX Measure Catalogue

The model contains **39 DAX measures** in an `All Measures` table, organised into display folders. The key definitions are below.

```dax
// ── Base measures ───────────────────────────────────────
Total Produced      = SUM ( Production[QuantityProduced] )
Total Defects       = SUM ( Production[DefectCount] )
Total Downtime (Hrs)= SUM ( Production[Downtime_Min] ) / 60
Defect Rate         = DIVIDE ( [Total Defects], [Total Produced], 0 ) * 100

// ── OEE ─────────────────────────────────────────────────
Availability = DIVIDE ( [Total Cycle Time (Min)] + [Total Setup Time (Min)],
                        [Total Cycle Time (Min)] + [Total Setup Time (Min)] + [Total Downtime (Min)], 0 )
Performance  = DIVIDE ( [Total Produced], [Total Cycle Time (Min)] / 2, 0 ) * 100   // 2 units/min standard
Quality      = DIVIDE ( [Total Produced] - [Total Defects], [Total Produced], 0 ) * 100
OEE          = [Availability] * DIVIDE ( [Performance], 100 ) * DIVIDE ( [Quality], 100 )

// ── Financial ───────────────────────────────────────────
Revenue                 = SUMX ( Production, Production[QuantityProduced] * RELATED ( Product[SellingPrice] ) )
Revenue Lost to Defects = SUMX ( Production, Production[DefectCount]      * RELATED ( Product[SellingPrice] ) )
Cost of Poor Quality    = [Revenue Lost to Defects] + ( [Total Defects] * 5 )      // $5 rework per defect

// ── Reliability ─────────────────────────────────────────
MTBF (Min) = DIVIDE ( [Total Cycle Time (Min)], COUNTROWS ( FILTER ( Production, Production[Downtime_Min] > 0 ) ) )
MTTR (Min) = DIVIDE ( [Total Downtime (Min)],   COUNTROWS ( FILTER ( Production, Production[Downtime_Min] > 0 ) ) )
```

| Folder | Measures |
|---|---|
| **Base** | Total Produced, Total Defects, Total Downtime (Min / Hrs), Total Cycle Time, Total Setup Time, Total Production Runs, Avg Cycle Time, Avg Setup Time, Defect Rate, Defect Pareto %, Rework Cost / Estimate, Downtime Reason, Total Operators, Overtime Hours, Best Shift Name, Experience Defect Correlation, Worst Machine OEE |
| **OEE** | Availability, Performance, Quality, OEE |
| **Financial** | Revenue, Revenue Lost to Defects, Cost of Production, Profit |
| **Targets & Benchmarks** | OEE Target (85%), Defect Rate Target (3%), Efficiency Target (90%), OEE vs Target |
| **MTBF & MTTR** | MTBF (Min), MTTR (Min) |
| **Advanced** | Production Efficiency, First Pass Yield, Cost of Poor Quality, Employee Productivity |

> 🎨 **Dynamic formatting:** KPI card colours change conditionally based on target thresholds, so good and poor performance is visible at a glance.

---

## 💡 Key Insights

> Findings come from analysing the 500 production runs (1 Jan 2023 – 29 Dec 2024). Differences between groups were tested with a chi-square test (α = 0.05). Where an insight depends on a group difference, it states whether the result is **statistically significant** or not, to avoid over-reading noise.

### 💰 Financial & Volume

| # | Insight | Evidence |
|---|---|---|
| 1 | **The plant generated ~$21.6M revenue and ~$11.0M gross profit** (50.8% margin) on 174,026 units. | Revenue = units × selling price; profit = revenue − standard cost |
| 2 | **Defects erase ~3.1% of revenue**: $664.7K lost revenue, or **$691.5K** Cost of Poor Quality including $5/defect rework. | 5,359 defects × selling price |
| 3 | **Volume ≠ value.** Brakes are 20.6% of units but only 7.0% of revenue, while Transmission is 8.9% of units but 18.0% of revenue. | Brakes $1.52M vs Transmission $3.88M |
| 4 | **Electrical and Cooling are the revenue engines**: $4.84M and $4.73M, about 44% of total revenue between them. | Category revenue |

### 🔍 Quality & Defects

| # | Insight | Evidence |
|---|---|---|
| 5 | **Overall defect rate is 3.08%, just above the 3% target**; **14 of 24 months missed target**. Best month: Nov 2024 (2.02%). Worst: May 2024 (4.24%). | Monthly defect rate |
| 6 | **Quality worsened in 2024**: defect rate rose from **2.96% to 3.20%** (significant, p = 0.004), while output fell 4.7% and lost revenue grew **+9.7%** ($317K → $348K). | 2023 vs 2024 |
| 7 | **Defect count is the wrong lens for prioritising.** Brake Rotor has the most defects (638) only because it has the most runs (63), and its rate is among the lowest (2.87%). Ranked by value, **Transmission Gear ($128K), Radiator ($107K) and Axle ($103K) cause ~51% of lost revenue**. | Pareto by lost revenue |
| 8 | **Highest defect rates by product**: Shock Absorber 3.39%, Transmission Gear 3.30%, Brake Pad 3.29% (product differences significant, p = 0.019). Brake Pad has a high rate but tiny cost ($13.6K, 2% of loss) because of its low price. | Product table |
| 9 | **Machine quality differs significantly (p < 0.001)**. Assembly-01 is worst at **3.53%** and Assembly-02 best at **2.66%**, even though both sit on Line C and run the same type of work. This points to machine-specific setup or calibration, not line design. | Machine defect rates |
| 10 | **Hot spots**: Pressing-02 × Brake Rotor (211 defects, 3.71%), Assembly-01 × Brake Pad (3.92%), Pressing-01 × Shock Absorber (3.75%). | Machine × product |
| 11 | **About 1 in 5 runs (96 of 500) exceeds a 5% defect rate**, so the problem comes from specific bad runs as much as from averages. | Run-level defect rate |

### ⏱️ Machines & Downtime

| # | Insight | Evidence |
|---|---|---|
| 12 | **185.6 hours of downtime across 490 of 500 runs** (98% of runs had some stoppage; average 22.3 min per run). | Total downtime |
| 13 | **Three machines cause ~58% of downtime**: CNC-Mill-02 (38.4 h), Pressing-02 (34.5 h) and Assembly-02 (34.3 h). **Line B** is the worst line with 68.4 h (36.9%). | Downtime by machine / line |
| 14 | **Major stoppages (> 30 min) are the biggest lever**: they are 33% of stoppage events but **55% of all downtime minutes**. Medium events (11–30 min) add 39%, and minor events (≤ 10 min) only 6%. | Downtime buckets |
| 15 | **The newest machines stop most per run**: Assembly-02 (0.5 yr) 23.9 min and CNC-Mill-02 (1 yr) 23.3 min, against 20.5–20.7 min for Assembly-01 and Pressing-01. The pattern suggests commissioning or ramp-up issues rather than wear, but with only 6 machines it needs confirming. | Downtime per run vs machine age |

### 👷 Shifts & Workforce

| # | Insight | Evidence |
|---|---|---|
| 16 | **Night shift produces the most (36.2% of units) because it runs the most batches** (178 vs 159–163). Output per run (354 vs 344–346) and defect rate (3.05–3.12%) do not differ significantly across shifts (p = 0.50 and 0.71). "Best shift" is a volume effect, not a performance gap. | Shift comparison |
| 17 | **Night shift carries the most downtime**: 69.2 h (37.3%), about 23.3 min per run vs 21.0 on Evening. It is the worst shift for downtime on 4 of 6 machines (Assembly-01/02, CNC-Mill-01, Pressing-01). | Shift × machine |
| 18 | **Role matters for quality (p = 0.004)**: Supervisors have the lowest defect rate (**2.78%**), then Operators (3.11%), then Quality Inspectors (3.31%). Employee18 (Supervisor) is the top producer (12,569 units) with a 2.50% defect rate. | Role comparison |
| 19 | **Experience and pay do not predict quality**: experience vs defect rate r = 0.15 (not significant), hourly rate vs defect rate r = −0.09. Output differences between employees are mostly explained by how many runs they were assigned. | Employee-level correlation |
| 20 | **Weekend runs have a lower defect rate (2.89%) than weekday runs (3.15%)** (significant, p = 0.006) and carry 28% of total output. Downtime per run is the same on both (about 22 min). | Weekend vs weekday |

### 📅 Seasonality

| # | Insight | Evidence |
|---|---|---|
| 21 | **Output peaks in Q1 and Q3** (~28% of units each) and **dips in Q2 (21%)**. August (17.6K) and January (17.1K) are the strongest months and April (11.8K) the weakest, a **1.5× peak-to-trough swing**. | Monthly output |
| 22 | **Line differences are not significant** (defect rate p = 0.68), so improvement effort should target individual machines and products, not whole lines. | Line comparison |

### ✅ Recommended Actions

1. **Fix Assembly-01 first** (highest defect rate), and audit why Assembly-02 on the same line performs 0.9 pp better. Replicate its setup.
2. **Attack major stoppages (> 30 min)** on CNC-Mill-02, Pressing-02 and Assembly-02. They hold over half of all downtime.
3. **Prioritise Transmission Gear, Radiator and Axle** for quality work, as they drive ~51% of lost revenue.
4. **Investigate night-shift downtime** (maintenance coverage, staffing, handover).
5. **Reverse the 2024 quality decline** by reviewing what changed after 2023.
6. **Share supervisor practices** with operators and inspectors, since the data shows supervisors run the lowest defect rate.

---

## 📁 Repository Structure

```text
Production-Manufacturing-Analytics/
│
├── 📊 Dashboard Screenshots
│   ├── Executive overview Dashboard Report1.png
│   ├── Production analysis Dashboard Report2.png
│   ├── Quality and defects Dashboard Report3.png
│   ├── Machine and downtime analysis Dashboard Report4.png
│   ├── Employee and shift performance Dashboard Report5.png
│   └── Data Model.png
│
├── 🗄️ Dataset (Star Schema)
│   ├── FactProduction.csv         # Fact table: production records
│   ├── DimDate.csv                # Date dimension
│   ├── DimEmployee.csv            # Employee dimension
│   ├── DimMachine.csv             # Machine dimension
│   ├── DimProduct.csv             # Product dimension
│   └── DimShift.csv               # Shift dimension
│
├── 🐍 Generate data.ipynb         # Jupyter notebook that generates the dataset
└── 📄 README.md
```

| File | Purpose |
|---|---|
| `FactProduction.csv` | Central fact table (cycle time, defects, downtime, keys) |
| `Dim*.csv` | Five dimension tables: Date, Employee, Machine, Product, Shift |
| `Generate data.ipynb` | Python notebook used to create the synthetic manufacturing data |
| `*.png` | Report page screenshots and the data model diagram used in this README |

---

## 🚀 Getting Started

### Prerequisites
- [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (latest version recommended)

### Building from scratch

1. Download the CSV files (`FactProduction` and the five `Dim*` files), or regenerate them by running `Generate data.ipynb`.
2. In Power BI Desktop, **Get Data → Text/CSV** and load every file.
3. In **Model view**, create the one-to-many relationships listed in [Data Model](#-data-model).
4. Mark `Date` as a date table and add the DAX measures.
5. Build the pages following the [Dashboard Walkthrough](#-dashboard-walkthrough).

---

## 👤 Author

**Vrushabh Patil**
📧 [Email Me](mailto:vrushabhpatil97711@gmail.com) · 💼 [LinkedIn](https://www.linkedin.com/in/patilvrushabh/) · 🐙 [GitHub](https://github.com/vrushabh-09)

---

<div align="center">

⭐ If you found this project useful, please consider giving it a star!

</div>
