---
id: query-event-analysis
sidebar_position: 1
---
# 项目-事件分析查询
## 接口说明 
获取指定事件分析的统计结果 
## 接口地址 
`http://${api-host}/v1/api/projects/${projectId}/analysis/olap_event/${id}/chartdata` 
## 请求方式 
GET 
## 公共请求参数 
[公共请求参数](https://docs.growingio.com/op-help/docs/2.6/developer-manual/open-api#%E5%85%AC%E5%85%B1%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)
## 查询参数 
| **名称** | **类型** | **必填** | **描述** | **示例值** |
| --- | --- | --- | --- | --- |
| forceRefresh  | boolean  | 否  | 忽略缓存  | false  |
| limit  | int  | 否  | 单次查询返回数据上限 
最大 50,000， 
默认1000  | 1000  |
| offset  | int  | 否  | 查询标示位 
默认0  | 0  |

## 返回数据 
paginationInfo 分页信息数据 

| **名称** | **类型** | **描述** |
| --- | --- | --- |
| offset  | int  | 查询标识位  |
| limit  | int  | 单次查询返回数据上限  |
| totalCount  | int  | 本次查询总计返回数据量  |
| hasNextPage  | boolean  | 是否有下一页 
false：否 
true：是  |
| hasPreviousPage  | boolean  | 是否有上一页 
false：否 
true：是  |

analysisInfo单图信息数据 

| **名称** | **类型** | **描述** |
| --- | --- | --- |
| name  | String  | 分析名称  |
| startTime  | String  | 开始事件  |
| endTime  | String  | 结束时间  |
| granularity  | String  | 时间粒度  |
| fetchedTime  | Long  | 数据查询时间  |

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
