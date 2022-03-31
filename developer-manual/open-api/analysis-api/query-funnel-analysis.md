---
id: query-funnel-analysis
sidebar_position: 2
---

# 项目-漏斗分析查询

## 接口说明

获取指定漏斗分析的统计结果

## 接口地址

```
http://${api-host}/v1/api/projects/${projectId}/analysis/funnel/${id}/chartdata
```

## 请求方式

GET

## 公共请求参数

[公共请求参数](../../open-api#公共请求参数)

## 请求参数

| 名称      | 类型   | 必填 | 描述                 | 示例值        |
| --------- | ------ | ---- | -------------------- | ------------- |
| projectId  | String | 是   | 所在项目ID | WlGk4Daj |
| id | String | 是   | 分析标识符 | zqQR5MDo |

注：您可以通过浏览器打开已保存的分析详情页，从URL中获取到项目ID和分析标识符，例如：分析详情页的URL为 https://xx.xxx.com/projects/nxGK0Da6/analysis/funnel/J1GlMVDj
其中项目ID为“nxGK0Da6“，分析标识符为”J1GlMVDj“


## 查询参数

| 名称         | 类型    | 必填 | 描述     | 示例值 |
| ------------ | ------- | ---- | -------- | ------ |
| forceRefresh | boolean | 否   | 忽略缓存 | false  |

## 返回数据

analysisInfo 单图信息数据

| **名称**          | **类型** | **描述**     |
| ----------------- | -------- | ------------ |
| name              | String   | 分析名称     |
| startTime         | String   | 开始事件     |
| endTime           | String   | 结束时间     |
| conversionWindow  | int      | 转化窗口期   |
| windowGranularity | String   | 窗口期粒度   |
| fetchedTime       | Long     | 数据查询时间 |

resultHeader 列名

resultRows 行数据

## 示例

查询访问到页面浏览的的转化信息

### 请求示例

```bash
curl --location --request GET 'http://${api-host}/v1/api/projects/${projectId}/analysis/funnel/${id}/chartdata?forceRefresh=false' \
--header 'Authorization: Bearer bbe40b12-96a5-459d-819d-feea0d9f85b5'
```

### 返回示例

```json
{
 "analysisInfo": {
 "name": "漏斗分析API示例",
 "startTime": "2022-03-03 00:00:00",
 "endTime": "2022-03-10 00:00:00",
 "conversionWindow": 1.0,
 "windowGranularity": "day",
 "fetchedTime": "1646879717428"
 },
 "resultHeader": [
 "时间",
 "总转化率",
 "访问",
 "第 1 步转化率",
 "访问"
 ],
 "resultRows": [
 [
 "全部",
 "0.0",
 "0.0",
 "0.0",
 "0.0"
 ],
 [
 "2022-03-03",
 "0",
 "0",
 "0",
 "0"
 ],
 ...
 ]
}
```
