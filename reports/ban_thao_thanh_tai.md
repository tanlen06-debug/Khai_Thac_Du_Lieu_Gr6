# BẢN THẢO VÀ MINH CHỨNG HOÀN THÀNH PHẦN VIỆC TV6 – THÀNH TÀI
**Học phần:** Khai thác dữ liệu  
**Đề tài:** Dry Bean Dataset | Nhóm Tấn Lên (Nhóm 6)  
**Thành viên:** TV6 – THÀNH TÀI  
**Notebook thực hiện:** `notebooks/tai.ipynb`  
**Nhánh Git:** `tai-brand`

---

## B. ĐIỀN MINH CHỨNG 6 ĐẦU VIỆC CHI TIẾT THEO BẢNG PHÂN CÔNG (CLUST-01 -> CLUST-06)

### CLUST-01 | Tạo ma trận X_cluster không có Class
- **Mục Notebook:** 11 | **Hạn:** 06/11/2026 | **Phối hợp/duyệt:** TV3, TV1.
- **Cách thực hiện:** Đọc dữ liệu từ `data/processed/dry_bean.csv` (13.611 dòng, 16 thuộc tính số); kiểm tra 0 giá trị thiếu; tách riêng nhãn `Class` thành `y_true`; chuẩn hóa 16 đặc trưng bằng `StandardScaler()`.
- **Đầu ra bàn giao:** `X_scaled` (ma trận chuẩn hóa với mean ≈ 0, std = 1).
- **Tiêu chí đạt:** Hoàn thành xuất sắc. Nhãn `Class` chỉ được dùng sau khi gom cụm xong để đánh giá ARI.
- **Minh chứng / liên kết cell notebook:** Cell `tai-todo-0` trong `notebooks/tai.ipynb`.

### CLUST-02 | K-Means k=7 và kiểm tra số cụm
- **Mục Notebook:** 11 | **Hạn:** 09/11/2026 | **Phối hợp/duyệt:** TV3, TV1.
- **Cách thực hiện:** Khởi tạo `KMeans(n_clusters=7, init='k-means++', n_init=10, max_iter=300, random_state=42)`. Dự đoán nhãn cụm `km_labels`, trích xuất `inertia_ = 48.811,96`. Thống kê kích thước 7 cụm và lập ma trận đối chiếu (crosstab) với nhãn thực tế.
- **Đầu ra bàn giao:** Vector nhãn cụm K-Means, bảng kích thước cụm `outputs/tables/kmeans_cluster_summary.csv`, ma trận đối chiếu `outputs/tables/kmeans_crosstab_class.csv`.
- **Tiêu chí đạt:** Không sử dụng `Class` để huấn luyện; số liệu chạy thực tế 100%.
- **Minh chứng / liên kết cell notebook:** Cell `tai-todo-1` trong `notebooks/tai.ipynb`, biểu đồ `outputs/figures/kmeans_crosstab_heatmap.png`.

### CLUST-03 | Viết phần lý thuyết và hạn chế K-Means
- **Mục Notebook:** 11 | **Hạn:** 10/11/2026 | **Phối hợp/duyệt:** TV1.
- **Cách thực hiện:** Trình bày nguyên lý thuật toán phân hoạch lặp, hàm mục tiêu WCSS (Inertia), phương pháp khuỷu tay (Elbow method với $k \in [2, 10]$). Phân tích 4 hạn chế lớn: cố định số cụm $k$, giả định cụm hình cầu đẳng hướng, thiên vị chia đều kích thước cụm và nhạy cảm với ngoại lai.
- **Đầu ra bàn giao:** Bản luận lý thuyết và hạn chế chi tiết, biểu đồ Elbow `outputs/figures/kmeans_elbow_inertia.png`.
- **Tiêu chí đạt:** Giải thích rõ ràng $k=7$ là lựa chọn thử nghiệm tương ứng 7 giống đậu.
- **Minh chứng / liên kết cell notebook:** Cell `tai-section-1`, `tai-kmeans-eval` trong `notebooks/tai.ipynb`.

