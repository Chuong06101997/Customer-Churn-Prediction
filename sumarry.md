# Analytical Summary — Customer Churn Prediction & Profit Optimization

## Why This Project Exists
Telecom companies routinely run retention campaigns on any customer flagged as "at risk." The implicit assumption is that retaining customers is always worth the cost. It often isn't.
This project starts from a different premise: churn probability alone is not a decision. A customer with 70% churn probability but $18/month in charges may not justify a $60 intervention. A customer with 40% churn probability but $100/month in charges very likely does.
The goal is not to minimize churn rate. It is to maximize the return on retention spend.

## Analytical Decisions and Why They Were Made
Why Logistic Regression
Logistic Regression was chosen deliberately over more complex models. For a business-oriented project, interpretability matters: the model needs to explain why a customer is at risk, not just that they are. Logistic Regression produces coefficients that can be directly interpreted as directional effects, which feeds into the business recommendation layer.
The model also converges cleanly on this dataset and generalizes reasonably well — 10-fold cross-validation accuracy of 80.3% — without requiring extensive tuning.
## Why Three Scalers Were Run
Coefficients from Logistic Regression are only comparable when features are on the same scale. Three versions were run for different analytical purposes:

* Unscaled — to confirm statistical significance. All features returned p-value < 0.05, meaning none should be dropped on significance grounds.
StandardScaler (Z-score) — to interpret effects in terms of standard deviation units. MonthlyCharges (+1.02) and tenure (−1.16) show moderate but meaningful effects per one-SD change.
MinMaxScaler — to compare relative magnitude across all features on a [0,1] scale. This is what the coefficient chart in the README reflects. MonthlyCharges (+3.40) and tenure (−3.39) emerge as the two dominant and nearly symmetric drivers — one pushing churn up, one pulling it down.

Running all three is not redundant. It confirms that the MonthlyCharges–tenure relationship is robust across scaling choices, not an artifact of one particular normalization.
Why Threshold 0.15 Was Selected
The default classification threshold of 0.50 assumes symmetric error costs — that a missed churner and a false alarm are equally bad. They are not.
In this business context:

A false negative (missed churner) costs $100 — the estimated cost of acquiring a replacement customer
A false positive (retained non-churner) costs $20 — the retention intervention cost

The cost ratio is 5:1. Under this asymmetry, the optimal threshold shifts toward catching more churners, even at the expense of more false alarms.
Sweeping thresholds from 0.10 to 0.85 and computing Total Cost = (FN × $100) + (FP × $20) at each point shows that total cost is minimized at threshold 0.15 ($11,260), compared to $18,540 at the default threshold. The $7,280 difference is the direct business value of threshold optimization.
At threshold 0.15, the model catches 93.5% of actual churners (recall = 0.935) while flagging 448 false positives — each costing only $20 to act on unnecessarily.
Why Expected Profit Instead of Churn Rate
Churn rate tells you who is leaving. It does not tell you whether stopping them is worth the cost.
Expected profit reframes the retention decision as a financial calculation:
Expected Profit = P(Churn) × Customer Value − Retention Cost
Customer Value = MonthlyCharges × 3
Retention Cost = $20 × 3 = $60
A customer with P(Churn) = 0.75 and MonthlyCharges = $53.85:
Expected Profit = 0.75 × $161.55 − $60 = $61.16 → retain
A customer with P(Churn) = 0.40 and MonthlyCharges = $18:
Expected Profit = 0.40 × $54 − $60 = −$38.40 → skip
The second customer has meaningful churn risk but is not worth the intervention. A model that treats both the same wastes budget.
Applied to the full test set, 512 customers show positive expected profit. The remaining 893 do not justify retention spend under current cost assumptions.

## What the EDA Findings Mean for Business
MonthlyCharges — Non-Linear Relationship
The LOWESS curve shows churn does not increase linearly with price. It remains low at lower price points, rises sharply in the $60–90 range, then declines at the highest tier.
This matters because it shifts the framing from "higher price = higher churn" to "there is a specific band where customers are most likely to feel the price is not justified." Customers paying above $90 may have more service dependencies or be on plans that deliver clearer value. The $60–90 band warrants targeted investigation — pricing restructure, service bundling, or proactive communication — rather than a blanket discount campaign.
Tenure — The Critical Early Period
The LOWESS curve on tenure shows a near-vertical drop in churn probability within the first 0–10 months, followed by near-zero churn for long-tenure customers. This is not a gradual relationship — it is a phase transition.
The business implication is direct: retention effort applied after month 10 has diminishing returns. Onboarding quality, early service experience, and first-month engagement are where retention investment has the highest leverage. A customer who reaches month 10 is very likely to stay.

Trade-offs and What This Model Does Not Do
Retention success is assumed to be 100%. The expected profit formula does not discount for the probability that an intervention actually works. In practice, retention campaigns succeed at some rate below 1.0 — which would reduce expected profit estimates for all customers and likely shift some from "retain" to "skip."
Cost-to-serve is assumed uniform. A customer calling support 15 times a month is more expensive to serve than one who never contacts the company, even if their monthly charges are identical. This model does not capture that dimension.
The 3-month retention horizon is fixed. Some customers, if retained, will stay for years. Others will churn again in month 4. A more sophisticated model would estimate expected lifetime rather than a fixed window.
These limitations do not invalidate the framework — they define where it should be refined with real business data before deployment.


## What This Demonstrates Analytically

Framing a prediction problem as a decision problem with asymmetric costs
Selecting evaluation metrics based on business context, not convention
Translating model outputs into actionable financial estimates
Communicating trade-offs and assumptions honestly rather than overstating model capability
