# Study_201507
I. Giới thiệu GRAPE-API
 1. API là gì?
 - Một API (Application Programming Interface) là một giao diện mà một hệ thống máy tính hay ứng dụng cung cấp để cho     phép các yêu cầu dịch vụ có thể được tạo ra từ các chương trình máy tính khác, và/hoặc cho phép dữ liệu có thể được trao  đổi qua lại giữa chúng
 - Một trong các mục đích chính của một API là cung cấp khả năng truy xuất đến một tập các hàm hay dùng. Một API tốt      thường cung cấp một "hộp đen" hay là một lớp trừu tượng (abstraction layer) bao bọc nó, nhằm đảm bảo là nhà lập trình    không thể biết cách hiện thực cụ thể bên trong của mỗi hàm trong API.
 - Có hai dòng chính sách đối với việc công bố các APIs:
  + Một số công ty không công bố cái APIs của họ mà chỉ những nhà phát triển đăng kí mới được phép sử dụng nhằm năng      cao doanh thu của họ
  + Một số công ty thì cung cấp miễn phí APIs họ cho những nhà phát triển có thể sử dụng mà không cần mất phí
 2. Giới thiệu về Grape-API
 - Grape là một REST-like API micro-framework cho Ruby. Nó được thiết kế để chạy trên Rack hoặc bổ sung cho mô hình ứng dụng web hiện có như Rails và Sinatra bằng việc cung cấp một DSL đơn giản để dễ dàng phát triển các RESTful API
 - Grape có ưu điểm so với `rails-api` là 
  + Khả năng phát triển nhanh đơn giản có thể dụng cùng ruby on rails hoặc sử dụng độc lập
  + Linh hoạt trong quản lý `version`(điều quan trọng đối với các `api`)
  + Có tốc độ xử lý cao hơn so với `rails-api`
 Một số kết quả so sánh giữa `grape-api` và `rails-api`

Markdown | Less | Pretty
--- | --- | ---
