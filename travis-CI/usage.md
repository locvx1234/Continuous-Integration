Sử dụng tài khoản Github để đăng nhập :

- [Travis-CI.org](https://travis-ci.org/) cho các repo public
- [Travis-CI.com](https://travis-ci.com/) cho các repo private

và chấp nhận xác thực.

Nháy vào dấu cộng `+` và nhấp vào project cần test.

![]()

![]()

Kiểm tra tra Github có tích hợp Travis chưa:

Vào project cần test, *Setting/Integrations & services*.
Trong danh sách các service nếu có Travis CI rồi thì ok, nếu chưa có thì chọn `Add service` và chọn `Travis CI`

![]()

Bước tiếp theo là tạo một file `.travis.yml` trong project của bạn và cấu hình để gọi để chương trình test.

Theo dõi log ở trang https://travis-ci.org hoặc https://travis-ci.com mỗi khi code có sự thay đổi trên nhánh được cấu hình.
