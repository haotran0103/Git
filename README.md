
### 1. **Data Engineer**
**Nhiệm vụ chính**: Thu thập dữ liệu và xây dựng hệ thống lưu trữ dữ liệu hợp lý.

#### Step 1: **Crawl dữ liệu**
- **Công cụ**:
  - **BeautifulSoup + Requests**: Để xử lý các trang web tĩnh.
  - **Selenium**: Nếu Shopee sử dụng JavaScript dynamic loading (dữ liệu không xuất hiện trực tiếp trong HTML).
  - **API Shopee**: Nếu có API công khai, ưu tiên sử dụng để tránh rủi ro khi crawl từ web.
  - **Proxy/Headless Browser**: Để tránh bị chặn bởi Shopee khi crawl dữ liệu quá nhiều.
  
  **Ví dụ dữ liệu cần thu thập**:
  - Tên sản phẩm, ID sản phẩm.
  - Giá hiện tại, giá trước khuyến mãi (nếu có).
  - Số lượng bán ra.
  - Số lượng đánh giá, điểm đánh giá.
  - Thông tin về cửa hàng (địa điểm, thời gian mở bán, số lượng sản phẩm).

#### Step 2: **Chuẩn hóa và tiền xử lý dữ liệu**
- **Tiền xử lý**:
  - **Xóa dữ liệu bị lỗi**: Xử lý các ngoại lệ như giá trị thiếu, dữ liệu trùng lặp.
  - **Định dạng nhất quán**: Chuyển đổi các định dạng số liệu như giá thành số nguyên (integer), đơn vị tiền tệ (currency).
  
#### Step 3: **Lưu trữ dữ liệu (Data Lake)**
- **Mô hình lưu trữ**:
  - **File-based**: Nếu lượng dữ liệu không quá lớn, có thể lưu dạng file CSV hoặc JSON.
  - **Database**: Nếu dữ liệu lớn và cần truy vấn hiệu quả, sử dụng **PostgreSQL** hoặc **MongoDB** (cho dữ liệu phi cấu trúc).
  - **Data Lake**: Để có mô hình lưu trữ linh hoạt, bạn có thể lưu dữ liệu thô vào **AWS S3** hoặc hệ thống **Hadoop**.
  
  **Kiến trúc lưu trữ Data Lake**:
  - **Raw Zone**: Lưu dữ liệu thô từ nguồn mà chưa qua xử lý.
  - **Cleansed Zone**: Sau khi đã xử lý, chuẩn hóa dữ liệu.
  - **Curated Zone**: Dữ liệu đã tổ chức theo các bảng dữ liệu cụ thể sẵn sàng cho phân tích.

#### Step 4: **Tích hợp và quản lý lịch trình crawl**
- **Cron Jobs**: Sử dụng cron jobs để crawl dữ liệu tự động hàng ngày/tuần.
- **Airflow**: Dùng Apache Airflow để điều phối và theo dõi quy trình xử lý dữ liệu.

---

### 2. **Data Analyst**
**Nhiệm vụ chính**: Phân tích dữ liệu và tạo báo cáo.

#### Step 1: **Nhận dữ liệu từ Data Engineer**
- **Truy cập dữ liệu** từ các bảng đã được xử lý, chuẩn hóa từ Data Lake hoặc database.

#### Step 2: **Phân tích dữ liệu**
- **Công cụ**:
  - **Python (Pandas)**: Để xử lý và phân tích dữ liệu.
  - **SQL**: Nếu dữ liệu được lưu trữ trong hệ quản trị cơ sở dữ liệu quan hệ như PostgreSQL, thực hiện các truy vấn SQL phức tạp để trích xuất dữ liệu cần thiết.
  
- **Những phân tích cần thực hiện**:
  - **Phân tích doanh thu theo thời gian**: Doanh thu tăng trưởng qua các giai đoạn khác nhau (theo ngày, tuần, tháng).
  - **Sản phẩm bán chạy nhất**: Sản phẩm nào có số lượng bán ra cao nhất và chiếm tỉ trọng bao nhiêu trong tổng doanh thu.
  - **Tương quan giữa đánh giá và doanh thu**: Đánh giá khách hàng ảnh hưởng như thế nào đến lượng bán ra.
  - **Phân tích khuyến mãi**: Ảnh hưởng của các chương trình khuyến mãi tới doanh thu.
  - **Phân tích về mùa vụ**: Những tháng cao điểm và thấp điểm trong năm.

#### Step 3: **Visualization (Trực quan hóa dữ liệu)**
- **Công cụ**:
  - **Tableau/Power BI**: Dùng để tạo ra các dashboard tương tác, dễ dàng chia sẻ và trực quan với các stakeholders.
  - **Python (Matplotlib, Seaborn)**: Nếu cần code trực tiếp để tạo ra các biểu đồ chi tiết hơn hoặc khi kết hợp với các phân tích phức tạp.

  **Các loại biểu đồ cần thiết**:
  - **Biểu đồ đường (Line chart)**: Doanh thu theo thời gian (theo ngày, tháng).
  - **Biểu đồ cột (Bar chart)**: Top sản phẩm bán chạy nhất.
  - **Biểu đồ tỉ lệ (Pie chart)**: Tỉ trọng doanh thu của từng loại sản phẩm hoặc phân tích doanh thu theo danh mục sản phẩm.
  - **Biểu đồ nhiệt (Heatmap)**: Tương quan giữa đánh giá và doanh thu.
  - **Biểu đồ phân tán (Scatter plot)**: Thể hiện sự ảnh hưởng của giá bán tới số lượng sản phẩm bán ra.

#### Step 4: **Tạo báo cáo cuối cùng**
- **Công cụ**:
  - **PowerPoint**: Tổng hợp và trình bày kết quả phân tích dưới dạng báo cáo dễ hiểu.
  - **Tableau/Power BI**: Tạo ra dashboard tương tác, chia sẻ trực tuyến để người xem có thể tự tương tác và phân tích thêm.

---

### **Tóm tắt workflow step-by-step**
1. **Data Engineer**:
   - Step 1: Crawl dữ liệu từ Shopee (Selenium, BeautifulSoup).
   - Step 2: Tiền xử lý và chuẩn hóa dữ liệu (Pandas).
   - Step 3: Lưu trữ dữ liệu vào Data Lake (AWS S3, Hadoop) hoặc database (PostgreSQL).
   - Step 4: Tích hợp lịch trình crawl dữ liệu tự động (Airflow, Cron).

2. **Data Analyst**:
   - Step 1: Truy cập dữ liệu từ Data Lake hoặc database.
   - Step 2: Phân tích các chỉ số quan trọng (doanh thu, sản phẩm bán chạy, đánh giá).
   - Step 3: Trực quan hóa dữ liệu (Tableau, Power BI, Matplotlib).
   - Step 4: Báo cáo kết quả phân tích và tạo dashboard tương tác.

### **Công nghệ/Tools sử dụng**:
- **Data Engineer**:
  - Crawl: **Selenium**, **BeautifulSoup**, **API**.
  - Lưu trữ: **AWS S3**, **Hadoop**, **PostgreSQL**, **MongoDB**.
  - Quản lý pipeline: **Apache Airflow**, **Cron**.
  
- **Data Analyst**:
  - Phân tích: **Python (Pandas, Numpy)**, **SQL**.
  - Visualization: **Tableau**, **Power BI**, **Matplotlib**, **Seaborn**.
  - Báo cáo: **PowerPoint**, **Google Slides**.
