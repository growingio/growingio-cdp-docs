---
id: space-segment-api-downloads-detail
sidebar_position: 10
---

# 群组授权任务明细数据查询

## 接口说明

查询空间中群组授权导出的任务明细数据

## 接口地址

```
http://{api-host}/v1/api/projects/{projectId}/spaces/{spaceId}/segment_api_downloads/{segment_api_download_id}/detail
```

## 请求方式

POST

## 公共请求参数

[公共请求参数](../../../open-api#公共请求参数)

## 请求参数

| 名称                    | 类型   | 必填 | 描述            | 示例值   |
| ----------------------- | ------ | ---- | --------------- | -------- |
| projectId               | String | 是   | 群组所在项目 ID | WlGk4Daj |
| spaceId                 | String | 是   | 群组所在空间 ID | VKwkPmqX |
| segment_api_download_id | String | 是   | 群组导出授权 ID | oyQYBnzW |

### 请求示例

```bash
curl --location --request POST 'http://{api-host}/v1/api/projects/WlGk4Daj/spaces/VKwkPmqX/segment_api_downloads/oyQYBnzW/detail' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer e782a8e4-87ae-4e39-8b06-38818a478ac7'
```

### 返回示例

```json
{}
```
