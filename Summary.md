# Customer Churn Prediction & Profit Optimization
## Executive Summary

Trong ngành viễn thông, việc mất khách hàng (churn) ảnh hưởng trực tiếp đến doanh thu. Tuy nhiên, không phải tất cả khách hàng đều đáng để giữ lại.

Dự án này xây dựng mô hình dự đoán churn với accuracy 75.7% và khả năng phát hiện 78% khách hàng có nguy cơ rời bỏ, từ đó kết hợp với giá trị khách hàng để đưa ra quyết định giữ chân dựa trên lợi nhuận.

## Business Problem

Thông thường, doanh nghiệp cố gắng giảm churn bằng mọi giá. Tuy nhiên, cách tiếp cận này dễ dẫn đến chi phí giữ chân cao nhưng hiệu quả không tối ưu.

Vấn đề thực sự cần giải quyết là:

Khách hàng nào nên giữ để tối đa hóa lợi nhuận ?

## Key Results

Mô hình Logistic Regression cho thấy hai yếu tố quan trọng nhất:

MonthlyCharges (+3.40): yếu tố làm tăng churn mạnh nhất
Tenure (−3.39): yếu tố giúp giảm churn mạnh nhất

Điều này cho thấy churn chủ yếu bị chi phối bởi giá dịch vụ và thời gian gắn bó của khách hàng.

## Key Insights
### 1. Pricing Effect – MonthlyCharges

Phân tích cho thấy churn không tăng đều theo giá mà có một ngưỡng rõ ràng:

Từ 60 trở lên, churn tăng mạnh
Cao nhất trong khoảng 60–90

→ Điều này cho thấy khách hàng bắt đầu trở nên nhạy cảm với giá sau một mức nhất định (pricing threshold)

### 2. Customer Lifecycle – Tenure
Churn giảm rất nhanh trong 0–10 tháng đầu
Sau đó gần như ổn định

→ Giai đoạn đầu là critical period, nếu giữ được khách trong giai đoạn này thì khả năng họ ở lại rất cao

Model Performance

Mô hình đạt recall = 0.78, nghĩa là bắt được phần lớn khách hàng churn.

Mặc dù precision không cao, điều này là chấp nhận được vì:

Chi phí giữ một khách hàng thấp hơn chi phí tìm khách hàng mới

Do đó, mô hình được thiết kế để ưu tiên không bỏ sót churn, ngay cả khi phải chấp nhận một số dự đoán nhầm.

Business Framework

Thay vì chỉ dự đoán churn, dự án đi thêm một bước:

Customer Value
Customer Value ≈ MonthlyCharges × Expected Tenure
Expected Profit
Expected Profit = P(Churn) × Customer Value − Retention Cost
Decision Strategy
Nếu Expected Profit > 0 → nên giữ khách
Nếu Expected Profit < 0 → không cần đầu tư

→ Tập trung nguồn lực vào đúng khách hàng, không phải tất cả khách hàng

Conclusion

Dự án cho thấy rằng:

Dự đoán churn chỉ là bước đầu
Giá trị thực nằm ở việc kết hợp xác suất churn + giá trị khách hàng
Quyết định giữ chân nên dựa trên lợi nhuận, không phải tỷ lệ churn

Churn prediction chỉ là bước đầu
Giá trị thực nằm ở việc kết hợp xác suất churn với giá trị khách hàng
Quyết định giữ chân nên dựa trên lợi nhuận kỳ vọng, không phải tỷ lệ churn đơn thuần

Giai đoạn đầu (0–10 tháng) là critical period
Nếu khách vượt qua giai đoạn này → khả năng ở lại rất cao


