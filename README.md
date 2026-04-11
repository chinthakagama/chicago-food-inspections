Chicago Food Inspections — Data Cleaning & EDA
________________________________________ 
Project Overview
This project demonstrates how messy, real-world inspection data can be transformed into a reliable, analysis-ready dataset. Through systematic data cleaning, feature engineering, and exploratory analysis, 
the work identifies key risk drivers behind inspection failures — including facility type, violation patterns, and seasonal effects — and prepares the data for downstream reporting and decision-making
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
•	Inspection Result: Pass, Conditional, Fail 
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
•	Not explored due to limited location data 
________________________________________
Hypothesis 5: Seasonality exists
•	Test: Monthly failure trends 
•	Insight: While failure rates remain steady at just above 20% for most of the year, a clear increase during July–September suggests seasonal pressure on operations. This period may require intensified inspections or targeted compliance measures to mitigate elevated risk.
________________________________________
Analytical Considerations
•	Inspection outcomes may be biased by non-random inspection allocation, particularly toward higher-risk or previously non-compliant facilities 
•	The observed correlation between violations and failures is not fully independent, as violations are part of the failure criteria 
•	Seasonal increases in failure rates may reflect capacity and demand pressures, not necessarily a decline in compliance standards 
•	Cross-category comparisons should be interpreted cautiously, as facility types differ significantly in operational complexity and constraints 
•	Conditional outcomes sit between compliance and failure, and can distort binary performance metrics if not handled explicitly
________________________________________
Tools Used
•	Excel Power Query 
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
•	Business-focused thinking 
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
Data Analyst | Freelancer
________________________________________
Next Steps
•	Develop an interactive Power BI dashboard 
•	Incorporate geographic analysis 
•	Apply statistical hypothesis testing 
•	Expand into a full case study