### CLUST-04 | Thử eps và min_samples cho DBSCAN
- **Mục Notebook:** 12 | **Hạn:** 12/11/2026 | **Phối hợp/duyệt:** TV1.
- **Cách thực hiện:** Trình bày lý thuyết mật độ, điểm lõi (Core), điểm biên (Border) và điểm nhiễu (Noise nhãn -1). Vẽ đồ thị 32-NN distance để tìm điểm uốn $\varepsilon \in [0.8, 1.2]$. Chạy Grid Search 27 cấu hình ($\varepsilon \in [0.5, 2.0]$, $min\_samples \in \{16, 32, 50\}$).
- **Đầu ra bàn giao:** Đồ thị `outputs/figures/dbscan_k_distance.png`, bảng Grid Search `outputs/tables/dbscan_grid_search.csv`.
- **Tiêu chí đạt:** Báo cáo đầy đủ số cụm, số điểm nhiễu, tỷ lệ nhiễu (%) và chỉ số ARI.
- **Minh chứng / liên kết cell notebook:** Cell `tai-section-2`, `tai-todo-2`, `tai-dbscan-eval` trong `notebooks/tai.ipynb`.

### CLUST-05 | Vẽ và phân tích kết quả DBSCAN trên PCA 2D
- **Mục Notebook:** 12 | **Hạn:** 13/11/2026 | **Phối hợp/duyệt:** TV3, TV1.
- **Cách thực hiện:** Giảm chiều PCA xuống 2 thành phần (PC1 giải thích 55.47%, PC2 giải thích 26.43%, tổng 81.90% phương sai). Vẽ biểu đồ K-Means kèm Centroids; biểu đồ DBSCAN làm nổi bật điểm nhiễu `-1` màu xám; lưới 4 biểu đồ đối chiếu (Nhãn thật vs K-Means vs DBSCAN tối ưu vs DBSCAN 1 cụm lớn).
- **Đầu ra bàn giao:** Các biểu đồ phân giải cao: `outputs/figures/kmeans_clusters_pca.png`, `outputs/figures/dbscan_clusters_pca.png`, `outputs/figures/clustering_comparison_pca.png`.
- **Tiêu chí đạt:** Phân biệt rõ cụm và nhiễu; phân tích hiện tượng "cụm khổng lồ" (single dense cluster) và hiệu ứng xích mật độ.
- **Minh chứng / liên kết cell notebook:** Cell `tai-section-pca-vis`, `tai-todo-3`, `tai-pca-eval` trong `notebooks/tai.ipynb`.

### CLUST-06 | Đánh giá ARI và so sánh hai thuật toán
- **Mục Notebook:** 13 | **Hạn:** 14/11/2026 | **Phối hợp/duyệt:** TV1.
- **Cách thực hiện:** Tính `adjusted_rand_score` cho K-Means ($ARI = 0.6687$) và các cấu hình DBSCAN (cao nhất $ARI = 0.2726$). Lập bảng tổng hợp theo đúng chuẩn Mẫu III; phân tích 3 lý do khoa học khiến phân cụm không giám sát sai khác với phân lớp có giám sát.
- **Đầu ra bàn giao:** Bảng kết quả `outputs/tables/clustering_comparison.csv`, bài luận so sánh và giải thích chuyên sâu.
- **Tiêu chí đạt:** Tính toán số liệu thật 100%, chỉ dùng nhãn thật để đánh giá sau cùng.
- **Minh chứng / liên kết cell notebook:** Cell `tai-section-3`, `tai-todo-4`, `tai-clust06-eval` trong `notebooks/tai.ipynb`.

---

## C. KHU VỰC THÀNH VIÊN TỰ SOẠN THẢO VÀ NỘP NỘI DUNG (DÁN VÀO GOOGLE DOCS)

