# BÁO CÁO KIỂM THỬ HIỆU SUẤT JMETER

- **Ngày Kiểm Thử**: 01/07/2025  
- **Người Kiểm Thử**: Bùi Ngọc Đức

## 1. Mục Tiêu Kiểm Thử

- Thực hiện kiểm thử các phương thức cơ bản trong API REST: GET, POST, PUT, DELETE
- Sử dụng công cụ Apache JMeter
- Làm quen với cách thiết lập Test Plan, gửi Request và kiểm tra Response
- Quan sát hiệu năng API qua các thông số như: Response Time, Status Code, Payload

## 2. Môi Trường Kiểm Thử

Quá trình kiểm thử được thực hiện trên môi trường đơn giản nhưng đảm bảo yêu cầu kỹ thuật:
- Công cụ kiểm thử: **Apache JMeter phiên bản 5.6.3**
- Hệ điều hành: **MacOS**
- Kết nối mạng ổn định, không bị giới hạn firewall khi truy cập API công khai
- Sử dụng hệ thống backend riêng.

## 3. Phương Pháp Kiểm Thử

Phương pháp kiểm thử được sử dụng trong đợt này là **kiểm thử hiệu suất tự động**, tập trung vào việc:
- Gửi các request đồng thời từ nhiều người dùng ảo (thread)
- Lặp lại các request để kiểm tra độ ổn định theo thời gian
- Theo dõi thời gian phản hồi, tỉ lệ thành công, và khả năng xử lý khi có tải tăng
- Phân tích các số liệu thống kê như throughput, latency, success rate...

JMeter được sử dụng để cấu hình chi tiết số lượng người dùng, thời gian ramp-up, vòng lặp, và các loại listener như Summary Report, Graph Results, View Results Tree để theo dõi kết quả trong thời gian thực.

## 4. Kịch Bản Kiểm Thử
### Kịch Bản Kiểm Thử Lần 1

- **Tên kịch bản**: Kiểm thử cơ bản với 1 người dùng
- **Mục đích**: Mục đích của kịch bản này là kiểm tra phản hồi cơ bản của API khi có duy nhất một người dùng gửi một yêu cầu đơn lẻ. Đây là trường hợp đơn giản nhất nhằm xác nhận rằng API đang hoạt động, có thể kết nối được, và trả về dữ liệu đúng như kỳ vọng.

| Thông số cấu hình         | Giá trị                                  |
|---------------------------|-------------------------------------------|
| HTTP Request              | `http://localhost:8081/api/buses?page=1&limit=10`      |
| Method                    | `GET`                                    |
| Number of Threads (User)  | `1`                                      |
| Ramp-up Period (s)        | `1`                                      |
| Loop Count                | `1`                                      |

- Kết quả:
![image](https://github.com/ducbn/jmeter-api-test/blob/main/image/http.png)
![image](https://github.com/ducbn/jmeter-api-test/blob/main/image/view1.png)
![image](https://github.com/ducbn/jmeter-api-test/blob/main/image/summary1.png)
![image](https://github.com/ducbn/jmeter-api-test/blob/main/image/graph1.png)

### Kịch Bản Kiểm Thử Lần 2

- **Tên kịch bản**: Kiểm thử với nhiều người dùng đồng thời
- **Mục đích**: Kịch bản này nhằm mô phỏng tình huống có nhiều người dùng cùng truy cập API trong một khoảng thời gian ngắn. Việc này giúp kiểm tra xem hệ thống có thể đáp ứng được nhiều yêu cầu đồng thời hay không, có xảy ra tình trạng nghẽn hoặc lỗi phản hồi hay không.

| Thông số cấu hình         | Giá trị                                  |
|---------------------------|-------------------------------------------|
| HTTP Request              | `http://localhost:8081/api/buses?page=1&limit=10`      |
| Method                    | `GET`                                    |
| Number of Threads (User)  | `1000`                                     |
| Ramp-up Period (s)        | `5`                                      |
| Loop Count                | `5`                                      |

- Kết quả:
![image](https://github.com/ducbn/jmeter-api-test/blob/main/image/http.png)
![image](https://github.com/ducbn/jmeter-api-test/blob/main/image/view.png)
![image](https://github.com/ducbn/jmeter-api-test/blob/main/image/summary.png)
![image](https://github.com/ducbn/jmeter-api-test/blob/main/image/graph.png)

## 5. Kết Luận

- Qua bài thực hành này, em đã hiểu cách sử dụng JMeter để test các loại request API REST.
- Biết cách cấu hình Header, Body Data, Thread Group và các Listener.
- Thực hành được các thao tác GET, POST, PUT, DELETE cơ bản trên môi trường giả lập.
- Bước đầu làm quen với kiểm thử hiệu năng API.
