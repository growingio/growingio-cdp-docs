# 接口说明

## 简介

GrowingIO 提供的接口统一使用 GraphQL 格式，下面是 GraphQL 接口的请求信息：

| Method | Path | Request Body | Response Body |
| :--- | :--- | :--- | :--- |
| POST | /graphql | application/json | application/json |

GraphQL 接口区分 Query 和 Mutation 两类，其中 Query 请求用于查询数据，Mutation 请求用于操作/修改数据。

### 平台级接口：

| **请求类型** | **API** | **接口描述** |
| :--- | :--- | :--- |
| Mutation | submitTagUserExportJobByKey | 提交导出标签用户任务 |
| Query | projects | 获取项目信息 |
| Query | jobResult | 根据任务ID查询任务结果 |
| Query | dataCenterUserProfile | 查询数据中心级别用户标签值或属性 |
| Query | dataCenterTags | 获取数据中心级别标签列表 |

### 项目级接口：

| **请求类型** | **API** | **接口描述** |
| :--- | :--- | :--- |
| Mutation | submitSegmentUserExportJob | 提交导出用户分群任务 |
| Mutation | submitAnalysisExportJob | 提交统计数据导出任务 |
| Query | userProfile | 查询单个用户的标签值或属性 |
| Query | segments | 获取用户分群列表 |
| Query | tags | 获取标签列表 |
| Query | funnelAnalyses | 获取漏斗分析列表 |
| Query | eventAnalyses | 获取事件分析列表 |
| Query | retentionAnalyses | 获取留存分析列表 |
| Query | frequencyAnalyses | 获取分布分析列表 |

{% hint style="danger" %}
请求项目级接口时，必须输入参数 **projectId**
{% endhint %}

## 系统自定义GraphQL标量

在数据导出相关的API中，使用了一些系统自定义的GraphQL标量，如下所示：

**HashId**: OP平台中的对象 \(如项目、标签等\) 拥有的一个独特的ID，以长度为8个字符的字符串表示，包含大小写英文字母与阿拉伯数字。

**DateTime**: 符合RFC 3339规范的日期时间表示形式。

**BytesJson**: 返回一个JSON。

