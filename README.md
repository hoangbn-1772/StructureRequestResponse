# Structure of HTTP Request and Response

## HTTP Request
- Để bắt đầu trao đổi dữ liệu, client khởi tạo một HTTP secsion bằng cách mở một kết nối TCP đến HTTP server sau đó gửi request đến server này.
- Một HTTP client gửi một HTTP request tới server theo định dạng sau:

<img src="images/form_request.png"/>

### Request-Line
- Request-Line bao gồm 3 thông tin:
	+ Method: Là phương thức mà HTTP Request này sử dụng, thường là GET, POST, ngoài ra còn một số phương thức khác như HEAD, PUT, DELETE, OPTION, CONNECT.
		+ GET: request lấy dữ liệu
		+ POST: Sử dụng để gửi một entity đến resource được chỉ định, thường gây ra thay đổi về state hoặc tác dụng phụ lên máy chủ.
		+ PUT: Sửa đổi dữ liệu
		+ DELETE: Xóa dữ liệu được chỉ định
		+ HEAD: Yêu cầu response giống như GET nhưng không có response body.
		...
	+ URI: Là địa chỉ định danh của tài nguyên. Hiểu đơn giản, URL là đường dẫn. Trong trường hợp Request không yêu cầu tài nguyên cụ thể, URI có thể là dấu *.
	+ HTTP version: Là phiên bản HTTP đang sử dụng.

### Request Header
- Request-header cho phép client thêm các thông tin bổ sung về HTTP Request và về chính Client. Các trường này đóng vai trò là công cụ sửa đổi request.
- Request header tuân theo cùng cấu trúc cơ bản của HTTP header: Chuỗi không phân biệt hoa thường theo sau là dấu hai chấm (':') và giá trị có cấu trúc phụ thuộc vào header.
- Có rất nhiều Request header có sẵn, chúng có thể được chia thành nhiều nhóm:
	+ General headers: Như Via, áp dụng cho toàn bộ message
	+ Request headers: Như User-Agent, Accept-Type sửa đổi request bằng cách chỉ định thêm (như Accept-Language), bằng cách đưa ra bối cảnh (như Referer) hoặc bằng cách hạn chế có điều kiện (If-None)
	+ Entity headers: Như Content-Lenght áp dụng cho body của request (Không có body sẽ không có header đó)

<img src="images/request_header.png"/>

- Danh sách một số Request-header quan trọng:
	+ Accept: Loại bỏ nội dung có thể nhận được từ thông điệp response. Ví dụ: text/plain, text/html...
	+ Accept-Encoding: Các kiểu nén được áp dụng. Ví dụ: gzip, xz, exi...
	+ Connection: Tùy chọn điều khiển cho kết nối hiện thời. Ví dụ: Keep alive, Upgrade...
	+ Cookie: Thông tin HTTP Cookie từ server
	+ User-Agent: thông tin về user agent của người dùng.

### Body
- Là thành phần cuối cùng của request. Có thể có hoặc không tùy thuộc vào request, thường dùng với POST request. Các request như GET, HEAD, DELETE hay OPTIONS thường không cần.
- Body có thể được chia làm 2 loại:
	+ Single-resource bodies: Bao gồm một tệp duy nhất, được xác định bởi hai tiêu đề: Content-Type và Content-Lenght.
	+ Multiple-resource bodies: Bao gồm một multipart body, mỗi phần chứa một thông tin khác nhau.

## HTTP Response
- Cấu trúc của HTTP response gần giống với HTTP Request, chỉ khác nhau Request-Line với HTTP request và Status-Line với HTTP-Response.

<img src="images/http_response.png"/>

### Status-Line
- Status-Line cũng có 3 phần như sau:
	+ HTTP-version: Phiên bản HTTP cao nhất mà server hỗ trợ.
	+ Status-Code: Mã kết quả trả về
	+ Reason-Phrase: Mô tả về Status-Code

- Status-Code thông dụng mà server trả về cho client như sau:
	+ 1xx: Information Message: Các status-code dạng này chỉ có tính chất tạm thời, client có thể không quan tâm.
	+ 2xx: Successful: Khi đã xử lý thành công request của client, server sẽ trả về status dạng này.
		+ 200 OK: request thành công.
		+ 202 Accepted: request đã được nhận, nhưng không có kết quả nào trả về, thông báo cho client tiếp tục chờ đợi.
		+ 204 No Content: request đã được xử lý nhưng không có thành phần nào được trả về.
		+ 205 Reset: Giống như 204 nhưng mã này còn yêu cầu client reset lại document view


## Tài liệu tham khảo
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages
- https://www.stdio.vn/articles/http-request-va-http-response-202
