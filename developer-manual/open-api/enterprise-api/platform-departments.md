---
id: platform-departments
sidebar_position: 3
---

# 平台部门列表

## 接口说明

查询平台部门列表

## 接口地址

http://{api-host}/v1/api/departments

## 请求方式

GET

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| ---- | ---- | ---- | ---- | ------ |
| 无   |      |      |      |        |

## 返回数据

| 名称 | 类型   | 描述     |
| ---- | ------ | -------- |
| id   | string | 项目 ID  |
| name | string | 项目名称 |

## 返回示例

```
[
    {
        "id": "WlGk4Daj",
        "name": "默认项目"
    },
    {
        "id": "y9pm1pme",
        "name": "wyl测试项目-勿动"
    },
    {
        "id": "AbQ3bDYe",
        "name": "测试删除项目"
    },
    {
        "id": "rRGoYQml",
        "name": "wyltest01"
    },
    {
        "id": "n1QVaDyR",
        "name": "dzf_test1"
    }
]
```

## 错误码

## 变更历史
