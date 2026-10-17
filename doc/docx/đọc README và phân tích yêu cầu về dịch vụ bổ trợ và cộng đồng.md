# Quy Trình Vận Hành Dành Cho Film Lab (Lab Operator)

## 1. Quản lý thông tin và dịch vụ

### 1.1. Thông tin Hồ sơ Lab (Lab Profile)
Mỗi Film Lab cần cung cấp đầy đủ thông tin để khách hàng tìm kiếm, chọn lựa và ra quyết định đặt đơn:
- **Thông tin cơ bản**: Tên Lab, Địa chỉ các cơ sở, Giờ mở cửa/đóng cửa, Số điện thoại, Email liên hệ.
- **Danh mục dịch vụ**: Các loại film nhận xử lý (135, 120, APS, 110, Large format) và quy trình áp dụng (C-41, Đen trắng/BW, E-6 Slide, Cross-process, Cine/Vision).
- **Chính sách & Cam kết**: Thời gian xử lý dự kiến (SLA) công khai, biểu phí niêm yết, hướng dẫn gửi film qua bưu điện/shipment.

### 1.2. Phân quyền quản lý (RBAC)
- **Chủ Lab (Lab Owner) / Quản lý (Lab Manager)**: Có toàn quyền thêm, sửa, ẩn/xóa hoặc điều chỉnh giá các dịch vụ.
- **Nhân viên vận hành (Lab Staff / Operator)**: Chỉ có quyền tiếp nhận đơn, cập nhật trạng thái đơn hàng, tải file scan và đóng gói trả film. Không được phép sửa giá hay thông tin danh mục dịch vụ.

### 1.3. Cấu trúc một Dịch vụ (Service Package)
Mỗi gói dịch vụ bao gồm các thông tin tối thiểu:
- **Tên dịch vụ**: Ví dụ *"Tráng + Scan Standard - Film màu 135"*.
- **Mô tả chi tiết**: Quy trình (C-41/BW/E-6), định dạng file trả (JPEG, TIFF), độ phân giải scan (Standard, Hi-Res).
- **Giá dịch vụ & Phụ phí**: Giá gốc theo cuộn/sheet + phụ phí cấu hình chọn thêm (Push/Pull, Scan Hi-Res, Tráng gấp/Express).
- **Thời gian xử lý (SLA)**: Cam kết hoàn thành tối đa kể từ khi nhận film và xác nhận thanh toán (ví dụ: Film màu 135/120 tối đa 72h, Film Slide E-6 tối đa 15 ngày).

### 1.4. Cơ chế Tạm ngừng dịch vụ (`PAUSED`)
- Khi Lab tạm ngừng nhận một loại dịch vụ (ví dụ: hết hóa chất BW hoặc gom đủ 6 cuộn Slide mới tráng), dịch vụ sẽ chuyển sang trạng thái `PAUSED`.
- **Nguyên tắc**: Dịch vụ bị ẩn khỏi danh mục đặt mới, nhưng **các đơn đã tạo trước đó vẫn phải tiếp tục được xử lý bình thường**, không bị hủy tự động.

---

## 2. Nhận, xác nhận và cập nhật đơn hàng

### 2.1. Kênh tiếp nhận thông báo đơn mới
- **Đơn đặt trước qua App/Web**: Đơn đẩy vào Hàng đợi sản xuất (Production Queue / Kanban Board) gần như tức thời kèm thông báo chuông/badge cho nhân viên.
- **Đơn gửi qua bưu điện/shipper**: Khi nhận kiện hàng thực tế, nhân viên đối chiếu SĐT/Tên khách hàng để tạo hoặc gắn đơn trên hệ thống.

### 2.2. Xác nhận đơn & Điều kiện chuyển trạng thái
- Nhân viên vận hành (`LAB_STAFF`) xác nhận đã nhận thông tin và kiểm tra cuộn film vật lý.
- Hệ thống lưu lại thông tin người xác nhận (`confirmed_by`) và thời điểm xác nhận (`confirmed_at`).
- **ĐIỀU KIỆN BẮT BUỘC**: Đơn hàng chỉ được chuyển sang giai đoạn xử lý phòng tối khi **đã thanh toán hoàn tất** (`PAID`).

### 2.3. Checklist thông tin khi nhận film vật lý
Khi cầm cuộn film trên tay, nhân viên cần nhập/đối chiếu các thông tin:
- **Mã đơn hàng (`Order ID`)**: Quét mã QR/mã vạch gắn trên vỏ film hoặc tra cứu theo SĐT.
- **Tình trạng film thực tế**: Film còn nguyên vỏ, đã bị tụt đầu film, film ẩm/móp vỏ, hoặc film tự chiết (hand-rolled).
- **Ghi chú kỹ thuật từ khách**: Yêu cầu Push/Pull stop, giữ lại vỏ/âm bản (cut-negatives).
- **Số lượng thực tế**: Đối chiếu số cuộn thực nhận so với khai báo trên đơn.

### 2.4. Bảng trạng thái vòng đời đơn hàng (State Machine)

