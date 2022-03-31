---
id: project-user
sidebar_position: 16
---

# 项目成员详情

## 接口说明

查询项目成员详情信息

## 接口地址

```
http://{api-host}/v1/api/projects/{项目ID}/users/{成员ID}
```

## 请求方式

GET

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| ---- | ---- | ---- | ---- | ------ |
| 无   |      |      |      |        |

## 返回数据

| 名称   | 类型   | 描述     |
| ------ | ------ | -------- |
| member | object | 成员信息 |
| role   | object | 角色信息 |

### 成员信息

| 名称        | 类型   | 描述             |
| ----------- | ------ | ---------------- |
| id          | string | 成员 ID          |
| name        | string | 成员名称         |
| email       | string | 成员邮箱         |
| phoneNumber | string | 成员手机号       |
| identity    | string | 成员账号         |
| lastVisitAt | string | 最后一次访问时间 |

### 角色信息

| 名称 | 类型   | 描述    |
| ---- | ------ | ------- |
| id   | string | 角色 ID |

## 返回示例

```
{
    "member": {
        "id": "WlGk4Daj",
        "name": "admin",
        "email": "admin@gdp.com",
        "identity": "admin@gdp.com",
        "identity": "13800000000"
        "lastVisitAt": "2021-12-01T07:38:48Z"
    },
    "role": {
        "id": "AbQ3bDYe"
    }
}
```

## 错误码

## 变更历史
