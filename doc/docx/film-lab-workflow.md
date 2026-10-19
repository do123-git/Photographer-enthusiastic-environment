# NGƯỜI 2 — FILM LAB
## Quy trình vận hành Film Lab trên nền tảng

> **Mục tiêu:** Hiểu rõ quy trình vận hành thực tế của một Film Lab khi tham gia nền tảng — từ quản lý dịch vụ, nhận đơn, xử lý phim, tải file scan, đến quản lý giá và lịch sử đơn hàng.
>
> **Cách đọc tài liệu:** Với mỗi nhóm nội dung, tài liệu ghi rõ: **ai thực hiện, thông tin cần nhập, kết quả đầu ra, và các trường hợp bất thường**.

---

## Mục lục

1. [Quản lý thông tin và dịch vụ](#1-quản-lý-thông-tin-và-dịch-vụ)
2. [Nhận, xác nhận và cập nhật đơn](#2-nhận-xác-nhận-và-cập-nhật-đơn)
3. [Tải file scan và trả kết quả](#3-tải-file-scan-và-trả-kết-quả)
4. [Quản lý giá và lịch sử đơn hàng](#4-quản-lý-giá-và-lịch-sử-đơn-hàng)
5. [Tóm tắt các trường hợp bất thường](#5-tóm-tắt-các-trường-hợp-bất-thường)

---

## 1. Quản lý thông tin và dịch vụ

### 1.1. Film Lab cần cung cấp thông tin gì?

Film Lab cần duy trì một **hồ sơ lab (Lab Profile)** đầy đủ, đóng vai trò "mặt tiền" của lab trên nền tảng. Đây là cơ sở để khách hàng tìm kiếm, so sánh và ra quyết định đặt dịch vụ.

**Thông tin bắt buộc phải có:**

| Nhóm thông tin | Nội dung cụ thể |
|---|---|
| **Thông tin định danh** | Tên lab, địa chỉ các cơ sở, giờ mở cửa, số điện thoại, email liên hệ, logo và mô tả ngắn |
| **Loại film nhận xử lý** | 35mm, 120, APS (240), 110, 4×5, 8×10 |
| **Quy trình xử lý** | C-41 (màu), BW (đen trắng), E-6 (slide), Cross E6→C41, Reversal, Cine/Vision (ECN-2) |
| **Thời gian trả file dự kiến** | Cam kết SLA cho từng loại film |
| **Biểu phí công khai** | Giá theo cuộn hoặc theo sheet, kèm phụ phí |
| **Chính sách lưu trữ** | Thời gian giữ file scan, thời gian giữ âm bản |
| **Phương thức nhận/trả phim** | Khách mang đến trực tiếp, gửi bưu điện, hay có pickup |

**Ví dụ thực tế từ LLab:**
- Giờ làm việc: **08:00 – 21:00**
- Film màu / BW / Vision: tối đa **72 giờ**
- Film Slide E-6: tối đa **15 ngày**
- Slide BW / reversal: trong vòng **30 ngày**
- File scan lưu trên Google Drive **60 ngày**, âm bản giữ **15 ngày**

**Người thực hiện:** Chủ lab (Lab Owner) khai báo và cập nhật hồ sơ.

**Kết quả đầu ra:** Lab Profile hoàn chỉnh, hiển thị công khai trên nền tảng.

---

### 1.2. Ai được phép thêm hoặc sửa dịch vụ?

**Phân quyền rõ ràng:**

| Vai trò | Quyền hạn |
|---|---|
| **Chủ lab (Lab Owner)** | Toàn quyền: thêm, sửa, xóa, pause dịch vụ; thay đổi giá; cấu hình chính sách |
| **Quản lý lab (Lab Manager)** | Được ủy quyền bởi chủ lab: có thể sửa dịch vụ nhưng không được xóa vĩnh viễn |
| **Nhân viên vận hành (Lab Operator)** | **Không được** sửa giá hoặc danh mục dịch vụ. Chỉ được cập nhật trạng thái đơn và xử lý nghiệp vụ hàng ngày |

**Lý do phân quyền chặt:**
- Giá và danh mục dịch vụ là **cam kết công khai với khách hàng** — cần một đầu mối chịu trách nhiệm duy nhất.
- Tránh tình trạng nhân viên vô tình sửa giá gây sai lệch hàng loạt đơn hàng.
- Mọi thay đổi giá/dịch vụ phải được **ghi log**: ai sửa, lúc nào, nội dung gì, lý do gì.

**Kết quả đầu ra:** Danh mục dịch vụ được cập nhật, có audit trail đầy đủ.

---

### 1.3. Một dịch vụ cần có giá, mô tả và thời gian xử lý nào?

Mỗi dịch vụ nên được mô hình hóa thành một **gói (package)** với các trường tối thiểu sau:

| Thuộc tính | Nội dung | Ví dụ từ LLab |
|---|---|---|
| **Tên dịch vụ** | Rõ ràng, dễ hiểu | "Tráng + Scan Standard - Film màu 135" |
| **Loại film / khổ film** | Xác định chính xác film nào được áp dụng | Film màu 135, 120, 110, APS |
| **Quy trình** | C-41 / BW / E-6 / Cross / ECN-2 | Film màu C41; Film Slide E-6 |
| **Giá cơ bản** | Giá theo cuộn hoặc sheet | Film màu 135: **80.000đ/cuộn**<br>Film màu 120: **85.000đ/cuộn**<br>Slide 135/120: **260.000đ/cuộn** |
| **Phụ phí (nếu có)** | Push/Pull, xử lý nhanh, scan nâng cao | Push/Pull màu: **+25.000đ/stop**<br>BW: **+30.000đ/stop**<br>Xử lý nhanh: **+20.000đ/cuộn**<br>Scan Hi-Res: **+25.000đ/cuộn** |
| **Định dạng đầu ra** | JPEG / TIFF / BMP | TIFF: +25.000đ/cuộn<br>BMP: +25.000đ/cuộn |
| **Thời gian xử lý (SLA)** | Thời gian tối đa tính từ lúc nhận film + thanh toán | 72 giờ (màu/BW/Vision)<br>15 ngày (Slide E-6) |
| **Mô tả chi tiết** | Giải thích quy trình, kết quả khách nhận được | "Film được tráng bằng máy C41, scan ở độ phân giải Standard, trả file JPEG qua Google Drive" |

**Lưu ý về SLA:**
- Các mốc 72 giờ / 15 ngày áp dụng trong **mùa thấp điểm hoặc lượng film bình thường**.
- Mùa cao điểm (lễ, Tết) thời gian có thể kéo dài — lab sẽ **xác nhận lại timeline khi nhận film**.
- Trường `SLA` nên là **giá trị tham chiếu**, không phải cam kết tuyệt đối trong mọi điều kiện.

**Kết quả đầu ra:** Mỗi dịch vụ là một bản ghi hoàn chỉnh, sẵn sàng hiển thị cho khách đặt.

---

### 1.4. Nếu Film Lab tạm ngừng dịch vụ thì sao?

**Cơ chế đúng: `PAUSED` (tạm ẩn), KHÔNG XÓA.**

| Hành vi | Chi tiết |
|---|---|
| **Hiển thị** | Dịch vụ **biến mất khỏi marketplace / danh sách công khai** — khách không thể tìm thấy hoặc đặt mới |
| **Dữ liệu** | **Toàn bộ cài đặt, đánh giá và lịch sử đơn hàng cũ vẫn được giữ nguyên** |
| **Đơn đã đặt** | **Các đơn đã đặt trước đó vẫn được xử lý bình thường** — vì giá và điều khoản tại thời điểm đặt là ràng buộc |
| **Ghi log** | Ghi lại: ai pause, lúc nào, lý do gì |
| **Thông báo** | Nếu khách đang xem dịch vụ đó, hiển thị rõ trạng thái "tạm ngừng nhận đơn mới" |

**Tình huống thực tế:** LLab có quy định film Slide cần đủ số cuộn mới tráng một lần. Lab có thể **tạm ngừng nhận đơn mới** cho dịch vụ slide, nhưng **không được hủy** các đơn slide khách đã gửi trước đó. Đây chính là lý do cần cơ chế `PAUSED` thay vì `DELETE`.

**Trường hợp bất thường:**
- Lab pause dịch vụ nhưng có đơn đang ở trạng thái `PENDING_PAYMENT` → đơn đó vẫn được xử lý bình thường sau khi thanh toán.
- Lab muốn xóa vĩnh viễn dịch vụ → chỉ được phép khi **không còn đơn nào đang tham chiếu** đến dịch vụ đó.

---

## 2. Nhận, xác nhận và cập nhật đơn

### 2.1. Film Lab nhận được thông báo đơn mới như thế nào?

Có **hai nguồn đơn** với cách thông báo khác nhau:

#### Nguồn 1: Đơn từ nền tảng / storefront

- Đơn được đẩy vào **hàng đợi sản xuất (production queue)** gần như tức thời — vài giây sau khi khách đặt.
- Hệ thống hiển thị đơn trên **bảng Kanban sản xuất**, phân loại theo quy trình (film processing, printing, v.v.).
- Lab nhận thông báo nội bộ qua: **âm thanh** (chuông thông báo), **badge** (số đơn mới chưa xử lý), **email nội bộ** cho nhân viên trực ca.

#### Nguồn 2: Đơn gửi bưu điện / từ xa

- Khi bưu kiện đến lab, nhân viên **mở và quét đơn vào hệ thống**.
- Hệ thống **tự động gửi email xác nhận đã nhận film** cho khách.
- Với khách từ xa lần đầu, LLab yêu cầu **đính kèm giấy ghi số điện thoại, tên, email** để lab tạo đơn và gửi biên nhận điện tử.

**Kết quả đầu ra:** Đơn xuất hiện trong hàng đợi của lab, khách nhận được xác nhận điện tử (nếu là đơn từ xa).

---

### 2.2. Ai xác nhận đơn?

**Nhân viên vận hành (Lab Operator)** là người xác nhận, nhưng cần phân biệt **hai bước xác nhận độc lập**:

| Bước | Nội dung | Điều kiện |
|---|---|---|
| **Bước 1: Xác nhận tiếp nhận thông tin** | Xác nhận đơn đã vào hệ thống, thông tin khách hàng và dịch vụ đã đúng | Ngay khi đơn xuất hiện trong hàng đợi |
| **Bước 2: Xác nhận nhận film thực tế + thanh toán** | Xác nhận đã cầm film trên tay và tiền đã vào | Khi film đến lab và thanh toán hoàn tất |

**Điều kiện bắt buộc:** Bước 2 là điều kiện để đơn chuyển sang trạng thái `PROCESSING`. LLab quy định rõ với khách gửi bưu điện: **đơn chỉ được xử lý và chia sẻ sau khi thanh toán được thực hiện**.

**Hệ thống cần ghi lại:** `confirmed_by` (ai xác nhận), `confirmed_at` (thời điểm xác nhận), `payment_confirmed_at` (thời điểm xác nhận thanh toán nếu khác).

---

### 2.3. Khi nhận phim thực tế, cần ghi nhận thông tin gì?

**Checklist nhận film tối thiểu:**

| Trường thông tin | Mục đích | Bắt buộc |
|---|---|---|
| **Mã đơn / order ID** | Đối chiếu với đơn đã đặt | ✅ |
| **Tình trạng film** | Còn nguyên cuộn / đã cắt / ẩm ướt / có ghi chú đặc biệt | ✅ |
| **Ghi chú đặc biệt từ khách** | Push/pull, giữ âm bản, tráng nhanh | ✅ (nếu có) |
| **Số lượng thực tế** | So với số khai báo — nếu lệch, ghi nhận và thông báo khách | ✅ |
| **Người giao film** | Khách trực tiếp hay đối tác vận chuyển | ✅ |
| **Thời điểm nhận** | Dùng để tính SLA xử lý | ✅ |
| **Trạng thái thanh toán** | Đã thanh toán hay chưa | ✅ |
| **Ảnh chụp tình trạng film** | Bằng chứng nếu có tranh chấp sau này | Khuyến khích |

**Trường hợp bất thường khi nhận film:**

| Tình huống | Cách xử lý |
|---|---|
| **Số lượng thực tế lệch so với khai báo** | Ghi nhận, thông báo khách qua app/email, chờ xác nhận trước khi xử lý |
| **Film hư hỏng / ẩm ướt** | Chụp ảnh, ghi chú, thông báo khách, thỏa thuận trước khi tráng |
| **Film tự chiết không an toàn** | Từ chối nhận, ghi lý do, thông báo khách |
| **Khách chưa thanh toán** | Giữ đơn ở `PENDING_PAYMENT`, không chuyển sang xử lý |

---

### 2.4. Những trạng thái nào phản ánh đúng quy trình xử lý?

**Bộ trạng thái tối thiểu:**

| Trạng thái | Ý nghĩa | Điều kiện chuyển | Người chuyển |
|---|---|---|---|
| `PENDING_PAYMENT` | Đơn đã tạo, chờ thanh toán | Khách đặt đơn từ xa / online | Hệ thống |
| `RECEIVED_AT_LAB` | Lab đã nhận film thực tế | Nhân viên quét mã / xác nhận | Lab Operator |
| `PROCESSING` | Đang tráng / scan | Đã thanh toán + film đã nhận | Lab Operator |
| `DEVELOPING` (tùy chọn) | Đang tráng | Bắt đầu công đoạn tráng | Lab Operator |
| `SCANNING` (tùy chọn) | Đang scan | Bắt đầu công đoạn scan | Lab Operator |
| `SCANS_UPLOADED` | File scan đã upload và gắn đúng đơn | Upload thành công + đã associate order | Lab Operator |
| `READY_FOR_PICKUP` | Film gốc / bản in sẵn sàng trả tại lab | Hoàn tất QC | Lab Operator |
| `READY_FOR_DELIVERY` | Sẵn sàng giao cho shipper | Hoàn tất QC | Lab Operator |
| `DELIVERED` | Đã giao cho khách / shipper | Có xác nhận giao | Lab Operator / Delivery Partner |
| `CLOSED` | Đơn kết thúc, mở đánh giá | Tất cả dịch vụ (kể cả in ấn) hoàn tất | Hệ thống |
