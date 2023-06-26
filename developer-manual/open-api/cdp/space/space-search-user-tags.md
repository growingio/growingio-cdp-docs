---
id: space-search-user-tags
sidebar_position: 3
---

# 用户标签列表查询

## 接口说明

查询空间中全部用户标签信息

## 接口地址

```
http://{api-host}/v1/api/projects/{projectId}/spaces/{spaceId}/user_tags
```

## 请求方式

GET

## 公共请求参数

[公共请求参数](../../../open-api#公共请求参数)

## 请求参数

| 名称      | 类型   | 必填 | 描述                | 示例值   |
| --------- | ------ | ---- | ------------------- | -------- |
| projectId | String | 是   | 用户标签所在项目 ID | WlGk4Daj |
| spaceId   | String | 是   | 用户标签所在空间 ID | VKwkPmqX |

## 查询参数

| 名称   | 类型 | 必填 | 描述                                                               | 示例值          |
| ------ | ---- | ---- | ------------------------------------------------------------------ | --------------- |
| limit  | Int  | 否   | 单次查询返回数据上限<br></br>最大值为 1,000<br></br>默认值为 1,000 | 1000            |
| offset | Int  | 否   | 查询标识位，默认值为 0                                             | 0、10000、20000 |

## 返回数据

| 名称            | 类型      | 描述                                            |
| --------------- | --------- | ----------------------------------------------- |
| limit           | Int       | 单次查询返回数据上限                            |
| offset          | Int       | 查询标识位                                      |
| totalCount      | Int       | 本次查询总计返回数据量                          |
| hasNextPage     | Bool      | 是否有下一页<br></br>false：否<br></br>true：是 |
| hasPreviousPage | Bool      | 是否有上一页<br></br>false：否<br></br>true：是 |
| values          | Objective | 全部群体画像信息                                |

### values 数据

| 名称        | 类型      | 描述                                                                                                                                                                                                                                        |
| ----------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id          | String    | 哈希 ID，ID 自增                                                                                                                                                                                                                            |
| name        | String    | 名称                                                                                                                                                                                                                                        |
| key         | String    | 标识符                                                                                                                                                                                                                                      |
| type        | String    | 标签类型<br></br>AGGREGATED：基础指标值<br></br>TOP_N_ATTRIBUTE：最大值/最小值的事件属性<br></br>ATTRIBUTION_ATTRIBUTE：首次/末次的事件属性<br></br>DATA_SET_ATTRIBUTE：列表类的事件属性<br></br>HORIZONTAL：分层标签<br></br>SQL：SQL 标签 |
| description | String    | 描述                                                                                                                                                                                                                                        |
| valueType   | Objective | 数值类型                                                                                                                                                                                                                                    |
| detector    | Objective | 更新状态信息                                                                                                                                                                                                                                |
| creatorId   | String    | 创建人 ID                                                                                                                                                                                                                                   |
| creator     | String    | 创建人                                                                                                                                                                                                                                      |
| createdAt   | Datetime  | 创建时间                                                                                                                                                                                                                                    |
| updaterId   | String    | 最近修改人 ID                                                                                                                                                                                                                               |
| updater     | String    | 最近修改人                                                                                                                                                                                                                                  |
| updatedAt   | Datetime  | 最近修改时间                                                                                                                                                                                                                                |

#### valueType 数据

| 名称    | 类型   | 描述                                                                                      |
| ------- | ------ | ----------------------------------------------------------------------------------------- |
| type    | String | 数值类型<br></br>STRING：字符串<br></br>INT：整数<br></br>DOUBLE：小数<br></br>DATE：日期 |
| isArray | Bool   | 是否为列表型<br></br>true：是<br></br>false：否                                           |

#### detector 数据

| 名称       | 类型     | 描述                                                                                                       |
| ---------- | -------- | ---------------------------------------------------------------------------------------------------------- |
| stage      | String   | 计算状态<br></br>NONE：计算未开始<br></br>RUNNING：计算中<br></br>FINISH：计算成功<br></br>ERROR：计算失败 |
| detectedAt | Datetime | 更新时间                                                                                                   |

## 示例：根据项目 ID 和空间 ID 查询用户标签列表

场景：在项目 WlGk4Daj 空间 VKwkPmqX 中查询已授权的全部用户标签信息

### 请求示例

```bash
curl --location --request GET 'http://{api-host}/v1/api/projects/WlGk4Daj/spaces/VKwkPmqX/user_tags?offset=0&limit=1000'
--header 'Authorization: Bearer c2ff9aa1-1824-4cc7-a01f-4094293a6af9'
```

### 返回示例

```json
{
    "offset": 0.0,
    "limit": 1000.0,
    "totalCount": 143.0,
    "hasNextPage": false,
    "hasPreviousPage": false,
    "values": [
        {
            "id": "WlGk4Daj",
            "name": "GrowingIO",
            "key": "tag_example_api",
            "type": "AGGREGATED",
            "description": "API示例",
            "valueType": {
                "type": "DOUBLE",
                "isArray": false
            },
            "detector": {
                "stage": "FINISH",
                "detectedAt": "2022-01-01T01:01:00.000Z"
            },
            "creatorId": "KzpNzpkv",
            "creator": "管理员",
            "createdAt": "2022-01-01T00:00:00.000Z",
            "updaterId": "KzpNzpkv",
            "updater": "管理员",
            "updatedAt": "2022-01-01T01:00:00.000Z"
        },
        ...
        ]
}
```
