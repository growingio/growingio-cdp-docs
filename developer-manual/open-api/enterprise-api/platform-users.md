---
id: platform-users
sidebar_position: 1
---

# 平台成员列表

## 接口说明
查询平台成员列表

## 接口地址
http://{api-host}/v1/api/user/{成员ID}?scopeId={企业ID}&scopeType=DataCenter&offset={偏移量}&limit={每页数量}

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| scopeId | string | 是 | 企业ID | WlGk4Daj |
| scopeType | string | 是 | 数据范围 | DataCenter |
| offset | int | 是 | 偏移量 | 0 |
| limit | int | 是 | 每页数量 | 10 |

提示：企业ID在前端的获取路径是【企业管理后台】 - 【企业概览】

## 请求方式
GET


## 公共请求参数
[公共请求参数](../../open-api#公共请求参数)

## 请求参数
| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| 无 |  |  |  |  |

## 返回数据
| 名称 | 类型 | 描述 |
| --- | --- | --- |
| offset | int | 偏移量 |
| limit | int | 每页数量 |
| totalCount | int | 总数 |
| hasNextPage | string | 是否有下一页 |
| hasPreviousPage | string | 是否有前一页 |
| values | object | 成员列表 |

### 成员列表
| 名称 | 类型 | 描述 |
| --- | --- | --- |
| id | string | 成员ID |
| name | string | 成员名称 |


## 返回示例
```
{
    "offset": 0,
    "limit": 10,
    "totalCount": 102,
    "hasNextPage": true,
    "hasPreviousPage": true,
    "values": [
        {
            "id": "nxGKqxQa",
            "name": "马XXX"
        },
        {
            "id": "zqQRv5Qo",
            "name": "李XXX"
        },
        {
            "id": "wWDr5vGM",
            "name": "朱XXX"
        }
    ]
}
```

## 错误码

## 变更历史