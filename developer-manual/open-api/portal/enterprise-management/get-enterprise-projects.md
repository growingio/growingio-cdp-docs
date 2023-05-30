---
id: get-enterprise-projects
sidebar_position: 3
---

# 企业项目列表

## 接口说明

查询企业下所有项目

## 接口地址

```
http://{api-host}/v2/api/enterprise/{enterpriseId}/projects
```

## 请求方式

GET

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| ---- | ---- | ---- | ---- | ------ |
| enterpriseId | string | 是 | 企业ID | WlGk4Daj |

提示：企业 ID 从企业概览中获取

## 公共请求参数

[公共请求参数](../../../open-api#公共请求参数)

## 返回数据

| 名称 | 类型   | 描述     |
| ---- | ------ | -------- |
| id   | string | 项目 ID  |
| name | string | 项目名称 |
| ownerId | string | 拥有者ID |

## 返回示例

```
[
  {
    "id": "WlGk4Daj",
    "name": "默认项目",
    "ownerId": "WlGk4Daj"
  }
]
```
