# Customer Churn Prediction – Business-Oriented Framework

<img width="1920" height="1280" alt="image" src="https://github.com/user-attachments/assets/ab986de4-1b8f-460c-8741-2e0dce7c1cfb" />



## 1. Context

A telecommunications company is experiencing customer churn in a competitive market. The dataset contains 7,043 customers with features related to contract type, billing behavior, service usage, and tenure.

Currently, the company has no systematic framework to:

* identify customers at risk of churn
* prioritize retention spending
* evaluate whether retaining a customer is financially worthwhile

Key business constraints:

* Retention budget is limited
* Acquiring a new customer costs more than retaining an existing one
* Customer value varies significantly across segments

---

## 2. Business Need

The business needs to answer two core questions:

1. Which customers are most likely to churn?
2. Which customers should receive retention investment?

The core problem is not simply reducing churn rate, but improving retention efficiency by allocating intervention budget toward customers with higher expected business value.

---

## 3. Project Vision

This project aims to build a business-oriented churn framework by combining:

* churn probability prediction
* customer value estimation
* cost-sensitive decision making

The framework will attempt to:

* estimate churn probability using Logistic Regression
* estimate customer value using monthly revenue
* calculate expected retention profitability
* segment customers into actionable business groups

---

## 4. Proposed Analytical Approach

### Churn Prediction

A Logistic Regression model will be trained to estimate the probability of churn for each customer.

### Customer Value Estimation

Customer value will be approximated using MonthlyCharges and a fixed retention horizon assumption.

### Expected Profit Framework

The project will evaluate whether retention intervention is financially justified by comparing:

* expected retained revenue
* estimated retention cost

### Threshold Optimization

Instead of using the default classification threshold (0.50), the project will test multiple thresholds to evaluate trade-offs between:

* recall
* false positives
* overall business cost

---

## 5. Expected Outcome

The expected outcome is a decision-support framework that helps:

* prioritize high-value at-risk customers
* reduce inefficient retention spending
* improve retention ROI
* translate churn prediction into actionable business strategy

Rather than minimizing churn alone, the project focuses on improving business decision quality through profit-oriented analysis.

---

## Dataset

* Source: IBM Telco Customer Churn
* 7,043 customers
* 21 features
* Binary target variable: Churn

  <img width="409" height="591" alt="image" src="https://github.com/user-attachments/assets/3cc97f0e-5efe-46f2-b336-61428cd66d1d" />

<img width="409" height="379" alt="image" src="https://github.com/user-attachments/assets/bfbb0439-0bb0-4925-99a5-aefa3016b935" />


Dataset Link:
https://www.kaggle.com/code/farazrahman/telco-customer-churn-logisticregression/input

                
                
