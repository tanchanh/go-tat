# GÕ TẮT (TEXT EXPANSION & SECURE VAULT)

**Tác giả:** Dương Tấn Chánh  
**Chuẩn mã hoá:** AES-256-GCM & PBKDF2 (Chuẩn định dạng `DTC_ENC_01`)  
**Kiến trúc:** Ứng dụng Web Single-Page (Độc lập, Offline 100%, Không qua máy chủ)

---

## 1. GIỚI THIỆU TỔNG QUAN

**GÕ TẮT** là phần mềm quản lý, tra cứu và sao chép nhanh danh sách phím tắt văn bản cá nhân hoá, được thiết kế tối ưu cho hiệu suất làm việc văn phòng và bảo mật dữ liệu tuyệt đối. 

Ứng dụng sở hữu cơ chế **Tự nhân bản độc lập (Standalone Self-Cloning)**: Cho phép người dùng trực tiếp soạn thảo dữ liệu, đặt mật mã và xuất ra một tập tin `index.html` mới đã được mã hoá toàn diện. Tập tin mới này chứa trọn vẹn cả dữ liệu bản mã lẫn giao diện phần mềm, có khả năng tự giải mã cục bộ mà không cần cài đặt thêm bất kỳ phần mềm hay tiện ích mở rộng nào.

---

## 2. QUY ƯỚC ĐỊNH DẠNG DỮ LIỆU GÕ TẮT

Trong khung soạn thảo (Tab **SỬA DỮ LIỆU & TẠO FILE**), mỗi dòng văn bản tương ứng với một mục phím tắt. Ứng dụng hỗ trợ linh hoạt 3 loại ký tự phân cách giữa **Phím tắt** và **Nội dung sao chép**:

| Ký tự phân cách | Cú pháp ví dụ | Kết quả nhận diện |
| :--- | :--- | :--- |
| **Dấu chấm phẩy (`;`)** | `dc; 123 Đường Lê Lợi, Quận 1` | Phím tắt: `dc`<br>Nội dung: `123 Đường Lê Lợi, Quận 1` |
| **Ký tự Tab (`\t`)** | `mail[TAB]contact@example.com` | Phím tắt: `mail`<br>Nội dung: `contact@example.com` |
| **Khoảng trắng (` `)** | `chuc Chúc bạn một ngày làm việc hiệu quả!` | Phím tắt: `chuc`<br>Nội dung: `Chúc bạn một ngày làm việc...` |

### Quy tắc định dạng nâng cao:
* **Xuống dòng trong nội dung sao chép:** Sử dụng ký hiệu `\n` để ngắt dòng trong nội dung.  
  *Ví dụ:* `ck; STK: 123456789\nNgân hàng: VCB\nChủ TK: DUONG TAN CHANH`  
  *Kết quả khi dán ra sẽ thành 3 dòng riêng biệt.*
* **Bảo toàn đường dẫn thư mục:** Ký hiệu `\\n` (hai dấu gạch chéo ngược) sẽ được bảo toàn nguyên bản dạng chuỗi, không bị biến thành dấu xuống dòng (thích hợp lưu đường dẫn Windows như `D:\notes\new_project`).
* **Bỏ qua dòng chú thích:** Các dòng bắt đầu bằng ký tự thăng (`#`) hoặc các dòng trống sẽ tự động được bỏ qua.

---

## 3. HƯỚNG DẪN CÁC CHỨC NĂNG CHÍNH

### 3.1. Bảng Tra Cứu & Sao Chép Nhanh (Tab 1: BẢNG GÕ TẮT)
* **Tra cứu tức thì:** Gõ từ khoá vào ô tìm kiếm ở đầu trang để lọc đồng thời cả phím tắt lẫn nội dung. Bộ tìm kiếm tự động chuẩn hoá Unicode `NFC`, hỗ trợ tìm chính xác tiếng Việt có dấu.
* **Xoá nhanh tìm kiếm:** Nhấn phím `Esc` khi đang ở ô tìm kiếm để xoá trắng từ khoá và hiển thị lại toàn bộ danh sách.
* **Sao chép nội dung:** Nhấp chuột hoặc chạm vào nút phím tắt (cột bên trái có chữ xoay dọc):
  - Nội dung tương ứng sẽ lập tức được chép vào bộ nhớ tạm (Clipboard).
  - Nút phím tắt chuyển sang màu xanh lá dịu xác nhận (`btn-copied`) và dòng tương ứng được đánh dấu viền sáng trong 1,5 giây.
  - Một thanh thông báo tĩnh xuất hiện ở đáy màn hình xác nhận sao chép thành công.
* **Tắt nhanh thông báo:** Nhấp vào nút `✕` trên thanh thông báo để tắt ngay lập tức.

---

