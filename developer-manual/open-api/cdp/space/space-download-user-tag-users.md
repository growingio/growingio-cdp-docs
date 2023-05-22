---
id: space-download-user-tag-users
sidebar_position: 6
---

# 用户标签用户列表下载

## 接口说明

下载指定空间指定用户标签覆盖用户的用户特征

## 接口地址

```
http://{api-host}/v1/api/projects/{projectId}/spaces/{spaceId}/user_tags/{tagKey}/export_jobs
```

## 请求方式

POST

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| projectId  | String | 是   | 用户标签所在项目ID | WlGk4Daj |
| spaceId  | String | 是   | 用户标签所在空间ID | VKwkPmqX 
| tagKey | String | 是   | 用户标签标识符 | tag_rfm |

## Body

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| properties | List | 否 | 查询的用户身份、用户属性、用户标签<br></br>最大查询60个，超过上限后查询失败 | id_$basic_userId |
| fileFormat | String | 否 | 数据导出格式，支持导出csv或json文件<br></br>默认值为csv | csv、json |
| csvHeaderType | String | 否 | csv文件header类型<br></br>支持设置为名称或标识符<br></br>仅当数据导出格式为csv时生效<br></br>默认类型为标识符 | name、key |

## 返回数据

文件名称：{群体画像名称}_{下载日期}_UserList

数据格式：

- fileFormat: csv  csvHeaderType: key

```csv
"gio_id","id_$basic_userId","usr_gender","tag_rfm",...
1,"C001","男","高",...
...
```

- fileFormat: csv  csvHeaderType: name

```csv
"gio_id","用户ID","性别","会员等级",...
1,"C001","男","高",...
...
```

- fileFormat: json

```json
{"gio_id": "1", "identifications": { "id_$basic_userId": "C001" }, "properties": { "usr_gender":"男", "tag_rfm": "高",... } }
...
```

## 示例 1：下载用户标签覆盖用户列表，并输入用户身份、用户属性、用户标签

场景：下载 用户标签 **tag_rfm** 的用户ID、性别、RFM标签

### 提交下载请求

Request:

```bash
curl --location --request POST 'http://{api-host}/v1/api/projects/WlGk4Daj/spaces/VKwkPmqX/user_tags/tag_rfm/export_jobs' \
--header 'Authorization: Bearer 4aaa22c7-679f-49be-b97d-073dad5dfc15' \
--header 'Content-Type: application/json' \
--data-raw '{
    "properties": [
        "ids_$basic_userId",
        "usr_gender",
        "tag_rfm"
    ]
    ,"fileFormat":"csv"
    ,"csvHeaderType":"name"
}'
```

Response:


```json
{
    "id": "kqQeWeGr",           // 下载任务ID
    "name": "DES-202205240136-5818534160000"
}
```

### 获取下载地址

Request:

```bash
curl --location --request GET 'http://{api-host}/v1/api/job/result/kqQeWeGr' \
--header 'Authorization: Bearer 4aaa22c7-679f-49be-b97d-073dad5dfc15'
```

Response:

```json
{
    "stage": "FINISH",
    "uris": [
        "%2Fjobs%2Fresults%2FDES-202205240136-5818534160000%2Fzxm_%E7%94%A8%E6%88%B7_%E5%AD%97%E7%AC%A6%E4%B8%B2_%E5%8A%A0%E5%AF%86_2022-04-26_UserList.csv"   // 下载地址
    ]
}
```

### 下载文件

下载地址："http://{api-host}/download?file=" + {下载地址}

文件格式：

```csv
“gio_id","用户ID",“性别","会员等级"
"603542","C001","男”,
"605419","C004",,"低"
...
```

## 示例 2：下载条件未输入用户身份、用户属性、用户标签

场景：下载 用户标签 **tag_rfm**

### 提交下载请求

Request:

```bash
curl --location --request POST 'http://{api-host}/v1/api/projects/WlGk4Daj/spaces/VKwkPmqX/user_tags/tag_rfm/export_jobs' \
--header 'Authorization: Bearer 4aaa22c7-679f-49be-b97d-073dad5dfc15' \
--header 'Content-Type: application/json' \
--data-raw '{
    "properties": []
    ,"fileFormat":"json"
}'
```

Response:


```json
{
    "id": "kqQeWeGr",           // 下载任务ID
    "name": "DES-202205240136-5818534160000"
}
```

### 获取下载地址

Request:

```bash
curl --location --request GET 'http://{api-host}/v1/api/job/result/kqQeWeGr' \
--header 'Authorization: Bearer 4aaa22c7-679f-49be-b97d-073dad5dfc15'
```

Response:

```json
{
    "stage": "FINISH",
    "uris": [
        "%2Fjobs%2Fresults%2FDES-202205240136-5818534160000%2Fzxm_%E7%94%A8%E6%88%B7_%E5%AD%97%E7%AC%A6%E4%B8%B2_%E5%8A%A0%E5%AF%86_2022-04-26_UserList.json"   // 下载地址
    ]
}
```

### 下载文件

下载地址："http://{api-host}/download?file=" + {下载地址}

文件格式：

```json
{"gio_id":603542}
{"gio_id":605419}
...
```