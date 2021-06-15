# Mô tả tổng quát


# Yêu cầu bảo mật

Các thông tin của The Coffee House luôn được bảo mật ở mức độ tối đa nhất. Hệ thống API của The Coffee House sử dụng kết hợp cùng lúc cả 3 phương thức sau đây để bảo mật API và các dữ liệu có liên quan:

### Sử dụng giao thức HTTPS
Giao thức HTTPS giúp đảm bảo các tính chất sau của thông tin:

* <b>Confidentiality</b>: sử dụng phương thức mã hóa (encryption) để đảm bảo rằng các thông điệp được trao đổi giữa server-side của The Coffee House và server-side của Haraworks không bị bên thứ ba đọc được.

* <b>Integrity</b>: sử dụng phương thức hashing để cả The Coffee House và Haraworks đều có thể tin tưởng rằng thông điệp mình nhận được không bị mất mát hay chỉnh sửa.

* <b>Authenticity</b>: sử dụng chứng chỉ số (digital certificate) để giúp The Coffee House và Haraworks tin tưởng rằng tài nguyên mà mình đang truy cập là chính xác và không bị giả mạo.


### Xác thực quyền truy cập API bằng API Key

* ##### <b>Xác thực quyền truy cập API của The Coffee House</b>
The Coffee House sẽ cung cấp API Key cho Haraworks để thực hiện cơ chế xác thực khi server-side của Haraworks gửi request truy vấn thông tin đến các API của The Coffee House.

* ##### <b>Xác thực quyền truy cập API của Haraworks</b>
Haraworks sẽ cung cấp API Key cho The Coffee House để thực hiện cơ chế xác thực khi server-side của The Coffee House gửi request truyền thông tin đến Webhook hoặc API của Haraworks khi có sự kiện rating xảy ra từ App của The Coffee House.


### Sử dụng mã hóa 2 lớp

Hệ thống API của The Coffee House sử dụng phương thức mã hóa 2 lớp phổ biến nhất để mã hóa một số thông tin quan trọng của cả The Coffee House và các đối tác bao gồm các quá trình được mô tả như sau:

#### Thiết lập cơ chế mã hóa và giải mã chung

* Haraworks tạo một một cặp khóa RSA 2048-bit bao gồm Public Key và Private Key.
* The Coffee House nhận Public Key từ Haraworks để sử dụng cho việc mã hóa các thông tin cần thiết trước khi gửi đi.
* Haraworks sử dụng Private Key để giải mã các thông tin đã được mã hóa bởi The Coffee House.

#### Quá trình mã hóa dữ liệu tại server-side của The Coffee House

* <b>Sử dụng thuật toán mã hóa đối xứng AES</b>
  * Thuật toán AES khá phổ biến và có ưu điểm là mã hóa khối lượng dữ liệu lớn với tốc độ tương đối nhanh, ít tiêu tốn tài nguyên của hệ thống và có độ bảo mật cao.
  * Tại mỗi request gửi đến hệ thống API của The Coffee House sẽ có một session key có độ dài 128-bit được sinh ra ngẫu nhiên từ server-side của The Coffee House.
  * Các dữ liệu của The Coffee House sẽ sử dụng dụng giải thuật AES với session key để mã hóa trước khi gửi đến server-side của Haraworks.
* <b>Sử dụng thuật toán mã hóa bất đối xứng RSA</b>
  * Thuật toán RSA có độ bảo mật cao và được sử dụng rộng rãi, có tốc độ mã hóa nhanh đối với khối lượng dữ liệu đầu vào nhỏ nhưng chậm hơn AES khá nhiều nếu khối lượng dữ liệu cần mã hóa lớn.
  * Server-side của The Coffee House sử dụng thuật toán mã hóa RSA dùng Public Key được lưu tại server-side của The Coffee House để mã hóa session key.
  * Session key đã được mã hóa bằng RSA cùng các các dữ liệu đã được mã hóa bằng AES sẽ được gửi đến server-side của Haraworks.

#### Quá trình giải mã dữ liệu tại server-side của Haraworks

* Server-side của Haraworks sử dụng thuật toán RSA dùng Private Key được lưu tại server-side của Haraworks để giải mã session key đã được mã hóa nhận được từ server-side của The Coffee House.
* Session key đã giải mã bằng thuật toán RSA sẽ được sử dụng để tiếp tục giải mã các dữ liệu được mã hóa bằng thuật toán AES tại server-side của The Coffee House.


# Mô tả chi tiết
### Thông tin chung cơ bản
* Staging API URL: https://partner.thecoffeehouse.com/
* API Request Method: POST method
* Request timeout: 20s
* Xử lý timeout: trả về response status code là 418 (Request Timeout)