### 3.2. Soạn Thảo & Nạp Dữ Liệu (Tab 2: SỬA DỮ LIỆU & TẠO FILE)
* **Phương thức nạp dữ liệu đa dạng:**
  1. *Bấm nút chọn file:* Nhấn **"📁 CHỌN TẬP TIN TỪ MÁY"** để nạp các file văn bản (`.txt`, `.tsv`, `.csv`).
  2. *Kéo thả:* Kéo tập tin văn bản từ máy tính thả trực tiếp vào vùng nét đứt `dropzoneArea`.
  3. *Dán trực tiếp:* Nhấn `Ctrl + V` tập tin từ bộ nhớ hệ điều hành, hoặc bấm nút **"DÁN"** trên thanh công cụ để chèn nội dung văn bản thông minh vào vị trí con trỏ chuột.
* **Nút TAB nổi công thái học:** Trên màn hình cảm ứng hoặc điện thoại di động không có phím Tab vật lý, bấm nút **"TAB"** nổi ở góc dưới khung soạn thảo để chèn nhanh ký tự phân cách Tab chuẩn.
* **Khôi phục dữ liệu gốc:** Nút **"🔄 KHÔI PHỤC DỮ LIỆU GỐC"** cho phép huỷ toàn bộ các chỉnh sửa nháp đang có trong khung soạn thảo để quay về danh sách dữ liệu gốc ban đầu của file.

---

### 3.3. Đo Độ Mạnh Mật Mã & Tạo File Mới Độc Lập
* **Thước đo mật mã thông minh:** Khi nhập mật mã mới vào ô bảo vệ, hệ thống tự động kích hoạt bộ phân tích an ninh:
  - Kiểm tra độ dài, chữ hoa, chữ thường, chữ số và ký hiệu đặc biệt.
  - Tự động phát hiện và hạ điểm cảnh báo nếu mật mã chứa từ điển phổ biến (`password`, `matkhau`, `admin`...), chuỗi số liên tiếp (`123456`, `7890`) hoặc biến thể thay thế ký tự Leetspeak (`@` thay `a`, `0` thay `o`).
* **Tiện ích sao chép mật mã:** Bấm nút **"Chép mật mã"** ngay cạnh ô nhập liệu để lưu trữ mật khẩu an toàn vào trình quản lý mật khẩu cá nhân trước khi xuất file.
* **Xuất tập tin TSV:** Bấm **"TẢI FILE TSV"** để lưu danh sách phím tắt dưới dạng file bảng tính `go-tat.tsv` (được gắn kèm tiền tố UTF-8 BOM để mở tiếng Việt không bị lỗi font trên Microsoft Excel).
* **Xuất tập tin HTML mã hoá mới:**
  1. Nhập mật mã bảo vệ vào ô *"Mật mã cho file HTML mới"*.
  2. Bấm **"TẢI FILE HTML"** (hoặc nhấn phím `Enter` tại ô mật mã, hoặc nhấn tổ hợp phím `Ctrl + S`).
  3. Trình duyệt sẽ tải về một tập tin hoàn chỉnh mang tên **`index.html`**. Tập tin này đã được mã hoá AES-256 an toàn và sẵn sàng lưu trữ, chuyển giao hoặc sử dụng độc lập.

---

### 3.4. Cơ Chế Khoá & Mở Khoá An Toàn
Trạng thái an ninh của phần mềm được thể hiện trực quan qua nút bấm góc trên bên phải thanh tiêu đề:

* **Trạng thái `FILE MẪU SẠCH` (Màu xanh lá):**  
  Hiển thị khi mở một file mẫu chưa cài đặt mật mã. Mọi tính năng soạn thảo và tra cứu đều mở sẵn sàng để nạp dữ liệu.
* **Trạng thái `KHOÁ LẠI` (Màu cam):**  
  Hiển thị khi file đã được mở khoá thành công. Nhấn nút này bất kỳ lúc nào để giấu toàn bộ dữ liệu, xoá trắng bảng tra cứu và khoá ứng dụng ngay lập tức.
* **Trạng thái `MỞ KHOÁ` (Màu xanh dương):**  
  Hiển thị khi ứng dụng đang ở chế độ khoá bảo vệ. Nhấn nút này để hiển thị hộp thoại mở khoá:
  - Nhập mật mã bảo vệ.
  - Bấm chuột vào nút **"🔓 MỞ KHOÁ"** hoặc nhấn phím **`Enter`** trên bàn phím.
  - Dữ liệu được xác thực và giải mã bung ra bảng chỉ trong khoảng **0.15 giây**.

---

## 4. BẢO MẬT & KIẾN TRÚC KỸ THUẬT

1. **Chuẩn Mật Mã Học AES-256-GCM:**  
   Toàn bộ dữ liệu phím tắt được đóng gói theo định dạng nhị phân độc quyền `DTC_ENC_01`:
   `````text
   [DTC_ENC_01 (10 Bytes)] + [Salt (16 Bytes)] + [IV (12 Bytes)] + [Ciphertext + Auth Tag (16 Bytes)]