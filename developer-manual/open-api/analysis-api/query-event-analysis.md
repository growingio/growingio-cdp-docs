---
id: query-event-analysis
sidebar_position: 1
---

# 空间-事件分析查询

## 接口说明

获取指定事件分析的统计结果

## 接口地址

```
http://${api-host}/v1/api/projects/${projectId}/analysis/olap_event/${id}/chartdata
```

## 请求方式

GET

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

| 名称      | 类型   | 必填 | 描述        | 示例值   |
| --------- | ------ | ---- | ----------- | -------- |
| projectId | String | 是   | 所在空间 ID | WlGk4Daj |
| id        | String | 是   | 分析标识符  | zqQR5MDo |

:::tip 小贴士

您可以通过浏览器打开已保存的分析详情页，从 URL 中获取到空间 ID 和分析标识符，例如：分析详情页的 URL 为

```
https://xx.xxx.com/projects/nxGK0Da6/analysis/olap-event/KzpN2opk
```

其中空间 ID 为“nxGK0Da6“，分析标识符为”KzpN2opk“

:::

## 查询参数

| **名称**     | **类型** | **必填** | **描述**             | **示例值**             |
| ------------ | -------- | -------- | -------------------- | ---------------------- |
| forceRefresh | boolean  | 否       | 忽略缓存             | false                  |
| limit        | int      | 否       | 单次查询返回数据上限 | 最大 50,000，默认 1000 |
| offset       | int      | 否       | 查询标示位默认 0     | 0                      |

## 返回数据

paginationInfo 分页信息数据

| **名称**        | **类型** | **描述**               | **示例值**         |
| --------------- | -------- | ---------------------- | ------------------ |
| offset          | int      | 查询标识位             |                    |
| limit           | int      | 单次查询返回数据上限   |                    |
| totalCount      | int      | 本次查询总计返回数据量 |                    |
| hasNextPage     | boolean  | 是否有下一页           | false：否 true：是 |
| hasPreviousPage | boolean  | 是否有上一页           | false：否 true：是 |

analysisInfo 单图信息数据

| **名称**    | **类型** | **描述**     |
| ----------- | -------- | ------------ |
| name        | String   | 分析名称     |
| startTime   | String   | 开始事件     |
| endTime     | String   | 结束时间     |
| granularity | String   | 时间粒度     |
| fetchedTime | Long     | 数据查询时间 |

resultHeader 列名

resultRows 行数据

## 示例

查询任意事件的图表信息

### 请求示例

```bash
curl --location --request GET 'http://${api-host}/v1/api/projects/${projectId}/analysis/olap_event/${id}/chartdata?forceRefresh=false&offset=0&limit=1000' \
--header 'Authorization: Bearer bbe40b12-96a5-459d-819d-feea0d9f85b5'
```

### 返回示例

```json
{
 "paginationInfo": {
 "offset": 0.0,
 "limit": 1000.0,
 "totalCount": 1.0,
 "hasNextPage": false,
 "hasPreviousPage": false
 },
 "analysisInfo": {
 "name": "事件分析API示例",
 "startTime": "2022-02-08 00:00:00",
 "endTime": "2022-03-10 00:00:00",
 "granularity": "DAY",
 "fetchedTime": "1646879291229"
 },
 "resultHeader": [
 "目标用户",
 "时间",
 "任意事件的总人数"
 ],
 "resultRows": [
 [
 "全部用户",
 "2022-02-28",
 "10"
 ]
 ]
```