### 1) Cơ sở lý thuyết / định nghĩa / công thức
- **Học không giám sát và Phân cụm dữ liệu (Clustering):** Gom cụm là kỹ thuật phân chia tập dữ liệu chưa gán nhãn thành các nhóm (cụm) sao cho các điểm dữ liệu trong cùng một nhóm có mức độ tương đồng cao, trong khi các điểm dữ liệu thuộc các nhóm khác nhau có mức độ khác biệt tối đa.
- **Thuật toán K-Means:**
  - Thuộc họ gom cụm phân hoạch lặp (partitional clustering). Thuật toán khởi tạo $k$ tâm cụm $\mu_1, \dots, \mu_k$, gán các điểm về tâm gần nhất theo khoảng cách Euclidean $d(x, \mu) = \|x - \mu\|_2$, sau đó cập nhật lại tâm bằng trung bình cộng tọa độ các điểm trong cụm.
  - Hàm mục tiêu Within-Cluster Sum of Squares (WCSS / Inertia):
    $$J = \sum_{j=1}^{k} \sum_{x \in S_j} \|x - \mu_j\|^2$$
- **Thuật toán DBSCAN (Density-Based Spatial Clustering of Applications with Noise):**
  - Định nghĩa cụm là vùng có mật độ điểm dữ liệu dày đặc, được bao quanh bởi các vùng có mật độ thấp.
  - Điểm lõi (Core point): Điểm $p$ có ít nhất `min_samples` điểm nằm trong vùng lân cận bán kính $\varepsilon$: $|N_\varepsilon(p)| \ge min\_samples$.
  - Điểm biên (Border point): Điểm nằm trong lân cận $\varepsilon$ của một điểm lõi nhưng bản thân không phải điểm lõi.
  - Điểm nhiễu (Noise point): Không phải điểm lõi và không thuộc lân cận của điểm lõi nào, được gán nhãn $-1$.
- **Chỉ số Adjusted Rand Index (ARI):**
  - Đo lường mức độ tương đồng giữa phân hoạch cụm tìm được $C$ và nhãn phân loại thực tế $Y$, có hiệu chỉnh theo xác suất ngẫu nhiên:
    $$ARI = \frac{RI - \mathbb{E}[RI]}{\max(RI) - \mathbb{E}[RI]}$$
  - $ARI = 1.0$: Phân hoạch trùng khớp hoàn hảo với nhãn thực tế.
  - $ARI = 0.0$: Phân hoạch tương đương với việc gán nhãn ngẫu nhiên.
  - ARI có tính bất biến với hoán vị nhãn cụm (permutation invariant), không phụ thuộc vào thứ tự đánh số cụm.
- **Chuẩn hóa StandardScaler:**
  $$z = \frac{x - \mu}{\sigma}$$
  Đưa 16 đặc trưng về cùng thang đo (mean = 0, std = 1), ngăn chặn đặc trưng diện tích (`Area` lên tới hàng trăm nghìn) áp đảo hoàn toàn các đặc trưng hình dạng (`ShapeFactor` $< 0.01$).

### 2) Mô tả quy trình thực nghiệm và lý do chọn tham số
1. **Tiền xử lý dữ liệu:** Tách riêng 16 đặc trưng hình thái hạt đậu số học thành $X_{cluster}$, kiểm tra tính toàn vẹn (0 giá trị thiếu). Nhãn `Class` được tách thành $y_{true}$ và lưu độc lập. Áp dụng `StandardScaler().fit_transform(X_cluster)`.
2. **Thực nghiệm K-Means:**
   - Số cụm $k=7$: Chọn có định hướng dựa trên việc bộ dữ liệu gốc có 7 giống đậu (BARBUNYA, BOMBAY, CALI, DERMASON, HOROZ, SEKER, SIRA).
   - Khảo sát phương pháp khuỷu tay (Elbow Method) với $k \in [2, 10]$ để quan sát quán tính Inertia.
   - Tham số: `KMeans(n_clusters=7, init='k-means++', n_init=10, max_iter=300, random_state=42)`. Thuật toán `k-means++` giúp khởi tạo các tâm cụm cách xa nhau, giảm thiểu nguy cơ rơi vào cực tiểu địa phương.
