Chicago Food Inspections Risk Analysis Dashboard
________________________________________ 
Project Overview
This project analyzes the Chicago Food Inspections dataset using Excel Power Query and Power BI to identify operational risks, inspection failures, violation trends, and geographic risk patterns.

The project demonstrates end-to-end data cleaning, exploratory data analysis (EDA), feature engineering, and dashboard development workflows.
________________________________________
Objectives
•	Clean and standardize complex, real-world inspection data with inconsistencies, missing values, and unstructured text 
•	Engineer actionable features from raw data, including violation counts, risk scoring, and time-based attributes 
•	Identify and quantify key risk drivers behind inspection failures across facility types and time periods 
•	Deliver an analysis-ready dataset designed for immediate use in dashboards and data-driven decision-making
________________________________________
Data Structure
The dataset is organized into four main components:
Category	           Fields
Identifiers	    - Inspection ID, License
Business Info	  - Facility Type, Risk
Outcomes	      - Results, Violations
Time & Location	- Inspection Date, ZIP Code, Coordinates
________________________________________
Data Audit
Initial profiling was conducted using Power Query tools:
•	Column Quality 
•	Column Distribution 
•	Column Profile 
 
Key Issues Identified
•	Missing values (e.g., ZIP codes, violations) 
•	Inconsistent categorical values (Results, Facility Type) 
•	Incorrect data types (dates stored as text) 
•	Unstructured text in the Violations field 
________________________________________
Data Cleaning Pipeline
1. Data Type Standardization
•	Dates → converted to date format 
•	ZIP codes → stored as text (to preserve leading zeros) 
•	Coordinates → converted to decimal 

2. Remove Redundant Fields
•	Dropped duplicate geographic fields 
•	Removed constant columns (e.g., City, State) 

3. Outcome Modelling
Inspection outcomes were decomposed into separate dimensions:
•	Inspection Result: Pass, Pass With Condition, Fail 
•	Inspection Status: Completed, Not Completed 
•	Exception Type: 
o	Not Ready 
o	No Entry 
o	Out of Business 
This avoids flattening outcomes and preserves analytical clarity.

4. Failure Flag
A binary indicator was introduced:
•	Is_Failed = 1 → Fail 
•	Is_Failed = 0 → Pass / Conditional 
•	NULL → Not Completed 

This enables accurate failure rate calculations and separates operational issues from business closures.
________________________________________
Feature Engineering
Risk Normalization
Raw	Clean
Risk 1	High
Risk 2	Medium
Risk 3	Low
Derived features:
•	Risk_Level 
•	Risk_Score (High=3, Medium=2, Low=1) 
________________________________________
Facility Type Standardization
Messy categories were grouped using keyword-based logic into:
•	Restaurant 
•	Retail Food 
•	Institutional 
•	Mobile Vendor 
•	Other 
________________________________________
 
Violations Processing
Violation Count
•	Extracted from unstructured text 
Severity Proxy
Violations	Severity
5+	High
2–4	Medium
1	Low
Keyword Flags
•	Hygiene issues 
•	Temperature issues 
•	Food handling issues 
Note: These are heuristic-based due to unstructured data.
________________________________________
Time Features
Extracted:
•	Year 
•	Month 
•	Year-Month 
•	Day of Week 
________________________________________
 
Data Modelling (Grain Clarification)
Original Structure
•	1 row = 1 inspection 
•	Violations stored as a delimited text field 
Transformation Approach
•	Violations were parsed from the text field 
•	Intermediate step (if applied): split into individual violation rows 
•	Final dataset restored to inspection-level granularity 
Final Structure
•	1 row = 1 inspection 
Derived Fields
•	Violation_Count 
•	Is_Failed
This ensures consistent aggregation and avoids duplication bias.
________________________________________
Exploratory Data Analysis

