# Intergate-django-with-graylog
Intergate django with graylog

Sử dụng thư viện `graypy`

### 1. Install graypy

```
soure env/bin/active
pip install graypy
```

### 2. Setup 

Tại file `setting.py` của `django`

```
LOGGING = {
    # ...
    'handlers': {
        # ...
        'gelf': {
            'class': 'graypy.GELFHandler',
            'host': 'graylog2.example.com',
            'port': 12201,
        },
    },
    # ...
    'loggers': {
        'django.request': {
            'handlers': ['mail_admins', 'console', 'graypy'],
            'level': 'ERROR',
            'propagate': True,
        },
        '': {
            'handlers': [
                'console', 'sentry', 'graypy', 'servers_file'
            ],
            'level': "INFO",
        },
    }
    
}
```

### 3. Setting Graylog

- Đăng nhập vào `Graylog`. Tại giao diện của `Graylog`

`System` -> `Inputs`

ảnh 1

- Tại màn inputs, tại `Select input` -> `GELF UDP` -> `Launch new input` 

ảnh 2


- Nhập các thông số như sau và `Save`

ảnh 3

### 4. Kiểm tra lại

- Thực hiện một số action để xuất hiện log trên `django` và kiểm tra tại `graylog`

ảnh 4



### Tham khảo

https://www.caktusgroup.com/blog/2013/09/18/central-logging-django-graylog2-and-graypy/
