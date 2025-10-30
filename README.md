# 🏠 Quản Lý Điện Nước Cho Khu Trọ Thành Đạt

**Mục tiêu dự án:** Xây dựng một ứng dụng web để đơn giản hóa quy trình nhập liệu, tính toán tự động, quản lý lịch sử và xuất báo cáo chi phí điện, nước hàng tháng cho Khu trọ Thành Đạt.

## ✨ Tính Năng Chính

Dự án được xây dựng dựa trên nhu cầu nghiệp vụ chi tiết, đảm bảo tính chính xác và hiệu quả trong việc tính toán hóa đơn hàng tháng.

  * **Ràng buộc Dữ liệu theo Tháng:**
      * Tự động **lấy chỉ số điện/nước mới của tháng trước** làm chỉ số cũ cho tháng hiện tại khi tạo bản ghi mới.
      * Cho phép người dùng chọn Tháng/Năm để xem, sửa, và nhập liệu.
  * **Tính toán Tự động & Tức thời (Real-time):**
      * Tự động tính **Số KW** và **Số M3** ngay khi nhập chỉ số mới.
      * Tự động tính **Tiền điện, Tiền nước, Tiền rác, và Tổng số tiền** dựa trên các đơn giá cố định.
  * **Logic Nghiệp vụ Đặc biệt:** Xử lý trường hợp **Phòng Quản lý** với **Tiền phòng = 0** và chỉ tính tổng tiền điện, nước, rác.
  * **Quản lý Dữ liệu (CRUD):** Hỗ trợ đầy đủ các thao tác **Thêm, Sửa, Xóa** bản ghi của từng phòng theo tháng đang chọn.
  * **Trải nghiệm người dùng:** Tích hợp tính năng **Loading tự động** sau mỗi thao tác Thêm/Sửa/Xóa để phản ánh quá trình cập nhật dữ liệu.
  * **Báo cáo:** Hỗ trợ tính năng **Xuất file Excel/CSV** toàn bộ dữ liệu đang hiển thị trên bảng.

## 📊 Cấu Trúc Bảng Dữ Liệu

Giao diện chính hiển thị bảng danh sách với 14 cột chi tiết (bao gồm cả các cột tính toán):

| \# | Tên Cột | Mô tả |
| :--- | :--- | :--- |
| 1 | **Phòng** | Số/Tên phòng (Dữ liệu cố định). |
| 2 | **Trạng thái** | Chức vụ/Loại phòng (Dùng cho logic "Quản lý"). |
| 3 | **Số điện cũ** | Chỉ số đầu kỳ (Tự động lấy từ tháng trước). |
| 4 | **Số điện mới** | **Nhập liệu** chỉ số cuối kỳ. |
| 5 | **Số KW** | (4) - (3) |
| 6 | **Tiền điện** | `Số KW` $\times$ 4,500 VND |
| 7 | **Số nước cũ** | Chỉ số đầu kỳ (Tự động lấy từ tháng trước). |
| 8 | **Số nước mới** | **Nhập liệu** chỉ số cuối kỳ. |
| 9 | **Số M3** | (8) - (7) |
| 10 | **Tiền nước** | `Số M3` $\times$ 12,000 VND |
| 11 | **Tiền rác** | Mặc định **30,000 VND** (Có thể sửa). |
| 12 | **Tiền phòng** | **Nhập liệu** thủ công (0 VND nếu là Quản lý). |
| 13 | **Tổng số tiền** | Tổng của (6)+(10)+(11)+(12). |
| 14 | **Ghi chú** | **Nhập liệu** tùy chọn. |

-----

## 🛠️ Hướng Dẫn Thiết Lập Dự Án

### Yêu cầu Tiên quyết

  * Node.js (LTS Version)
  * NPM hoặc Yarn
  * Một nền tảng Database (Ví dụ: MongoDB Atlas, PostgreSQL, hoặc file SQLite nếu chạy trên máy chủ có Persistent Storage).

### 1\. Cấu hình Database

Dự án này cần một database back-end để lưu trữ dữ liệu. Các thông tin về chỉ số (cũ, mới), tiền phòng, trạng thái phòng sẽ được lưu trữ theo Tháng/Năm.

  * **Kết nối:** Cập nhật chuỗi kết nối database (ví dụ: `MONGO_URI` hoặc `DATABASE_URL`) trong file `.env` của dự án Back-end.
  * **Khởi tạo:** Chạy các lệnh migration hoặc seed data để tạo cấu trúc bảng/collection và chèn dữ liệu phòng trọ ban đầu.

### 2\. Thiết lập Back-end API (Node.js/Express)

```bash
# Giả sử bạn đang sử dụng Node.js/Express
cd backend/
npm install
# Khởi động server
npm start 
# Hoặc: node server.js
```

### 3\. Thiết lập Front-end (HTML/CSS/JS)

  * **Cập nhật URL API:** Đảm bảo file JavaScript Front-end (`script.js`) trỏ đúng đến địa chỉ API của Back-end (ví dụ: `http://localhost:3000/api/readings` hoặc URL sau khi deploy).

### 4\. Triển khai (Deployment)

1.  **Đẩy code lên GitHub:** Commit toàn bộ code Front-end và Back-end lên repository này.
2.  **Triển khai Back-end:** Triển khai thư mục Back-end lên các nền tảng như Render, Heroku hoặc Vercel (sử dụng Serverless Functions nếu cần).
3.  **Triển khai Front-end:** Triển khai HTML/CSS/JS lên các nền tảng hosting tĩnh (ví dụ: Vercel, Netlify).

**Lưu ý:** Nếu bạn sử dụng SQLite, hãy đảm bảo nền tảng hosting hỗ trợ Persistent File Storage, nếu không dữ liệu sẽ bị mất.

-----

## 🤝 Đóng Góp

Mọi đóng góp nhằm cải thiện tính năng hoặc sửa lỗi đều được hoan nghênh. Vui lòng tạo một **Pull Request** hoặc mở **Issue** để báo cáo lỗi.
