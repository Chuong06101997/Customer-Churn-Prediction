# Customer Churn Prediction – Business-Oriented Framework

<img width="1920" height="1280" alt="image" src="https://github.com/user-attachments/assets/ab986de4-1b8f-460c-8741-2e0dce7c1cfb" />


## Problem Definition
### 1. Context
A telecommunications company is losing customers to competitors. The dataset contains 7,043 customers with 21 features including service usage, contract type, billing, and tenure. The company has no systematic way to identify at-risk customers, nor any framework to determine whether a specific customer justifies retention investment.
Key constraints:

Retention budget is limited — cannot intervene with every at-risk customer
Acquiring a new customer costs ~$100, retaining costs ~$20/month
Customer value varies widely: monthly charges range from $18 to $119

### 2. Need
The business needs to answer two questions:

Who is likely to churn? — identify at-risk customers before they leave
Who is worth retaining? — allocate budget where it generates positive return

The real pain point is not churn rate itself, but inefficient retention spending — missing high-value churners or wasting budget on unprofitable customers.
### 3. Vision
Combine churn probability with customer value to build a profit-driven retention framework:

Estimate P(churn) per customer via Logistic Regression
Estimate customer value based on MonthlyCharges × retention horizon
Calculate expected profit per retention decision
Segment customers into actionable groups

### 4. Outcome

Retention team can focus on 367 High Risk – High Value customers with highest ROI
Cost-optimized threshold (0.15) reduces total business cost to $11,260 vs $18,540 at default threshold (0.50) — saving $7,280
893 out of 1,405 customers identified as not worth retaining at current cost structure — avoiding unnecessary spend
Decision-makers get a clear framework: retain based on expected profit, not churn probability alone


Dataset

Source: IBM Telco Customer Churn
link : https://www.kaggle.com/code/farazrahman/telco-customer-churn-logisticregression/input
7,043 customers, 21 features
Churn rate: ~26.5%


Approach
Churn Prediction
Logistic Regression trained on 80% of data, evaluated on 20% holdout set.

Feature selection based on statistical significance (p-value < 0.05) from statsmodels summary — used to interpret coefficient direction and magnitude, while sklearn handles prediction pipeline.

Customer Value Estimation

Customer Value = MonthlyCharges × RETENTION_MONTHS (3)

Represents expected revenue if the customer is retained for 3 months following intervention.

Expected Profit Framework

Expected Profit = P(Churn) × Customer Value − (Retention Cost × Retention Months)
                = P(Churn) × (MonthlyCharges × 3) − ($20 × 3)
                
→ Retain if Expected Profit > 0
