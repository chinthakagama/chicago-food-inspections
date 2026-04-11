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
This ensures consistent aggregation and avoids duplication bias
