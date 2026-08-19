# Đánh giá mô hình CNN trên MNIST

Sau khi huấn luyện mô hình CNN bằng **PyTorch** và tối ưu bằng **Adam**, mô hình được đánh giá trên tập kiểm thử MNIST thông qua các độ đo phổ biến gồm **Accuracy, Precision, Recall, F1-score, Confusion Matrix, ROC Curve và AUC**.

## 1. Accuracy

Accuracy thể hiện tỷ lệ số mẫu được mô hình dự đoán đúng trên tổng số mẫu.

[
Accuracy = \frac{TP + TN}{TP + TN + FP + FN}
]

Trong đó:

* **TP (True Positive):** số mẫu Positive được dự đoán đúng.
* **TN (True Negative):** số mẫu Negative được dự đoán đúng.
* **FP (False Positive):** số mẫu Negative nhưng bị dự đoán thành Positive.
* **FN (False Negative):** số mẫu Positive nhưng bị dự đoán thành Negative.

Accuracy càng gần `1` hoặc `100%` thì khả năng dự đoán tổng thể của mô hình càng tốt.

---

## 2. Precision

Precision cho biết trong số các mẫu mà mô hình dự đoán thuộc một lớp cụ thể, có bao nhiêu mẫu thực sự thuộc lớp đó.

[
Precision = \frac{TP}{TP + FP}
]

Precision cao cho thấy mô hình ít đưa ra các dự đoán dương tính sai.

Ví dụ, khi xét chữ số `7`, Precision trả lời câu hỏi:

> Trong tất cả các ảnh mà mô hình dự đoán là số 7, có bao nhiêu ảnh thực sự là số 7?

---

## 3. Recall

Recall cho biết trong tất cả các mẫu thực sự thuộc một lớp, mô hình nhận diện chính xác được bao nhiêu mẫu.

[
Recall = \frac{TP}{TP + FN}
]

Recall còn được gọi là **Sensitivity** hoặc **True Positive Rate (TPR)**.

Ví dụ, khi xét chữ số `7`, Recall trả lời câu hỏi:

> Trong tất cả các ảnh thực sự là số 7, mô hình nhận diện đúng được bao nhiêu ảnh?

---

## 4. F1-score

F1-score là trung bình điều hòa giữa Precision và Recall.

[
F1 = 2 \times \frac{Precision \times Recall}{Precision + Recall}
]

F1-score được sử dụng khi cần đánh giá đồng thời khả năng hạn chế **False Positive** và **False Negative** của mô hình.

Giá trị F1-score càng gần `1` thì mô hình càng cân bằng tốt giữa Precision và Recall.

---

## 5. Đánh giá đối với bài toán MNIST nhiều lớp

MNIST là bài toán phân loại gồm **10 lớp**, tương ứng với các chữ số:

```text
0, 1, 2, 3, 4, 5, 6, 7, 8, 9
```

Đối với từng lớp, các độ đo Precision, Recall và F1-score có thể được tính theo phương pháp **One-vs-Rest**.

Ví dụ khi đánh giá chữ số `7`:

```text
Positive = chữ số 7
Negative = các chữ số 0, 1, 2, 3, 4, 5, 6, 8, 9
```

Sau khi tính cho từng lớp, có thể sử dụng:

* **Macro Average:** tính trung bình các metric của 10 lớp và xem các lớp có mức độ quan trọng như nhau.
* **Weighted Average:** tính trung bình có trọng số dựa trên số lượng mẫu của từng lớp.
* **Micro Average:** tính metric dựa trên tổng TP, FP và FN của toàn bộ các lớp.

---

## 6. Confusion Matrix

Confusion Matrix cho phép quan sát chi tiết số lượng mẫu được dự đoán đúng và sai giữa các lớp.

Trong ma trận:

* **Hàng:** nhãn thực tế.
* **Cột:** nhãn mô hình dự đoán.
* **Đường chéo chính:** các mẫu được dự đoán chính xác.
* **Các ô ngoài đường chéo:** các trường hợp mô hình nhận diện nhầm giữa các chữ số.

Confusion Matrix đặc biệt hữu ích để xác định các cặp chữ số mà CNN thường nhầm lẫn với nhau.

---

## 7. ROC Curve

ROC (**Receiver Operating Characteristic**) thể hiện mối quan hệ giữa:

[
TPR = \frac{TP}{TP + FN}
]

và:

[
FPR = \frac{FP}{FP + TN}
]

Trong đó:

* **TPR (True Positive Rate):** tỷ lệ nhận diện đúng các mẫu Positive.
* **FPR (False Positive Rate):** tỷ lệ các mẫu Negative bị dự đoán sai thành Positive.

Đối với MNIST, ROC được tính theo phương pháp **One-vs-Rest** cho từng chữ số.

Ví dụ khi vẽ ROC cho chữ số `3`:

```text
Positive = chữ số 3
Negative = tất cả các chữ số còn lại
```

Quá trình này được thực hiện tương tự cho toàn bộ 10 lớp.

---

## 8. AUC

AUC (**Area Under the ROC Curve**) là diện tích nằm dưới đường cong ROC.

Giá trị AUC nằm trong khoảng:

[
0 \leq AUC \leq 1
]

Có thể diễn giải như sau:

| AUC       | Mức độ phân biệt                   |
| --------- | ---------------------------------- |
| 0.5       | Gần tương đương dự đoán ngẫu nhiên |
| 0.6 - 0.7 | Trung bình                         |
| 0.7 - 0.8 | Khá                                |
| 0.8 - 0.9 | Tốt                                |
| 0.9 - 1.0 | Rất tốt                            |

AUC càng gần `1` thì khả năng phân biệt giữa một chữ số và các chữ số còn lại càng tốt.

Đối với bài toán MNIST nhiều lớp, có thể sử dụng:

* **AUC của từng lớp:** đánh giá riêng từng chữ số.
* **Macro AUC:** trung bình AUC của tất cả 10 lớp.
* **Weighted AUC:** trung bình AUC có xét đến số lượng mẫu của từng lớp.

---

## 9. Các chỉ số sử dụng trong quá trình đánh giá

Mô hình CNN được đánh giá bằng các chỉ số:

```text
Accuracy
Precision
Recall
F1-score
Confusion Matrix
ROC Curve
AUC từng lớp
Macro AUC
Weighted AUC
```

Những độ đo này giúp đánh giá mô hình toàn diện hơn so với việc chỉ sử dụng Accuracy. Trong đó, Accuracy thể hiện hiệu suất tổng thể, Precision và Recall đánh giá khả năng phân loại của từng lớp, F1-score thể hiện sự cân bằng giữa Precision và Recall, còn ROC và AUC phản ánh khả năng phân biệt giữa các lớp tại nhiều ngưỡng dự đoán khác nhau.
