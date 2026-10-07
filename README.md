# ⏱️ Video Time Study Tool (IE & Lean Motion Analysis)

> **Công cụ đo lường và phân tích thời gian thao tác chu kỳ qua video trên trình duyệt Web dành cho Kỹ sư Kỹ thuật Công nghiệp (IE / Lean Engineering).**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Platform: Web Browser](https://img.shields.io/badge/Platform-Web%20Browser%20(Chrome%20%2F%20Edge)-success.svg)]()
[![Zero Installation](https://img.shields.io/badge/Installation-Zero%20Install%20(Portable)-orange.svg)]()
[![Security](https://img.shields.io/badge/Security-Zero%20Data%20Leak%20(Local%20Only)-brightgreen.svg)]()

---

## 📌 1. Giới thiệu dự án (Overview)

Trong sản xuất công nghiệp, việc nghiên cứu thời gian và động tác (**Time & Motion Study** / **Cycle Time Analysis**) của công nhân trên chuyền lắp ráp là nhiệm vụ cốt lõi của bộ phận IE (Industrial Engineering) và Cải tiến liên tục (Lean / Kaizen).

Trước đây, kỹ sư thường phải xem video, bấm đồng hồ thủ công, ghi chép ra sổ tay hoặc tự gõ vào bảng tính Excel, sau đó tính toán thủ công từng bước. Quá trình này tốn nhiều thời gian và dễ sai sót.

**Video Time Study Tool** được thiết kế như một ứng dụng web gọn nhẹ, chạy trực tiếp trên trình duyệt, cho phép kỹ sư:
1. Mở video độ phân giải cao và kích thước lớn (1GB – 5GB) tức thì.
2. Bấm ghi nhận mốc thời gian (**Measuring point**) chính xác bằng phím tắt bàn phím.
3. Tự động tính toán thời gian chu kỳ và quy đổi sang đơn vị tiêu chuẩn **HM (Hundredths of a Minute)**.
4. Tự động điền dữ liệu theo form mẫu chuẩn 4 hàng của doanh nghiệp.
5. Xuất báo cáo Excel (`.xls`) giữ nguyên 100% định dạng, màu sắc và cấu trúc gộp ô (merged cells).

---

## 🚀 2. Điểm nổi bật & Tính năng chính (Key Features)

### 2.1. Tuân thủ chính sách IT & Bảo mật dữ liệu tuyệt đối (IT Compliance & Zero Data Leak)
- **Không cần cài đặt (No `.exe`):** Hoạt động hoàn toàn trên trình duyệt Web hiện đại (Chrome, Edge). Vượt qua mọi rào cản hạn chế quyền Admin của bộ phận IT công ty.
- **Bảo mật nội bộ 100%:** Sử dụng HTML5 File API (`URL.createObjectURL`), video được phát trực tiếp từ bộ nhớ RAM máy cục bộ. Không tải bất kỳ hình ảnh hay video nào lên server bên ngoài, đảm bảo bí mật quy trình sản xuất.
- **Mở video tức thì:** Không độ trễ tải video, không tốn băng thông mạng nội bộ.

### 2.2. Trình phát Video chuyên dụng cho IE (Industrial Video Player)
- **Hiển thị lớp phủ thông tin (HUD):** Hiển thị trực tiếp Tên bước thao tác (**Process sequence**), Mốc dừng (**Measuring point**), Số bước và Chu kỳ hiện tại ngay trên khung hình video.
- **Điều khiển chính xác:** Tua lùi/tiến 1 giây, thanh kéo tiến trình (Scrubber) mượt mà.
- **Hệ thống phím tắt tối ưu tốc độ bấm giờ:**
  - `Enter`: Bắt đầu chu kỳ / Ghi mốc kết thúc bước thao tác.
  - `Space`: Tạm dừng / Tiếp tục phát video.
  - `←` / `→`: Tua lùi / tiến 1 giây.
  - `↑` / `↓`: Chuyển đổi qua lại giữa các bước thao tác.
  - `Ctrl + Z`: Hoàn tác (Undo) mốc vừa bấm nếu bấm nhầm.

### 2.3. Quy trình đo liên tục & Tự động tính toán (Continuous Timing & Auto Calculation)
- **Phương pháp đo liên tục (Continuous Timing Method):**
  - Mốc bắt đầu bước $i$: $Start_i = F_{i-1}$
  - Mốc kết thúc bước $i$: $F_i$ (giây video thực tế)
  - Thời gian thao tác theo giây: $t_i = F_i - Start_i$
- **Tự động quy đổi sang HM (Hundredths of a Minute / Centiminute):**
  $$ti(hm) = \text{round}\left(\frac{\text{Thời gian đo được (giây)}}{60} \times 100\right)$$
  - Tự động làm tròn thành số nguyên theo chuẩn IE (Ví dụ: `65.9s` $\rightarrow$ `110 hm`, `5.0s` $\rightarrow$ `8 hm`).
- **Tự động tạm dừng để Review:** Ngay sau khi bấm mốc dừng của một bước, video tự động dừng lại và đưa con trỏ chuột vào ô nhận xét để kỹ sư kịp ghi chú đánh giá thao tác của công nhân.

### 2.4. Bảng tính chuẩn Form mẫu công ty & Đồng bộ 2 chiều (Bidirectional Sync)
- **Cấu trúc 4 hàng chuẩn cho mỗi bước:**
  - Hàng 1: `No.`, `Process sequence`, `Ref. Quantity`, `Measured values`, `Nhận xét`
  - Hàng 2: `L` (Rating Factor - Hệ số đánh giá tốc độ làm việc)
  - Hàng 3: `ti(hm)` (Thời gian thao tác tính theo HM)
  - Hàng 4: `Measuring point` (Mốc dừng), `F` (Mốc thời gian tích lũy trên video)
- **Thẻ Sidebar điều khiển:** Cho phép xem và chỉnh sửa nhanh bước hiện tại. Có cơ chế khóa số 🔒 chống gõ nhầm; có sẵn danh sách gợi ý nhận xét mẫu và hệ số $L$.
- **Đồng bộ 2 chiều:** Bất kỳ thay đổi nào trên Sidebar đều cập nhật tức thì xuống Bảng tính và ngược lại.

### 2.5. Tùy biến giao diện linh hoạt & Lưu trữ an toàn
- **Thanh kéo phân chia tỷ lệ (Resizers):**
  - Kéo dọc giữa Video và Sidebar để cân chỉnh góc nhìn.
  - Kéo ngang giữa Khung video và Bảng tính phía dưới.
  - Kéo cột chu kỳ để thay đổi số lượng chu kỳ hiển thị (5, 8, 10, 15 chu kỳ...).
- **Tự động lưu trạng thái (Auto-save):** Lưu tức thì mọi thay đổi vào `LocalStorage` của trình duyệt. Tắt tab mở lại không bị mất dữ liệu.
- **Sao lưu & Chuyển máy (JSON Backup):** Hỗ trợ nút **💾 Lưu dự án** (tải file `.json`) và **📂 Mở dự án** để chuyển giao dữ liệu giữa các máy tính.

### 2.6. Xuất báo cáo Excel chuẩn Form mẫu
- Bấm nút **"📥 Xuất Excel (.xls)"** để tải về file Excel chuẩn.
- File xuất ra giữ nguyên màu sắc (ô vàng, tiêu đề xanh), kẻ viền ô, căn lề và các ô gộp dòng `rowspan`.
- Cột `Cy / mt` hiển thị dòng `ti(hm)` với định dạng số chuẩn `Number`.

---

## 🛠️ 3. Cấu trúc thư mục (Project Structure)

```text
Tool_Video/
│
├── TimeStudy_Tool.html     # Mã nguồn ứng dụng hoàn chỉnh (Single Page Web Application)
├── PROJECT_SPEC.md         # Tài liệu đặc tả kỹ thuật dự án
├── README.md               # Tài liệu hướng dẫn và giới thiệu dự án (Tài liệu này)
└── video-audit-tool/       # Module / công cụ kiểm tra video mở rộng
```

---

## 📖 4. Hướng dẫn sử dụng (How to Use)

### Bước 1: Mở ứng dụng
- Không cần cài đặt `Node.js` hay server backend.
- Chỉ cần nhấp đúp vào file `TimeStudy_Tool.html` để mở trực tiếp bằng Google Chrome hoặc Microsoft Edge.

### Bước 2: Nạp video & Thiết lập công đoạn
1. Bấm **"📁 Nạp Video"** hoặc kéo thả file video (`.mp4`, `.webm`, `.mov`) vào khung phát video.
2. Kiểm tra danh sách các bước thao tác trên bảng dưới. Bạn có thể bấm trực tiếp vào ô để sửa tên bước (**Process**), mốc dừng (**Measuring point**), hoặc bấm **"➕ Thêm hàng"** / **"🗑️"** để xóa.

### Bước 3: Tiến hành bấm giờ
1. Bấm `Enter` (hoặc nút xanh) để bắt đầu chu kỳ đo.
2. Quan sát video. Khi thấy công nhân chạm đúng điểm kết thúc (**Measuring point**) của bước đó:
   - Bấm `Enter` để ghi mốc kết thúc ($F$) và tự động tính $t_i(hm)$.
   - Video sẽ tự động tạm dừng để bạn nhập **Nhận xét** hoặc điều chỉnh hệ số **L**.
3. Bấm `Enter` lần tiếp theo để tiếp tục phát video và đo bước kế tiếp.
4. Sau khi kết thúc bước cuối cùng của chu kỳ, hệ thống sẽ tự động chuyển sang chu kỳ tiếp theo.

### Bước 4: Xuất báo cáo & Lưu dự án
- Bấm **"📥 Xuất Excel (.xls)"** để tải báo cáo về máy.
- Bấm **"💾 Lưu dự án"** để lưu file `.json` làm bản sao lưu dự phòng.

---

## ⚙️ 5. Công nghệ sử dụng (Tech Stack)

| Thành phần | Công nghệ | Ưu điểm |
| :--- | :--- | :--- |
| **Kiến trúc** | Client-Side Single Page Application (SPA) | Hoạt động độc lập, không phụ thuộc mạng, không cần backend |
| **Giao diện & Logic** | HTML5, Modern CSS3 (Grid/Flexbox), Vanilla JS (ES6+) | Gọn nhẹ, phản hồi tức thì, không phát sinh lỗi dependency |
| **Xử lý Video** | HTML5 Video API + File Object URL | Phát video mượt mà, định vị mốc thời gian chính xác |
| **Lưu trữ** | Web Storage API (LocalStorage) + JSON File API | Tự động lưu tiến độ, phòng tránh mất dữ liệu khi mất điện |
| **Xuất Excel** | XML Spreadsheet 2003 (`.xls`) Engine | Tạo bảng tính Excel với màu sắc, borders và merge cell không cần thư viện nặng |

---

## 📄 6. Bản quyền & Đóng góp (License & Contribution)

- Dự án được phát triển phục vụ mục đích nội bộ và tối ưu hóa hoạt động kỹ thuật công nghiệp (IE / Lean Manufacturing).
- Giấy phép phân phối: [MIT License](https://opensource.org/licenses/MIT). Mọi ý kiến đóng góp và cải tiến đều được hoan nghênh.
