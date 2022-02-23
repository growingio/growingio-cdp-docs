---
id: dc-search-user
sidebar_position: 1
---

# 客户数据平台-单用户查询

## 接口说明

查询客户数据平台指定用户特征

## 接口地址

```
http://{api-host}/v1/api/users/{user_key}/{search_ID}
```

## 请求方式

GET

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| user_key  | String | 是   | 搜索的用户身份标识符 | $basic_userId |
| search_ID | String | 是   | 搜索的用户身份值     | U3803180317   |

## 返回数据

| 名称            | 类型      | 描述                             |
| --------------- | --------- | -------------------------------- |
| gioId           | Int       | GrowingIO 系统生成的用户标示     |
| identifications | < String , List > | 系统用户的全部用户身份值         |
| properties      | Objective | 系统用户的全部用户属性和用户标签 |

## 示例 1：根据用户ID搜索用户

场景：搜索 **用户 ID** 为 **U3803180317** 用户的全部用户身份、用户属性和用户标签

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/v1/api/users/$basic_userId/U3803180317'
--header 'Authorization: Bearer c2ff9aa1-1824-4cc7-a01f-4094293a6af9'
```

### 返回示例

```json
{
    "gioId": "13831",
    "identifications": {
        "ids_$basic_userId": ["U3803180317"],
        "ids_$anonymous_user": ["X","Y"]
    },
    "properties": {
        "usr_$basic_name": "陈一一",
        "usr_age": "28",
        "usr_address": null,
        ...
        "tag_30day_payment_sum": "3519.3",
        "tag_RFM_level": "高",
        "tag_last_buy": null,
        ...
    }
}
```

## 示例 2：根据设备ID搜索用户

场景：搜索 **设备 ID** 为 **X** 用户的全部用户身份、用户属性和用户标签

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/v1/api/users/$anonymous_user/X'
--header 'Authorization: Bearer c2ff9aa1-1824-4cc7-a01f-4094293a6af9'
```

### 返回示例

```json
{
    "gioId": "13831",
    "identifications": {
        "ids_$basic_userId": ["U3803180317"],
        "ids_$anonymous_user": ["X","Y"]
    },
    "properties": {
        "usr_$basic_name": "陈一一",
        "usr_age": "28",
        "usr_address": null,
        ...
        "tag_30day_payment_sum": "3519.3",
        "tag_RFM_level": "高",
        "tag_last_buy": null,
        ...
    }
}
```

## 示例 3：搜索用户不存在

场景：搜索用户不存在

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/v1/api/users/$anonymous_user/Z'
--header 'Authorization: Bearer c2ff9aa1-1824-4cc7-a01f-4094293a6af9'
```

### 返回示例

```json
{
  "gioId": "0",
  "identifications": {},
  "properties": {}
}
```
