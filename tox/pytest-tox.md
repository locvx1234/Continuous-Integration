Pytest là một framework giúp bạn dễ dàng viết các bài test nhỏ, nhưng vẫn có khả năng mở rộng cho những ứng dụng phức tạp.

Pytest dễ dàng tích hợp với tox.

### Ví dụ cơ bản

```
[tox]
envlist = py35,py36

[testenv]
deps = pytest               # PYPI package providing pytest
commands = pytest {posargs} # substitute with tox' positional arguments
```

### Sử dụng nhiều CPUs cho bài test

Với những bài test lớn, để nhanh hơn cần dùng nhiều CPUs để xử lý.

`pytest` hỗ trợ điều này bằng việc sử dụng plugin `pytest-xdist`

Ví dụ:

```
[testenv]
deps=pytest-xdist
changedir=tests
commands= pytest --basetemp={envtmpdir}  \
                 --confcutdir=..         \
                 -n 3                    \ # use three sub processes
                 {posargs}
```


