---
id: project-role
sidebar_position: 14
---

# 项目角色详情

## 接口说明
查询项目角色详情信息

## 接口地址
http://{api-host}/v1/api/projects/{项目ID}/roles/{角色ID}

## 请求方式
GET


## 公共请求参数
[公共请求参数](../open-api-overview#公共请求参数)

## 请求参数
| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| 无 |  |  |  |  |

## 返回数据

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| id | string | 角色ID |
| name | string | 角色名称 |
| description | string | 角色描述 |

## 返回示例
```
{
    "id": "WlGk4Daj",
    "name": "负责人",
    "description": "负责人拥有最高功能权限，同时拥有所有资源权限。可将系统管理者、项目负责人设置为该角色。"
}
```

## 错误码

## 变更历史