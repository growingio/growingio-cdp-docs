---
id: project-user-role-upt
sidebar_position: 22
---

# 修改项目成员角色

## 接口说明
修改项目成员所属的项目角色

## 接口地址
http://{api-host}/v1/api/projects/{项目ID}/users/{成员ID}

## 请求方式
PUT

## 公共请求参数
[公共请求参数](../common-args)

## 请求参数
Body中放置请求参数，参数详情如下：
| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| projectId | string | 是 | 项目ID | rRGoYQml |
| userId | string | 是 | 成员ID | zZDbKQ9o |
| roleId | string | 是 | 项目角色ID | AbQ3bDYe |

## 返回数据
无返回值

## 返回示例

## 错误码

## 变更历史