| Trạng thái | Ý nghĩa | Hành động kích hoạt / Ghi chú |
|---|---|---|
| `PENDING_PAYMENT` | Đã tạo đơn, chờ thanh toán | Đơn chưa vào hàng đợi xử lý tráng |
| `RECEIVED_AT_LAB` | Lab đã nhận film vật lý | Nhân viên quét mã / xác nhận đủ film |
| `PROCESSING` | Đang tráng (`DEVELOPING`) hoặc scan (`SCANNING`) | Film đang trong máy tráng / máy scan |
| `SCANS_UPLOADED` | File scan đã tải lên thành công | Tự động gửi thông báo cho khách xem ảnh |
| `READY_FOR_PICKUP` | Âm bản/bản in sẵn sàng trả | Chuẩn bị xong vỏ film đã tráng cho khách |
| `DELIVERED` | Khách đã nhận film/ảnh | Hoàn tất giao hàng vật lý |
| `CLOSED` | Đơn kết thúc | Tự động đóng đơn và mở tính năng đánh giá |

---

## 3. Tải file scan và trả kết quả

### 3.1. Thời điểm Upload & Phân tách trạng thái
- File scan được tải lên ngay sau công đoạn **`SCANNING`** và bước kiểm tra chất lượng (QC).
- **Quy tắc quan trọng**: Trạng thái `SCANS_UPLOADED` độc lập với `CLOSED`. Đơn hàng chỉ `CLOSED` khi đã bàn giao đầy đủ cả file số lẫn sản phẩm vật lý (âm bản gốc / bản in) nếu có.

### 3.2. Cấu trúc lưu trữ & Quyền riêng tư
- Mỗi bộ ảnh scan phải gắn chặt với mã **`Order ID`**, **`FilmRoll ID`** và **`Customer ID`**.
- Lưu trữ dưới dạng thư mục bảo mật (mã hóa Presigned URL hoặc cấp quyền theo Email khách hàng). Không công khai link công cộng để bảo vệ riêng tư ảnh chụp của khách.

### 3.3. Thông báo cho khách hàng
- Hệ thống tự động gửi **Push Notification** trên App và **Email** kèm link xem/tải ảnh ngay sau khi upload hoàn tất 100%.
- Nội dung thông báo: *"File scan cho đơn hàng #[Order ID] đã sẵn sàng. Nhấn để xem và tải về."*

### 3.4. Xử lý sự cố & Trường hợp bất thường (Exception Handling)
- **Tải thất bại (Lỗi mạng/File hỏng)**: Đổi trạng thái tạm thành `UPLOAD_FAILED`, kích hoạt cơ chế thử lại (`retry`), không gửi thông báo rác cho khách.
- **Tải nhầm file**: Cho phép Lab đè file/thay thế file mới trong thời hạn cho phép. Hệ thống bắt buộc ghi log lịch sử (`Audit Log`) gồm: *Ai thao tác, thời gian, file cũ/file mới* để đối soát khi có khiếu nại.

---

## 4. Quản lý giá và lịch sử đơn hàng

### 4.1. Nguyên tắc Snapshot giá
- Lab có quyền thay đổi bảng giá niêm yết bất kỳ lúc nào.
- **Nguyên tắc kỹ thuật**: Đơn hàng cũ **BẮT BUỘC giữ nguyên giá** tại thời điểm đặt.
- Hệ thống thực hiện **Snapshot (chụp lại)** toàn bộ giá dịch vụ, phụ phí, giảm giá vào bảng chi tiết đơn hàng (`OrderDetails`) ngay khi đơn được tạo.

### 4.2. Truy tra Lịch sử đơn hàng (Order History)
Dữ liệu đơn hàng đã hoàn tất phục vụ cho quản lý và khiếu nại bao gồm:
- **Lịch sử khách hàng**: Tần suất đặt đơn, ưu đãi tích lũy (ví dụ: tráng 10 cuộn tặng 1 cuộn).
- **Thông số kỹ thuật**: Loại film, quy trình tráng, máy scan sử dụng, kỹ thuật viên phụ trách.
- **Log thời gian (Timeline Log)**: Thời điểm nhận film, bắt đầu xử lý, thời điểm upload file và thời điểm giao film gốc.
- **Phản hồi**: Đánh giá sao và nhận xét từ khách hàng.

---

## 5. Tóm tắt các trường hợp ngoại lệ (Edge Cases)

| Tình huống ngoại lệ | Cách xử lý hệ thống / Nghiệp vụ |
|---|---|
| **Film bị trắng (Blank / Unexposed)** | Chỉ tính phí tráng, hoàn trả/miễn phí tiền scan hoặc in ấn cho khách. |
| **Film hư hỏng / Quá hạn nặng** | Lab từ chối nhận xử lý, cập nhật trạng thái đơn thành `REJECTED`, ghi rõ lý do và hoàn trả film. |
| **Số lượng film nhận thực tế lệch với đơn đặt** | Cập nhật lại số lượng thực tế, hệ thống tính toán lại tổng tiền và phát hành yêu cầu thanh toán bổ sung/hoàn tiền thừa. |
| **Khách làm mất đường link tải ảnh** | Lab tra cứu lịch sử đơn hàng và bấm "Gửi lại link" (`Re-send Notification`) trong vòng 30 - 90 ngày lưu trữ. |
