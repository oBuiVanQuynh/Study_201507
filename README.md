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

Ruby Version | Grape | Rails::API
--- | --- | ---
`ruby 2.1.2p95` | dd | `Concurrency Level:      1`<br/>`Time taken for tests:   251.025 seconds`<br/>`Complete requests:      100000`<br/>`Failed requests:        0`<br/>`Write errors:           0`<br/>`Non-2xx responses:      100000`<br/>`Total transferred:      182900000 bytes`<br/>`HTML transferred:       156400000 bytes`<br/>`Requests per second:    398.37 [#/sec] (mean)`<br/>`Time per request:       2.510 [ms] (mean)`<br/>`Time per request:       2.510 [ms] (mean, across all concurrent requests)`<br/>`Transfer rate:          711.54 [Kbytes/sec] received`


 - Cách cài đặt:
  + Grape là 1 gem nên có thể cài đặt nó như 1 gem thông thường: `$ gem install grape`
  + Nếu sử dụng `Bundler` thêm `gem "grape"` vào `Gemfile` và chạy: `$ bundle install`
 
II. Grpe API
 1. Cách sử dụng cơ bảndd
  - `Grape APIs` là các ứng dụng `Rack` được tạo bởi lớp con `Grape::API`
  - Ví dụ về 1 lớp về việc `Grape` định nghĩa 1 số chức năng của `dd`<br>
    `class API::V1::TestsAPI < Grape::API`
       `resources :tests do`
         `get do`
           `Test.all`
         `end`
       `end`
     `end`
