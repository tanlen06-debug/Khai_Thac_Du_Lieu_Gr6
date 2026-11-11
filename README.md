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
│   ├── raw/                 # Dry Bean Excel gốc (D03 - Dry_Bean_Dataset.xlsx)
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

 
### Tài liệu quản lý nhóm
- [Google Sheet phân công nhiệm vụ]( https://docs.google.com/spreadsheets/d/1S9UvotHgvdllcwYeqMPWLBd3pDKOompiFLVUkymPGUs/edit?gid=2091037363#gid=2091037363)
- [Google Docs viết nội dung nhóm](https://docs.google.com/document/d/1vohV3X3LTFEFVwLI99yi0-1EKy5PKIB24TQ7zveuZOY/edit)
- [Dry Bean dataset — UCI](https://archive.ics.uci.edu/dataset/602/dry+bean+dataset)

> Git không theo dõi thư mục trống; các file `.gitkeep` giúp giữ cấu trúc khi chưa có dữ liệu.
