# Giới thiệu

Order API là RESTful API phục vụ cho việc tạo đơn đặt hàng với Ninja Van, và các thao tác khác như in nhãn đơn hàng hay huỷ đơn hàng.

# Yêu cầu khi tích hợp API
Xin hãy lưu ý những điểm sau cho việc tích hợp

## API tạo mã xác thực OAuth
Ninja Van yêu cầu đối tác lưu lại mã xác thực vào bộ nhớ cache để sử dụng nhiều lần.

***Hãy đảm bảo quy trình sau đây trong quá trình tích hợp***:
* Tạo mã xác thực (tham khảo API bên dưới).
* Lưu mã trong bộ nhớ database hoặc bộ nhớ cache và đồng thời lưu lại thời gian hết hạn.
* Đính kèm mã xác thực dưới dạng bearer trong mọi yêu cầu API đến Ninja Van.
    * Nghĩa là giá trị trong `Authorization` HTTP header là `Bearer <ACCESS TOKEN>`.
* 5 phút trước khi đến thời gian hết hạn hoặc nếu yêu cầu đến Ninja Van API được phản hồi với lỗi ***HTTP 401***, hãy tạo mã xác thực mới.

***LƯU Ý:*** Thời gian hiệu lực của mã xác thực là không cố định và có thể thay đổi theo thời gian.

## API tạo đơn và API huỷ đơn
* Đối tác được khuyến khích thử lại các yêu cầu tạo đơn hàng NẾU có lỗi ***HTTP 5xx*** trả về từ API.
* Nếu gặp lỗi ***HTTP 4xx***, hãy lưu lại kết quả trả về cho mục đích gỡ lỗi của bạn.
* Vui lòng ***KHÔNG*** thử lại cùng một yêu cầu tạo đơn hàng mà chưa sửa lỗi được chỉ định trong phản hồi.

## API in nhãn đơn hàng
Nếu đối tác cần quyền truy cập vào API in nhãn đơn hàng, xin lưu ý rằng quyền truy cập vào API này cần yêu cầu thêm.
Đối tác ***phải*** lưu lại nhãn đơn hàng vào bộ nhớ cache sau khi tạo để tránh gọi quá nhiều đến API này.

# Cách xin quyền truy cập Production
Ninja Van cần thực hiện đánh giá tích hợp trước khi cấp cho đối tác quyền truy cập vào API trên Production.
* Vui lòng gửi 3 đơn đặt hàng khác nhau, nội dung tương tự loại đơn đặt hàng bạn sẽ gửi trong môi trường thật, với địa chỉ chính xác cùng các thông tin khác.
* Gửi email cho Ninja Van tại devsupport@ninjavan.co kèm theo mã vận đơn của các đơn đặt hàng đó và các yêu cầu nghiệp vụ, chúng tôi sẽ kiểm tra.

# Môi trường tích hợp

| Môi trường | Base URL | URL có mã quốc gia |
|-------------|----------|----------|
| Production  | https://api.ninjavan.co | https://api.ninjavan.co/VN
| Sandbox     | https://api-sandbox.ninjavan.co | https://api-sandbox.ninjavan.co/SG |

***LƯU Ý:*** Vui lòng gửi tất cả các API thử nghiệm đến môi trường Sandbox Singapore. Tuy nhiên, nội dung API có thể chứa địa chỉ và thông tin của Việt Nam.

Nói cách khác, bạn có thể tạo yêu cầu API trên môi trường Sandbox như cách bạn sẽ làm trên môi trường Production; sự khác biệt duy nhất là URL.
