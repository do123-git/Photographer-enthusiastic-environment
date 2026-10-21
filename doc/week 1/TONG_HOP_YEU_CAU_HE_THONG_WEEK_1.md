# TỔNG HỢP ĐẶC TẢ YÊU CẦU HỆ THỐNG
> **Nền tảng kết nối cộng đồng nhiếp ảnh phim và các Film Lab (MiniLab)**  
> *Đồ án Term Project — Nhóm 8*

---

## MỤC LỤC

1. [Phân hệ Khách hàng / Nhiếp ảnh gia (Photographer / Customer)](#1-phân-hệ-khách-hàng--nhiếp-ảnh-gia-photographer--customer)
2. [Phân hệ Quản trị vận hành Film Lab (Film Lab Owner)](#2-phân-hệ-quản-trị-vận-hành-film-lab-film-lab-owner)
3. [Phân hệ Chuyên gia nhiếp ảnh & Cộng đồng (Photography Expert & Community)](#3-phân-hệ-chuyên-gia-nhiếp-ảnh--cộng-đồng-photography-expert--community)
4. [Phân hệ Đối tác vận chuyển (Delivery Partner)](#4-phân-hệ-đối-tác-vận-chuyển-delivery-partner)
5. [Phân hệ Quản trị hệ thống (System Administrator)](#5-phân-hệ-quản-trị-hệ-thống-system-administrator)
6. [Sàn trao đổi thiết bị (Marketplace)](#6-sàn-trao-đổi-thiết-bị-marketplace)
7. [Ma trận phân quyền hệ thống (RBAC)](#7-ma-trận-phân-quyền-hệ-thống-rbac)

---

## 1. PHÂN HỆ KHÁCH HÀNG / NHIẾP ẢNH GIA (PHOTOGRAPHER / CUSTOMER)

### 1.1 Đăng ký và Quản lý tài khoản
* **Đăng ký / Đăng nhập:**
  * Thông tin cơ bản: Họ tên, Email, Số điện thoại, Mật khẩu.
  * Xác thực tài khoản qua OTP (Email/SMS) để bảo mật và tránh tài khoản ảo.
  * Quên mật khẩu: Gửi mã OTP hoặc liên kết đặt lại mật khẩu về Email/SĐT đã đăng ký.
* **Hồ sơ cá nhân:** Cập nhật họ tên, ảnh đại diện, số điện thoại, địa chỉ nhận hàng mặc định.

### 1.2 Tìm kiếm và So sánh Film Lab
* **Tìm kiếm Film Lab đa tiêu chí:**
  * Theo vị trí địa lý (tỉnh/thành phố, khoảng cách gần nhất qua định vị).
  * Theo định dạng film hỗ trợ: 35mm (135), 120 (Medium Format), 110...
  * Theo quy trình dịch vụ: Film màu (C-41), film đen trắng (B&W), film điện ảnh (ECN-2), film slide (E-6).
* **So sánh trực quan giữa các Lab:**
  * Bảng giá công khai từng gói dịch vụ.
  * Cam kết thời gian hoàn thành (SLA: 24h, 48h, 72h...).
  * Điểm đánh giá (Rating) và nhận xét thực tế từ cộng đồng.
  * Năng lực xử lý đặc biệt và tùy chọn hỗ trợ lấy film tận nơi (Pickup).

### 1.3 Đặt dịch vụ trực tuyến & Tính giá
* **Tạo đơn hàng tráng / scan / in:**
  * Chọn khổ film và số lượng cuộn.
  * Chọn dịch vụ: Tráng + Scan (mặc định), Chỉ tráng, hoặc kèm In ảnh.
  * Tùy chọn kỹ thuật: Mức chất lượng scan (Standard / Hi-Res / TIFF), xử lý đặc biệt (Push/Pull sáng).
  * Yêu cầu in ảnh: Kích thước ảnh (10x15, 13x18...), số lượng ảnh cần in.
  * Phương thức gửi film: Tự mang đến tiệm (Drop-off) hoặc yêu cầu shipper đến lấy (Pickup).
* **Công thức tính giá:**
  ```
  Tổng tiền = (Giá dịch vụ tráng/scan × Số cuộn)
            + (Phụ phí Scan Hi-res/Push × Số cuộn)
            + (Giá in ảnh × Số ảnh in)
            + Phí vận chuyển (nếu có)
  ```

### 1.4 Vòng tuần hoàn đơn hàng & Theo dõi tiến độ thời gian thực
Quy trình xử lý một đơn hàng film diễn ra theo các giai đoạn tuần tự:
1. **Đặt dịch vụ & Thu nhận film:** Khách hàng tạo đơn trực tuyến, thanh toán online (hoặc tiền mặt khi tự mang đến tiệm) và chọn gửi film qua shipper hoặc tự mang đến tiệm.
2. **Xác nhận & Tiếp nhận:** Film Lab xác nhận đơn, tiếp nhận cuộn film thực tế tại tiệm hoặc từ shipper và lên lịch xử lý.
3. **Quy trình xử lý film:** Lab thực hiện từng công đoạn: Nhận film -> Tráng hóa chất -> Rửa & Sấy khô -> Scan ảnh -> Kiểm tra chất lượng (QC). Mỗi bước được ghi nhận và đồng bộ lên ứng dụng của khách theo thời gian thực.
4. **Giao file số & Quản lý Archive:** Lab upload file scan lên cloud storage an toàn; hệ thống tự động đẩy file vào Digital Film Archive của khách, gửi thông báo đẩy để khách xem, tải về và quản lý kèm metadata.
5. **Giao trả vật lý (nếu có yêu cầu):** Trường hợp khách có đặt dịch vụ in ảnh hoặc yêu cầu nhận lại cuộn film đã tráng (âm bản), Lab bàn giao cho đối tác vận chuyển giao trả tận nơi cho khách.
6. **Hoàn tất & Đóng đơn:** Khách hàng nhận đủ kết quả, đơn hàng hoàn tất đóng lại và mở tính năng đánh giá chất lượng dịch vụ của Film Lab.

* **Chuỗi trạng thái đơn hàng hiển thị:**  
  `Chờ thanh toán` -> `Chờ Lab xác nhận` -> `Đang xử lý (Tráng & Scan)` -> `Hoàn thành (Đã trả file scan vào Archive)` -> `Đang giao (nếu có ship film/ảnh)` -> `Đã nhận / Đóng đơn` (hoặc `Đã hủy`).
* **Phương thức thanh toán:** Tích hợp thanh toán online qua cổng thanh toán (VNPAY / Momo / Thẻ ngân hàng / QR Code). Với khách tự mang phim đến tiệm, có thể chọn trả tiền mặt (COD) tại quầy.

### 1.5 Quy định hủy đơn và Hoàn tiền
* Khách hàng được phép hủy đơn và nhận lại 100% tiền khi đơn ở trạng thái `Chờ Lab xác nhận` (Lab chưa nhận film thực tế và chưa cử shipper đi lấy). Khi film đã vào quy trình xử lý tại tiệm, đơn không thể hủy thông thường.
* Trường hợp cuộn film bị trắng (Blank Film) do lỗi từ thiết bị của khách: Lab chụp ảnh cuộn phim trắng làm bằng chứng; hệ thống tự động hoàn trả 100% chi phí scan và in ấn, chỉ giữ lại chi phí hóa chất tráng.

### 1.6 Tải và Quản lý kho lưu trữ số (Digital Film Archive)
* **Nguyên tắc trả kết quả cốt lõi:** Kết quả chính của dịch vụ là **File scan số** chất lượng cao được tải lên Cloud Storage an toàn và tự động nạp vào **Digital Film Archive** của khách hàng; việc giao nhận vật lý cuộn film âm bản hoặc ảnh in chỉ phát sinh khi khách có nhu cầu.
* **Nhận file scan:** Khách nhận thông báo đẩy tức thời để xem và tải file gốc (không nén) về thiết bị mọi lúc.
* **Hệ thống Metadata đầy đủ:**
  * Tự động từ Lab: Tên Film Lab thực hiện, ngày scan, thông số scan (độ phân giải, định dạng).
  * Khách hàng tự bổ sung: Loại cuộn film (VD: Kodak Portra 400), máy ảnh sử dụng (VD: Canon AE-1), ống kính, ngày chụp, cách xử lý (Push/Pull), ghi chú cá nhân.
* **Quản lý ảnh:** Xem dạng lưới, gom ảnh theo album chuyến đi/dự án, chia sẻ link ảnh.

### 1.7 Đánh giá Film Lab
* Sau khi đơn hàng hoàn tất, khách hàng được chấm điểm (1–5 sao) và viết nhận xét công khai về chất lượng màu sắc, độ sạch bụi và thái độ phục vụ của Lab.

---

## 2. PHÂN HỆ QUẢN TRỊ VẬN HÀNH FILM LAB (FILM LAB OWNER)

### 2.1 Quản lý hồ sơ tiệm (Lab Profile)
* Cấu hình thông tin công khai: Tên Lab, logo, địa chỉ các chi nhánh, số điện thoại, giờ mở cửa, mô tả tiệm.
* Khai báo danh mục năng lực kỹ thuật: Các loại khổ film nhận xử lý (135, 120, 110), các quy trình hóa chất hỗ trợ (C-41, BW, ECN-2, E-6).

### 2.2 Cấu hình gói dịch vụ và bảng giá
* Thiết lập các gói dịch vụ: Tráng + Scan, Chỉ tráng, In ảnh, các mức phụ phí (Push/Pull, Scan TIFF, phụ thu film điện ảnh).
* Thiết lập thời gian cam kết trả file (SLA).
* **Cơ chế tạm ngưng dịch vụ:** Khi quá tải hoặc thiếu hóa chất, Lab có thể chuyển dịch vụ sang trạng thái `Tạm ngưng (PAUSED)` để ẩn khỏi trang tìm kiếm mà không làm mất dữ liệu đơn cũ.
* **Bảo lưu giá đơn cũ (Price Snapshotting):** Khi Lab đổi giá, các đơn hàng khách đã tạo trước đó vẫn giữ nguyên giá tại thời điểm đặt.

### 2.3 Tiếp nhận đơn và Quản lý vòng đời xử lý film (Production Lifecycle)
* **Tiếp nhận đơn hàng:** Đơn mới xuất hiện tức thời trên bảng điều khiển của Lab. Lab đối soát thông tin khi nhận film thực tế tại tiệm hoặc từ shipper.
* **Cập nhật từng công đoạn theo thời gian thực:**
  * Tiếp nhận film -> Tráng hóa chất -> Rửa & Sấy khô -> Scan ảnh -> Kiểm tra chất lượng (QC).
  * Mỗi lần Lab chuyển trạng thái, hệ thống tự động đồng bộ lên ứng dụng của khách.
* **Xử lý cuộn film bị trắng (Blank Film):** Nếu phim bị trắng hoàn toàn do lỗi từ phía máy ảnh của khách, Lab chụp ảnh dải phim trắng làm bằng chứng và gửi thông báo; hệ thống tự động hoàn tiền phần phí scan/in cho khách.

### 2.4 Upload file scan số lên Cloud Storage
* Lab tải file scan chất lượng cao lên Cloud Storage an toàn thông qua Web Portal.
* Hệ thống tự động gắn file với đúng khách hàng và đơn hàng, đồng thời bắn thông báo để khách truy cập kho Digital Film Archive.

### 2.5 Quản lý khách hàng, Doanh thu và Báo cáo vận hành
* Theo dõi danh sách khách hàng, lịch sử các đơn hàng đã thực hiện.
* Thống kê doanh thu theo ngày/tuần/tháng, số lượng cuộn film đã xử lý, tỷ lệ hoàn thành đúng hạn cam kết (SLA).

---

## 3. PHÂN HỆ CHUYÊN GIA NHIẾP ẢNH & CỘNG ĐỒNG (PHOTOGRAPHY EXPERT & COMMUNITY)

### 3.1 Đăng bài hướng dẫn và Chia sẻ kỹ thuật
* Chuyên gia nhiếp ảnh (Photography Expert) được cấp huy hiệu chứng nhận uy tín.
* Đăng tải các bài viết chuyên môn: Kỹ thuật chụp phim, cách đo sáng cho film slide, kinh nghiệm chọn mua máy ảnh cơ, review đánh giá các dòng film, ống kính và chất lượng các Film Lab.

### 3.2 Tổ chức sự kiện Workshop & Photowalk
* Chuyên gia có thể tạo và quản lý sự kiện:
  * Buổi chụp ảnh thực tế ngoài trời (Photowalk).
  * Buổi hướng dẫn tự tráng phim đen trắng tại nhà (Workshop).
* Thành viên cộng đồng có thể xem chi tiết, đăng ký tham gia và thảo luận trực tiếp trong trang sự kiện.

### 3.3 Thảo luận cộng đồng & Hỏi đáp
* Mọi thành viên đã đăng ký đều có thể tham gia bình luận dưới bài viết, đặt câu hỏi cho chuyên gia hoặc chia sẻ ảnh chụp từ kho cá nhân để giao lưu.

---

## 4. PHÂN HỆ ĐỐI TÁC VẬN CHUYỂN (DELIVERY PARTNER)

### 4.1 Quy trình giao nhận film hai chiều
* **Chiều 1 (Pickup film từ khách đến Lab):**
  * Khách đặt đơn chọn yêu cầu giao nhận -> Hệ thống điều phối đơn vị vận chuyển (Ahamove, Lalamove hoặc shipper của tiệm).
  * Shipper đến địa chỉ của khách để nhận cuộn film -> Giao film đến tận tay Film Lab.
* **Chiều 2 (Trả film đã xử lý cho khách):**
  * Khi khách có nhu cầu nhận lại cuộn film đã tráng (âm bản) hoặc nhận các bản ảnh in vật lý.
  * Lab đóng gói film/ảnh -> Bàn giao cho Shipper giao trả về địa chỉ của khách.

### 4.2 Cập nhật trạng thái vận chuyển thời gian thực
* Lưu trữ thông tin vận chuyển: Mã vận đơn (Tracking Code), tên shipper/đơn vị đối tác, số điện thoại, thời gian lấy và thời gian giao dự kiến.
* Trạng thái giao nhận được đồng bộ real-time để khách hàng và Film Lab cùng theo dõi.
* **Xử lý sự cố giao hàng:** Nếu không liên lạc được với khách lấy film (tối đa 2 lần thử), yêu cầu pickup được hủy và khách chuyển sang tự mang phim đến tiệm.

---

## 5. PHÂN HỆ QUẢN TRỊ HỆ THỐNG (SYSTEM ADMINISTRATOR)

### 5.1 Quản lý người dùng và Phân quyền (RBAC)
* Quản lý danh sách tài khoản: Khách hàng, Chủ Film Lab, Chuyên gia, Đối tác vận chuyển.
* Khóa tài khoản vi phạm: Khóa các tài khoản có hành vi gian lận, spam hoặc vi phạm quy định cộng đồng; có cơ chế gửi thông báo lý do và tiếp nhận yêu cầu xem xét lại.

### 5.2 Thẩm định và Duyệt Film Lab
* Tiếp nhận hồ sơ đăng ký mở tiệm từ đối tác: Tên tiệm, địa chỉ thực tế, giấy phép/CCCD chủ tiệm, hình ảnh máy tráng scan.
* Admin thẩm định thông tin thực tế -> Bấm "Duyệt" để tiệm chính thức xuất hiện trên ứng dụng của khách.

### 5.3 Quản lý Marketplace và Danh mục dịch vụ
* **Kiểm duyệt tin đăng Marketplace (Tiền kiểm 100%):** Kiểm tra hình ảnh thật của máy ảnh/ống kính và thông tin mô tả tình trạng trước khi duyệt hiển thị lên sàn.
* Quản lý danh mục dịch vụ chuẩn của hệ thống (các chuẩn loại film, quy trình C41, BW, ECN2, E6).
* Có quyền ẩn các dịch vụ của Lab nếu phát hiện thông tin sai lệch hoặc phản cảm (Admin không tự ý can thiệp sửa giá của Lab).

### 5.4 Cấu hình phí giao dịch & Giám sát thanh toán
* Cấu hình tỷ lệ phí hoa hồng nền tảng trên mỗi đơn hàng tráng/scan.
* Giám sát các giao dịch thanh toán trực tuyến, theo dõi luồng đối soát doanh thu giữa nền tảng và các Film Lab.

### 5.5 Kiểm duyệt nội dung & Xử lý khiếu nại tranh chấp
* Kiểm duyệt bài viết cộng đồng và đánh giá của khách theo cơ chế **Hậu kiểm**: Tiếp nhận báo cáo vi phạm từ người dùng để xem xét gỡ bỏ nội dung xấu, độc hại.
* **Xử lý tranh chấp, khiếu nại:** Tiếp nhận khiếu nại từ khách hàng (khi phim bị hỏng/mất hoặc dịch vụ không đúng cam kết) -> Xem xét bằng chứng từ hai phía và đưa ra phán quyết hoàn tiền hoặc yêu cầu đền bù.
* **Nhật ký thao tác (Audit Log):** Lưu trữ lịch sử toàn bộ các hành động nhạy cảm của Admin (duyệt lab, xóa tin, khóa tài khoản, xử lý tiền) để đảm bảo tính minh bạch.
* **Theo dõi hiệu năng nền tảng:** Giám sát thời gian phản hồi hệ thống, lượng truy cập và tính sẵn sàng của các dịch vụ.

---

## 6. SÀN TRAO ĐỔI THIẾT BỊ (MARKETPLACE)

### 6.1 Phạm vi sản phẩm mua bán
* Các danh mục cho phép: Máy ảnh analog (SLR, Rangefinder, Point & Shoot, Medium Format), ống kính máy ảnh, cuộn film (film mới, film outdate), phụ kiện nhiếp ảnh (filter, dây đeo, bao da, flash rời).

### 6.2 Quản lý tin đăng (Tiền kiểm 100%) & Tìm kiếm nâng cao
* **Đăng tin bán thiết bị:**
  * Người bán khai báo: Tên thiết bị, danh mục, giá bán niêm yết, địa điểm giao dịch.
  * Mô tả tình trạng cơ học chi tiết: Hoạt động đo sáng, tốc độ màn trập, tình trạng buồng phim kín sáng, thấu kính có trầy xước/mốc rễ tre hay không.
  * Hình ảnh: Bắt buộc cung cấp tối thiểu 3 ảnh chụp thật các góc cạnh của thiết bị.
  * **Cơ chế tiền kiểm 100%:** Tin đăng sau khi tạo sẽ chuyển vào hàng đợi kiểm duyệt để Admin kiểm tra ảnh thật và nội dung mô tả trước khi được duyệt hiển thị lên sàn.
* **Tìm kiếm nâng cao:** Khách hàng tìm kiếm theo từ khóa, lọc theo mức giá, danh mục thiết bị, khu vực địa lý và độ uy tín của người bán.

### 6.3 Nhắn tin trao đổi và Theo dõi giao dịch
* Tích hợp tính năng **Nhắn tin trực tiếp giữa người mua và người bán** ngay trên ứng dụng để trao đổi chi tiết về tình trạng máy móc và hẹn phương thức giao dịch.
* **Theo dõi giao dịch & Đánh giá người bán:**
  * Hệ thống cho phép ghi nhận trạng thái giao dịch mua bán.
  * Sau khi hoàn tất giao dịch, người mua được đánh giá độ uy tín (số sao và nhận xét) cho người bán để xây dựng cộng đồng mua bán minh bạch, an toàn.

---

## 7. MA TRẬN PHÂN QUYỀN HỆ THỐNG (RBAC)

| Chức năng chính | Customer | Film Lab | Expert | Delivery Partner | System Admin |
|---|:---:|:---:|:---:|:---:|:---:|
| Đăng ký, quản lý tài khoản cá nhân | Có | Có (Chờ duyệt) | Có | Có | Có |
| Tìm kiếm, so sánh & Đặt dịch vụ | Có | - | Có | - | - |
| Quản lý dịch vụ & Cài đặt bảng giá Lab | - | Có (Chỉ Owner) | - | - | Ẩn dịch vụ |
| Tiếp nhận đơn & Cập nhật tiến độ tráng/scan | - | Có | - | - | Xem / Can thiệp |
| Upload file scan trả khách lên Cloud | - | Có | - | - | Không (Bảo mật riêng tư) |
| Kho lưu trữ số Digital Film Archive | Cá nhân | - | Cá nhân | - | Không (Chỉ xem khi có khiếu nại) |
| Nhận đơn pickup & Cập nhật vị trí vận chuyển | - | - | - | Có | Tra cứu |
| Đăng tin mua bán trên Marketplace | Có (Chờ duyệt) | Có (Chờ duyệt) | Có (Chờ duyệt) | - | Duyệt / Xóa tin |
| Nhắn tin mua bán & Đánh giá người bán | Có | Có | Có | - | - |
| Đăng bài kỹ thuật, review, tạo Workshop | Thảo luận | Thảo luận | Có (Đăng bài / Tổ chức) | - | Kiểm duyệt hậu kiểm |
| Duyệt mở Lab, cấu hình phí sàn, xử lý khiếu nại | - | - | - | - | Có (Toàn quyền) |
