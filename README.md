# 📊 QUẢN TRỊ DỮ LIỆU BÁN HÀNG VÀ ỨNG DỤNG KHAI PHÁ DỮ LIỆU TẠI CHUỖI BÁN LẺ SUPERSTORE

Dự án nghiên cứu và triển khai hệ thống **Kho dữ liệu (Data Warehouse)** kết hợp với **Khai phá dữ liệu (Data Mining & Machine Learning)** nhằm tối ưu hóa chiến lược bán chéo (Cross-selling), quản trị hàng tồn kho và dự báo phân lớp đơn hàng cho chuỗi bán lẻ Superstore.

---

## 👨‍💻 Đội Ngũ Thực Hiện & Phân Công Công Việc (Group 01)

| Họ và tên | Vai trò | Phân công công việc chính |
| :--- | :--- | :--- |
| **Lê Anh Kiệt** | **Leader / Reviewer** | Quản lý dự án, Review mã nguồn, Đánh giá & Tổng hợp báo cáo |
| **Cao Thị Kim Hằng** | Member | Soạn thảo Chương 1 (Giới thiệu, RQ1–RQ3) & Định dạng file báo cáo chuẩn UEH |
| **Đỗ Ngọc Hân** | Member | Soạn thảo Chương 2 (Cơ sở lý thuyết, Data Warehouse & Associative Classification) |
| **Hồ Thanh Duy Khánh** | Member | Viết code Python (EDA, Tiền xử lý, Mining Apriori & Mô hình phân lớp, Kiểm định McNemar & Bootstrap) |
| **Trần Thị Thùy Trang** | Member | Xây dựng Data Warehouse (Star Schema) trên Google BigQuery, Trực quan hóa báo cáo trên Looker Studio | Check đạo văn
| **Nguyễn Lê Hạnh Trang** | Member | Soạn thảo Chương 5 (Kết luận / Ý nghĩa & Hạn chế) 

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
