
## tox là gì ?

tox là một công cụ dòng lệnh để test và managerment các virtualenv. Nó có thể được sử dụng cho:

- Kiểm tra các package được cài đặt đúng với các phiên bản Python khác nhau.
- Chạy các bài test trên từng môi trường, với các công cụ test mà bạn lựa chọn.
- Đóng vai trò như font-end của Continuous Integration server.

## Tính năng

Tự động hóa các hoạt động thử nghiệm liên quan đến Python

Kiểm tra các package Python có phù hợp trên các trình thông dịch và cấu hình khác nhau

Hệ thống plugin có thể liên kết với các hook.

Tương thích với các phiên bản Python và các platform (Windows, Unix)

Tích hợp được với các CI-server như Jenkins

Khả năng tương tác đầy đủ với devpi:

Điều khiển bởi một tập tin cấu hình ini đơn giản


## Cài đặt

Cài bằng pip:

```
pip install tox
```

Cài bằng source:
```
git clone https://github.com/tox-dev/tox
cd tox
python setup.py install
```

## Cấu hình

File `tox.ini` sử dụng chuẩn [ConfigParser](https://docs.python.org/3/library/configparser.html)

### Cài đặt các biến tox global:

```
[tox]
minversion=ver    # phiên bản tox tối thiểu
toxworkdir=path   # thư mục làm việc, mặc định {toxinidir}/.tox
setupdir=path     # mặc định {toxinidir}
distdir=path      # mặc định {toxworkdir}/dist
distshare=path    # mặc định {homedir}/.tox/distshare
envlist=ENVLIST   # mặc định là tất cả các môi trường
skipsdist=BOOL    # mặc định là false
```

Để xem cấu hình tox :

```
tox --showconfig
```

tox tự động phát hiện nếu biến `JENKINS_URL` được cài đặt và nó sẽ thực hiện môi trường test

```
[tox:jenkins]
...               # override [tox] settings for the jenkins context
# note: for jenkins distshare defaults to ``{toxworkdir}/distshare`` (DEPRECATED)
```

#### `skip_missing_interpreters=BOOL`

Nếu đặt là `True` thì khi test nó sẽ bỏ qua nếu trình thông dịch đó chưa có.
Điều này hữu ích trong quá trình phát triển phần mềm, khi bạn không có đủ tất cả các môi trường, bạn chỉ có thể test được với một vài môi trường thôi.
Và bạn chắc sẽ không muốn bị thông báo là không vượt qua bài test mãi chỉ vì không test qua đủ môi trường.

Mặc định của biến này là `False`

#### `envlist=CSV`

Danh sách các môi trường để tox hoạt động.

Nó được chỉ ra trong:

- Dòng lệnh là -eENVLIST
- Biến môi trường là TOXENV
- File `tox.ini` là `envlist`

### Virtualenv test environment settings

Test environment được định nghĩa bởi :

```
[testenv:NAME]
...
```

Các setting mặc định được tìm kiếm trong

```
[testenv]
...
```

Các setting có thể sử dụng trong 2 phần bên trên :

#### basepython=NAME-OR-PATH

Tên của bộ thông dịch Python. Mặc định là python mặc định

#### commands=ARGVLIST

Lệnh để gọi để việc test.

Mỗi lệnh được viết trên một hoặc nhiều dòng. Nếu lệnh nhiều dòng thì cuối dòng là dấu `\`

#### install_command=ARGV

Cài đặt các package trong virtual environment

Mặc định tox sử dụng pip để cài đặt gói. Bạn có thể thay đổi lệnh cài đặt ở biến này.

Ví dụ thay đổi lệnh pip để sử dụng các option `--find-links` và `--no-index`

```
[testenv]
install_command = pip install --pre --find-links http://packages.example.com --no-index {opts} {packages}
```

#### list_dependencies_command

Liệt kê các package được cài đặt trong virtual environment

Mặc định :

```
pip freeze
```

#### changedir=path

Thay đổi thư mục làm việc khi thực thi lệnh test.

Mặc định là `{toxinidir}`

#### deps=MULTI-LINE-LIST

Những phụ thuộc được cài đặt vào môi trường trước khi cài đặt các package

#### setenv=MULTI-LINE-LIST

Mỗi dòng chứa một cặp biến môi trường NAME=VALUE, nó sẽ sử dụng cho tất cả các lệnh test và cài đặt các package nguồn vào môi trường ảo.

Còn nhiều cấu hình khác, xem thêm http://tox.readthedocs.io/en/latest/config.html
