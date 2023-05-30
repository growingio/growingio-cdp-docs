---
id: get-enterprise-user-detail
sidebar_position: 2
---

# 企业成员详情

## 接口说明

查询企业成员详情

## 接口地址

```
http://{api-host}/v2/api/enterprise/{enterpriseId}/user/{userId}
```

## 请求方式

GET

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| ---- | ---- | ---- | ---- | ------ |
| enterpriseId | string | 是 | 企业ID | WlGk4Daj |
| userId | string | 是 | 用户ID | WlGk4Daj |

提示：企业 ID 从企业概览中获取

## 公共请求参数

[公共请求参数](../../../open-api#公共请求参数)

## 返回数据

| 名称 | 类型   | 描述     |
| ---- | ------ | -------- |
| id   | string | 成员 ID  |
| name | string | 成员名称 |
| phone | string | 手机号 |
| email | string | 邮箱 |
| roleId | string | 邮箱 |
| email | string | 邮箱 |
| email | string | 邮箱 |
| email | string | 邮箱 |

## 返回示例

```
{
  "id": "V0G5vDAR",
  "name": "zhangdaoquan",
  "nickName": "zhangdaoquan",
  "roleId": "WlGk4Daj",
  "roleName": "企业管理员",
  "createdAt": {
    "nano": 270769000,
    "epochSecond": 1683710342
  },
  "lastLoginAt": {
    "nano": 287895000,
    "epochSecond": 1683710387
  }
}
```
