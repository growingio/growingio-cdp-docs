---
id: get-project-spaces
sidebar_position: 3
---

# 项目空间列表

## 接口说明

查询项目空间列表

## 接口地址

```
http://{api-host}/v2/api/enterprise/{enterpriseId}/projects/{projectId}/spaces
```

## 请求方式

GET

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| ---- | ---- | ---- | ---- | ------ |
| enterpriseId | string | 是 | 企业ID | WlGk4Daj |
| projectId | string | 是 | 项目ID | WlGk4Daj |

提示：企业 ID 从企业概览中获取; 项目 ID 从项目概览中获取

## 公共请求参数

<!-- [公共请求参数](../../open-api#公共请求参数) -->

## 返回数据

| 名称 | 类型   | 描述     |
| ---- | ------ | -------- |
| id   | string | 空间 ID  |
| name | string | 空间名称 |
| ownerId | string | 空间拥有者ID |

## 返回示例

```
[
  {
    "id": "WlGk4Daj",
    "name": "default_space",
    "ownerId": "WlGk4Daj"
  }
]
```

## 错误码

## 变更历史
