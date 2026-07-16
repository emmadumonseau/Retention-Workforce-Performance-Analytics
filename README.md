# Data-Driven Retention & Workforce Performance Analytics

## Project Directory
* **Tableau Dashboard:** [View Live Interactive Dashboard (Tableau Public)](https://public.tableau.com/app/profile/emma.dumonseau/viz/HRAnalyticsExecutiveDashboard_17841510951080/HRAnalyticsExecutiveDashboard)
* **Python Notebook:** [View Python Cleaning & EDA Code]()
* **Cleaned HR Dataset:** [Access Cleaned Dataset (Excel)]()
* **Raw Dataset:** [Access Raw Source Data (CSV)]()

---

## Project Overview
This project identifies systemic retention risks, demographic patterns, and training expenditures across a workforce of **3,000 employees**. Utilizing an end-to-end data engineering and analytics pipeline spanning Python, Excel, and Tableau, the project cleanses inconsistent employee records, engineers logical sentiment-risk profiles, evaluates training investment efficiency, and structures these critical findings into an executive-level HR dashboard optimized for strategic decision-making.

---

## Data Pipeline & Technical Methodology

### 1. Data Wrangling & Feature Engineering (Python)
The data pipeline began in Python using the `pandas`, `numpy`, and `xlsxwriter` libraries to automate data cleansing, handle null values, and dynamically engineer features.

* **Data Exploration & Structural Cleansing:** Examined raw datatypes and identified critical data inconsistencies. Categorical text strings were standardized by stripping hidden leading/trailing whitespaces, and system-wide default text entries like `"Unk"`, `"nan"`, and `"None"` were programmatic replaced with true `NaN` values to ensure grouping integrity.
* **Inconsistent Date Parsing:** Evaluated and parsed highly irregular, mixed-format date columns (`StartDate`, `ExitDate`, `DOB`, `Survey Date`, `Training Date`) into unified `YYYY-MM-DD` timestamps, handling null termination records for active employees.
* **Feature Engineering:**
    * **Retention Status Flags:** Formulated binary metrics `Is_Active` (1 for current employees, 0 for terminated) and `Is_Turnover` (1 for departed employees, 0 for active) to streamline quantitative calculations in Tableau.
    * **Tenure Calculation:** Calculated real-time workforce tenure by computing the date difference between start and exit dates (or using the current system date for active employees), subsequently binning records into brackets (`< 1 Year`, `1-3 Years`, `3-5 Years`, `5+ Years`).
    * **Demographic Age Classification:** Calculated exact employee age based on DOB records and established standard demographic bands (`Under 25`, `25-34`, `35-49`, `50+`) to track behavioral correlation.
* **Database Record Auditing:** Conducted exact-row duplication checks across `Employee ID` keys to ensure that each record represented a single, unique employee instance without duplicate system profiles.

### 2. Dashboard Architecture & Visual Design (Tableau)
The structured dataset was compiled and imported into Tableau to construct a responsive, executive-ready interface designed to identify systemic organizational risks instantly.

* **Grid Layout & Information Hierarchy:** Configured a highly structured three-row dashboard framework:
    * **Row 1 (Top):** High-level summary KPI Cards (*Active Headcount*, *Historical Turnover Rate*, *Average Engagement Score*) to anchor global workforce status.
    * **Row 2 (Middle):** Behavioral and demographic metrics (*Active Headcount by Tenure* and *Age & Gender Distribution*) to provide cultural context.
    * **Row 3 (Bottom):** Operational views (*Turnover by Department*, *Training Spend vs. Rating* scatter plot, and *Turnover Risk Heatmap*) to drive specific managerial interventions.
* **Color Palette Control:** Implemented a cohesive, accessibility-conscious palette utilizing blues for baseline metrics, reserving orange and warm red tones specifically to represent critical turnover metrics and high risk levels.
* **Polishing & Formatting Details:** Stripped distracting default gridlines and zero lines from all visual sheets. Corrected technical database legend labels (e.g., renaming `Gender Code` to `Gender`), resolved department name text wrapping, adjusted axis ranges, and placed compact global dropdown filters in the top-right header to maximize visual real estate.

---

## Analytical Insights & Proposed Interventions

### 1. Retention Turnover & Vulnerabilities
* **The Findings:** Organizational turnover is highly concentrated within the **Production** department, which accounts for the largest volume of historic employee departures. Analysis of the *Active Headcount by Tenure* bar chart shows a critical volume reduction in the first year of employment, demonstrating that onboarding drop-off is a primary driver of the high 51.10% historical turnover rate.
* **Proposed Intervention:** Redesign the onboarding and integration program specifically within high-volume roles. Establish structured 30, 60, and 90-day progress checks for new hires, and deploy peer-mentorship structures inside the Production division to mitigate early-career turnover.

### 2. Sentiment Analytics & Systemic Turnover Risk
* **The Findings:** The *Turnover Risk Heatmap* (evaluating combinations of Engagement and Satisfaction Scores) isolates a critical risk pocket. The **Production** department exhibits a massive, dominant cluster of active employees categorizing as **High Risk** (Satisfaction $\le 2$, Engagement $\le 2$). Conversely, departments like *Software Engineering* show highly positive sentiment clustering, pointing to strong leadership and cultural alignment.
* **Proposed Intervention:** Launch a targeted leadership and workspace assessment within the Production division. The high concentration of low engagement and low satisfaction indicates local management or physical work environment friction. Implement a confidential feedback loop to identify and resolve local leadership bottlenecks.

### 3. Training Program ROI & Performance Alignment
* **The Findings:** The *Training Spend vs. Average Current Employee Rating* scatter plot reveals significant budget inefficiencies. Several high-cost training initiatives ($600+ per employee) yield relatively flat or low subsequent employee performance scores (averaging around 2.0 to 3.0 out of 5). Meanwhile, certain cost-efficient internal programs maintain comparable, if not higher, average employee rating outcomes.
* **Proposed Intervention:** Conduct a comprehensive audit of training program content. Reallocate budget away from underperforming, high-cost external courses and reinvest those resources into expandi
