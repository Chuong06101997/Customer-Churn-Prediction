# Customer Churn Prediction & Profit Optimization
## 1. Project Overview

Customer churn là một trong những vấn đề quan trọng trong ngành viễn thông, ảnh hưởng trực tiếp đến doanh thu và chi phí marketing. Tuy nhiên, không phải tất cả khách hàng đều cần được giữ lại.

Dự án này tập trung vào việc:

Dự đoán xác suất churn của khách hàng
Đánh giá giá trị kinh tế của từng khách hàng
Hỗ trợ quyết định giữ chân dựa trên lợi nhuận kỳ vọng

## 2. Business Problem

Doanh nghiệp thường cố gắng giảm churn bằng mọi giá, dẫn đến chi phí retention cao nhưng hiệu quả không tối ưu.

Vấn đề cốt lõi:

Nên giữ khách hàng nào để tối đa hóa lợi nhuận?

## 3. Methodology

### 3.1 Data Processing
Làm sạch dữ liệu: xử lý kiểu dữ liệu, missing values, duplicate
Encoding biến categorical
Kiểm tra phân phối và outliers

### 3.2 Exploratory Data Analysis

Phân tích các yếu tố ảnh hưởng đến churn:

Tenure (thời gian sử dụng)
MonthlyCharges (chi phí hàng tháng)
Contract (loại hợp đồng)
InternetService, TechSupport

### 3.3 Modeling

Sử dụng Logistic Regression để dự đoán xác suất churn
Lý do lựa chọn:
Dễ diễn giải (interpretability)
Phù hợp bài toán business decision
Trả về xác suất (probability) phục vụ tính toán kinh tế
### 3.4 Model Evaluation
Accuracy ~76%
Recall tập trung vào lớp churn
F1-score để cân bằng precision và recall
