# Quy trình làm việc với GitHub

**Repository:** `tanlen06-debug/Khai_Thac_Du_Lieu_Gr6`

## 1. Chỉ tạo nhánh khi thành viên bắt đầu làm
Nhánh phải đặt theo cấu trúc **`tên-brand`**:

- `len-brand`
- `lan-brand`
- `linh-brand`
- `bao-brand`
- `thong-brand`
- `tai-brand`

Các tên trên chỉ là **ví dụ**, hiện nhóm trưởng chưa tạo nhánh cho bất kỳ thành viên nào.

## 2. Mỗi thành viên tạo nhánh của mình từ main

```bash
git clone https://github.com/tanlen06-debug/Khai_Thac_Du_Lieu_Gr6.git
cd Khai_Thac_Du_Lieu_Gr6
git checkout main
git pull origin main
git checkout -b lan-brand             # thay lan bằng tên của bạn
```

## 3. Sửa đúng notebook và push nhánh

```bash
git add notebooks/lan.ipynb           # thay thành notebook của bạn
git commit -m "Hoan thanh EDA Dry Bean"
git push -u origin lan-brand
```

Trên GitHub, tạo Pull Request: `lan-brand` → `main`, đính kèm kết quả chạy/nhận xét và yêu cầu trưởng nhóm duyệt.

## 4. Quy tắc làm việc
- Không tự push trực tiếp vào `main` sau giai đoạn khởi tạo.
- Không xóa hoặc sửa notebook thành viên khác.
- Nếu cần thêm file chung, báo nhóm trưởng trước.
- Trước khi mở PR, chạy Restart & Run All, kiểm tra đầu ra và báo cáo.
- Nếu đồng bộ thay đổi từ `main`, pull/fetch và giải quyết xung đột có kiểm chứng.
