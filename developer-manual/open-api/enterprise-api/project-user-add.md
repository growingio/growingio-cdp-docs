---
id: project-user-add
sidebar_position: 21
---

# 添加项目成员

## 接口说明

添加平台成员到指定项目

## 接口地址

```
http://{api-host}/v1/api/projects/{项目ID}/users

```

## 请求方式

PUT

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

Body 中放置请求参数，参数详情如下：

| 名称          | 类型   | 必填 | 描述         | 示例值                  |
| ------------- | ------ | ---- | ------------ | ----------------------- |
| userIds       | array  | 是   | 成员 ID 数组 | ["zZDbKQ9o","WlGk4Daj"] |
| projectRoleId | string | 是   | 项目角色 ID  | y9pm1pme                |

## 返回数据

无返回值

## 返回示例

## 错误码

## 变更历史
