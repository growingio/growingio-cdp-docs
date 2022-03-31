---
id: project
sidebar_position: 12
---

# 项目详情

## 接口说明

查询项目详情信息

## 接口地址

```
http://{api-host}/v1/api/projects/{项目ID}
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

| 名称        | 类型   | 描述          |
| ----------- | ------ | ------------- |
| id          | string | 项目 ID       |
| name        | string | 项目名称      |
| description | string | 项目描述      |
| creator     | string | 项目创建者    |
| creatorId   | string | 项目创建者 ID |
| createdAt   | string | 项目创建时间  |
| owner       | string | 项目拥有者    |
| ownerId     | string | 项目拥有者 ID |

## 返回示例

```
{
    "id": "y9pm1pme",
    "name": "wyl测试项目-勿动",
    "description": "wyl测试项目-勿动wyl测试项目-勿动",
    "creator": "",
    "creatorId": "J1GlEDjl",
    "createdAt": "2021-12-09T02:20:34.099072Z",
    "owner": "wyltest01-系统创建",
    "ownerId": "rRGoYQml"
}
```

## 错误码

## 变更历史
