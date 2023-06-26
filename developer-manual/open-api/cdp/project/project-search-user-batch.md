---
id: project-search-user
sidebar_position: 6
---

# 多用户标签值查询

## 接口说明

查询客户数据平台中多个用户的标签值

## 接口地址

```
http://{api-host}/cdp/api/v2/projects/{projectId}/tags/{tagKey}/users
```

## 请求方式

POST

## 公共请求参数

[公共请求参数](../../../open-api#公共请求参数)

## 请求参数

| 名称          | 类型   | 必填 | 描述                 | 示例值        |
| ------------- | ------ | ---- | -------------------- | ------------- |
| projectId     | String | 是   | 搜索用户所在项目 ID  | WlGk4Daj      |
| tagKey   | String | 是   | 搜索的用户标签的标识符| tag_123 |
| identityKey   | String | 是   | 搜索的用户身份| $basic_userId |
| identityValues | List | 是   | 搜索的多个用户ID，支持最多1000个用户     |  ["u001","u002"] |

## 返回数据

| 名称            | 类型              | 描述                             |
| --------------- | ----------------- | -------------------------------- |
| totalCount           | Int               | 返回条数     |
| values | List | 返回批量用户数据        |

### 返回数据values中用户数据的结构
| 名称            | 类型              | 描述                             |
| --------------- | ----------------- | -------------------------------- |
| identityValue           | String               | 用户ID     |
| tagValue | Object | 用户标签值        |


## 示例 1：根据项目 ID 和用户 ID 搜索用户

场景：搜索 **用户 ID** 为 **U3803180317** 用户的全部用户身份、用户属性和用户标签

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/cdp/api/v2/projects/WlGk4Daj/tags/tag_123/users'
--header 'Authorization: Bearer c2ff9aa1-1824-4cc7-a01f-4094293a6af9'
```

### 返回示例

```json
{
    "totalCount":1,
    "values":[
        {
            "identityValue":"u001",
            "tagValue":[
                "26"
            ]
        }
    ]
}
```

