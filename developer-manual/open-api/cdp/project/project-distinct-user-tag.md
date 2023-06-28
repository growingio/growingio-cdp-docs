---
id: project-distinct-user-tag
sidebar_position: 5
---

# 用户标签枚举值查询

## 接口说明

查询客户数据平台中某个用户标签的所有枚举值，比如性别的枚举值有：男、女、NULL。

## 接口地址

```
http://{api-host}/cdp/api/v2/projects/{projectId}/tags/{tagKey}/values?top={limit}
```

## 请求方式

GET

## 公共请求参数

[公共请求参数](../../../open-api#公共请求参数)

## 请求参数

| 名称      | 类型   | 必填 | 描述                                | 示例值   |
| --------- | ------ | ---- | ----------------------------------- | -------- |
| projectId | String | 是   | 搜索用户所在项目 ID                 | WlGk4Daj |
| tagKey    | String | 是   | 搜索的用户标签的标识符              | tag_123  |
| limit     | Int    | 否   | 最大返回条数。默认 100，最大值 1000 | 100      |

## 返回数据

| 名称       | 类型 | 描述     |
| ---------- | ---- | -------- |
| totalCount | Int  | 返回条数 |
| values     | List | 返回值   |

## 示例：根据项目 ID 和 用户标签=性别 搜索该标签的所有枚举值

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/cdp/api/v2/projects/WlGk4Daj/tags/tag_123/values?top=100'
--header 'Authorization: Bearer c2ff9aa1-1824-4cc7-a01f-4094293a6af9'
```

### 返回示例

```json
{
    "totalCount": "2",
    "values": [
        "男","女",NULL
    ]
}
```
