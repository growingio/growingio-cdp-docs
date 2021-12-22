---
id: platform-user
sidebar_position: 2
---

# 平台成员信息

## 接口说明
查询平台成员信息

## 接口地址
http://{api-host}/v1/api/users/{成员ID}

## 请求方式
GET


## 公共请求参数
[公共请求参数](../open-api-overview#公共请求参数)

## 请求参数
| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| 无 |  |  |  |  |

## 返回数据
| 名称 | 类型 | 描述 |
| --- | --- | --- |
| id | string | 成员ID |
| name | string | 成员名称 |
| identity | string | 成员账号 |
| email | string | 成员邮箱 |
| phoneNumber | string | 成员手机号 |
| creatorId | string | 创建者ID |
| lastVisitAt | string | 最后一次访问时间 |

## 返回示例
```
{
    "id": "nxGKqxQa",
    "name": "马XXX",
    "identity": "xxx@growingio.com",
    "email": "xxx@growingio.com",
    "phoneNumber": "13800000000",
    "creatorId": "WlGk4Daj",
    "lastVisitAt": "2021-12-22T09:55:51Z"
}
```

## 错误码

## 变更历史