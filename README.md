# Hiển thị ảnh GIF lên màn hình OLED bằng ESP32 🐹

Dự án nhỏ này hướng dẫn cách chuyển đổi và hiển thị một ảnh động (GIF) lên màn hình OLED 0.96 inch sử dụng vi điều khiển ESP32. Code được thiết lập hiệu ứng "Ping-pong" (chạy tiến và lùi) giúp hoạt ảnh lặp lại vô tận.

## 🛠 Phần cứng sử dụng
* Mạch phát triển **ESP32 DevKit V1**
* Màn hình **OLED 0.96 inch** (Giao tiếp I2C - Chip SSD1306)
* Dây cắm Breadboard (Jumper wires)

## 🔌 Sơ đồ nối dây (Pinout)

| Màn hình OLED | Chân ESP32 DevKit V1 | Ghi chú |
| :---: | :---: | :--- |
| **VCC** | `3V3` | Cấp nguồn 3.3V (Không dùng 5V/VIN) |
| **GND** | `GND` | Nối đất |
| **SCL** | `D22` (GPIO 22) | Xung nhịp đồng hồ I2C |
| **SDA** | `D21` (GPIO 21) | Truyền dữ liệu I2C |

## 💻 Môi trường và Thư viện
* **IDE:** VS Code + PlatformIO
* **Framework:** Arduino
* **Thư viện yêu cầu:**
  * `Adafruit GFX Library`
  * `Adafruit SSD1306`

## ⚙️ Các bước thực hiện nhanh
1. **Xử lý ảnh:** Resize ảnh GIF gốc về kích thước `128x64` pixel bằng [Ezgif](https://ezgif.com/resize) và tách thành từng khung hình (frames).
2. **Chuyển đổi sang C++:** Sử dụng công cụ [image2cpp](https://javl.github.io/image2cpp/) để chuyển đổi hàng loạt khung hình đã tách thành các mảng byte (`PROGMEM const unsigned char`).
3. **Hiển thị:** Dùng hàm `drawBitmap()` của thư viện Adafruit để vẽ lần lượt các mảng byte lên màn hình OLED trong vòng lặp `loop()`.

## 📝 Lưu ý về phần cứng
Màn hình OLED sử dụng trong dự án này là loại Dual-color (1/4 Vàng phía trên, 3/4 Xanh dương phía dưới). Đây là đặc tính vật lý của màn hình, nên khi hiển thị toàn màn hình (128x64), hình ảnh sẽ tự động được chia thành 2 dải màu này.

---
*Dự án được thực hiện để làm quen với lập trình nhúng C++ trên ESP32 và giao thức I2C.*

1st time update