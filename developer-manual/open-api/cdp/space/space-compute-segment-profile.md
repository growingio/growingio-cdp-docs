---
id: space-compute-segment-profile
sidebar_position: 8
---

# 群体画像更新

## 接口说明

更新计算指定空间指定群体画像

## 接口地址

```
http://{api-host}/v1/api/projects/{projectId}/spaces/{spaceId}/segment_profiles/{segmentKey}/computes
```

## 请求方式

POST

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| projectId  | String | 是   | 群体画像所在项目ID | WlGk4Daj |
| spaceId  | String | 是   | 群体画像所在空间ID | VKwkPmqX 
| segmentKey | String | 是   | 群体画像标识符 | seg_0513sbbwk |

## 限制条件

仅支持更新 计算成功 和 计算失败 的群体画像，无法更新 等待计算中 和 计算中 的群体画像

### 请求示例

```bash
curl --location --request POST 'http://{api-host}/v1/api/projects/WlGk4Daj/spaces/VKwkPmqX/segment_profiles/seg_0513sbbwk/computes' \
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