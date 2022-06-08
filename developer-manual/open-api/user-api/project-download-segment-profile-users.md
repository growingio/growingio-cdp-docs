---
id: project-download-segment-profile-users
sidebar_position: 11
---

# 项目-群体画像用户列表下载

## 接口说明

下载指定项目指定群体画像覆盖用户的用户特征

## 接口地址

```
http://{api-host}/v1/api/projects/{project_ID}/segment_profiles/{segment_key}/users/export_jobs
```

## 请求方式

POST

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| project_ID  | String | 是   | 群体画像所在项目ID | WlGk4Daj |
| segment_key | String | 是   | 群体画像标识符 | seg_51activity |

## Body

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| properties | List | 否 | 查询的用户身份、用户属性、用户标签<br></br>最大查询60个，超过上限后查询失败 | id_$basic_userId |
| fileFormat | String | 否 | 数据导出格式，支持导出csv或json文件<br></br>默认值为csv | csv、json |
| csvHeaderType | String | 否 | csv文件header类型<br></br>支持设置为名称或标识符<br></br>仅当数据导出格式为csv时生效<br></br>默认类型为标识符 | name、key |

## 返回数据

文件名称：{群体画像名称}_{下载日期}_UserList

数据格式：

- fileformat: csv  csvHeaderType: key

```csv
"gio_id","id_$basic_userId","usr_gender","tag_rfm",...
1,"C001","男","高",...
...
```

- fileformat: csv  csvHeaderType: name

```csv
"gio_id","用户ID","性别","会员等级",...
1,"C001","男","高",...
...
```

- fileformat: json

```json
{"gio_id": "1", "identifications": { "id_$basic_userId": "C001" }, "properties": { "usr_gender":"男", "tag_rfm": "高",... } }
...
```

## 示例 1：下载用户画像覆盖用户列表，并输入用户身份、用户属性、用户标签

场景：下载 群体画像 **seg_51activity** 的用户ID、性别、RFM标签

### 提交下载任务

Request:

```bash
curl --location --request POST 'http://{api-host}/v1/api/projects/WlGk4Daj/segment_profiles/seg_51activity/export_jobs' \
--header 'Authorization: Bearer 4aaa22c7-679f-49be-b97d-073dad5dfc15' \
--header 'Content-Type: application/json' \
--data-raw '{
    "properties": [
        "ids_$basic_userId",
        "usr_gender",
        "tag_rfm"
    ]
    ,"fileformat":"csv"
    ,"csvHeaderType":"key"
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
“gio_id","d_$basic_userId","usr_gender","tag_rfm"
"603542","C001","男”,
"605419","C004",,"低"
...
```

## 示例 2：下载条件未输入用户身份、用户属性、用户标签

场景：下载 群体画像 **seg_51activity**

### 提交下载请求

Request:

```bash
curl --location --request POST 'http://{api-host}/v1/api/projects/WlGk4Daj/segment_profiles/seg_51activity/export_jobs' \
--header 'Authorization: Bearer 4aaa22c7-679f-49be-b97d-073dad5dfc15' \
--header 'Content-Type: application/json' \
--data-raw '{
    "properties": []
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
“gio_id"
"603542"
"605419"
...
```