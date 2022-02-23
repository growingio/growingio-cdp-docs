---
id: dc-search-user-tag-users
sidebar_position: 3
---

# 客户数据平台-用户标签用户列表查询

## 接口说明

查询客户数据平台指定用户标签覆盖用户的用户特征

## 接口地址

```
http://{api-host}/v1/api/user_tags/{tag_key}/users
```

## 请求方式

GET

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| tag_key | String | 是   | 用户标签标识符 | tag_rfm |

## 查询参数

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| limit  | Int | 否   | 单次查询返回数据上限<br></br>最大值为1,000<br></br>默认值为1,000 | 1000 |
| offset | Int | 否   | 查询标识位，默认值为0 | 0、10000、20000 |
| properties[] | String | 否 | 查询的用户身份、用户属性、用户标签<br></br>最大查询20个，超过上限后查询失败 | id_$basic_userId |

## 返回数据

| 名称            | 类型      | 描述                             |
| --------------- | --------- | -------------------------------- |
| limit | Int | 单次查询返回数据上限  |
| offset | Int | 查询标识位  |
| totalCount | Int | 本次查询总计返回数据量 |
| hasNextPage | Bool | 是否有下一页<br></br>false：否<br></br>true：是 |
| hasPreviousPage | Bool | 是否有上一页<br></br>false：否<br></br>true：是 |
| values | Objective | 群体画像查询数据 |

### values数据

| 名称            | 类型      | 描述                             |
| --------------- | --------- | -------------------------------- |
| gioId | Int | GrowingIO 系统生成的用户标示 |
| identifications | < String , List > | 查询的用户身份值 |
| properties | Objective | 查询的用户属性和用户标签值 |

## 示例 1：用户标签标识符不存在

场景：搜索 **未定义** 的用户标签 **tag_rfm** 的用户ID，单次查询返回数据上限为100，标识位为0。

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/v1/api/user_tags/tag_rfm/users?limit=100&offset=0&properties[]=ids_$basic_userId'
--header 'Authorization: Bearer c2ff9aa1-1824-4cc7-a01f-4094293a6af9'
```

### 返回示例

```json
Internal Server Error
```

## 示例 2：搜索条件未输入用户身份、用户属性、用户标签

场景：搜索 群体画像 **tag_rfm** ,单次查询返回数据上限为100，标识位为0。

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/v1/api/user_tags/tag_rfm/users?limit=100&offset=0'
--header 'Authorization: Bearer c2ff9aa1-1824-4cc7-a01f-4094293a6af9'
```

### 返回示例

```json
{
    "offset": 0.0,
    "limit": 100.0,
    "totalCount": 100.0,
    "hasNextPage": true,
    "hasPreviousPage": false,
    "values": [
        {
            "gioId": "603542",
            "identifications": {},
            "properties": {}
        },
        {
            "gioId": "605419",
            "identifications": {},
            "properties": {}
        },
        ... 
        ]
}
```

## 示例 3：搜索群体画像用户列表，并输入用户身份、用户属性、用户标签

场景：搜索 群体画像 **tag_rfm** 的用户ID、性别、RFM标签,单次查询返回数据上限为100，标识位为100。

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/v1/api/user_tags/tag_rfm/users?limit=100&offset=100&properties[]=ids_$basic_userId&properties[]=usr_gender&properties[]=tag_rfm'
--header 'Authorization: Bearer c2ff9aa1-1824-4cc7-a01f-4094293a6af9'
```

### 返回示例

```json
{
    "offset": 100.0,
    "limit": 100.0,
    "totalCount": 100.0,
    "hasNextPage": true,
    "hasPreviousPage": true,
    "values": [
        {
            "gioId": "603542",
            "identifications": {
                "id_$basic_userId": ["C001"]
                },
            "properties": {
                "usr_gender":"男",
                "tag_rfm": null
            }
        },
        {
            "gioId": "605419",
            "identifications": {
                "id_$basic_userId": ["C004"]
                },
            "properties": {
                "usr_gender": null,
                "tag_rfm": "低"
            }
        },
        ... 
        ]
}
```