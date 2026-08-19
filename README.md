# CNN Handwritten Digit Recognition with PyTorch

Dự án xây dựng một mô hình **Convolutional Neural Network (CNN)** bằng **PyTorch** cho bài toán nhận diện chữ số viết tay trên bộ dữ liệu **MNIST**.

Mô hình được huấn luyện để phân loại các chữ số từ **0 đến 9**, sau đó được đánh giá trên tập kiểm thử bằng các độ đo **Accuracy, Precision, Recall, F1-score, Confusion Matrix, ROC Curve và AUC**. Ngoài ra, mô hình còn có khả năng nhận diện các ảnh chữ số viết tay do người dùng tự upload.

---

## 1. Mục tiêu của dự án

Mục tiêu chính của dự án là:

* Xây dựng mô hình CNN bằng thư viện PyTorch.
* Huấn luyện mô hình trên bộ dữ liệu MNIST.
* Sử dụng thuật toán tối ưu Adam để cập nhật trọng số.
* Đánh giá hiệu quả của mô hình trên tập test.
* Phân tích kết quả bằng các độ đo phổ biến trong bài toán phân loại.
* Xây dựng chức năng nhận diện ảnh chữ số viết tay từ bên ngoài.
* Trực quan hóa kết quả dự đoán và đường cong ROC.

---

## 2. Bộ dữ liệu MNIST

MNIST là bộ dữ liệu phổ biến trong các bài toán Computer Vision và Deep Learning.

Bộ dữ liệu gồm các ảnh chữ số viết tay thuộc 10 lớp:

```text
0, 1, 2, 3, 4, 5, 6, 7, 8, 9
```

Mỗi ảnh có kích thước:

```text
28 × 28 pixels
```

và chỉ có một kênh màu grayscale.

Bộ dữ liệu được chia thành:

* **60,000 ảnh** dùng để huấn luyện.
* **10,000 ảnh** dùng để kiểm thử.

Dữ liệu được tải trực tiếp thông qua `torchvision.datasets.MNIST`.

---

## 3. Tiền xử lý dữ liệu

Trước khi đưa ảnh vào mô hình, dữ liệu được thực hiện các bước tiền xử lý:

* Chuyển ảnh sang Tensor.
* Chuẩn hóa giá trị pixel.
* Chia dữ liệu thành các mini-batch bằng `DataLoader`.
* Xáo trộn dữ liệu trong quá trình training.

Kích thước đầu vào của một batch có dạng:

```text
[Batch Size, Channel, Height, Width]
```

Ví dụ với `batch_size = 64`:

```text
[64, 1, 28, 28]
```

---

## 4. Kiến trúc mô hình CNN

Mô hình được xây dựng dựa trên kiến trúc CNN đơn giản theo hướng tương tự LeNet.

Cấu trúc tổng quát:

```text
Input Image
    ↓
Convolution Layer 1
    ↓
ReLU
    ↓
Max Pooling
    ↓
Convolution Layer 2
    ↓
ReLU
    ↓
Max Pooling
    ↓
Flatten
    ↓
Fully Connected Layer
    ↓
Fully Connected Layer
    ↓
Output Layer
```

Chi tiết kích thước:

```text
Input:
1 × 28 × 28

Conv1:
1 → 6 channels
Kernel: 3 × 3
Output: 6 × 26 × 26

MaxPool:
Output: 6 × 13 × 13

Conv2:
6 → 16 channels
Kernel: 3 × 3
Output: 16 × 11 × 11

MaxPool:
Output: 16 × 5 × 5

Flatten:
16 × 5 × 5 = 400 features

Fully Connected:
400 → 120
120 → 84
84 → 10
```

Lớp output gồm 10 giá trị tương ứng với 10 chữ số từ 0 đến 9.

---

## 5. Hàm mất mát

Dự án sử dụng:

```text
CrossEntropyLoss
```

Đây là hàm mất mát phù hợp cho bài toán phân loại nhiều lớp.

Mô hình trả về các giá trị logits và `CrossEntropyLoss` được sử dụng để đo mức độ khác biệt giữa kết quả dự đoán và nhãn thật.

---

## 6. Thuật toán tối ưu

Mô hình sử dụng thuật toán:

```text
Adam Optimizer
```

với learning rate ban đầu:

```text
0.001
```

Adam là một thuật toán tối ưu thích nghi, sử dụng thông tin từ gradient trong các bước trước để điều chỉnh mức cập nhật trọng số cho từng tham số.

