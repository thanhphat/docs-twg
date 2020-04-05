---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:

search: true
---

# Introduction

Server URL: [https://api.twghealthcare.com](https://api.twghealthcare.com)

# DS Tỉnh thành

```shell
curl "https://api.twghealthcare.com/api/v1/address_locations"
```

> Lệnh trên trả về JSON chứa các tỉnh/thành phố trên toàn quốc

```shell
curl "https://api.twghealthcare.com/api/v1/address_locations?parent=50"
```
> Lệnh trên trả về JSON chứa các quận/huyện trực thuộc thành phố Hồ Chí Minh có cấu trúc như thế này:

```json
[
  {
    "id": 634,
    "name": "Huyện Bình Chánh",
    "level": 1,
    "parent_id": 50
  },
  {
    "id": 636,
    "name": "Huyện Cần Giờ",
    "level": 1,
    "parent_id": 50
  }
]
```

### HTTP Request

`GET {{server}}/api/v1/address_locations?parent=50`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
parent | - | Truyền vào Id của 1 cơ sở hành chính để lấy các cơ sở hành chính con
level | - | Gán là 0 nếu muốn lấy danh sách các tỉnh của cả nước, 1 là quận/huyện, 2 là phường/xã

# Đăng ký user

```shell
curl --location --request POST 'https://api.twghealthcare.com/user_auth' \
--header 'Content-Type: application/json' \
--data-raw '{
    "email": "test@gmail.com",
    "password": "123456",
    "password_confirmation": "123456",
    "confirm_success_url": "http://www.benhvientwg.vn/"
}'
```
> Lệnh trên trả về JSON có cấu trúc như thế này:

```json
{
    "status": "success",
    "data": {
        "id": 3,
        "provider": "email",
        "uid": "test@gmail.com",
        "allow_password_change": false,
        "full_name": null,
        "username": null,
        "phone_number": null,
        "gender": null,
        "day_of_birth": null,
        "email": "test@gmail.com",
        "created_at": "2020-04-04T08:12:55.950Z",
        "updated_at": "2020-04-04T08:12:55.950Z"
    }
}
```

### HTTP Request

`POST {{server}}/user_auth`

### Body Parameters

Parameter | Description
--------- | -----------
email | Email của user đăng ký
password | password do người dùng chọn
password_confirmation | sử dụng lại value password ở trên để truyền
confirm_success_url | Hiện tại gắn mặc định là http://www.benhvientwg.vn/