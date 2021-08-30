# Giới thiệu

Order API là RESTful API phục vụ cho việc tạo đơn đặt hàng với Ninja Van, và các thao tác khác như in nhãn đơn hàng hay huỷ đơn hàng.

#### Những lưu ý trong việc tích hợp API

* Vui lòng lưu access token vào database

* Khi gặp lỗi ***HTTP 500***, bạn có thể retry yêu cầu tạo đơn hàng

* Khi gặp lỗi ***HTTP 4xx***, hãy lưu lại kết quả trả về để debug
    * ***Không được*** retry cùng một yêu cầu tạo đơn hàng khi chưa sửa lỗi mô tả trong kết quả trả về

# Cấu hình chung

## Môi trường

| Môi trường | URL |
|-------------|----------|
| Production  | https://api.ninjavan.co/vn |
| Sandbox     | https://api-sandbox.ninjavan.co/sg |

# Webhooks

Ninja Van cung cấp webhook API dưới dạng ***PUSH*** để cập nhật trạng thái đơn hàng. 


Hiện nay, Ninja Van chưa hỗ trợ API để ***PULL*** trạng thái.
