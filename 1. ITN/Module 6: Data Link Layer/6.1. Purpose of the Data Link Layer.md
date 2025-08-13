
| **Title** | 6.1. Purpose of the Data Link Layer |
|:---------:|:----------------------------------:|
| **ID**    | CCNET031                           |
| **Tag**   | CCNA, Cisco, NetAcad, OSI, DataLink, Layer2 |

---

## 6.1.1. The Data Link Layer

Data Link Layer (L2) là tầng thứ 2 trong mô hình OSI, đóng vai trò **trung gian giữa Layer 3 (Network) và Layer 1 (Physical)**.  
Chức năng chính:

- **Chuẩn bị dữ liệu** từ Network Layer để truyền qua media vật lý.
- **Đóng gói (Encapsulation)** packet L3 thành **frame L2** với thông tin địa chỉ MAC nguồn/đích.
- **Phát hiện lỗi** nhờ trường FCS (Frame Check Sequence).
- **Quản lý truy cập media** – quyết định khi nào thiết bị có thể truyền dữ liệu.
- **Bỏ đóng gói (Decapsulation)** khi nhận frame để lấy packet gửi lên Layer 3.

💡 L2 xử lý **giao tiếp NIC-to-NIC**, nghĩa là giữa card mạng của thiết bị nguồn và đích.

<p align="center">
  <img src="../../images/kì 1/module 6/6.1.1.jpg" width="400"/>
</p>

---

## 6.1.2. IEEE 802 LAN/MAN Data Link Sublayers

IEEE định nghĩa Layer 2 gồm **2 sublayer**:

1. **LLC (Logical Link Control)** – IEEE 802.2  
   - Giao tiếp với Layer 3.  
   - Xác định loại protocol trong frame (IPv4, IPv6, ARP...).  
   - Đảm bảo frame tới đúng dịch vụ mạng.

2. **MAC (Media Access Control)** – IEEE 802.3 (Ethernet), 802.11 (Wi-Fi), 802.15 (Bluetooth)  
   - Định địa chỉ MAC nguồn/đích.  
   - Xác định cách truy cập media (CSMA/CD, CSMA/CA...).  
   - Đóng gói/giải đóng gói frame và kiểm tra lỗi.
   
<p align="center">
  <img src="../../images/kì 1/module 6/6.1.2.jpg" width="400"/>
</p>

> MAC cho phép nhiều thiết bị giao tiếp qua 1 phương tiện chung ( half-duplex: song công) 

---

## 6.1.3. Providing Access to Media


Chức năng quan trọng của Data Link Layer là **kiểm soát cách thiết bị truy cập và truyền dữ liệu qua môi trường mạng**.

###  Media Access Control

Tùy vào loại kết nối, MAC sublayer sẽ quyết định **khi nào** và **cách nào** để truyền dữ liệu:

- **Point-to-Point**: chỉ 2 thiết bị → không cần cạnh tranh truy cập.
- **Multi-access (Ethernet LAN)**: nhiều thiết bị dùng chung → cần cơ chế điều khiển truy cập (CSMA/CD hoặc CSMA/CA).
- **Half-duplex**: truyền/nhận luân phiên → cần tránh xung đột.
- **Full-duplex**: truyền và nhận đồng thời → không xảy ra xung đột.

###  Đóng gói và gửi dữ liệu

Khi Network Layer gửi xuống packet (IPv4, IPv6...), Data Link Layer sẽ:

1. **Đóng gói (Encapsulation)**: thêm **header** (địa chỉ MAC nguồn/đích) và **trailer** (FCS) → tạo thành **frame**.
2. **Gửi frame** qua media (cáp đồng, cáp quang, sóng vô tuyến…).

###  Nhận và xử lý dữ liệu

Khi một thiết bị nhận frame từ media:

1. **Kiểm tra địa chỉ MAC đích**:
   - Nếu trùng MAC của thiết bị → xử lý tiếp.
   - Nếu không trùng → bỏ frame.
2. **Xác minh FCS** để phát hiện lỗi truyền.
3. **Bỏ header/trailer** L2, gửi packet lên Network Layer.

###  Chuyển tiếp qua nhiều mạng

Khi dữ liệu đi qua **nhiều mạng khác nhau** (host → router → router → host):

- **Địa chỉ IP nguồn/đích**: **không đổi** trong suốt hành trình.
- **Địa chỉ MAC**: **thay đổi tại mỗi hop** để phù hợp với đoạn media kế tiếp.

Ví dụ:  
PC gửi dữ liệu tới Web Server qua router:

| Chặng truyền           | Source MAC   | Destination MAC |
|------------------------|--------------|-----------------|
| PC → Router1           | MAC-PC       | MAC-R1          |
| Router1 → Router2      | MAC-R1       | MAC-R2          |
| Router2 → Web Server   | MAC-R2       | MAC-Server      |

> Điều này giúp Data Link Layer **tương thích với nhiều loại media** (Ethernet, Wi-Fi, PPP, Frame Relay…).

---

## 6.1.4. Data Link Layer Standards

Chuẩn Layer 2 đảm bảo thiết bị **tương thích** khi kết nối:

- **IEEE** – chuẩn Ethernet, Wi-Fi.  
- **ITU** – chuẩn viễn thông quốc tế (ATM, Frame Relay...).  
- **ISO** – chuẩn hóa cấu trúc frame.  
- **ANSI** – chuẩn tại Bắc Mỹ.

Các chuẩn này áp dụng cho **Network Access Layer** (Physical + Data Link), đảm bảo việc đóng gói/giải đóng gói thống nhất.

<p align="center">
  <img src="../../images/kì 1/module 6/6.1.4.jpg" width="400"/>
</p>
