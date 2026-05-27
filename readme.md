
# Customer Churn Prediction & Profit Optimization

**Stack:** Python · Pandas · Scikit-learn · Statsmodels · Matplotlib · Seaborn

---

## Executive Summary

Most churn projects stop at "who will leave." This one goes further: **is it actually worth spending money to keep them?**

Built a Logistic Regression churn model, then layered a profit framework on top — combining churn probability with customer value to decide which customers justify retention spend.

**Bottom line on a 1,405-customer test set:**
- Optimized threshold saves **$7,280** vs default model
- **367 high-risk, high-value customers** identified as top retention targets
- **893 customers** flagged as not worth retaining at current cost structure

---

## Business Problem

A telecom company loses customers to competitors. Standard response: run retention campaigns on everyone flagged as "at risk."

A major limitation of this approach is that **not every churner generates enough value to justify retention spending.** A customer paying $18/month with low churn probability doesn't justify a $60 intervention.

**Two questions this project answers:**
1. Who is likely to churn?
2. Who is actually worth retaining?

**Cost structure:**
- Acquiring a new customer: ~$100
- Retaining an existing one: ~$20/month

---

## Dataset

- Source: [IBM Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- 7,043 customers, 21 features
- Churn rate: ~26.5%
  
<img width="455" height="478" alt="image" src="https://github.com/user-attachments/assets/6e7d1ce9-4829-4fcd-b6b8-412f2e37bb59" />

- Features include tenure, monthly charges, contract type, payment method, and service usage

---

## Methodology

**1. Churn Prediction**
Logistic Regression trained on 80/20 train-test split. Statsmodels used separately to interpret coefficient direction and statistical significance — all features significant at p < 0.05.

**2. Customer Value Estimation**
```
Customer Value = MonthlyCharges × 3
```
Revenue expected if customer is retained for 3 months post-intervention.

**3. Expected Profit Framework**
```
Expected Profit = P(Churn) × Customer Value − (Retention Cost × 3)
               = P(Churn) × (MonthlyCharges × 3) − $60
```
Retain if Expected Profit > 0. Skip if not.

**4. Cost-Sensitive Threshold Optimization**

Instead of default threshold 0.5, sweep thresholds from 0.10 to 0.85 and minimize:
```
Total Cost = (FN × $100) + (FP × $20)
```
Missing a churner costs $100 to replace. A false alarm costs $20 to retain unnecessarily. This asymmetry means **recall matters more than precision.**

---

## Key Results

**Threshold optimization:**

<img width="451" height="305" alt="image" src="https://github.com/user-attachments/assets/9ec503cd-59f1-4723-ace7-117a1cf9b6f8" />

Threshold 0.15 minimizes total cost at $11,260 — compared to $18,540 at default threshold 0.50. That's a **$7,280 saving** on 1,405 customers, driven by catching 93.5% of churners while accepting more false positives at low cost.

**Model performance at threshold 0.15:**

<img width="487" height="455" alt="image" src="https://github.com/user-attachments/assets/99cc325c-4ae0-4b28-a156-4a1dfc9144cc" />


- Recall: 0.935 — catches 93.5% of actual churners
- Precision: 0.423 — acceptable given FP only costs $20
- Accuracy: 66% — intentionally lower than baseline (74.9%) to minimize business cost
- 10-fold cross-validation accuracy: 80.3%

> Accuracy is lower than a naive baseline. That's expected — the model trades accuracy for lower total business cost. One missed churner costs 5× more than one false alarm.

**Top churn drivers (MinMaxScaler coefficients):**
- MonthlyCharges: **+3.40** — strongest driver of churn
- tenure: **−3.39** — strongest protective factor
- PhoneService: −1.11
- TechSupport: −0.71
- Electronic check payment: +0.46
- Paperless billing: +0.43

**Customer segmentation:**

<img width="811" height="537" alt="image" src="https://github.com/user-attachments/assets/23c15fa4-9ff4-452e-89bf-0039948f7013" />


| Segment | Count | Action |
|---|---|---|
| High Risk – High Value | 367 | Prioritize retention |
| High Risk – Low Value | 168 | Skip or minimal spend |
| Low Risk – High Value | 336 | Monitor |
| Low Risk – Low Value | 534 | No action |

**Expected profit analysis:**
- 512 customers worth retaining (Expected Profit > 0)
- 893 customers not worth the $60 intervention cost

---

## Business Recommendations

**Focus retention budget on 367 High Risk – High Value customers.** These are the customers where intervention ROI is highest. Spending $60 on a customer with $150+ expected value and 60%+ churn probability makes business sense. Spending the same on a $30/month customer with 35% churn probability does not.

**Intervene early.** Churn drops sharply in the first 0–10 months and stabilizes near zero after that. Onboarding and early engagement have the highest leverage — a customer who survives month 10 is very likely to stay long-term.

**Review pricing in the $60–90/month range.** Customers in the $60–90/month range show elevated churn rates relative to higher-priced segments, suggesting a potential value-perception issue worth further investigation.

**Flag electronic check and paperless billing users.** Both correlate positively with churn. May indicate a less engaged or more price-sensitive customer profile worth monitoring separately.

---

## Assumptions & Limitations

- Retention cost ($20/month) and acquisition cost ($100) are assumed — real deployment needs actual business figures
- Customer Value assumes a fixed 3-month retention window post-intervention
- The framework assumes retention interventions are fully effective. In real-world deployment, retention success probability would likely be lower and reduce expected profit estimates
- Dataset is public (IBM Telco) — business context is simulated to demonstrate analytical thinking

---

## Project Structure

```
├── notebook/
│   └── churn_analysis.ipynb
├── data/
│   └── WA_Fn-UseC_-Telco-Customer-Churn.csv
├── README.md
├── proposal.md
└── summary.md
```

---

## Tools

| Purpose | Library |
|---|---|
| Data manipulation | Pandas |
| Modeling & evaluation | Scikit-learn |
| Statistical interpretation | Statsmodels |
| Visualization | Matplotlib, Seaborn |

---

## How to Run

```bash
# Clone the repo
git clone https://github.com/your-username/churn-prediction

# Install dependencies
pip install pandas scikit-learn statsmodels matplotlib seaborn

# Open notebook
jupyter notebook notebook.ipynb
```

---

