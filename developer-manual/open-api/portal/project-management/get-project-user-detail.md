---
id: get-project-user-detail
sidebar_position: 2
---

# 项目成员详情

## 接口说明

查询项目下指定成员详情

## 接口地址

```
http://{api-host}/v2/api/enterprise/{enterpriseId}/projects/{projectId}/users/{userId}
```

## 请求方式

GET

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| ---- | ---- | ---- | ---- | ------ |
| enterpriseId | string | 是 | 企业ID | WlGk4Daj |
| projectId | string | 是 | 项目ID | WlGk4Daj |
| userId | string | 是 | 用户ID | WlGk4Daj |

提示：企业 ID 从企业概览中获取; 项目 ID 从项目概览中获取

## 公共请求参数

[公共请求参数](../../../open-api#公共请求参数)

## 返回数据

| 名称 | 类型   | 描述     |
| ---- | ------ | -------- |
| id   | string | 成员 ID  |
| name | string | 成员名称 |
| phone | string | 手机号 |
| email | string | 邮箱 |
| roleId | string | 角色 ID |
| roleName | string | 角色姓名 |
| lastLoginAt | timestamp | 最后登录时间 |

## 返回示例

```
{
  "id": "WlGk4Daj",
  "name": "demo",
  "phone": "1234567890",
  "email": "demo@demo.co",
  "roleId": "WlGk4Daj",
  "roleName": "项目管理员",
  "lastLoginAt": {
    "nano": 849675000,
    "epochSecond": 1684223186
  }
}
```

