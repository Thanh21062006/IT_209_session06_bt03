# Báo cáo Bài 3: Cấu hình tường lửa UFW và chuẩn đoán cổng mạng

## 1. Mục tiêu
- Sử dụng công cụ tường lửa UFW (Uncomplicated Firewall) để bảo vệ máy chủ.
- Thiết lập quy tắc chặn/mở cổng mạng phục vụ cho việc deploy ứng dụng một cách an toàn.
- Sử dụng các công cụ chẩn đoán mạng để kiểm tra cổng kết nối.

## 2. Các bước cấu hình UFW
Để thiết lập tường lửa bảo vệ máy chủ nhưng vẫn cho phép ứng dụng web và kết nối quản trị hoạt động, em thực hiện tuần tự các bước sau:

Đảm bảo chính sách mặc định an toàn tuyệt đối bằng cách chặn mọi kết nối vào (incoming) và mở toàn bộ kết nối ra (outgoing):
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Mở cổng SSH (Port 22) để không bị mất kết nối quản trị:
```bash
sudo ufw allow 22/tcp
```

Mở cổng 8080 cho ứng dụng Web:
```bash
sudo ufw allow 8080/tcp
```

Bật tường lửa (nhấn `y` khi có cảnh báo ngắt kết nối):
```bash
sudo ufw enable
```

## 3. Kết quả kiểm tra (Ảnh chụp cấu hình)
Để kiểm tra lại các thiết lập của tường lửa, em sử dụng lệnh xem trạng thái chi tiết:
```bash
sudo ufw status verbose
```

**Đầu ra kết quả trả về của lệnh:**

```text
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
8080/tcp                   ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
8080/tcp (v6)              ALLOW IN    Anywhere (v6)
```

*(Ghi chú: Tường lửa hiển thị trạng thái `active`. Trong danh sách rule có đủ cả 22/tcp và 8080/tcp với action `ALLOW IN`, đáp ứng chính xác yêu cầu đề bài).*
