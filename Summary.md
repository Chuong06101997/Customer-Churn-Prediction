Customer Churn Prediction & Business Optimization
📌 Project Overview

Customer churn là vấn đề quan trọng trong ngành viễn thông, nơi doanh nghiệp có nguy cơ mất khách hàng và doanh thu nếu không có chiến lược giữ chân phù hợp. Churn được định nghĩa là việc khách hàng ngừng sử dụng dịch vụ trong tháng gần nhất.

Mục tiêu của dự án này không chỉ dừng lại ở việc dự đoán churn, mà tập trung vào việc:

Hiểu hành vi khách hàng
Xác định yếu tố ảnh hưởng churn
Tối ưu quyết định giữ khách dựa trên lợi nhuận
🎯 Business Objective
Dự đoán xác suất churn của từng khách hàng
Xác định nhóm khách hàng có nguy cơ rời bỏ cao
Tính toán giá trị kinh tế của từng khách hàng
Đưa ra quyết định giữ hay không giữ dựa trên Expected Profit
📂 Dataset Description

Dataset bao gồm 7043 khách hàng với 21 biến, bao gồm:

Thông tin nhân khẩu học (gender, SeniorCitizen, Partner, Dependents)
Thông tin dịch vụ (InternetService, TechSupport, Streaming, …)
Thông tin tài khoản (Contract, PaymentMethod, MonthlyCharges, TotalCharges)
Biến mục tiêu: Churn (Yes/No)

Mỗi dòng đại diện cho một khách hàng và hành vi sử dụng dịch vụ của họ.

🔍 Key Insights
Khách hàng có tenure thấp dễ churn hơn → churn xảy ra ở giai đoạn đầu
MonthlyCharges cao làm tăng khả năng churn
Khách hàng dùng Fiber Optic có churn cao nhất
Contract dài hạn giúp giảm churn đáng kể
TechSupport là yếu tố giữ chân mạnh

👉 Nhóm nguy cơ cao:
khách hàng mới + phí cao + contract ngắn

🤖 Modeling Approach
Model chính: Logistic Regression
Output: xác suất churn (probability)

Lý do chọn Logistic Regression:

Dễ giải thích (coef, odds ratio)
Phù hợp bài toán business decision
Cung cấp xác suất trực tiếp để tính profit
📈 Model Evaluation
Accuracy: ~76%
Recall (churn): cao → giảm bỏ sót khách churn
F1-score: cân bằng giữa precision và recall

👉 Không tối ưu accuracy mà tối ưu khả năng phát hiện churn có giá trị

💰 Business Decision Framework

Dự án không dừng ở prediction mà đi đến quyết định:

1. Tính xác suất churn

→ từ model

2. Ước tính giá trị khách hàng
Customer Value ≈ MonthlyCharges × Expected Tenure
3. Tính Expected Profit
Expected Profit = P(Churn) × Customer Value − Retention Cost
🎯 Final Strategy
Nếu Expected Profit > 0
→ nên giữ khách (invest retention)
Nếu Expected Profit < 0
→ không cần giữ (tối ưu chi phí)

👉 Không giữ tất cả khách hàng
👉 Chỉ giữ khách hàng có giá trị

🚀 Key Takeaway

Mục tiêu của bài toán không phải là giảm churn bằng mọi giá,
mà là giữ đúng khách hàng để tối ưu lợi nhuận.
