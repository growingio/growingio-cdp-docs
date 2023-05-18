---
id: delete-enterprise-user
sidebar_position: 3
---

# 移除企业成员

## 接口说明

移除企业下指定成员

## 接口地址

```
http://{api-host}/v2/api/enterprise/{enterpriseId}/user/{userId}
```

## 请求方式

DELETE

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| ---- | ---- | ---- | ---- | ------ |
| enterpriseId | string | 是 | 企业ID | WlGk4Daj |
| userId | string | 是 | 用户ID | WlGk4Daj |

提示：企业 ID 从企业概览中获取

## 公共请求参数

<!-- [公共请求参数](../../open-api#公共请求参数) -->

## 返回数据

无

## 返回示例
**成功**

HTTP Status `204`

**异常**
```
{
  "success": false,
  "code": "100004",
  "message": "调用后端服务异常"
}
```

## 错误码

## 变更历史
