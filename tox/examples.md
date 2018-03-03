### a simple tox.ini / default environments

Viết một file tox.ini chứa các thông tin cơ bản của project, file này đặt cùng thư mục với file setup.py

```
# content of: tox.ini , put in same dir as setup.py
[tox]
envlist = py27,py36
[testenv]
deps=pytest # or 'nose' or ...
commands=pytest  # or 'nosetests' or ...
```

Bạn cũng có thể tạo file tox.ini bằng cách `tox-quickstart` và trả lời các câu hỏi.


Để cài đặt mã nguồn và test project, bạn có thể gõ lệnh:

```
tox
```

Nếu muốn chạy một môi trường xác định, ví dụ `py36`:

```
tox -e py36
```

Một số tên môi trường mặc định :

```
py
py2
py27
py3
py34
py35
py36
py37
jython
pypy
pypy3
```


### Xác định platform

Nếu muốn xác định platform cho môi trường test của bạn, sử dụng các biểu thức chính quy như:

```
platform = linux2|darwin
```

Nếu giá trị platform không khớp với `sys.platform` thì nó được bỏ qua.

Các platform xem tại https://docs.python.org/2/library/sys.html#sys.platform

### Các lệnh không thuộc môi trường ảo

Thỉnh thoảng bạn muốn sử dụng một số công cụ không thuộc môi trường ảo như `make`, `bash`,...

Để tránh cảnh báo, bạn có thể sử dụng cấu hình  `whitelist_externals`:

```
# content of tox.ini
[testenv]
whitelist_externals = make
                      /bin/bash
```

### Các gói trong `requirements.txt` hoặc `constraints.txt`

Để cài đặt các gói được định nghĩa trong `requirements.txt` hoặc `constraints.txt`, bạn có thể thêm nó vào giá trị biến `desp`:

```
deps = -rrequirements.txt
```

hoặc

```
deps = -cconstraints.txt
```

hoặc

```
deps = -rrequirements.txt -cconstraints.txt
```

Lệnh `pip` sẽ được gọi để chạy `{toxinidir}/requirements.txt` hoặc `{toxinidir}/contrains.txt`.


### Sử dụng một url PyPI khác

Để cài đặt các gói phụ thuộc sử dụng PyPI server khác mặc định, bạn sử dụng option `-i`:

```
tox -i http://pypi.my-alternative-index.org
```

Hoặc có thể định nghĩa trong file `tox.ini`:

```
[tox]
indexserver =
    default = http://pypi.my-alternative-index.org
```

### Sử dụng nhiều PyPI server

Phân tích ví dụ:

```
[tox]
indexserver =
    DEV = http://mypypiserver.org

[testenv]
deps =
    docutils        # comes from standard PyPI
    :DEV:mypackage  # will be installed from custom "DEV" pypi url
```

Với cấu hình này, `docutils` sẽ được cài đặt sử dụng PyPI mặc định, còn `mypackage` sẽ sử dụng server DEV

### Tạo lại môi trường ảo

Để buộc tox tạo lại một môi trường ảo, sử dụng:

```
tox --recreate -e py27
```

### Bỏ qua một lệnh

Sử dụng tiền tố `-` trước lệnh cần bỏ qua

```
[testenv:py27]
commands = coverage erase
       {envbindir}/python setup.py develop
       coverage run -p setup.py test
       coverage combine
       - coverage html
       {envbindir}/flake8 loads
```




