# Phân chia notebook (dự kiến)

| Thành viên | Notebook | Trách nhiệm đề xuất |
|---|---|---|
| Tấn Lên (nhóm trưởng) | `notebooks/len.ipynb` | Thiết kế thực nghiệm, kiểm tra, tích hợp, kết luận |
| Lan | `notebooks/lan.ipynb` | EDA: thống kê, chất lượng dữ liệu, trực quan |
| Linh | `notebooks/linh.ipynb` | PCA 2D, biểu đồ theo nhãn và hỗ trợ biểu đồ cụm |
| Bảo | `notebooks/bao.ipynb` | KNN, SVM, 10-fold CV |
| Thông | `notebooks/thong.ipynb` | Random Forest, so sánh F1 3 mô hình |
| Tài | `notebooks/tai.ipynb` | K-Means, DBSCAN, ARI |

Đây là **phân vai gợi ý** dựa trên 6 nhóm nhiệm vụ đã chốt, chưa được xác nhận bằng họ tên đầy đủ; có thể đổi vai mà không cần đổi tên notebook.

## Nguyên tắc bàn giao
- Mỗi người chỉ sửa notebook của mình, trừ khi được nhóm trưởng giao phần chung.
- Mỗi mục có: mục tiêu, kiến thức liên quan, code, kết quả, nhận xét.
- Các kết quả đánh giá phải có từ code, không tự điền số.
- Cột `Class` không dùng để huấn luyện gom cụm (chỉ dùng để tô màu PCA theo nhãn thật và đánh giá ARI).
- Việc chuẩn hóa phục vụ phân lớp phải fit trên train của từng fold, không để test rò rỉ vào huấn luyện.

**Theo dõi chi tiết tại:** https://docs.google.com/spreadsheets/d/1S9UvotHgvdllcwYeqMPWLBd3pDKOompiFLVUkymPGUs/edit
