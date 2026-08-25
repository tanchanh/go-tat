# ⚡ GÕ TẮT - BẢNG TRA CỨU & SAO CHÉP NHANH MÃ HOÁ AES-256

> **Ứng dụng Single-Page (1 tập tin HTML duy nhất) chạy hoàn toàn Offline, tích hợp chuẩn mã hoá quân sự AES-256 kết hợp nén Gzip và cơ chế tự đóng gói tập tin độc lập.**

---

## 📌 GIỚI THIỆU

**GÕ TẮT** là công cụ hỗ trợ công việc hàng ngày, giúp bạn lưu trữ, quản lý, tra cứu và sao chép 1-chạm các phím tắt, câu lệnh mẫu (AI prompts), thông tin cá nhân, mẫu văn bản hành chính...

Chương trình được thiết kế chạy trực tiếp trên mọi trình duyệt (máy tính và điện thoại) mà không cần cài đặt, không phụ thuộc internet và **không gửi bất kỳ dữ liệu nào ra máy chủ bên ngoài**.

---

## ✨ TÍNH NĂNG NỔI BẬT

### 🛡️ 1. Bảo mật chuẩn quân sự AES-256-GCM

- **Dẫn xuất khoá an toàn**: Sử dụng thuật toán PBKDF2 với **600.000 vòng lặp (iterations)** và băm SHA-256 chống lại mọi hình thức tấn công dò mật mã (Brute-force bằng GPU).

- **Mã hoá có xác thực**: AES-GCM 256-bit phát hiện ngay lập tức nếu nhập sai mật mã hoặc tập tin bị chỉnh sửa.

- **Nén Gzip tự động**: Dữ liệu được nén Gzip trước khi mã hoá, giúp tập tin cá nhân siêu nhẹ (chỉ khoảng 15 KB – 20 KB).

---

### 🔒 2. Tự động khoá & Bảo vệ bản nháp

- **Khoá nhanh khi mất Focus**: Tự động xoá sạch dữ liệu khỏi màn hình và bộ nhớ RAM khi chuyển cửa sổ, tắt màn hình hoặc chuyển ứng dụng.

- **Mã hoá bản nháp tức thì**: Nếu bạn đang gõ thêm dữ liệu giữa chừng mà bị khoá, nội dung gõ thêm sẽ được mã hoá AES-256 ngay trong phiên làm việc. Mở khoá ra là phục hồi nguyên vẹn 100%.

---

### 📦 3. Tự tạo & Xuất tập tin HTML mới (Self-Bundler)

- **Tập tin mẫu sạch 100%**: Bản mã nguồn tải lên GitHub không chứa dữ liệu cá nhân, mở lên dùng ngay không hỏi mật mã.

- **Tự đóng gói trong 1 giây**: Chỉ cần dán dữ liệu vào Tab 2 ➔ Đặt mật mã ➔ Bấm **`TẢI FILE HTML`** để nhận tập tin cá nhân đã mã hoá riêng cho bạn.

---

### 📱 4. Giao diện siêu tối ưu cho màn hình di động

- **Thiết kế 2 Tab riêng biệt**: Tab 1 dành cho tra cứu/sao chép tốc độ cao; Tab 2 dành cho chỉnh sửa và quản lý.

- **Cột phím tắt siêu gọn**: Tiêu đề mang biểu tượng phím `[A]`, chữ phím tắt xoay 90° ngược chiều kim đồng hồ giúp Cột 2 (nội dung) chiếm tới 90% diện tích hiển thị.

- **Sao chép 1-chạm (Click-to-Copy)**: Bấm phím tắt ở Cột 1 là nạp ngay nội dung Cột 2 vào Clipboard kèm hiệu ứng phản hồi thị giác đổi màu trực quan.

---

## 🚀 HƯỚNG DẪN SỬ DỤNG

### Bước 1: Mở tập tin mẫu

- Tải tập tin `go-tat.html` về máy và nhấp đúp để mở bằng bất kỳ trình duyệt nào (Chrome, Edge, Safari, Firefox,...).

- Tập tin mẫu ban đầu mở ra sẽ vào thẳng giao diện mà không yêu cầu mật mã.

---

### Bước 2: Nạp dữ liệu của bạn

- Chuyển sang **`Tab 2: SỬA DỮ LIỆU & TẠO FILE`**.

- Dán danh sách của bạn vào ô soạn thảo theo cấu trúc mẫu sau:

> `phím_tắt` **[Dấu Tab]** `Nội dung cần sao chép`

- *(Hỗ trợ kéo thả tập tin `.txt`/`.tsv` hoặc bấm nút chọn tập tin từ máy).*

---

### Bước 3: Đặt mật mã & Xuất tập tin cá nhân

- Nhập mật mã bảo vệ tại ô: **`Mật mã cho file HTML mới (Bắt buộc):`**

- Nhấp nút **`💾 TẢI FILE HTML`**.

- Trình duyệt sẽ tự động tải về tập tin `go-tat.html` mới đã được mã hoá AES-256.

---

### Bước 4: Sử dụng hàng ngày

- Mở tập tin vừa tải về ➔ Nhập mật mã của bạn để giải mã và tra cứu.

- Bấm vào phím tắt để sao chép nội dung vào Clipboard.

- Bấm nút **`🔒 KHOÁ LẠI`** ở góc trên bất cứ khi nào cần giấu dữ liệu tức thì.

---

## 🛠️ THÔNG SỐ KỸ THUẬT

| Hạng mục | Chi tiết kỹ thuật |
| :--- | :--- |
| **Kiến trúc** | Single-Page Application (SPA) - 1 tập tin HTML duy nhất |
| **Công nghệ** | Pure HTML5, CSS3 Variables, Vanilla JavaScript (Không thư viện ngoài) |
| **Mã hoá** | AES-GCM (256-bit Key, 12-byte IV, 16-byte Salt) |
| **Dẫn xuất khoá** | PBKDF2 (SHA-256, 600.000 Iterations) qua Web Crypto API |
| **Nén dữ liệu** | Gzip qua Streams Compression API |
| **Bảng màu** | Chuẩn 11 mã màu Dark Mode tối ưu độ tương phản |
| **Bảng mã** | UTF-8 chuẩn hoá dấu tiếng Việt mới |

---

## 👤 THÔNG TIN TÁC GIẢ

- **Tác giả:** Dương Tấn Chánh

- **Mã nguồn:** Thuần JavaScript nguyên bản, bảo mật phía máy khách (Client-side Only).

- **Giấy phép:** Miễn phí sử dụng và chia sẻ cho mục đích cá nhân và công việc.