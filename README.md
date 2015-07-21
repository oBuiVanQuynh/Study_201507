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
`ruby 2.1.2p95` | dd | `Concurrency Level:      1`<br/>`Time taken for tests:   1819.450 seconds`<br/>`Complete requests:      100000`<br/>`Failed requests:        0`<br/>`Write errors:           0`<br/>`Total transferred:      1115000000 bytes`<br/>`HTML transferred:       1069300000 bytes`<br/>`Requests per second:    54.96 [#/sec] (mean)`<br/>`Time per request:       18.194 [ms] (mean)`<br>`Time per request:       18.194 [ms] (mean, across all concurrent requests)`<br/>`Transfer rate:          598.46 [Kbytes/sec] received`



 - Cách cài đặt:
  + Grape là 1 gem nên có thể cài đặt nó như 1 gem thông thường: `$ gem install grape`
  + Nếu sử dụng `Bundler` thêm `gem "grape"` vào `Gemfile` và chạy: `$ bundle install`
 
II. Grpe API
 1. Cách sử dụng cơ bản
  - `Grape APIs` là các ứng dụng `Rack` được tạo bởi lớp con `Grape::API`
  - Ví dụ về 1 lớp về việc `Grape` định nghĩa 1 số chức năng của `dd`
   ```ruby
   class API::V1::TestsAPI < Grape::API
     version "v1", using: :header, vendor: "twitter"
      format :json
      prefix :api
  
      helpers do
        def current_user
        @current_user ||= User.authorize!(env)
      end
  
      def authenticate!
        error!("401 Unauthorized", 401) unless current_user
        end
      en
      
      resources :tests do
        get do
          Test.all
        end
      end
    end
   ```
 2. Mounting<br>
  a. Rack
  - Các mẫu trên tạo ra một ứng dụng `rack` nên có thể được chạy từ `config.ru` với rackup:
   ```ruby
    ENV['RACK_ENV'] ||= :production

    Bundler.require(:default, ENV['RACK_ENV']) if defined?(Bundler)
    require 'bundler/setup'
    
    lib_path = File.expand_path('../lib', __FILE__)
    $LOAD_PATH.unshift(lib_path) unless $LOAD_PATH.include?(acklib_path)
    
    require 'app'
    require 'api'
    
    run API::V1::TestsAPI.new
   ```
  b. Rails 
   - Với vị trí file tại `lib/api`, thì các `module` phải được nối chính xác với các `subdirectory`.Ví dụ với `TestAPI`   file là `lib/api/v1/test_api.rb` thì tên của `class` là `API::V1::TestsAPI`
   - Sửa `applicaton.rb`
    ```ruby 
     config.autoload_paths << Rails.root.join("lib")
    ```
   - Sửa `config/routes.rb`
    ```ruby
     mount API::V1::TestsAPI => "api"
    ```
   - Với version `Rails 4.0+` và các ứng dụng sử dụng `model` của `ActiveRecord` bạn có thể sử dụng                      [hashie-forbidden_attributes link](https://github.com/Maxim-Filimonov/hashie-forbidden_attributes) đẻ tắt tính năng    bảo mật của `strong_params` của `model layer`, cho phép sử dụng các `params` riêng
   ```ruby
    # Gemfile
    gem "hashie-forbidden_attributes"
   ```
  c. Modules
   - Ta có thể `mount` nhiều `API` thành phần cùng nhau có thể là các phiên bản khác nhau
    ```ruby
    class API::V1 < Grape::API
      version "v1", using: :path
      desc "Returns the current API version, v1."
      get do
        {version: "v1"}
      end
      mount TestsAPI
    end
   ```
   ```ruby
    class API < Grape::API
      format :json
      helpers do
        def render_api_error!(message, status)
          error!({message: message}, status)
        end
      end
      mount API::V1
    end
   ```