3. **Thực nghiệm DBSCAN:**
   - Xác định `min_samples`: Theo lý thuyết Ester et al. (1996), với số chiều $m=16$, chọn $min\_samples \ge 2 \times m = 32$. Thử nghiệm mở rộng với các mốc 16, 32, 50.
   - Định hướng $\varepsilon$ qua đồ thị 32-NN Distance: Tính khoảng cách tới láng giềng thứ 32 của từng điểm, sắp xếp tăng dần, phát hiện điểm uốn (knee) trong khoảng $\varepsilon \in [0.8, 1.4]$.
   - Grid Search trên 27 cặp tham số: $\varepsilon \in [0.5, 0.6, 0.7, 0.8, 1.0, 1.2, 1.4, 1.6, 2.0]$ kết hợp với $min\_samples \in \{16, 32, 50\}$.
4. **Giảm chiều và trực quan hóa PCA 2D:**
   - Dùng `PCA(n_components=2, random_state=42)` trên dữ liệu chuẩn hóa. PC1 giải thích $55.47\%$ và PC2 giải thích $26.43\%$, tổng giữ lại $81.90\%$ thông tin cấu trúc.
   - Trực quan hóa 4 bảng đồ thị đối chiếu nhằm phân tích trực quan ranh giới và hiện tượng xích mật độ.

### 3) Kết quả thực tế (bảng số liệu, ảnh biểu đồ, log các cell)

#### a) Bảng tổng hợp so sánh theo Mẫu III (File: `outputs/tables/clustering_comparison.csv`):
| Thuật toán | Tham số | Số cụm (không gồm nhiễu) | Số điểm nhiễu | Tỷ lệ nhiễu (%) | ARI |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **K-Means** | $k=7, init=k-means++, n\_init=10, random\_state=42$ | 7 | 0 | 0.00% | **0.6687** |
| **DBSCAN (Tối ưu ARI)** | $\varepsilon=0.8, min\_samples=32$ | 4 | 4400 | 32.33% | **0.2726** |
| **DBSCAN (Khảo sát $\varepsilon=1.0$)** | $\varepsilon=1.0, min\_samples=16$ | 2 | 1234 | 9.07% | **0.0441** |
| **DBSCAN (Khảo sát $\varepsilon=1.2$)** | $\varepsilon=1.2, min\_samples=32$ | 2 | 935 | 6.87% | **0.0398** |

#### b) Bảng thống kê chi tiết từng cụm K-Means (File: `outputs/tables/kmeans_cluster_summary.csv`):
- **Giá trị Inertia (WCSS):** $48.811,96$.
- **Thống kê phân bố cụm:**
  - `Cluster 5` ($520$ mẫu, $3.82\%$): Giống BOMBAY chiếm $520/520$ mẫu $\rightarrow$ **Độ thuần khiết 100.00%**.
  - `Cluster 3` ($1.769$ mẫu, $13.00\%$): Giống HOROZ chiếm $1.661/1.769$ mẫu $\rightarrow$ **Độ thuần khiết 93.89%**.
  - `Cluster 4` ($3.157$ mẫu, $23.19\%$): Giống DERMASON chiếm $2.912/3.157$ mẫu $\rightarrow$ **Độ thuần khiết 92.24%**.
  - `Cluster 2` ($2.033$ mẫu, $14.94\%$): Giống SEKER chiếm $1.874/2.033$ mẫu $\rightarrow$ **Độ thuần khiết 92.18%**.
  - `Cluster 1` ($3.111$ mẫu, $22.86\%$): Giống SIRA chiếm $2.326/3.111$ mẫu $\rightarrow$ **Độ thuần khiết 74.77%**.
  - `Cluster 0` ($2.480$ mẫu, $18.22\%$): Giống CALI chiếm $1.303$ mẫu, BARBUNYA chiếm $1.142$ mẫu $\rightarrow$ Độ thuần khiết $52.54\%$.
  - `Cluster 6` ($541$ mẫu, $3.97\%$): Giống CALI chiếm $270$ mẫu, HOROZ chiếm $187$ mẫu $\rightarrow$ Độ thuần khiết $49.91\%$.