Hypothesis 1: Higher-risk facilities fail more often
•	Test: Failure rate by risk level 
•	Insight: Manufacturing category represent the highest compliance risk and may require stricter monitoring or targeted training due to operational constraints. Shared kitchens demonstrate consistently low failure rates, likely benefiting from standardized processes and infrastructure, making them a lower-risk category. Other facility types remain stable at approximately 25% failure rates, suggesting predictable but moderate compliance risk across these segments. 
________________________________________
Hypothesis 2: Facility type influences failures
•	Test: Failure rate by facility category 
•	Insight: Restaurants undergo the highest inspection volume yet maintain comparatively low failure rates, suggesting stable compliance despite operational complexity. This indicates that higher inspection frequency in this category does not necessarily correspond to higher risk, and may reflect regulatory focus rather than performance.
________________________________________
Hypothesis 3: Violations correlate with failure
•	Test: Average violations by inspection result 
•	Insight: With approximately 57% of inspections resulting in passes or minor conditional violations, most establishments operate within acceptable compliance thresholds. This suggests that enforcement efforts may be more effective if focused on the smaller subset of high-risk, non-compliant facilities.
•	Note: This relationship is partly structural, not purely causal 
________________________________________
Hypothesis 4: Geography impacts outcomes
•	Geographic hotspot identification
________________________________________
Hypothesis 5: Seasonality exists
•	Test: Monthly failure trends 
•	Insight: While failure rates remain steady at just above 20% for most of the year, a clear increase during July–September suggests seasonal pressure on operations. This period may require intensified inspections or targeted compliance measures to mitigate elevated risk.
________________________________________
Dashboard Features
• KPI monitoring
• Failure trend analysis
• Facility risk segmentation
• Geographic inspection mapping
• Interactive slicers and filters
________________________________________
KPIs
• Total Inspections
• Completed Inspections
• Fail Count
• Fail Rate
• Average Violations
________________________________________
Key Insights
• High-risk facilities produced the highest failure rates
• Restaurants showed the largest concentration of violations
• Conditional passes represented a significant portion of inspections
• Geographic clustering revealed localized operational risks
________________________________________
Tools & Technologies Used
• Excel Power Query
• Power BI
• DAX
• Data Modeling
• Exploratory Data Analysis (EDA)
________________________________________
Key Outcomes
•	Cleaned and standardized complex, real-world inspection data with missing values and inconsistent formats 
•	Transformed unstructured violation text into measurable metrics (counts, severity proxies, keyword flags) 
•	Revealed concentrated risk in specific facility types and seasonal periods 
•	Delivered a dataset structured for immediate use in business intelligence and decision-making
________________________________________
Portfolio Value
This project highlights:
•	Practical data cleaning skills 
•	Handling of unstructured text data 
•	Feature engineering techniques 
•	Hypothesis-driven analysis
• Skills in generating interactive Power BI daskboard
•	Business-focused thinking 
________________________________________
Business Value
This dashboard enables operational monitoring, compliance tracking, and risk assessment for food inspection activities using interactive business intelligence reporting.
________________________________________
## Before Cleaning
![Raw Data](assets/before)

## After Cleaning
![Cleaned Data](assets/after)

## Example Insight
![Charts](assets/charts)
________________________________________
Dataset Source
Chicago Food Inspections Dataset
(https://www.kaggle.com/datasets/chicago/chicago-food-inspections)
________________________________________
Author
Chathura
Data Analyst | Power BI | Excel Power Query | EDA | Freelancer
________________________________________
Next Steps
• Expand into a full case study
________________________________________
Dashboard interactive views
<img width="1953" height="1100" alt="Screenshot (270)" src="https://github.com/user-attachments/assets/722095d9-4d0e-431a-9caa-4bbc1567910c" />
<img width="1929" height="1225" alt="Screenshot (269)" src="https://github.com/user-attachments/assets/ab0aa325-6b2a-42d4-bf42-b86b85b8cc3e" />
<img width="1946" height="1098" alt="Screenshot (268)" src="https://github.com/user-attachments/assets/07e4d99b-bb16-4334-ad7d-a5932936d8f6" />
<img width="1964" height="1103" alt="CFIdb1" src="https://github.com/user-attachments/assets/b091460e-0b7a-474a-a25f-130169141b0f" />


