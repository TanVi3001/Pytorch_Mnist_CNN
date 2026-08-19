## 1. Accuracy

Accuracy thể hiện tỷ lệ số mẫu được mô hình dự đoán đúng trên tổng số mẫu.

```math
\mathrm{Accuracy} =
\frac{TP + TN}{TP + TN + FP + FN}
```

Trong đó:

- **TP (True Positive):** số mẫu Positive được dự đoán đúng.
- **TN (True Negative):** số mẫu Negative được dự đoán đúng.
- **FP (False Positive):** số mẫu Negative nhưng bị dự đoán thành Positive.
- **FN (False Negative):** số mẫu Positive nhưng bị dự đoán thành Negative.

---

## 2. Precision

Precision cho biết trong số các mẫu mà mô hình dự đoán thuộc một lớp cụ thể, có bao nhiêu mẫu thực sự thuộc lớp đó.

```math
\mathrm{Precision} =
\frac{TP}{TP + FP}
```

---

## 3. Recall

Recall cho biết trong số các mẫu thực sự thuộc một lớp, mô hình nhận diện đúng được bao nhiêu mẫu.

```math
\mathrm{Recall} =
\frac{TP}{TP + FN}
```

Recall còn được gọi là **Sensitivity** hoặc **True Positive Rate (TPR)**.

---

## 4. F1-score

F1-score là trung bình điều hòa giữa Precision và Recall.

```math
F1 =
2 \times
\frac{\mathrm{Precision} \times \mathrm{Recall}}
{\mathrm{Precision} + \mathrm{Recall}}
```

---

## 5. True Positive Rate

```math
TPR =
\frac{TP}{TP + FN}
```

---

## 6. False Positive Rate

```math
FPR =
\frac{FP}{FP + TN}
```

---

## 7. AUC

AUC là diện tích nằm dưới đường cong ROC.

```math
AUC =
\int_{0}^{1} TPR(FPR)\,d(FPR)
```

Giá trị AUC nằm trong khoảng:

```math
0 \leq AUC \leq 1
```
