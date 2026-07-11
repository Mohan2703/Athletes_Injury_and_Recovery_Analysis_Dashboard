# 🏋️ Athletes Injury & Recovery Analysis Dashboard. 

[![View Portfolio](https://img.shields.io/badge/View%20Portfolio-%23000000.svg?style=for-the-badge&logo=firefox&logoColor=#FF7139)](https://www.datascienceportfol.io/mohan_Srinivas)
[![View Dashboard](https://img.shields.io/badge/View%20Dashboard-%23000000.svg?style=for-the-badge&logo=Codeforces&logoColor=gold)](https://app.powerbi.com/view?r=eyJrIjoiNWU0MmMyNGQtODFiMS00NzI3LTk1MDMtYWU3OTNlNmE1MjM4IiwidCI6IjQ2NTRiNmYxLTBlNDctNDU3OS1hOGExLTAyZmU5ZDk0M2M3YiIsImMiOjl9)

## Table of Contents
- [Problem Statement](#problem-statement)
- [Project Planning using Star Method](#project-planning-using-star-method)
- [Data Source](#data-source)
- [Data Preprocessing \& ETL](#data-preprocessing--etl)
- [Data Modelling](#data-modelling)
- [Data Analysis](#data-analysis)
- [Dashboard](#dashboard)
- [Findings](#findings)
- [Tools And Softwares](#tools-and-softwares)


## Problem Statement
<details>
<summary>
$\textsf{\color{blue}{View Problem Statement ➡️}}$
</summary><br>

**Problem**

In this Challenge, you will work on Athlete Health & Injury Dataset to help sports organizations minimize downtime, control costs, and enhance player availability through rigorous, data-backed injury management. Doctors, leagues, athletic trainers, and front-office executives - all benefit from granular injury insights to preserve competitive edge and safeguard athlete welfare.

**Challenges:**

- Which types of injuries occur most frequently?
- Which sports or events have the highest rate of injury?
- Are injuries more common in specific athlete age groups or genders?
- How does injury severity vary across different types of sports or positions?
- How long does recovery typically take for various injury types?
- Which treatment methods are most effective for speeding up recovery?
- Do certain coaches or teams have consistently lower injury rates?
- Are there regional differences in injury frequency or severity?
- Does the playing surface or competition level affect injury occurrence?

**Use Case & Main Goal:**

- Tests your ability to model relationships, handle conformed dimensions, and optimize DAX measures.
- Build a portfolio piece that simulates genuine business requirements in a high-stakes, performance-driven sport industry.
- Use-case allows you to craft compelling narratives around player health, financial stewardship, and competitive advantage.

</details>


## Project Planning using Star Method

<details>
<summary>
$\textsf{\color{blue}{View Stratergy ➡️}}$
</summary><br>

- **Understand key KPIs:** Total Engagement, Views, Impressions, Click-Through Rate (CTR), and Engagement Rate.
- **Build hierarchical view:** Platform → Content Category → Post Type → Post-Level Details.
- **Enable drilldowns:** from a high-level overview → campaign analysis → regional performance → content-specific insights.
- **Design dashboards:** clear filters for platform, country, campaign, content type, and date range.

### 📝 S - Situation

Sports organizations were struggling to track and analyze athlete health data at scale. Medical staff, coaches, and management faced the following challenges:

- Rising treatment costs without visibility into drivers.

- Lack of insight into injury causes, vulnerable body parts, and recurrence patterns.

- Difficulty measuring treatment effectiveness and coach impact on recovery.

- Limited ability to compare trends regionally, by sport, or by competition level.

**Context:**

- This project is part of the Athlete Health & Injury Analytics challenge, designed to simulate real-world requirements in the high-stakes sports industry. The ultimate goal is to help organizations minimize downtime, control costs, and enhance player availability through data-backed decisions.

### 🎯 T - Task

The objective was to design and implement a centralized analytics solution that:

- Consolidates raw data from injury logs, treatments, costs, and player details.

- Provides multi-dimensional insights at player, regional, and organizational levels.

- Enables stakeholders (doctors, trainers, coaches, executives) to explore:

    - Most frequent injury types and affected body parts.

    - Recovery timelines by severity, treatment, and sport.

    - Cost trends (MOM, YOY) across treatments and surfaces.

    - Coach and team effectiveness in reducing recovery times.

    - Regional and demographic (age, gender) variations.

### ⚡ A - Action

- Collected and cleaned raw data from injury reports, treatment logs, and cost data.

- Designed a data model with fact and dimension tables (injuries, players, treatments, costs, surfaces, coaches).

- Built an interactive Power BI dashboard with drill-downs by sport, injury type, region, and recovery outcomes.

- Used DAX measures for KPIs like treatment success %, YOY cost change, recovery rate, and coach impact.

- Visualized metrics using maps, bar charts, line graphs, pie charts, and custom visuals Visuals of Zoom Charts.

### 🏆 R - Result

The analytics solution delivered measurable impact:

- Enhanced visibility into injury distribution and treatment costs across 15 countries.

- Identified top sports and body parts prone to injuries, guiding prevention strategies.

- Highlighted most effective treatments and coaches that reduced recovery times.

- Provided strategic insights to reduce costs, lower recurrence rates, and safeguard athlete welfare.

- Built a portfolio-grade dashboard that demonstrates real-world decision support in sports analytics.

</details>


## Data Source
<details>
<summary>
$\textsf{\color{blue}{View Data Source ➡️}}$
</summary><br>

>- **Dataset:** Data Set Provided By [ZoomCharts](https://zoomcharts.com/en/microsoft-power-bi-custom-visuals/challenges/fp20-analytics-august-2025)
>- Injury Dataset: Player-level injury records including type, body part, severity, cause, and event type (competition, training, warm-up).
>- Treatment Dataset: Recovery methods (medication, massage, physiotherapy, surgery), days to recover, and success outcome.
>- Cost Dataset: Treatment costs broken down by sport, surface type (grass, gym floor, ring, etc.), and year.
>- Demographics: Age group, gender, coach assignment, and country-level data.

</details>


## Data Preprocessing & ETL
<details>
<summary>
$\textsf{\color{blue}{View PreProcssing Steps ➡️}}$
</summary><br>

The dataset used for this project followed a Star Schema design, with multiple dimension tables (Players, Clubs, Coaches, Injuries, Treatments, Events, Locations) and a central FactInjuries table. To ensure data quality and usability in Power BI, an ETL pipeline was implemented within Power Query.

**Steps Performed**

**1. Data Ingestion**

- Imported the raw dataset from Excel (Challenge_29_Athlete Health & Injury Dataset (Star Schema).xlsx).

- Each worksheet (DimClub, DimCoach, DimPlayer, DimInjuryType, DimTreatment, DimLocation, DimEvent, FactInjuries) was extracted individually using Excel.Workbook() function.

**3. Header Promotion & Schema Alignment**

- Promoted first row to column headers across all tables.

- Renamed columns where needed to maintain consistency.

- Applied appropriate data types (e.g., text for names, integer for keys, date for injury dates, currency for cost values).

**2. Data Cleaning**

- Removed unnecessary columns (like blank index columns sometimes created by Excel exports).

- Handled missing or null values in cost, recovery days, and outcomes with either replacement (0 for numeric, "Unknown" for categorical) or filtering if irrelevant.

- Standardized categorical fields (e.g., "Minor", "Moderate", "Severe" in DimInjuryType → ensured consistent casing).

**4. Calendar Table Creation**

- Built a dynamic Calendar Table using:
```
 CALENDAR(MIN(FactInjuries[InjuryDate]), MAX(FactInjuries[InjuryDate])).
```

- Enriched with Year, Quarter, Month, Week, and Day attributes to support time intelligence measures (YOY, MOM).

**5. Fact-Dimension Relationships**

- Ensured referential integrity by matching foreign keys in FactInjuries with dimension primary keys (e.g., PlayerDimKey → DimPlayer, ClubDimKey → DimClub).

- Verified one-to-many relationships across the schema.

**6.Data Transformation & Derived Columns**

- Created calculated columns for Age Bins (e.g., <20, 20-30, 30+) and Cost Bins for better filtering.

- Applied conditional transformations to derive severity levels, recurrent injury flags, and treatment outcomes.

✅ After ETL, the dataset was clean, typed, and structured in a Star Schema — enabling efficient DAX calculations for KPIs such as Total Injuries, Avg Recovery Days, Treatment Success %, YOY/MOM comparisons, and Cost Analysis.
</details>


## Data Modelling
<details>
<summary>
$\textsf{\color{blue}{View Modelling ➡️}}$
</summary> <br>

<img width="700" height="500" alt="Image" src="https://github.com/user-attachments/assets/8c3c1b7f-1171-42df-bfc9-a9083726a8b5" /> <br>

**The Athlete Analytics solution is built on a Star Schema, designed to balance performance with analytical flexibility.**

**Fact Table**

FactInjuries → Central transaction table that records every injury incident with key metrics and foreign keys.

- Columns: InjuryID, InjuryDate, CostOfTreatmentEuros, DaysToRecovery, EstimatedDaysAbsent, Cost_Bins.

- Foreign Keys: ClubDimKey, CoachDimKey, EventDimKey, InjuryTypeDimKey, PlayerDimKey, TreatmentDimKey, LocationDimKey, Date (Calendar).



Relationships

- FactInjuries → DimClub (Many-to-One)
Each injury belongs to one club, but a club can have many injuries.

- FactInjuries → DimCoach (Many-to-One)
Each injury is linked to one coach, but a coach may manage many injuries.

- FactInjuries → DimEvent (Many-to-One)
Injuries are tied to events (e.g., training, match), with multiple injuries per event type.

- FactInjuries → DimInjuryType (Many-to-One)
Each injury has one injury type; an injury type can apply to multiple injuries.

- FactInjuries → DimLocation (Many-to-One)
An injury occurs in a single location, but one location can host many injuries.

- FactInjuries → DimPlayer (Many-to-One)
Each injury is recorded for a single player, while players can have multiple injuries.

- FactInjuries → DimTreatment (Many-to-One)
Each injury is treated with a method, but a treatment method may apply to multiple injuries.

- FactInjuries → Calendar (Many-to-One)
Injuries are mapped to a single date, but a date can have many injuries.

</details>


## Data Analysis
<details>
<summary>
$\textsf{\color{blue}{Power BI: View Created Dax Measures, Columns, Tables ➡️}}$
</summary><br>

To derive insights, multiple DAX measures were created in Power BI. These measures enabled tracking of injuries, treatments, recoveries, costs, and regional patterns across athletes. Below is the full set of measures used, categorized by dashboard page.

**Measures:**
**📊 Athlete Health Intelligence (Page 1)**

1. Injury Metrics

```
1. Total Injuries = COUNT(Injury_ID)

2. % Minor Injuries = DIVIDE([Minor Injuries], [Total Injuries])

3. % Moderate Injuries = DIVIDE([Moderate Injuries], [Total Injuries])

4. % Severe Injuries = DIVIDE([Severe Injuries], [Total Injuries])

5. Recurrent Injury Rate = DIVIDE([Recurrent Injuries], [Total Injuries])

6. MOM Injury % = DIVIDE([Total Injuries] - [PM Total Injury], [PM Total Injury])

7. YOY Injury % = DIVIDE([Total Injuries] - [PY Total Injury], [PY Total Injury])

```
2. Recovery Metrics

```
1. Avg Days to Recover = AVERAGE(RecoveryDays)

2. Avg Days Missed per Injury Type = AVERAGE(RecoveryDays)

3. YOY Avg Recovery % = DIVIDE([Avg Days to Recover] - [PY Avg Recovery], [PY Avg Recovery])

```
**👤 Player & Treatment Analytics (Page 2)**

1. Treatment & Player Outcomes

```
1. Unique Players = DISTINCTCOUNT(Player_ID)

2. Treatment Success % = DIVIDE([Fully Recovered], [Total Treatments])

3. Limitation Recovery % = DIVIDE([Recovered with Limitation], [Total Treatments])

4. Retired Players % = DIVIDE([Retired], [Unique Players])     
```
2. Time-Based Measures

```
1. MoM Success % = DIVIDE([Treatment Success %] - [PM Success %], [PM Success %])

2. YOY Success % = DIVIDE([Treatment Success %] - [PY Success %], [PY Success %])
```
3. Coach & Group Impact
```
1. Coach Impact = AVERAGEX(VALUES(Coach), [Avg Days to Recover])

2. Recovery Rate by Gender = CALCULATE([Treatment Success %], FILTER(Players, Players[Gender] = "Male/Female"))

3. Recovery Rate by Age Group = CALCULATE([Treatment Success %], FILTER(Players, Players[AgeGroup]))
```

**💶 Cost & Regional Insights (Page 3)**

1. Cost Metrics

```
1. Total Cost = SUM(Cost)

2. Average Treatment Cost = AVERAGE(Cost)

3. Avg Monthly Cost = AVERAGEX(VALUES(Month), [Total Cost])

4. Avg Treatment Cost per Sport = AVERAGEX(VALUES(Sport), [Total Cost])

5. Running Total Treatment Cost (€) =
CALCULATE([Total Cost], FILTER(ALLSELECTED(Date), Date <= MAX(Date)))
```

2. Time-Based Cost Analysis

```
1. PM Total Cost = CALCULATE([Total Cost], DATEADD(Date[Date], -1, MONTH))

2. PY Total Cost = CALCULATE([Total Cost], DATEADD(Date[Date], -1, YEAR))

3. Total Cost (Latest Month) = CALCULATE([Total Cost], LASTDATE(Date[Date]))

4. Total Cost (Latest Year) = CALCULATE([Total Cost], YEAR(Date[Date]) = MAX(Date[Year]))
```
3. Variance / KPI Metrics

```
1. MOM Cost Change (€) = [Total Cost] - [PM Total Cost]

2. MOM Cost % = DIVIDE([Total Cost] - [PM Total Cost], [PM Total Cost])

3. YOY Cost Change (€) = [Total Cost] - [PY Total Cost]

4. YOY Cost % = DIVIDE([Total Cost] - [PY Total Cost], [PY Total Cost])
```
**🛠 Shared Utility Measures (Across Pages)**

```
1. Count Active Filters = COUNTROWS(ALLSELECTED(Table))

2. Count Active Filters Tooltip =CONCATENATEX(VALUES(Table[FilterName]), Table[FilterName], ", ")
```
</details>

## Dashboard
<details>
<summary>
$\textsf{\color{blue}{View Images ➡️}}$
</summary>

> ### 1. Athlete Health Intelligence
> <a href="https://app.powerbi.com/view?r=eyJrIjoiNWU0MmMyNGQtODFiMS00NzI3LTk1MDMtYWU3OTNlNmE1MjM4IiwidCI6IjQ2NTRiNmYxLTBlNDctNDU3OS1hOGExLTAyZmU5ZDk0M2M3YiIsImMiOjl9" target="_blank"><img width="700" height="420" alt="Image" src="https://github.com/user-attachments/assets/55b78cd7-d4f9-4a75-aacf-6642dbe37639" />
</a>

> ### 2. Player & Treatment Analytics
> <img width="700" height="420" alt="Image" src="https://github.com/user-attachments/assets/fa9fcd91-5e34-4553-99b6-68172bdcf08e" />

> ### 3. Cost & Regional Insights 
> <img width="700" height="420" alt="Image" src="https://github.com/user-attachments/assets/f2777a2e-65fc-43ec-acd3-e9dbf9c87b0b" />

</details>


## Findings
<details>
<summary>
$\textsf{\color{blue}{View Findings ➡️}}$
</summary><br>

1. Injury Trends

- Athletics had the most injuries (3,041 cases).
- Knee injuries were most common (10.8%).
- UK reported the highest injury count (1,071).

2. Recovery Timelines

- Success rate: 79.9% full recovery, 14.9% partial.
- Best treatments: Physiotherapy & medication; surgery less effective.
- Coach impact: Some coaches cut recovery time (e.g., Adélaïde Thomas – 8 days).

3. Cost Trends

- Total cost: €27.7M across all years.
- YOY costs dropped -51.5% (€6.3M → €3.1M).
- Tennis & Football were costliest sports.
- Gym floors & indoor courts drove most treatment expenses.

4. Coach & Team Effectiveness

- Recovery varied by coach and treatment.
- Some coaches directly shortened recovery timelines.
- Coaching style proved as important as medical care.

5. Demographics & Regions

- Males had more injuries (65.5%).
- Females recovered slightly better (83% success rate).
- Younger athletes healed faster than older groups.

</details>


## Tools And Softwares
<details>
<summary>
$\textsf{\color{blue}{View Tools ➡️}}$
</summary><br>

- **Power BI** → data modeling & dashboard development
- **DAX** → Custom KPIs & calculated measures
- **Excel/CSV** → Raw dataset handling
- **Icons/Images** → For visual representation in dashboard
- **Power Query (M Language)** → Data cleaning, ETL.
- **Figma/Canva (optional)** → UI design references.

</details>
