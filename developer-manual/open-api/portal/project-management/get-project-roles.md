---
id: get-project-user-detail
sidebar_position: 3
---

# 项目角色列表

## 接口说明

查询项目角色列表

## 接口地址

```
http://{api-host}/v2/api/enterprise/{enterpriseId}/projects/{projectId}/roles
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
| id   | string | 角色 ID  |
| name | string | 角色名称 |

## 返回示例

```
[
  {
    "id": "WlGk4Daj",
    "name": "管理员",
  }
]
```

## 错误码

## 变更历史