#### c) Bảng khảo sát Grid Search DBSCAN (Top 5 cấu hình ARI cao nhất):
- $\varepsilon=0.8, min\_samples=32$: $4$ cụm, $4.400$ điểm nhiễu ($32.33\%$), **ARI $= 0.2726$**.
- $\varepsilon=0.7, min\_samples=16$: $4$ cụm, $4.554$ điểm nhiễu ($33.46\%$), **ARI $= 0.2617$**.
- $\varepsilon=0.8, min\_samples=50$: $4$ cụm, $5.494$ điểm nhiễu ($40.36\%$), **ARI $= 0.2392$**.
- $\varepsilon=0.7, min\_samples=32$: $4$ cụm, $6.109$ điểm nhiễu ($44.88\%$), **ARI $= 0.2143$**.
- $\varepsilon=0.6, min\_samples=16$: $9$ cụm, $6.356$ điểm nhiễu ($46.70\%$), **ARI $= 0.1919$**.

#### d) Danh mục hình ảnh biểu đồ minh chứng (thư mục `outputs/figures/`):
- `kmeans_elbow_inertia.png`: Biểu đồ đường cong khuỷu tay của K-Means ($k=2..10$).
- `kmeans_crosstab_heatmap.png`: Ma trận nhiệt đối chiếu cụm K-Means với 7 giống đậu.
- `dbscan_k_distance.png`: Đồ thị khoảng cách 32-NN định hướng chọn $\varepsilon$.
- `kmeans_clusters_pca.png`: Đồ thị phân cụm K-Means và 7 Centroids trên PCA 2D.
- `dbscan_clusters_pca.png`: Đồ thị phân cụm DBSCAN làm nổi bật các điểm nhiễu $-1$.
- `clustering_comparison_pca.png`: Bảng 4 biểu đồ đối chiếu trực quan tổng thể.

### 4) Phân tích/nhận xét và nêu giới hạn

#### a) Đánh giá mô hình K-Means:
- **Ưu điểm thực nghiệm:** K-Means với $k=7$ đạt điểm **ARI $= 0.6687$**, thể hiện sự tương thích hình học rất cao với bộ dữ liệu Dry Bean. Cụm 5 tách biệt hoàn hảo giống BOMBAY ($100\%$), Cụm 3 tách biệt rất tốt giống HOROZ ($93.89\%$), Cụm 2 tách biệt giống SEKER ($92.18\%$) và Cụm 4 bắt được giống DERMASON ($92.24\%$).
- **Giới hạn:** Do K-Means giả định các cụm hình cầu lồi (spherical) và có phương sai đồng nhất, nó không thể tách được giống CALI và BARBUNYA (hai giống đậu đốm lớn có hình thái gần như tương đồng), buộc phải gộp chúng lại trong Cụm 0. Ngoài ra, ranh giới Voronoi phẳng của K-Means cắt ngang qua vùng pha trộn giữa DERMASON và SIRA.

#### b) Đánh giá mô hình DBSCAN và Hiện tượng "Cụm khổng lồ":
- **Hạn chế nghiêm trọng trên Dry Bean:** DBSCAN chỉ đạt điểm **ARI cao nhất là $0.2726$** (tại $\varepsilon=0.8, min\_samples=32$), kém xa so với K-Means.
- **Nguyên nhân cốt lõi:**
  1. *Hiệu ứng xích mật độ (Density Chaining):* Bộ dữ liệu Dry Bean là một dải phân bố liên tục về kích thước và hình thái. Các giống đậu không có ranh giới mật độ thưa ngăn cách rõ ràng. Khi $\varepsilon \ge 1.0$, các điểm lõi nối thông liên tục, khiến DBSCAN gộp $> 89\%$ dữ liệu vào một cụm khổng lồ duy nhất (ARI sụt xuống $0.0441$).
  2. *Bùng nổ điểm nhiễu:* Khi giảm $\varepsilon \le 0.7$ để cố gắng chia nhỏ cụm khổng lồ, thuật toán lại xem hơn $33\% - 80\%$ dữ liệu là nhiễu, làm mất mát lượng lớn thông tin.
  3. *Mật độ không đồng nhất:* DBSCAN dùng một bán kính $\varepsilon$ toàn cục, không thể thích ứng đồng thời với giống DERMASON/SIRA (mật độ rất dày) và giống BOMBAY (mật độ thưa hơn).

