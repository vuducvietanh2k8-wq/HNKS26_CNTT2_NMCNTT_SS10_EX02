# HƯỚNG DẪN CÀI ĐẶT CẢM BIẾN ĐỘ ẨM — TRANG TRẠI LAN

## 1. Tổng quan

Cảm biến độ ẩm giúp theo dõi độ ẩm đất, hỗ trợ hệ thống tưới tự động và tối ưu lượng nước cho cây trồng tại trang trại Lan.

### Thiết bị cần chuẩn bị

- Cảm biến độ ẩm DHT22 hoặc AM2302 (nếu đo độ ẩm không khí).
- Raspberry Pi hoặc bo mạch tương thích.
- Dây nối và nguồn điện phù hợp.
- Máy bơm nước và module rơ-le tương thích.
- Python 3 và thư viện điều khiển thiết bị.

**Lưu ý:** DHT22 đo độ ẩm không khí, không đo trực tiếp độ ẩm đất. Nếu cần theo dõi độ ẩm đất, hãy sử dụng cảm biến độ ẩm đất phù hợp.

## 2. Phân tích Input / Output (I/O)

### Input — Văn bản thô

Nội dung Markdown bao gồm văn bản giải thích, lệnh Terminal, mã Python, bảng so sánh và danh sách kiểm tra.

### Output — Giao diện render

Tài liệu được hiển thị với tiêu đề rõ ràng, lệnh Terminal có định dạng riêng, mã Python có Syntax Highlighting, bảng so sánh và Task List dễ theo dõi.

## 3. Các bước cài đặt

### Bước 1: Cập nhật hệ thống

Mở Terminal và nhập lệnh:

```bash
sudo apt update && sudo apt upgrade -y
```

### Bước 2: Cài đặt Python và thư viện

```bash
sudo apt install -y python3 python3-pip
```

Cài thư viện phù hợp với loại cảm biến và nền tảng đang sử dụng trước khi viết chương trình.

### Bước 3: Kiểm tra kết nối

Xác định đúng chân nguồn, chân GND và chân tín hiệu theo tài liệu của nhà sản xuất. Không tự áp dụng sơ đồ chân của một loại cảm biến cho loại khác.

### Bước 4: Tạo chương trình Python

Tạo file `pump_control.py` và viết chương trình điều khiển máy bơm.

## 4. Code Python điều khiển máy bơm


```python
MOISTURE_THRESHOLD = 35

def read_moisture():
    # Giá trị mô phỏng để thử logic chương trình
    return 28

def set_pump(enabled):
    if enabled:
        print("Máy bơm: BẬT")
    else:
        print("Máy bơm: TẮT")

def main():
    moisture = read_moisture()
    print(f"Độ ẩm đất: {moisture}%")

    if moisture < MOISTURE_THRESHOLD:
        set_pump(True)
    else:
        set_pump(False)

if __name__ == "__main__":
    main()
```

### Bước 5: Chạy chương trình

Nhập lệnh sau vào Terminal:

```bash
python3 pump_control.py
```

Kết quả minh họa:

```text
Độ ẩm đất: 28%
Máy bơm: BẬT
```

**Chú ý:** Chương trình trên chỉ mô phỏng việc bật/tắt máy bơm bằng thông báo. Muốn điều khiển máy bơm thật, phải tích hợp phần cứng phù hợp, kiểm tra trạng thái an toàn và không kết nối máy bơm điện lưới trực tiếp với GPIO.

## 5. Bảng so sánh cảm biến cũ và cảm biến mới

| Tiêu chí | Cảm biến cũ | Cảm biến mới |
|---|---|---|
| Công nghệ | Điện trở | Điện dung |
| Cấu tạo | Hai điện cực tiếp xúc với đất | Đầu dò đo theo nguyên lý điện dung |
| Ăn mòn | Có thể bị ăn mòn theo thời gian | Thường ít bị ăn mòn hơn |
| Chi phí | Thường thấp | Thường cao hơn |
| Độ ổn định | Có thể suy giảm khi điện cực bị ăn mòn | Phụ thuộc chất lượng và điều kiện sử dụng |
| Hiệu chuẩn | Cần hiệu chuẩn | Cần hiệu chuẩn |
| Ứng dụng | Đo độ ẩm đất | Đo độ ẩm đất |

*Lưu ý: Bảng trên so sánh hai loại cảm biến độ ẩm đất phổ biến. Cần kiểm tra thông số của từng model trước khi mua và lắp đặt.*

## 6. Task List kiểm tra thiết bị

- [ ] Kiểm tra model cảm biến.
- [ ] Xác định điện áp hoạt động.
- [ ] Kiểm tra sơ đồ chân và dây kết nối.
- [ ] Xác nhận Python đã được cài đặt.
- [ ] Kiểm tra thư viện cần thiết.
- [ ] Đọc thử giá trị cảm biến.
- [ ] Hiệu chuẩn ngưỡng `MOISTURE_THRESHOLD`.
- [ ] Kiểm tra logic bật/tắt máy bơm bằng mô phỏng.
- [ ] Kiểm tra rơ-le và biện pháp cách ly điện.
- [ ] Ghi lại kết quả kiểm tra trước khi vận hành.

## 7. Sử dụng Inline Code và Escape

### Inline Code

Sử dụng dấu huyền ngược để định dạng lệnh ngắn và tên biến.

Ví dụ: `python3 pump_control.py`, `MOISTURE_THRESHOLD`, `read_moisture()`.

### Escape ký tự đặc biệt

Sử dụng dấu gạch chéo ngược `\` trước ký tự Markdown khi muốn hiển thị ký tự đó theo nghĩa đen.

Ví dụ:

- `\*Văn bản\*` hiển thị thành \*Văn bản\*.
- `\# Tiêu đề` hiển thị thành \# Tiêu đề.