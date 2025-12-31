# DỰ ĐOÁN KẾT QUẢ HỌC TẬP CỦA HỌC SINH  
*(Student Performance Prediction – Machine Learning)*

---

## 1. Giới thiệu đề tài
### Bài toán
Đề tài được xây dựng dưới dạng **bài toán hồi quy (Regression)** với mục tiêu
**dự đoán điểm cuối kỳ môn Toán (G3)** của học sinh tại thời điểm kết thúc năm học,
dựa trên các thông tin cá nhân, gia đình, quá trình học tập và hành vi của học sinh.

### Mục tiêu
- Xây dựng pipeline Machine Learning hoàn chỉnh
- Khám phá và tiền xử lý dữ liệu
- Huấn luyện và so sánh nhiều mô hình hồi quy
- Đánh giá mô hình bằng các chỉ số phù hợp
- Xây dựng ứng dụng demo để dự đoán điểm G3 cho học sinh mới

---

## 2. Dataset
### Nguồn dữ liệu
Dataset **Student Performance** được lấy từ:
- Kaggle:  
  https://www.kaggle.com/datasets/rxshark/uci-student-performance-dataset-by-paulo-cortez/code
- Gốc từ: **UCI Machine Learning Repository**

### Thông tin dataset
- Số lượng mẫu: **395 học sinh**
- Số lượng đặc trưng: **33 đặc trưng đầu vào**
- Biến mục tiêu: **G3 – Điểm cuối kỳ môn Toán**
- File sử dụng: `student-mat.csv`

### Mô tả các cột dữ liệu
| Nhóm | Các cột |
|----|----|
| Thông tin cá nhân | age, sex, address |
| Gia đình | Medu, Fedu, Mjob, Fjob, famsup |
| Học tập & hành vi | studytime, failures, freetime, goout, health |
| Kết quả học tập | G1, G2 |
| Khác | absences, schoolsup, paid, internet, romantic |
| Target | **G3** |

---

## 3. Pipeline xử lý
Pipeline của dự án gồm các bước:

### 3.1. Tiền xử lý dữ liệu
- Kiểm tra và làm sạch dữ liệu (dataset không có missing values)
- Phân loại biến:
  - **Numeric features** → StandardScaler
  - **Categorical features** → One-Hot Encoding
- Xử lý outlier:
  - Biến `absences` có phân phối lệch phải và chứa giá trị ngoại lai
  - Áp dụng biến đổi:  
    `absences_log = log(1 + absences)`
- Tách dữ liệu:
  - 80% tập huấn luyện
  - 20% tập kiểm tra

### 3.2. Huấn luyện mô hình
- Huấn luyện mô hình trên tập train
- So sánh hiệu năng giữa các mô hình

### 3.3. Đánh giá mô hình
- Đánh giá trên tập test
- Sử dụng các chỉ số MAE, RMSE, R²

### 3.4. Inference
- Dự đoán điểm G3 cho dữ liệu học sinh mới
- Thực hiện thông qua ứng dụng Streamlit

---

## 4. Mô hình sử dụng
Các mô hình Machine Learning được áp dụng:

- **Linear Regression**  
  Mô hình cơ bản, dễ diễn giải, làm baseline
- **Lasso Regression (L1)**  
  Giảm overfitting, thực hiện chọn lọc đặc trưng
- **Decision Tree Regressor**  
  Học quan hệ phi tuyến, nhưng dễ overfitting nếu cây sâu
- **Random Forest Regressor**  
  Mô hình ensemble, giảm overfitting và cho kết quả ổn định nhất

---

## 5. Kết quả
Các mô hình được đánh giá bằng các chỉ số:
- **MAE (Mean Absolute Error)**
- **RMSE (Root Mean Squared Error)**
- **R² Score**

### Mô hình A (có sử dụng G1, G2)
| Model | MAE | RMSE | R² |
|----|----|----|----|
| Random Forest | **1.212** | **1.987** | **0.807** |
| Lasso Regression | 1.488 | 2.146 | 0.775 |
| Linear Regression | 1.691 | 2.311 | 0.739 |
| Decision Tree | 1.354 | 2.548 | 0.683 |

### Mô hình B (không sử dụng G1, G2)
| Model | MAE | RMSE | R² |
|----|----|----|----|
| Random Forest | **2.979** | **3.837** | **0.282** |
| Linear Regression | 3.384 | 4.192 | 0.143 |
| Lasso Regression | 3.419 | 4.234 | 0.126 |
| Decision Tree | 3.620 | 4.695 | -0.075 |

=> **Random Forest** là mô hình cho kết quả tốt nhất ở cả hai trường hợp.

---

## 6. Hướng dẫn chạy

# 6.1. Cài môi trường
pip install numpy pandas scikit-learn matplotlib seaborn streamlit joblib

# 6.2. Chạy train
jupyter notebook
# Mở và chạy file: 12423020_DoanThiThuLinh.ipynb

# 6.3. Chạy demo / inference
streamlit run app.py


## 7. Cấu trúc thư mục dự án
MachineLearning/
│
├── data/
│   └── student-mat.csv
├── app/
│   └── 12423020_DoanThiThuLinh.ipynb
├── demo/
│   └── app.py
├── student_g3.pkl
├── student_g3_model_b1_no_g1g2.pkl
├── slide/
│   └── 12423TN_12423020_DoanThiThuLinh_ML.pdf
├── README.md
└── requirements.txt

## 8. Tác giả
- **Họ tên**: Đoàn Thị Thu Linh  
- **Mã sinh viên**: 12423020  
- **Lớp**: 12423TN