#### c) Lý giải vì sao kết quả gom cụm có sự khác biệt với nhãn phân lớp thực tế:
1. **Khác biệt về triết lý học:** Phân lớp có giám sát sử dụng trực tiếp nhãn $Y$ để tìm ranh giới tối ưu cho bài toán phân loại sinh học; trong khi gom cụm không giám sát thuần túy tìm kiếm các cấu trúc hình học khoảng cách nội tại.
2. **Sự chồng lấn sinh học tự nhiên:** Các giống đậu thực tế là các giống cây trồng biến thiên liên tục về mặt sinh học, kích thước và hình dạng có sự giao thoa tự nhiên (nhất là giữa CALI - BARBUNYA và SIRA - DERMASON), không tạo thành các cụm tách rời biệt lập tuyệt đối.
3. **Kết luận lựa chọn mô hình:** K-Means ($k=7$) là giải thuật gom cụm phù hợp và vượt trội hơn hẳn so với DBSCAN đối với tập dữ liệu Dry Bean Dataset.

### 5) Tệp/đường dẫn minh chứng và nguồn tham khảo
- **Notebook chính:** `repo/notebooks/tai.ipynb` (Chạy toàn vẹn từ đầu đến cuối không lỗi).
- **Báo cáo HTML xuất từ notebook:** `repo/reports/tai.html`.
- **Dữ liệu xuất bảng kết quả:**
  - `repo/outputs/tables/clustering_comparison.csv`
  - `repo/outputs/tables/kmeans_cluster_summary.csv`
  - `repo/outputs/tables/kmeans_crosstab_class.csv`
  - `repo/outputs/tables/dbscan_grid_search.csv`
- **Hình ảnh biểu đồ:** `repo/outputs/figures/*.png` (6 biểu đồ).
- **Tài liệu tham khảo:**
  1. Koklu, M. & Ozkan, I. A. (2020). *Multiclass Classification of Dry Beans Using Computer Vision and Machine Learning Techniques.* Computers and Electronics in Agriculture, 174, 105507.
  2. Ester, M., Kriegel, H. P., Sander, J., & Xu, X. (1996). *A density-based algorithm for discovering clusters in large spatial databases with noise.* In KDD-96 (Vol. 96, pp. 226-231).
  3. Hubert, L., & Arabie, P. (1985). *Comparing partitions.* Journal of Classification, 2(1), 193-218.

### 6) Trạng thái để TV1 duyệt:
**Hoàn thành** (Đã thực hiện đủ 6 đầu việc CLUST-01 đến CLUST-06, kết quả thực nghiệm từ code 100%, đã xuất HTML/biểu đồ/bảng số liệu).

---

## III. MẪU BẢNG GOM CỤM PHẢI ĐIỀN SAU THỰC NGHIỆM (THEO MỤC III ĐỀ CƯƠNG)

| Thuật toán | Tham số | Số cụm (không gồm nhiễu) | Số điểm nhiễu | ARI |
| :--- | :--- | :---: | :---: | :---: |
| **K-Means** | $k=7, init=k-means++, n\_init=10, random\_state=42$ | 7 | 0 | **0.6687** |
| **DBSCAN** | $\varepsilon=0.8, min\_samples=32$ | 4 | 4400 | **0.2726** |
| *DBSCAN (Khảo sát phụ)* | $\varepsilon=1.0, min\_samples=16$ | 2 | 1234 | 0.0441 |
| *DBSCAN (Khảo sát phụ)* | $\varepsilon=1.2, min\_samples=32$ | 2 | 935 | 0.0398 |
