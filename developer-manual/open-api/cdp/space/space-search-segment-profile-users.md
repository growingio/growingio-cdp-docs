---
id: space-search-segment-profile-users
sidebar_position: 6
---

# 群体画像用户列表查询

## 接口说明

查询空间指定群体画像的用户特征

## 接口地址

```
http://{api-host}/v1/api/projects/{projectId}/spaces/{spaceId}/segment_profiles/{segmentKey}/users
```

## 请求方式

GET

## 公共请求参数

[公共请求参数](../../../open-api#公共请求参数)

## 请求参数

| 名称       | 类型   | 必填 | 描述                | 示例值         |
| ---------- | ------ | ---- | ------------------- | -------------- |
| projectId  | String | 是   | 群体画像所在项目 ID | WlGk4Daj       |
| spaceId    | String | 是   | 群体画像所在空间 ID | VKwkPmqX       |
| segmentKey | String | 是   | 群体画像标识符      | seg_51activity |

## 查询参数

| 名称         | 类型   | 必填 | 描述                                                                          | 示例值            |
| ------------ | ------ | ---- | ----------------------------------------------------------------------------- | ----------------- |
| limit        | Int    | 否   | 单次查询返回数据上限<br></br>最大值为 1,000<br></br>默认值为 1,000            | 1000              |
| offset       | Int    | 否   | 查询标识位，默认值为 0                                                        | 0、10000、20000   |
| properties[] | String | 否   | 查询的用户身份、用户属性、用户标签<br></br>最大查询 20 个，超过上限后查询失败 | id\_$basic_userId |

## 返回数据

| 名称            | 类型      | 描述                                            |
| --------------- | --------- | ----------------------------------------------- |
| limit           | Int       | 单次查询返回数据上限                            |
| offset          | Int       | 查询标识位                                      |
| totalCount      | Int       | 本次查询总计返回数据量                          |
| hasNextPage     | Bool      | 是否有下一页<br></br>false：否<br></br>true：是 |
| hasPreviousPage | Bool      | 是否有上一页<br></br>false：否<br></br>true：是 |
| values          | Objective | 群体画像查询数据                                |

### values 数据

| 名称            | 类型              | 描述                         |
| --------------- | ----------------- | ---------------------------- |
| gioId           | Int               | GrowingIO 系统生成的用户标示 |
| identifications | < String , List > | 查询的用户身份值             |
| properties      | Objective         | 查询的用户属性和用户标签值   |

## 示例 1：群体画像标识符不存在

场景：搜索 **未定义** 的群体画像 **seg_undefine** 的用户 ID，单次查询返回数据上限为 100，标识位为 0。

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/v1/api/projects/WlGk4Daj/segment_profiles/seg_undefine/users?limit=100&offset=0&properties[]=ids_$basic_userId'
--header 'Authorization: Bearer c2ff9aa1-1824-4cc7-a01f-4094293a6af9'
```

### 返回示例

```json
Internal Server Error
```

## 示例 2：搜索条件未输入用户身份、用户属性、用户标签

场景：搜索 群体画像 **seg_51activity** ,单次查询返回数据上限为 100，标识位为 0。

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/v1/api/projects/WlGk4Daj/segment_profiles/seg_51activity/users?limit=100&offset=0'
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

场景：搜索 群体画像 **seg_51activity** 的用户 ID、性别、RFM 标签,单次查询返回数据上限为 100，标识位为 100。

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/v1/api/projects/WlGk4Daj/segment_profiles/seg_51activity/users?limit=100&offset=100&properties[]=ids_$basic_userId&properties[]=usr_gender&properties[]=tag_rfm'
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
