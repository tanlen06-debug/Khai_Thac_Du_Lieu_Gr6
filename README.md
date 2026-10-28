# Khai_Thac_Du_Lieu_Gr6

## Bài tập lớn Khai thác dữ liệu — Dry Bean

Repository làm việc nhóm 6 thành viên. **Nhóm trưởng:** Tấn Lên.

Đề tài: Ứng dụng các thuật toán khai thác dữ liệu để phân lớp và phân cụm các giống đậu dựa trên các đặc trưng hình thái (Dry Bean).

### Nội dung bắt buộc
1. Đọc dữ liệu, kích thước, kiểu dữ liệu, phân bố nhãn, min/max/mean.
2. Chọn đặc trưng số, giảm chiều PCA xuống 2D và trực quan các lớp.
3. Thử **3 mô hình phân lớp**, tối ưu siêu tham số, **10-fold cross-validation** và so sánh F-score.
4. Bỏ cột nhãn, chạy **K-Means** và **DBSCAN**, đánh giá bằng nhãn thật.

### Tổ chức repository

```text
Khai_Thac_Du_Lieu_Gr6/
├── README.md
├── .gitignore
├── requirements.txt
├── data/
│   ├── raw/                 # Dry Bean Excel gốc (chưa đưa lên)
│   └── processed/           # CSV và dữ liệu tiền xử lý
├── notebooks/
│   ├── len.ipynb            # Trưởng nhóm: đánh giá & tổng hợp
│   ├── lan.ipynb            # EDA và chất lượng dữ liệu
│   ├── linh.ipynb           # PCA 2D & trực quan
│   ├── bao.ipynb            # KNN & SVM
│   ├── thong.ipynb          # Random Forest & so sánh
│   └── tai.ipynb            # K-Means & DBSCAN
├── docs/
│   ├── phan_cong.md
│   └── git_workflow.md
├── src/
│   └── README.md           # Hàm xử lý chung (khi cần)
├── outputs/
│   ├── figures/
│   └── tables/
└── reports/
```

**Lưu ý:** Chỉ tên notebook được cố định theo danh sách nhóm. Vai trò ghi trong file là gợi ý dựa trên bảng phân công 6 người; nhóm trưởng có thể điều chỉnh sau. File Excel/CSV chưa được thêm vào repo.

### Cách bắt đầu
1. Clone repo rồi cài thư viện: `pip install -r requirements.txt`.
2. Khi nhận dataset của giảng viên, lưu `dry_bean.xlsx` vào `data/raw/` ở máy hoặc Colab; có thể xuất CSV vào `data/processed/`.
3. Mở đúng `notebooks/<ten>.ipynb` và làm theo các ô TODO.
4. **Tự tạo nhánh tên-brand** (ví dụ `lan-brand`), commit/push và tạo PR về `main`. **Chưa tạo nhánh nào trước.**
5. Trưởng nhóm chỉ merge sau khi Notebook chạy đủ ô, có kết quả, nhận xét và đáp ứng yêu cầu giảng viên.

### Tài liệu quản lý nhóm
- [Google Sheet phân công nhiệm vụ](https://docs.google.com/spreadsheets/d/1S9UvotHgvdllcwYeqMPWLBd3pDKOompiFLVUkymPGUs/edit)
- [Google Docs viết nội dung nhóm](https://docs.google.com/document/d/1vohV3X3LTFEFVwLI99yi0-1EKy5PKIB24TQ7zveuZOY/edit)
- [Dry Bean dataset — UCI](https://archive.ics.uci.edu/dataset/602/dry+bean+dataset)

> Git không theo dõi thư mục trống; các file `.gitkeep` giúp giữ cấu trúc khi chưa có dữ liệu.
