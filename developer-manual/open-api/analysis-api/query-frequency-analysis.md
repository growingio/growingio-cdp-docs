---
id: query-frequency-analysis
sidebar_position: 4
---

#项目-事件分析查询
##  接口说明 
获取指定分布分析的统计结果 
## 接口地址 
http://${api-host}/v1/api/projects/${projectId}/analysis/frequency/${id}/chartdata 
## 请求方式 
GET 
## 公共请求参数 
[公共请求参数](https://docs.growingio.com/op-help/docs/2.6/developer-manual/open-api#%E5%85%AC%E5%85%B1%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)
## 查询参数 
| 名称  | 类型  | 必填  | 描述  | 示例值  |
| --- | --- | --- | --- | --- |
| forceRefresh  | boolean  | 否  | 忽略缓存  | false  |

## 返回数据 
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
查询任意行为到任意行为的的留存信息 
### 请求示例
```bash
curl --location --request GET 'http://${api-host}/v1/api/projects/${projectId}/analysis/frequency/${id}/chartdata?forceRefresh=false' \ --header 'Authorization: Bearer bbe40b12-96a5-459d-819d-feea0d9f85b5' 
```

### 返回示例
```json
{ 
 "analysisInfo": { 
 "name": "分布分析API示例", 
 "startTime": "2022-03-07 00:00:00", 
 "endTime": "2022-03-10 00:00:00", 
 "granularity": "", 
 "fetchedTime": "1646880275623" 
 }, 
 "resultHeader": [ 
 "活跃天数 区间范围", 
 "用户量", 
 "用户量占比" 
 ], 
 "resultRows": [ 
 [ 
 "[0.0,0.0]", 
 "0", 
 "0.0" 
 ] 
 ] 
}
```
