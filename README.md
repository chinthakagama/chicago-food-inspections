# chicago-food-inspections
This project demonstrates an end-to-end workflow for cleaning and EDA of the Chicago Food Inspections dataset. The goal is to transform raw, inconsistent inspection data into a structured dataset suitable for analysis, and to explore the key factors associated with inspection failures.
________________________________________
Objectives
•	Clean and standardize real-world, messy data 
•	Engineer features that support meaningful analysis 
•	Identify patterns linked to inspection outcomes 
•	Prepare a dataset suitable for dashboards and decision-making 
________________________________________
Data Structure
The dataset is organized into four main components:
Category	Fields
Identifiers	Inspection ID, License
Business Info	Facility Type, Risk
Outcomes	Results, Violations
Time & Location	Inspection Date, ZIP Code, Coordinates
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
•	Insight: A pattern exists, but may be influenced by inspection bias 
________________________________________
Hypothesis 2: Facility type influences failures
•	Test: Failure rate by facility category 
•	Insight: Restaurants show higher failure rates, likely due to operational complexity 
________________________________________
 
Hypothesis 3: Violations correlate with failure
•	Test: Average violations by inspection result 
•	Insight: Failed inspections have significantly higher violation counts 
•	Note: This relationship is partly structural, not purely causal 
________________________________________
Hypothesis 4: Geography impacts outcomes
•	Not explored due to limited location data 
________________________________________
Hypothesis 5: Seasonality exists
•	Test: Monthly failure trends 
•	Insight: Some variation observed; requires multi-year validation 
________________________________________
Analytical Considerations
•	Correlation does not imply causation 
•	Inspection frequency may introduce bias 
•	Facility composition varies across categories 
•	Conditional results require careful handling 
________________________________________
Tools Used
•	Excel Power Query 
________________________________________
Key Outcomes
•	Built a structured dataset from inconsistent raw data 
•	Engineered features suitable for analysis 
•	Identified key drivers of inspection outcomes 
•	Created a foundation for BI reporting 
________________________________________
 
Portfolio Value
This project highlights:
•	Practical data cleaning skills 
•	Handling of unstructured text data 
•	Feature engineering techniques 
•	Hypothesis-driven analysis 
•	Business-focused thinking 
________________________________________
Dataset Source
Chicago Food Inspections Dataset
(https://www.kaggle.com/datasets/chicago/chicago-food-inspections.https://www.kaggle.com/datasets/chicago/chicago-food-inspections.)
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
