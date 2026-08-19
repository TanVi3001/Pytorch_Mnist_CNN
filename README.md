# Các Độ Đo Đánh Giá Mô Hình Phân Loại (Classification Metrics)

Tài liệu này tổng hợp các công thức toán học và ý nghĩa của các độ đo phổ biến dùng để đánh giá hiệu năng của mô hình học máy.

---

## 1. Accuracy (Độ chính xác tổng thể)

Accuracy thể hiện tỷ lệ số mẫu được mô hình dự đoán đúng trên tổng số mẫu.

$$
\mathrm{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}
$$

**Trong đó:**
* **TP (True Positive):** Số mẫu Positive được dự đoán đúng.
* **TN (True Negative):** Số mẫu Negative được dự đoán đúng.
* **FP (False Positive):** Số mẫu Negative nhưng bị dự đoán nhầm thành Positive.
* **FN (False Negative):** Số mẫu Positive nhưng bị dự đoán nhầm thành Negative.

---

## 2. Precision (Độ chính xác trên dự đoán dương)

Precision cho biết trong số các mẫu mà mô hình dự đoán là Positive, có bao nhiêu mẫu thực sự là Positive.

$$
\mathrm{Precision} = \frac{TP}{TP + FP}
$$

---

## 3. Recall (Độ bao phủ / Độ nhạy)

Recall cho biết trong số các mẫu thực sự là Positive, mô hình nhận diện đúng được bao nhiêu mẫu.

$$
\mathrm{Recall} = \frac{TP}{TP + FN}
$$

*Lưu ý:* Recall còn được gọi là **Sensitivity** hoặc **True Positive Rate (TPR)**.

---

## 4. F1-score

F1-score là trung bình điều hòa (harmonic mean) giữa Precision và Recall, giúp đánh giá mô hình khi tập dữ liệu bị mất cân bằng.

$$
F1 = 2 \times \frac{\mathrm{Precision} \times \mathrm{Recall}}{\mathrm{Precision} + \mathrm{Recall}}
$$

---

## 5. True Positive Rate (TPR)

Tỷ lệ dự đoán đúng lớp dương trên tổng số mẫu thực tế thuộc lớp dương (chính là Recall).

$$
TPR = \frac{TP}{TP + FN}
$$

---

## 6. False Positive Rate (FPR)

Tỷ lệ dự đoán sai mẫu âm thành mẫu dương trên tổng số mẫu thực tế thuộc lớp âm.

$$
FPR = \frac{FP}{FP + TN}
$$

---

## 7. AUC (Area Under the Curve)

AUC là phần diện tích nằm phía dưới đường cong ROC (Receiver Operating Characteristic), thể hiện qua tích phân:

$$
AUC = \int_{0}^{1} TPR(FPR) \, d(FPR)
$$

**Giá trị giới hạn:**
$$
0 \leq AUC \leq 1
$$

* **Ý nghĩa:** Chỉ số AUC càng gần `1.0` thì mô hình càng có khả năng phân biệt tốt và chính xác giữa lớp Positive và Negative.
