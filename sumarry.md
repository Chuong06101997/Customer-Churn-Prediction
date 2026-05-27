# Customer Churn Prediction & Profit Optimization

## Executive Summary
Dự án xây dựng mô hình dự đoán churn kết hợp với framework tối ưu hóa lợi nhuận, nhằm giúp doanh nghiệp viễn thông quyết định khách hàng nào đáng giữ chân — không phải giảm churn bằng mọi giá.
Kết quả chính: threshold tối ưu (0.15) tiết kiệm $7,280 so với threshold mặc định trên tập test 1,405 khách hàng, xác định 367 khách hàng High Risk – High Value cần ưu tiên can thiệp, và loại 893/1,405 khách hàng ra khỏi danh sách giữ chân vì không sinh lời ở cấu trúc chi phí hiện tại.
Business Problem
## Context
Công ty viễn thông đang mất khách hàng vào tay đối thủ. Hiện tại chưa có framework hệ thống nào để xác định khách nào có nguy cơ rời bỏ, và liệu chi phí giữ chân có đáng hay không. Chi phí tìm khách mới (~$100) cao hơn chi phí giữ chân (~$20/tháng) — nhưng không phải khách hàng nào cũng sinh lời đủ để justify việc can thiệp.
## Need
Doanh nghiệp cần trả lời hai câu hỏi: ai có khả năng rời bỏ, và ai thực sự đáng để giữ chân?
## Vision
Kết hợp xác suất churn với giá trị khách hàng để xây dựng retention framework dựa trên lợi nhuận kỳ vọng — không phải churn rate đơn thuần.
## Outcome
Đội retention có framework rõ ràng để phân bổ ngân sách hiệu quả: giữ chân dựa trên expected profit, tập trung vào đúng khách hàng thay vì can thiệp đại trà.

### Key Results
Model Performance
Mô hình đạt recall 0.935 ở threshold 0.15, nghĩa là bắt được 93.5% khách hàng thực sự churn. Accuracy ở mức 66% — thấp hơn baseline 74.9% — là có chủ đích: model được tối ưu cho tổng chi phí kinh doanh, không phải accuracy. Bỏ sót 1 churner tốn $100 để tìm khách mới, trong khi giữ nhầm 1 người chỉ tốn $20 — asymmetry này justifies việc ưu tiên recall. Cross-validation 10-fold cho mean accuracy 80.3%, cao hơn test accuracy do CV chạy trên unscaled data — test accuracy là con số đáng tin hơn để report.

Cost-Sensitive Threshold Optimization
Tổng chi phí được tính theo công thức: 

Total Cost = (FN × $100) + (FP × $20). 

Sweep threshold từ 0.10 đến 0.85 cho thấy threshold 0.15 đạt tổng chi phí thấp nhất là $11,260, với recall 0.935, chỉ bỏ sót 23 churner thực sự (FN) và giữ nhầm 448 người (FP). So với threshold mặc định 0.50 có tổng chi phí $18,540, threshold 0.15 tiết kiệm $7,280 trên tập test 1,405 khách hàng.

### Business Framework
Customer Value

<img width="391" height="48" alt="image" src="https://github.com/user-attachments/assets/e4f02b80-269e-4b01-9f97-13d46ad43938" />


Đại diện cho revenue kỳ vọng nếu giữ được khách thêm 3 tháng sau can thiệp.

### Expected Profit

<img width="647" height="75" alt="image" src="https://github.com/user-attachments/assets/8e87e2d9-bd85-406c-9f92-8ddaa8c9a857" />

               
Nếu Expected Profit > 0 thì nên giữ. Nếu ≤ 0 thì không cần đầu tư.

### Customer Segmentation
Dựa trên churn probability (ngưỡng 0.30) và customer value median, 1,405 khách hàng được chia thành 4 nhóm. Nhóm High Risk – High Value gồm 367 khách cần được ưu tiên giữ chân vì có ROI cao nhất. Nhóm High Risk – Low Value gồm 168 khách nên hạn chế hoặc không can thiệp. Nhóm Low Risk – High Value gồm 336 khách cần theo dõi và duy trì quan hệ. Nhóm Low Risk – Low Value gồm 534 khách không cần hành động ngay.
Về expected profit, với retention cost $20/tháng trong 3 tháng, có 512 khách hàng đáng giữ và 893 khách hàng không đáng đầu tư ở cấu trúc chi phí hiện tại.

Limitations & Assumptions
Customer Value giả định retention horizon cố định 3 tháng sau can thiệp. Chi phí giữ chân ($20/tháng) và tìm khách mới ($100) là assumed values — triển khai thực tế cần số liệu chi phí thực của doanh nghiệp. P(retention success | intervention) được giả định bằng 1.0 — trong thực tế con số này thấp hơn và sẽ làm giảm expected profit. Model cũng không tính đến sự chênh lệch cost-to-serve giữa các khách hàng. Dataset là public (IBM Telco) — bối cảnh và ràng buộc được mô phỏng để thể hiện business-oriented thinking.

Tools
Python · Pandas · Scikit-learn · Statsmodels · Matplotlib · Seaborn

Churn prediction chỉ là bước đầu. Giá trị thực nằm ở việc kết hợp xác suất churn với giá trị khách hàng để đưa ra quyết định giữ chân dựa trên lợi nhuận kỳ vọng — không phải tỷ lệ churn đơn thuần.
