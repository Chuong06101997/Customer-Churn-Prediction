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
Accuracy 75.7%
Recall tập trung vào lớp churn
F1-score để cân bằng precision và recall

## 4. Model Performance

Mô hình Logistic Regression đạt:

Accuracy: 75.7%

Kết quả này cho thấy mô hình có khả năng dự đoán churn ở mức khá tốt, đồng thời vẫn giữ được tính diễn giải cao để phục vụ phân tích business.

### 4.1 Key Drivers from Logistic Regression
Biến làm tăng churn

MonthlyCharges là yếu tố làm tăng churn mạnh nhất với hệ số +3.40, cho thấy chi phí hàng tháng có tác động rất lớn đến xác suất rời bỏ của khách hàng.

Ngược lại, Tenure là yếu tố giúp giảm churn mạnh nhất với hệ số −3.39, phản ánh rằng khách hàng càng gắn bó lâu thì khả năng rời bỏ càng thấp.

### 4.2 Insight – MonthlyCharges (Non-linear Effect)

Mặc dù hệ số của MonthlyCharges là dương, phân tích EDA cho thấy mối quan hệ không hoàn toàn tuyến tính:

20–40: churn thấp, tăng nhẹ
40–60: dao động, chưa rõ xu hướng
60–90: churn tăng mạnh → vùng rủi ro cao nhất
>90: churn giảm nhẹ

Điều này cho thấy tồn tại threshold effect (~60), nơi khách hàng bắt đầu trở nên nhạy cảm với giá.

### 4.3 Insight – Tenure (Customer Lifecycle Effect)
Churn giảm mạnh trong giai đoạn 0–10 tháng
Sau đó, xu hướng giảm chậm lại và dần ổn định

### 4.4 Key Business 
MonthlyCharges là driver chính của churn, đặc biệt sau ngưỡng ~60
Tenure là yếu tố giữ khách mạnh nhất, đặc biệt trong giai đoạn đầu
Các dịch vụ bổ sung như TechSupport giúp tăng retention
Không phải tất cả biến có coef lớn đều mang ý nghĩa nhân quả (ví dụ: PhoneService cần kiểm chứng thêm)

# 5. Business Framework
## 5.1 Customer Value Estimation

Giá trị khách hàng mới được ước tính dựa trên:

<img width="461" height="71" alt="image" src="https://github.com/user-attachments/assets/bbd96d7e-5251-4dca-b244-7ac6a3999f8d" />


## 5.2 Expected Profit

Quyết định giữ khách dựa trên:


<img width="586" height="67" alt="image" src="https://github.com/user-attachments/assets/db7866c7-3f18-4d64-a0b3-fa5272ce6de6" />


# 6. Decision Strategy

Nếu Expected Profit > 0
→ Nên giữ khách hàng
Nếu Expected Profit < 0
→ Không cần đầu tư giữ chân

Tập trung nguồn lực vào khách hàng mang lại giá trị thực

# 7. Conclusion

Dự án cho thấy rằng:

Churn prediction chỉ là bước đầu
Giá trị thực nằm ở việc kết hợp xác suất churn với giá trị khách hàng
Quyết định giữ chân nên dựa trên lợi nhuận kỳ vọng, không phải tỷ lệ churn đơn thuần

Giai đoạn đầu (0–10 tháng) là critical period
Nếu khách vượt qua giai đoạn này → khả năng ở lại rất cao


