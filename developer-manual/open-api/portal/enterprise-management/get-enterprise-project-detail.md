---
id: get-enterprise-project-detail
sidebar_position: 4
---

# 企业项目详情

## 接口说明

查询企业下指定项目详情

## 接口地址

```
http://{api-host}/v2/api/enterprise/{enterpriseId}/project/{projectId}
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

[公共请求参数](../../../open-api#公共请求参数)

## 返回数据

| 名称 | 类型   | 描述     |
| ---- | ------ | -------- |
| id   | string | 项目 ID  |
| name | string | 项目名称 |
| ownerId | string | 拥有者ID |
| owner | string | 拥有者姓名 |
| products | Product[] | 产品 |
| integrates | Integrate[] | 集成应用 |
| spaceQuota | integer | 空间配额 |

**Product**

| 名称 | 类型   | 描述     |
| ---- | ------ | -------- |
| uniqueId | string | 产品唯一编码 |
| name | string | 产品名称 |
| description | string | 描述 |

**Integrate**

| 名称 | 类型   | 描述     |
| ---- | ------ | -------- |
| id | string | 产品唯一编码 |
| name | string | 产品名称 |
| description | string | 描述 |

## 返回示例

```
{
  "id": "WlGk4Daj",
  "name": "默认项目",
  "ownerId": "WlGk4Daj",
  "owner": "admin",
  "products": [
    {
      "uniqueId": "DC",
      "name": "数据中心",
      "description": "全域全渠道数据底座"
    },
    {
      "uniqueId": "UBA",
      "name": "增长分析",
      "description": "增长分析：用户全渠道分析"
    },
    {
      "uniqueId": "AD",
      "name": "获客分析",
      "description": "获客分析"
    },
    {
      "uniqueId": "CDP",
      "name": "客户数据平台",
      "description": "用户全渠道行为CDP"
    },
    {
      "uniqueId": "MAP",
      "name": "智能运营",
      "description": "智能运营增长：智能运营平台"
    }
  ],
  "integrates": [
    {
      "id": "WlGk4Daj",
      "name": "渠道质量分析"
    }
  ],
  "spaceQuota": 25
}
```

## 错误码

## 变更历史
