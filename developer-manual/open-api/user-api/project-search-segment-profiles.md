---
id: project-search-segment-profiles
sidebar_position: 7
---

# 项目-群体画像列表查询

## 接口说明

查询项目中已定义的全部群体画像信息

## 接口地址

```
http://{api-host}/v1/api/projects/{project_ID}/segment_profiles
```

## 请求方式

GET

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| project_ID  | String | 是   | 群体画像所在项目ID | WlGk4Daj |

## 查询参数

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| limit  | Int | 否   | 单次查询返回数据上限<br></br>最大值为1,000<br></br>默认值为1,000 | 1000 |
| offset | Int | 否   | 查询标识位，默认值为0 | 0、10000、20000 |

## 返回数据

| 名称            | 类型      | 描述                             |
| --------------- | --------- | -------------------------------- |
| limit | Int | 单次查询返回数据上限  |
| offset | Int | 查询标识位  |
| totalCount | Int | 本次查询总计返回数据量 |
| hasNextPage | Bool | 是否有下一页<br></br>false：否<br></br>true：是 |
| hasPreviousPage | Bool | 是否有上一页<br></br>false：否<br></br>true：是 |
| values | Objective | 全部群体画像信息 |

### values数据

| 名称            | 类型      | 描述                             |
| --------------- | --------- | -------------------------------- |
| id | String | 哈希ID，ID自增 |
| name | String | 名称 |
| key | String | 标识符 |
| createdBy | String | 分群类型<br></br>DIRECT：规则创建<br></br>FROM_FUNNEL：漏斗创建<br></br>FROM_RETENTION：留存创建<br></br>FROM_FREQUENCY：分布分析创建<br></br>FROM_FILES：文件上传 |
| description | String | 描述 |
| scheduler | String | 更新频次<br></br>DAILY：每日更新<br></br>ONCE：手动 |
| detector | Objective | 更新状态信息 |
| creatorId | String | 创建人ID |
| creator | String | 创建人 |
| createdAt | Datetime | 创建时间 |
| updaterId | String | 最近修改人ID |
| updater | String | 最近修改人 |
| updatedAt | Datetime | 最近修改时间 |

#### detector数据

| 名称            | 类型      | 描述                             |
| --------------- | --------- | -------------------------------- |
| stage | String | 计算状态<br></br>NONE：计算未开始<br></br>RUNNING：计算中<br></br>FINISH：计算成功<br></br>ERROR：计算失败 |
| detectedAt | Datetime | 更新时间 |

## 示例：根据项目ID查询群体画像列表

场景：在项目 WlGk4Daj 中查询已定义的全部群体画像信息


### 请求示例

```bash
curl --location --request GET 'http://{api-host}/v1/api/projects/WlGk4Daj/segment_profiles?offset=0&limit=1000'
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
            "key": "seg_example_api",
            "createdBy": "DIRECT",
            "description": "API示例",
            "scheduler": "DAILY",
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
