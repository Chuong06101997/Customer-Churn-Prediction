# Customer Churn Prediction – Business-Oriented Framework
## 1. Context
In the telecommunications industry, customer acquisition costs are significantly higher than retention costs. Therefore, reducing customer churn is a critical business objective to maintain stable revenue and improve profitability.
However, not all customers contribute equally to business value. Some customers generate high revenue over time, while others may yield low or even negative returns when considering acquisition and servicing costs.
## 2. Problem Statement
Traditional churn prediction focuses on identifying whether a customer will churn. However, this approach is incomplete from a business perspective.
The key challenge is:
>How can the company identify which customers are worth retaining and allocate retention resources efficiently to maximize profit?

## 3. Business Needs

The business does not simply require a high-accuracy model. Instead, it needs:

* Identification of high-risk customers (likely to churn)
* Evaluation of customer value (e.g., revenue contribution, lifetime value)
* Decision-making support on:
  >Whether to retain a customer
  >How much to invest in retention efforts

## 4. Key Insight

Not all churn events have the same impact:

Losing a high-value customer results in significant revenue loss
Losing a low-value customer may have minimal impact
Retaining a low-value or unprofitable customer may lead to unnecessary costs
Therefore:
>The goal is not to minimize churn, but to optimize retention decisions for maximum business value.

## 5. Analytical Approach

This project combines:

5.1 Churn Prediction
* Estimate the probability of each customer churning
5.2 Customer Value Assessment
  
  Approximate customer value using:
  
* Monthly Charges
* Tenure
* Total Charges
* Optionally extend to Customer Lifetime Value (CLV)
5.3 Decision Framework
  
  Retention decisions are made based on both churn risk and customer value:
  
* High churn risk + high value → prioritize retention
* High churn risk + low value → consider limited or no intervention
* Low churn risk → no immediate action required

## 6. Evaluation Metrics

Instead of relying solely on machine learning metrics such as accuracy or AUC, this project emphasizes business-oriented metrics:

6.1 Expected Profit

Profit is defined as:

Revenue retained from customers who would have churned
Minus the cost of retention actions (e.g., discounts, promotions)

6.2 Retention ROI

Return on investment for retention strategies:

Measures whether the cost of retaining customers is justified by the revenue preserved
