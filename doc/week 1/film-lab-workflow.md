# Quy trình vận hành Film Lab trên nền tảng

> **Mục tiêu:** Nắm quy trình vận hành thực tế của Film Lab: quản lý dịch vụ, nhận đơn, xử lý phim, tải file scan, quản lý giá và lịch sử đơn.

## Mục lục

1. [Quản lý thông tin và dịch vụ](#1-quản-lý-thông-tin-và-dịch-vụ)
2. [Nhận, xác nhận và cập nhật đơn](#2-nhận-xác-nhận-và-cập-nhật-đơn)

---

## 1. Quản lý thông tin và dịch vụ

### 1.1 Thông tin Film Lab cần cung cấp

Lab duy trì một **hồ sơ lab (Lab Profile)** đầy đủ làm "mặt tiền" trên nền tảng, giúp khách tìm kiếm, so sánh và đặt dịch vụ.

| Nhóm thông tin | Nội dung |
|---|---|
| Định danh | Tên lab, địa chỉ các cơ sở, giờ mở cửa, số điện thoại, email, logo, mô tả ngắn |
| Loại film nhận xử lý | 35mm, 120, APS (240), 110, 4×5, 8×10 |
| Quy trình xử lý | C-41 (màu), BW (đen trắng), E-6 (slide), Cross E6→C41, Reversal, Cine/Vision (ECN-2) |
| Thời gian trả file dự kiến | Cam kết SLA cho từng loại film |
| Biểu phí công khai | Giá theo cuộn hoặc sheet, kèm phụ phí |
| Chính sách lưu trữ | Thời gian giữ file scan, thời gian giữ âm bản |
| Phương thức nhận/trả phim | Khách mang đến, gửi bưu điện hoặc pickup |

**Ví dụ thực tế (LLab):**
- Giờ làm việc: 08:00 – 21:00
- Film màu / BW / Vision: tối đa 72 giờ
- Film Slide E-6: tối đa 15 ngày
- Slide BW / reversal: trong vòng 30 ngày
- File scan lưu trên Google Drive 60 ngày, âm bản giữ 15 ngày

**Người thực hiện:** Chủ lab (Lab Owner). **Kết quả:** Lab Profile hoàn chỉnh, hiển thị công khai.

### 1.2 Phân quyền thêm/sửa dịch vụ

| Vai trò | Quyền hạn |
|---|---|
| Chủ lab (Lab Owner) | Toàn quyền: thêm, sửa, xóa, pause dịch vụ; đổi giá; cấu hình chính sách |
| Quản lý lab (Lab Manager) | Được chủ lab ủy quyền: sửa dịch vụ nhưng không xóa vĩnh viễn |
| Nhân viên vận hành (Lab Operator) | **Không** được sửa giá hoặc danh mục dịch vụ; chỉ cập nhật trạng thái đơn và nghiệp vụ hằng ngày |

**Lý do phân quyền chặt:**
- Giá và dịch vụ là cam kết công khai với khách, cần một đầu mối chịu trách nhiệm.
- Tránh nhân viên vô tình sửa giá gây sai lệch hàng loạt đơn.
- Mọi thay đổi giá/dịch vụ phải ghi log: ai sửa, lúc nào, nội dung gì, lý do gì.

**Kết quả:** Danh mục dịch vụ được cập nhật, có audit trail đầy đủ.

### 1.3 Thông tin của một dịch vụ (gói/package)

| Thuộc tính | Nội dung | Ví dụ từ LLab |
|---|---|---|
| Tên dịch vụ | Rõ ràng, dễ hiểu | "Tráng + Scan Standard - Film màu 135" |
| Loại / khổ film | Film được áp dụng | Film màu 135, 120, 110, APS |
| Quy trình | C-41 / BW / E-6 / Cross / ECN-2 | Film màu C41; Slide E-6 |
| Giá cơ bản | Theo cuộn hoặc sheet | Màu 135: 80.000đ/cuộn; màu 120: 85.000đ/cuộn; Slide 135/120: 260.000đ/cuộn |
| Phụ phí | Push/Pull, xử lý nhanh, scan nâng cao | Push/Pull màu +25.000đ/stop; BW +30.000đ/stop; xử lý nhanh +20.000đ/cuộn; Scan Hi-Res +25.000đ/cuộn |
| Định dạng đầu ra | JPEG / TIFF / BMP | TIFF +25.000đ/cuộn; BMP +25.000đ/cuộn |
| Thời gian xử lý (SLA) | Tối đa, tính từ lúc nhận film + thanh toán | 72 giờ (màu/BW/Vision); 15 ngày (Slide E-6) |
| Mô tả chi tiết | Quy trình và kết quả khách nhận | "Tráng bằng máy C41, scan Standard, trả file JPEG qua Google Drive" |

**Lưu ý về SLA:**
- Mốc 72 giờ / 15 ngày áp dụng khi lượng film bình thường hoặc mùa thấp điểm.
- Mùa cao điểm (lễ, Tết) có thể kéo dài; lab xác nhận lại timeline khi nhận film.
- Trường `SLA` là giá trị tham chiếu, không phải cam kết tuyệt đối.

**Kết quả:** Mỗi dịch vụ là một bản ghi hoàn chỉnh, sẵn sàng cho khách đặt.

### 1.4 Khi Film Lab tạm ngừng dịch vụ

**Cơ chế đúng: `PAUSED` (tạm ẩn), KHÔNG xóa.**

| Hạng mục | Hành vi |
|---|---|
| Hiển thị | Biến mất khỏi marketplace/danh sách công khai, khách không tìm thấy hoặc đặt mới được |
| Dữ liệu | Giữ nguyên toàn bộ cài đặt, đánh giá và lịch sử đơn cũ |
| Đơn đã đặt | Vẫn xử lý bình thường (giá và điều khoản lúc đặt là ràng buộc) |
| Ghi log | Ai pause, lúc nào, lý do gì |
| Thông báo | Nếu khách đang xem dịch vụ, hiển thị "tạm ngừng nhận đơn mới" |

**Tình huống thực tế:** LLab quy định film Slide cần đủ số cuộn mới tráng một lần. Lab có thể tạm ngừng nhận đơn slide mới nhưng không được hủy các đơn slide đã gửi trước đó, vì vậy cần `PAUSED` thay vì `DELETE`.

**Trường hợp bất thường:**
- Lab pause dịch vụ nhưng có đơn đang `PENDING_PAYMENT` → vẫn xử lý bình thường sau khi thanh toán.
- Muốn xóa vĩnh viễn dịch vụ → chỉ được khi không còn đơn nào tham chiếu đến dịch vụ đó.

---

## 2. Nhận, xác nhận và cập nhật đơn

### 2.1 Cách Lab nhận thông báo đơn mới

**Nguồn 1: Đơn từ nền tảng / storefront**
- Đơn vào **hàng đợi sản xuất (production queue)** gần như tức thời (vài giây sau khi khách đặt).
- Hiển thị trên **bảng Kanban sản xuất**, phân loại theo quy trình (film processing, printing, v.v.).
- Thông báo nội bộ: chuông âm thanh, badge số đơn mới chưa xử lý, email nội bộ cho nhân viên trực ca.

**Nguồn 2: Đơn gửi bưu điện / từ xa**
- Khi bưu kiện đến, nhân viên mở và **quét đơn vào hệ thống**.
- Hệ thống **tự động gửi email xác nhận đã nhận film** cho khách.
- Khách từ xa lần đầu (theo LLab) cần đính kèm giấy ghi số điện thoại, tên, email để lab tạo đơn và gửi biên nhận điện tử.

**Kết quả:** Đơn xuất hiện trong hàng đợi của lab; khách đơn từ xa nhận xác nhận điện tử.

### 2.2 Ai xác nhận đơn?

**Nhân viên vận hành (Lab Operator)** xác nhận qua **hai bước độc lập**:

| Bước | Nội dung | Điều kiện |
|---|---|---|
| 1. Xác nhận tiếp nhận thông tin | Đơn đã vào hệ thống, thông tin khách và dịch vụ đúng | Ngay khi đơn xuất hiện trong hàng đợi |
| 2. Xác nhận nhận film thực tế + thanh toán | Đã cầm film trên tay và tiền đã vào | Khi film đến lab và thanh toán hoàn tất |

- Bước 2 là điều kiện để đơn chuyển sang `PROCESSING`. LLab quy định với khách gửi bưu điện: đơn chỉ được xử lý và chia sẻ sau khi thanh toán.
- Hệ thống ghi lại: `confirmed_by`, `confirmed_at`, `payment_confirmed_at` (nếu khác thời điểm xác nhận).

### 2.3 Thông tin cần ghi nhận khi nhận film thực tế

| Trường thông tin | Mục đích | Bắt buộc |
|---|---|---|
| Mã đơn / order ID | Đối chiếu với đơn đã đặt | ✅ |
| Tình trạng film | Còn nguyên cuộn / đã cắt / ẩm ướt / ghi chú đặc biệt | ✅ |
| Ghi chú đặc biệt từ khách | Push/pull, giữ âm bản, tráng nhanh | ✅ (nếu có) |
| Số lượng thực tế | So với số khai báo; lệch thì ghi nhận và báo khách | ✅ |
| Người giao film | Khách trực tiếp hay đối tác vận chuyển | ✅ |
| Thời điểm nhận | Tính SLA xử lý | ✅ |
| Trạng thái thanh toán | Đã thanh toán hay chưa | ✅ |
| Ảnh chụp tình trạng film | Bằng chứng nếu có tranh chấp | Khuyến khích |

**Trường hợp bất thường khi nhận film:**

| Tình huống | Cách xử lý |
|---|---|
| Số lượng lệch so với khai báo | Ghi nhận, báo khách qua app/email, chờ xác nhận trước khi xử lý |
| Film hư hỏng / ẩm ướt | Chụp ảnh, ghi chú, báo khách, thỏa thuận trước khi tráng |
| Film tự chiết không an toàn | Từ chối nhận, ghi lý do, báo khách |
| Khách chưa thanh toán | Giữ ở `PENDING_PAYMENT`, không chuyển sang xử lý |

### 2.4 Các trạng thái đơn

| Trạng thái | Ý nghĩa | Điều kiện chuyển | Người chuyển |
|---|---|---|---|
| `PENDING_PAYMENT` | Đơn đã tạo, chờ thanh toán | Khách đặt đơn từ xa/online | Hệ thống |
| `RECEIVED_AT_LAB` | Lab đã nhận film thực tế | Nhân viên quét mã / xác nhận | Lab Operator |
| `PROCESSING` | Đang tráng / scan | Đã thanh toán + film đã nhận | Lab Operator |
| `DEVELOPING` (tùy chọn) | Đang tráng | Bắt đầu công đoạn tráng | Lab Operator |
| `SCANNING` (tùy chọn) | Đang scan | Bắt đầu công đoạn scan | Lab Operator |
| `SCANS_UPLOADED` | File scan đã upload và gắn đúng đơn | Upload thành công + đã associate order | Lab Operator |
| `READY_FOR_PICKUP` | Film gốc / bản in sẵn sàng trả tại lab | Hoàn tất QC | Lab Operator |
| `READY_FOR_DELIVERY` | Sẵn sàng giao cho shipper | Hoàn tất QC | Lab Operator |
| `DELIVERED` | Đã giao cho khách / shipper | Có xác nhận giao | Lab Operator / Delivery Partner |
| `CLOSED` | Đơn kết thúc, mở đánh giá | Tất cả dịch vụ (kể cả in ấn) hoàn tất | Hệ thống |