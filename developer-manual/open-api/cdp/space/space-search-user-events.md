---
id: space-search-user-events
sidebar_position: 2
---

# 用户行为轨迹查询

## 接口说明

查询空间中单个用户的所有行为

## 接口地址

```
http://{api-host}/cdp/api/v2/spaces/{spaceId}/users/$basic_userId/{userId}/events?startTime={startTime}&endTime={endTime}&limit={limit}&order={order}
```

## 请求方式

GET

## 公共请求参数

[公共请求参数](../../../open-api#公共请求参数)

## 请求参数

| 名称          | 类型   | 必填 | 描述                 | 示例值        |
| ------------- | ------ | ---- | -------------------- | ------------- |
| spaceId       | String | 是   | 搜索用户所在空间 ID  | VKwkPmqX      |
| userId   | String | 是   | 搜索用户ID，其用户身份为$basic_userId | U3803180317 |
| startTime | Long | 是   | 行为起始时间     | 1682929685000   |
| endTime | Long | 是   | 行为结束时间     | 1685608085000   |
| limit | Int | 否   | 返回行为条数，默认100，最大1000     | 100   |
| order | String | 否   | 行为时序的排序方式，默认asc——时间正序排列，可选desc——时间倒序排列     | asc   |

## 返回数据

| 名称            | 类型              | 描述                             |
| --------------- | ----------------- | -------------------------------- |
| totalCount           | Int               | 返回用户行为的条数     |
| startTime | Long | 行为起始时间         |
| endTime   | Long | 行为结束时间 |
| values   | List | 返回的行为数据 |


### 返回值values中单个事件的数据结构
| 名称            | 类型              | 描述                             |
| --------------- | ----------------- | -------------------------------- |
| name           | String               | 事件名称     |
| key | String | 事件标识符         |
| properties   | List | 事件属性 |

#### 返回值某事件properties中单个事件属性的数据结构
| 名称            | 类型              | 描述                             |
| --------------- | ----------------- | -------------------------------- |
| name           | String               | 事件属性名称     |
| key | String | 事件属性标识符         |
| value   | Object | 事件属性值 |
| valueType   | String | 事件属性的数据类型 |


## 示例：根据项目 空间 ID 和 用户 ID 搜索用户的行为数据

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/cdp/api/v2/spaces/VKwkPmqX/users/$basic_userId/U3803180317/events?startTime=1682929685000&endTime=1685608085000'
--header 'Authorization: Bearer c2ff9aa1-1824-4cc7-a01f-4094293a6af9'
```

### 返回示例

```json
{
    "totalCount":2,
    "startTime":1682929685000,
    "endTime":1685608085000,
    "values":[
        {
            "name":"zxm_埋点_复属_A",
            "key":"test_zxm_cstm_ds_A",
            "properties":[
                {
                    "name":"zxm_事属_字符串",
                    "key":"test_zxm_var_string",
                    "value":"collector_zc_user_052401",
                    "valueType":"STRING"
                },
                {
                    "name":"zxm_事属_整数",
                    "key":"test_zxm_var_int",
                    "value":"500",
                    "valueType":"INT"
                }
            ]
        }
    ]
}
```