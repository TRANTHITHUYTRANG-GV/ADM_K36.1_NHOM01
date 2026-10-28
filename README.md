# 📊 QUẢN TRỊ DỮ LIỆU BÁN HÀNG VÀ ỨNG DỤNG KHAI PHÁ DỮ LIỆU TẠI CHUỖI BÁN LẺ SUPERSTORE

Dự án nghiên cứu và triển khai hệ thống **Kho dữ liệu (Data Warehouse)** kết hợp với **Khai phá dữ liệu (Data Mining & Machine Learning)** nhằm tối ưu hóa chiến lược bán chéo (Cross-selling), quản trị hàng tồn kho và dự báo phân lớp đơn hàng cho chuỗi bán lẻ Superstore.

---

| STT | Thành viên | MSSV | Vai trò | Nhiệm vụ phân công cụ thể |
| :---: | :--- | :---: | :--- | :--- |
| 1 | **Đỗ Ngọc Hân** | 526102180488 | Member | • Soạn thảo **Chương 2 (Tổng quan nghiên cứu & Lý thuyết nền tảng)**.<br> • Lập trình Python: Mô hình phân lớp (LR, DT, RF), Kiểm định thống kê (McNemar, Bootstrap).
| 2 | **Hồ Thanh Duy Khánh** | 526102180487 | **Leader** | • Lập trình Python: Phân tích thăm dò dữ liệu (EDA), Tiền xử lý, Khai phá luật kết hợp (Apriori 1 chiều & Đa chiều).<br>• Soạn thảo **Chương 3 (Phương pháp luận)**. |
| 3 | **Trần Thị Thùy Trang** | 526102180015 | Member | • Thiết kế Data Warehouse (Star Schema) & Viết truy vấn SQL (`ROLLUP`, `CUBE`) trên **Google BigQuery**.<br>• Xây dựng Dashboard báo cáo tương tác 4 trang trên **Looker Studio**.<br>• Soạn thảo **Chương 4 (Phần Data Warehouse & OLAP)**. |
| 4 | **Lê Anh Kiệt** | 526102180484 | Member | Đồng soạn thảo **Chương 4 (Phần Kết quả Khai phá luật & Phân lớp)** dựa trên output code. <br>• Review tổng thể mã nguồn, kiểm tra tính nhất quán dữ liệu & duyệt báo cáo cuối cùng. |
| 5 | **Cao Thị Kim Hằng** | 526102180006 | Member | • Soạn thảo **Chương 1 (Giới thiệu, Mục tiêu & Câu hỏi nghiên cứu RQ1–RQ3)**.<br>• Định dạng (Format) toàn bộ file báo cáo Word chuẩn quy định UEH & Thiết kế Slide thuyết trình. |
| 6 | **Nguyễn Lê Hạnh Trang** | 526102180506 | Member | • Soạn thảo **Chương 5 (Kết luận, Ý nghĩa, Hạn chế & Hướng phát triển)**.<br>• Chạy kiểm tra đạo văn (Plagiarism Check), rà soát lỗi trích dẫn APA & Quản lý GitHub. |

---

## 📌 Mục Tiêu Nghiên Cứu (Research Questions)

* **RQ1:** Dữ liệu Superstore có những đặc điểm gì ảnh hưởng đến việc lựa chọn bài toán khai phá?
* **RQ2:** Luật kết hợp một chiều và luật kết hợp đa chiều khác nhau thế nào về độ phủ dữ liệu?
* **RQ3:** Bổ sung đặc trưng từ luật kết hợp có cải thiện mô hình phân lớp đơn hàng giá trị cao một cách có ý nghĩa thống kê hay không?

---

## 🏗 Kiến Trúc Hệ Thống & Quy Trình Thực Hiện

```text
[ Raw Data (Superstore CSV) ]
             │
             ▼
[ Data Preprocessing & Cleaning (Pandas) ]
             │
             ├───► [ Data Warehouse - Google BigQuery (Star Schema) ]
             │              │
             │              ▼
             │     [ Business Intelligence - Looker Studio Dashboard ]
             │
             └───► [ Data Mining & Machine Learning (Python) ]
                    ├── Market Basket Analysis (Apriori Algorithm)
                    ├── Machine Learning (Logistic Regression, DT, Random Forest)
                    └── Model Evaluation (McNemar Test & Bootstrap 95% CI)
```

---

## 💡 Kết Quả & Phát Hiện Chính

1. **Data Warehouse & OLAP:**
   * Phân khúc khách hàng, vùng địa lý và hình thức giao hàng chỉ khác nhau về số lượng đơn, không làm thay đổi đáng kể giá trị trung bình mỗi đơn. Giá trị đơn hàng phụ thuộc chính vào **nhóm hàng con (Sub-Category)**.
2. **Khai Phá Luật Kết Hợp (Association Rules):**
   * Luật kết hợp 1 chiều đạt độ phủ **~30.6%**, cao gấp 1.6 lần luật đa chiều (**~19.1%**). Việc thêm ngữ cảnh (vùng, phân khúc) làm thu hẹp độ phủ mà không tăng đáng kể độ tin cậy.
3. **Mô Hình Phân Lớp (Classification):**
   * Việc bổ sung các đặc trưng từ luật kết hợp giúp nâng cao hiệu năng dự báo đơn hàng giá trị cao. Mô hình **Random Forest** kết hợp luật đạt ROC-AUC tăng từ `0.8157` lên `0.8346` (Khoảng tin cậy Bootstrap 95% nằm hoàn toàn trên 0 có ý nghĩa thống kê).

---

## 📁 Cấu Trúc Repository

```text
├── data/
│   ├── raw/                      # Dữ liệu thô từ Kaggle (train.csv)
│   ├── processed/                # Dữ liệu sạch (superstore_clean.csv)
│   └── ml_datasets/              # Dataset A, B, C cho bài toán phân lớp
├── sql_bigquery/
│   ├── 01_schema_setup.sql       # Script tạo Bảng Fact & Dimensions (Star Schema)
│   ├── 02_etl_transform.sql      # Quy trình nạp & biến đổi dữ liệu
│   └── 03_cuboid_queries.sql     # Truy vấn ROLLUP, CUBE cho OLAP
├── notebooks/
│   ├── 01_eda_preprocessing.ipynb # Notebook EDA & Tiền xử lý dữ liệu
│   ├── 02_association_rules.ipynb # Notebook khai phá luật Apriori & Multi-dimensional
│   └── 03_classification_eval.ipynb# Notebook huấn luyện mô hình & Kiểm định thống kê
├── reports/
│   └── Baocaocuoiky_ADM_Superstore.docx # File Báo cáo đồ án hoàn chỉnh
└── README.md                     # File mô tả dự án
```

---

## 🚀 Hướng Dẫn Chạy Mã Nguồn

### 1. Yêu cầu môi trường
* Python 3.8+
* Thư viện yêu cầu:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn mlxtend scipy
```

### 2. Thứ tự thực thi
1. Clone dự án về máy:
   ```bash
   git clone https://github.com/your-username/ADM_Superstore_Sales_Group01.git
   cd ADM_Superstore_Sales_Group01
   ```
2. Chạy lần lượt các file notebook trong thư mục `notebooks/`:
   * `01_eda_preprocessing.ipynb`: Làm sạch dữ liệu và tạo bộ nhãn.
   * `02_association_rules.ipynb`: Khai phá luật kết hợp và tạo bộ đặc trưng mới.
   * `03_classification_eval.ipynb`: Huấn luyện mô hình và thực hiện kiểm định McNemar & Bootstrap.