Adam thường giúp quá trình huấn luyện hội tụ nhanh và ổn định đối với các mô hình Deep Learning có quy mô nhỏ và trung bình.

---

## 7. Quá trình huấn luyện

Trong mỗi batch, quá trình training gồm các bước chính:

```text
Reset Gradient
      ↓
Forward Propagation
      ↓
Calculate Loss
      ↓
Backward Propagation
      ↓
Update Weights with Adam
```

Mô hình được huấn luyện qua nhiều epoch.

Trong quá trình training, các giá trị được theo dõi gồm:

* Training Loss
* Training Accuracy

Loss được kỳ vọng giảm dần qua các epoch, trong khi Accuracy tăng dần khi mô hình học được đặc trưng của các chữ số.

---

## 8. Đánh giá mô hình

Sau khi huấn luyện, mô hình được đánh giá trên tập test gồm 10,000 ảnh.

Các độ đo được sử dụng gồm:

* Accuracy
* Precision
* Recall
* F1-score
* Confusion Matrix
* ROC Curve
* AUC

---

## 9. Accuracy

Accuracy thể hiện tỷ lệ số mẫu được mô hình dự đoán đúng trên tổng số mẫu.

```math
\mathrm{Accuracy}
=
\frac{TP + TN}
{TP + TN + FP + FN}
```

Trong đó:

* **TP - True Positive:** dự đoán Positive và thực tế cũng là Positive.
* **TN - True Negative:** dự đoán Negative và thực tế cũng là Negative.
* **FP - False Positive:** dự đoán Positive nhưng thực tế là Negative.
* **FN - False Negative:** dự đoán Negative nhưng thực tế là Positive.

Accuracy càng gần `1` thì hiệu suất tổng thể của mô hình càng tốt.

---

## 10. Precision

Precision cho biết trong số các mẫu mà mô hình dự đoán thuộc một lớp, có bao nhiêu mẫu thực sự thuộc lớp đó.

```math
\mathrm{Precision}
=
\frac{TP}
{TP + FP}
```

Precision cao cho thấy mô hình ít đưa ra các dự đoán dương tính sai.

---

## 11. Recall

Recall đo khả năng mô hình phát hiện đúng các mẫu thực sự thuộc một lớp.

```math
\mathrm{Recall}
=
\frac{TP}
{TP + FN}
```

Recall còn được gọi là:

```text
Sensitivity
```

hoặc:

```text
True Positive Rate
```

---

## 12. F1-score

F1-score là trung bình điều hòa giữa Precision và Recall.

```math
F1
=
2 \times
\frac{\mathrm{Precision} \times \mathrm{Recall}}
{\mathrm{Precision} + \mathrm{Recall}}
```

F1-score giúp đánh giá sự cân bằng giữa Precision và Recall.

---

## 13. Confusion Matrix

Confusion Matrix được sử dụng để quan sát chi tiết các trường hợp dự đoán đúng và sai của từng chữ số.

Trong ma trận:

* Hàng biểu diễn nhãn thực tế.
* Cột biểu diễn nhãn dự đoán.
* Các phần tử trên đường chéo chính biểu diễn số mẫu được dự đoán chính xác.
* Các phần tử ngoài đường chéo cho biết các trường hợp mô hình nhầm lẫn giữa các chữ số.

Confusion Matrix giúp xác định các cặp chữ số mà CNN thường gặp khó khăn khi phân biệt.

---

## 14. ROC Curve

ROC Curve được sử dụng để đánh giá khả năng phân biệt giữa các lớp.

ROC biểu diễn mối quan hệ giữa:

```math
TPR
=
\frac{TP}
{TP + FN}
```

và:

```math
FPR
=
\frac{FP}
{FP + TN}
```

Trong đó:

* **TPR:** True Positive Rate.
* **FPR:** False Positive Rate.

Do MNIST là bài toán phân loại 10 lớp, ROC được tính theo phương pháp:

```text
One-vs-Rest
```

Ví dụ khi đánh giá chữ số `7`:

```text
Positive: chữ số 7

Negative:
0, 1, 2, 3, 4, 5, 6, 8, 9
```

Quá trình tương tự được thực hiện cho từng chữ số từ 0 đến 9.

---

## 15. AUC

AUC là viết tắt của:

```text
Area Under the ROC Curve
```

AUC đại diện cho diện tích nằm dưới đường cong ROC.

```math
AUC
=
\int_{0}^{1}
TPR(FPR)\,d(FPR)
```

Giá trị AUC nằm trong khoảng:

```math
0 \leq AUC \leq 1
```

AUC càng gần `1` thì mô hình càng có khả năng phân biệt tốt giữa lớp đang xét và các lớp còn lại.

Trong dự án này, **AUC được tính riêng cho từng chữ số từ 0 đến 9**.

Kết quả AUC của từng lớp giúp đánh giá khả năng phân biệt của mô hình đối với từng chữ số cụ thể.

Không sử dụng các biến thể tổng hợp AUC khác như Macro AUC hay Weighted AUC trong phạm vi dự án này.

---

## 16. Nhận diện ảnh chữ số viết tay từ bên ngoài

Ngoài việc đánh giá trên tập test MNIST, mô hình còn hỗ trợ nhận diện ảnh chữ số do người dùng tự viết và upload.

Ảnh bên ngoài được tiền xử lý trước khi đưa vào CNN.

Quy trình:

```text
Upload Image
      ↓
Convert to Grayscale
      ↓
Invert Color
      ↓
Crop Digit Region
      ↓
Resize Digit
      ↓
Place on 28 × 28 Canvas
      ↓
Normalize
      ↓
CNN Prediction
```

Việc tiền xử lý là cần thiết vì ảnh người dùng tự chụp thường khác với dữ liệu MNIST về:

* kích thước,
* màu nền,
* vị trí chữ số,
* tỷ lệ của chữ số,
* khoảng trắng xung quanh.

Sau khi tiền xử lý, ảnh được đưa về định dạng gần giống ảnh MNIST trước khi đưa vào mô hình.

---

## 17. Kết quả dự đoán ảnh tự viết

Sau khi đưa ảnh vào CNN, mô hình trả về:

* chữ số được dự đoán,
* xác suất của từng lớp,
* độ tin cậy của lớp được dự đoán.

Kết quả cuối cùng có dạng:

```text
Predicted Digit: X
Confidence: XX.XX%
```

Ảnh sau tiền xử lý cũng được hiển thị để kiểm tra chính xác dữ liệu mà CNN thực sự nhận được.

---

## 18. Công nghệ sử dụng

Dự án sử dụng các thư viện chính:

* Python
* PyTorch
* Torchvision
* NumPy
* Matplotlib
* Scikit-learn
* Pillow
* Google Colab / Jupyter Notebook

---

## 19. Cấu trúc dự án

Ví dụ cấu trúc repository:

```text
project/
│
├── README.md
│
├── CNN_MNIST.ipynb
│
├── mnist_cnn.pth
│
└── images/
```

Trong đó:

```text
CNN_MNIST.ipynb
```

chứa toàn bộ quá trình:

* tiền xử lý dữ liệu,
* xây dựng CNN,
* huấn luyện,
* kiểm thử,
* tính các độ đo,
* ROC và AUC,
* nhận diện ảnh viết tay bên ngoài.

File:

```text
mnist_cnn.pth
```

lưu trọng số của mô hình sau khi huấn luyện.

---

## 20. Quy trình tổng quát

Toàn bộ pipeline của dự án:

```text
MNIST Dataset
      ↓
Preprocessing
      ↓
DataLoader
      ↓
CNN Model
      ↓
CrossEntropyLoss
      ↓
Adam Optimizer
      ↓
Training
      ↓
Testing
      ↓
Accuracy
Precision
Recall
F1-score
Confusion Matrix
ROC Curve
AUC
      ↓
Handwritten Image Prediction
```

---

## 21. Kết luận

Dự án đã xây dựng thành công một mô hình CNN bằng PyTorch cho bài toán nhận diện chữ số viết tay MNIST.

Thông qua hai lớp Convolution kết hợp với ReLU, Max Pooling và các lớp Fully Connected, mô hình có khả năng học được các đặc trưng hình ảnh cần thiết để phân biệt 10 chữ số từ 0 đến 9.

Adam được sử dụng làm thuật toán tối ưu trong quá trình cập nhật trọng số. Hiệu suất mô hình được đánh giá thông qua Accuracy, Precision, Recall, F1-score, Confusion Matrix, ROC Curve và AUC của từng lớp.

Ngoài việc phân loại dữ liệu MNIST, mô hình còn có khả năng tiếp nhận và dự đoán các ảnh chữ số viết tay do người dùng tự cung cấp sau khi thực hiện các bước tiền xử lý phù hợp.

Toàn bộ phần cài đặt chi tiết, quá trình training, testing và visualization được trình bày trong file notebook `.ipynb` của dự án.
