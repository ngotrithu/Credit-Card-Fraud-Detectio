# Credit-Card-Fraud-Detection
## Mô tả:
- Điều quan trọng của công ty tín dụng phát hành thẻ là phát hiện được các KH có hành vi gian lận thẻ tín dụng để khi họ mua các sản phẩm, dịch vụ họ sẽ không bị tính phí cho các sản phẩm, dịch vụ đấy.
## Mục đích:
- Với những thông tin đã cung cấp xây dựng mô hình dự báo liệu KH này có thực hiện hành vi gian lận khi sử dụng thẻ tín dụng hay không?
## Thông tin về bộ dữ liệu:
- Bộ dữ liệu này chứa các thông tin giao dịch có 492 TH gian lận trong tổng số 284.807 giao dịch. Đây là bộ dữ liệu mất cân bằng nghiêm trọng với positive class (gian lận) chiếm 0,172% tổng số giao dịch. Do đó, chúng ta không nên sử dụng metrics `Accuracy` để đánh giá mô hình vì số lượng nhãn 0 quá nhiều, thay vào đó, chúng ta nên tập trung vào F1 Score, Precision/Recall, ROC_AUC hoặc Confusion matrix để có sự đánh giá chính xác hơn về hiệu suất của các mô hình.
## Techniques:
- Exploratory Data Analysis (EDA)
- Feature Engineering
- Feature Scaling
- SMOTE
- Build Models
- Model Selection
- Fine Tune Hyperparameters with `Optuna`
## Model Metrics:
- Đây là bộ dữ liệu mất cân bằng nghiêm trọng với positive class (gian lận) chiếm 0,172% tổng số giao dịch. Do đó, chúng ta không nên sử dụng metrics `Accuracy` để đánh giá mô hình vì số lượng nhãn 0 quá nhiều, thay vào đó, chúng ta nên tập trung vào `f1_score`, `Precision`/`Recall`, `ROC_AUC` hoặc Confusion matrix để có sự đánh giá chính xác hơn về hiệu suất của các mô hình.

=> Ở đây tôi chọn metrics `f1_score` để đánh giá hiệu suất của các mô hình
## Modeling:
- Logistic Regression
- Decision Tree
- Random Forest
- LightGBM
- Catboost
- XGBoost
- AdaBoost
## Model Selection
<a href="https://drive.google.com/uc?export=view&id=1fRa79JmKwQXdixq-iCXkSjOTAVOL2SJ_"><img src="https://drive.google.com/uc?export=view&id=1fRa79JmKwQXdixq-iCXkSjOTAVOL2SJ_" style="width: 500px; max-width: 100%; height: auto" title="Click for the larger version." /></a>
- Mô hình Random Forest cho kết quả `f1_score` tốt nhất nhưng thời gian huấn luyện lâu và tốn chi phí tính toán nên để tối ưu chúng ta sẽ lựa chọn mô hình `LightGBM` để fine-tuning
## Fine Tune Hyperparameters with `Optuna`

<a href="https://drive.google.com/uc?export=view&id=1ceDy2AfE8azR2fmdS8d4a4jN29ZplPWu"><img src="https://drive.google.com/uc?export=view&id=1ceDy2AfE8azR2fmdS8d4a4jN29ZplPWu" style="width: 500px; max-width: 100%; height: auto" title="Click for the larger version." /></a>

- Mô hình đã có sự cải thiện đáng kể với chỉ số `f1_score` từ 65.3% đã tăng lên 81.13%
- Với bài toán Credit Card Fraud Detection, chúng ta nên chú trọng vào việc giảm số lượng sai lầm loại I (FP) mà mô hình phán đoán được. Những khách hàng thuộc sai lầm loại I về thực tế họ đã thực hiện hành vi gian lận nhưng mô hình dự đoán những khách hàng này không có hành vi gian lận. Điều dẫn đến một sự mất mát lớn cho tổ chức tín dụng khi chúng ta đã dự đoán sai những đối tượng KH này.
- Do đó, ngoài việc lựa chọn mô hình tốt, chúng ta cũng cần lựa chọn những mô hình có các TH thuộc sai lầm loại I là thấp nhất.

=> Mô hình `LightGBM` sẽ là mô hình được lựa chọn đề giải quyết bài toán này!
