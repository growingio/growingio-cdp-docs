---
id: project-compute-user-tag
sidebar_position: 5
---

# 用户标签更新

## 接口说明

更新计算指定用户标签

## 接口地址

```
http://{api-host}/v1/api/projects/{projectId}/user_tags/{tagKey}/computes
```

## 请求方式

POST

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| projectId  | String | 是   | 用户标签所在项目ID | WlGk4Daj |
| tagKey | String | 是   | 用户标签标识符 | tag_rfm |

## 限制条件

仅支持更新 计算成功 和 计算失败 的用户标签，无法更新 等待计算中 和 计算中 的用户标签

### 请求示例

```bash
curl --location --request POST 'http://{api-host}/v1/api/projects/WlGk4Daj/user_tags/tag_rfm/computes' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer e782a8e4-87ae-4e39-8b06-38818a478ac7' 
```

### 返回示例

```json
{
    "value": true,
    "message": "触发计算成功"
}
```