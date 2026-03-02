# Kiểm thử hiệu năng website với Apache JMeter

## 1. Mục tiêu
- làm quen với công cụ Apache JMeter trong kiểm thử hiệu năng
- thiết kế nhiều kịch bản kiểm thử với tham số khác nhau
- thu thập, phân tích và đánh giá các chỉ số hiệu năng của website

## 2. Website được kiểm thử
- https://vnexpress.net

## 3. Môi trường kiểm thử
- công cụ: Apache JMeter 5.6.3
- hệ điều hành: Windows
- giao thức: HTTPS

## 4. Các kịch bản kiểm thử

### 4.1 Thread Group 1 – Kịch bản cơ bản
- số lượng người dùng: 10
- số vòng lặp: 5
- hành vi: gửi HTTP GET đến trang chủ (/)

### 4.2 Thread Group 2 – Kịch bản tải nặng
- số lượng người dùng: 50
- ramp-up period: 30 giây
- hành vi: gửi HTTP GET đến trang chủ (/) và trang con (/thoi-su)

### 4.3 Thread Group 3 – Kịch bản tuỳ chỉnh
- số lượng người dùng: 20
- thời gian chạy: 60 giây
- hành vi: gửi HTTP GET đến các trang con (/kinh-doanh, /the-thao)

## 5. Kết quả kiểm thử

| Kịch bản | Avg Response Time (ms) | Throughput (request/s) | Error Rate |
|--------|------------------------|------------------------|------------|
| Basic Test | 1106 | 7.62 | 0% |
| Load Test  | 167  | 3.37 | 0% |
| Custom Test | 66 (trung bình) | 4.17 | 50% |

## 6. Phân tích và nhận xét
- ở kịch bản cơ bản, website phản hồi ổn định với thời gian phản hồi trung bình khoảng 1.1 giây và không ghi nhận lỗi
- ở kịch bản tải nặng với 50 người dùng đồng thời, thời gian phản hồi giảm do nội dung được cache, tuy nhiên throughput giảm do số lượng request lớn hơn
- ở kịch bản tuỳ chỉnh, do người dùng truy cập liên tục trong thời gian dài nên xuất hiện một số request lỗi (error rate 50%), nguyên nhân có thể do giới hạn truy cập (rate limiting) hoặc timeout từ phía server
- nhìn chung website vẫn hoạt động ổn định, không xảy ra lỗi nghiêm trọng làm gián đoạn toàn bộ hệ thống

## 7. Kết luận
Apache JMeter là công cụ hiệu quả để kiểm thử hiệu năng website. Thông qua các kịch bản khác nhau, có thể đánh giá được khả năng chịu tải và hành vi của hệ thống dưới các mức truy cập khác nhau.