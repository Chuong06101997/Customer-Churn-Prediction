# Customer Churn Prediction & Profit Optimization
Stack: Python · Pandas · Scikit-learn · Statsmodels · Matplotlib · Seaborn

What This Project Is
A churn prediction model that goes one step further: instead of just flagging at-risk customers, it calculates whether retaining each customer is actually profitable.
Core insight: not every churner is worth retaining.

Key Results: 

<img width="484" height="441" alt="image" src="https://github.com/user-attachments/assets/b875b613-df24-4aa7-8169-49402dafeb28" />

<img width="803" height="333" alt="image" src="https://github.com/user-attachments/assets/61bbd781-ac71-4380-92f5-2da07080b227" />


Why This Is Different From a Typical Churn Model
Most churn models output a probability and stop there. This project adds two layers:
1. Cost-sensitive threshold optimization
Instead of default threshold 0.50, the model sweeps thresholds and minimizes total business cost:

<img width="386" height="77" alt="image" src="https://github.com/user-attachments/assets/c0c04bb9-25ec-488e-a74e-421ee5a13011" />

Missing a churner costs 5× more than a false alarm — so recall is prioritized deliberately, not by accident.
2. Expected profit framework

<img width="566" height="76" alt="image" src="https://github.com/user-attachments/assets/dcb355ac-e91f-41d2-b899-f91509ca2dcc" />

Customers with negative expected profit are excluded from retention campaigns — regardless of churn probability.

Key Visuals
(Tenure vs Churn — LOWESS curve showing sharp drop in first 10 months)
<img width="765" height="637" alt="image" src="https://github.com/user-attachments/assets/ca34c281-a9d7-4599-98ed-2903e25f568b" />

(MonthlyCharges vs Churn — non-linear relationship peaking at $60–90)

<img width="598" height="565" alt="image" src="https://github.com/user-attachments/assets/94b6ce2a-44c6-40f9-ae65-f01a3e839444" />

(Customer Segmentation — 4-quadrant bar chart)
(Threshold vs Total Cost — optimal at 0.15)

Customer Segmentation

<img width="812" height="243" alt="image" src="https://github.com/user-attachments/assets/16662bc2-b80f-4a41-aa15-f4e3be62d22f" />

<img width="849" height="521" alt="image" src="https://github.com/user-attachments/assets/645e69af-abfa-4536-baca-1b4360562f27" />

Business Recommendations

Target the 367 High Risk – High Value customers first. These are where retention ROI is highest.
Invest in early onboarding. Churn drops sharply after month 10 — early engagement has the highest leverage.
Investigate the $60–90/month pricing band. This segment shows elevated churn relative to higher-paying customers, suggesting a value-perception gap worth exploring.
Monitor electronic check and paperless billing users. Both correlate positively with churn.


Methodology Overview

1. Logistic Regression on 80/20 train-test split
2. Statsmodels for coefficient interpretation (p-value, direction, magnitude)
3. MinMaxScaler to compare feature importance across variables
4. Cost-sensitive threshold sweep (0.10 → 0.85)
5. Expected profit calculation per customer
6. 2×2 segmentation by churn risk × customer value


Project Structure

<img width="822" height="232" alt="image" src="https://github.com/user-attachments/assets/0248f6c3-1df0-4743-8387-fa2d9a5ee90a" />

How to Run
bashgit clone https://github.com/your-username/churn-prediction
pip install pandas scikit-learn statsmodels matplotlib seaborn
jupyter notebook notebook/churn_analysis.ipynb
