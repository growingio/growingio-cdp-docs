---
id: project-roles
sidebar_position: 13
---

# 项目角色列表

## 接口说明

查询项目角色列表

## 接口地址

```
http://{api-host}/v1/api/projects/{项目ID}/roles
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

| 名称        | 类型   | 描述     |
| ----------- | ------ | -------- |
| id          | string | 角色 ID  |
| name        | string | 角色名称 |
| description | string | 角色描述 |

## 返回示例

```
[
    {
        "id": "WlGk4Daj",
        "name": "负责人",
        "description": "负责人拥有最高功能权限，同时拥有所有资源权限。可将系统管理者、项目负责人设置为该角色。"
    },
    {
        "id": "y9pm1pme",
        "name": "管理员",
        "description": "管理员拥有所有功能权限，同时拥有所有资源权限。可将辅助负责人管理事务的同事设置为该角色。"
    },
    {
        "id": "AbQ3bDYe",
        "name": "普通成员",
        "description": "普通成员为数据的主要消费者。 可将不需要进行数据分析的同事设置为该角色。"
    },
    {
        "id": "n1QVaDyR",
        "name": "分析师",
        "description": "分析师为主要数据生产者，拥有分析功能的所有权限。可将团队内主要负责生产数据看板、数据分析的同事设置为该角色。"
    },
    {
        "id": "rRGoYQml",
        "name": "运营人员",
        "description": "运营人员为主要负责运营相关工作的使用者，拥有运营相关功能的所有权限。"
    },
    {
        "id": "klGvyp7E",
        "name": "管理员test01",
        "description": ""
    },
    {
        "id": "bVG2Ap68",
        "name": "aa1",
        "description": ""
    },
    {
        "id": "ExQWOQ79",
        "name": "e",
        "description": ""
    },
    {
        "id": "7RDYeDA8",
        "name": "tedst011tedst011tedst011",
        "description": "tedst011tedst011tedst011tedst011tedst011tedst011"
    },
    {
        "id": "kqQewGry",
        "name": "wyltest01",
        "description": ""
    }
]
```

## 错误码

## 变更历史
