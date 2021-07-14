# 项目级接口

## 概览

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

## Mutation类型接口

### submitSegmentUserExportJob

描述：提交导出分群用户任务

请求类型：Mutation

接口签名：submitSegmentUserExportJob\(projectId: HashId!, segmentId: HashId!, tags: \[HashId!\], properties: \[String!\], charset: String\): SegmentUserExportJob!

参数说明：

| **参数名称** | **参数类型** | **参数描述** |
| :--- | :--- | :--- |
| projectId | HashId! | 所属项目ID |
| segmentId | HashId! | 用户分群 ID |
| tags | \[HashId!\] | 需要导出的用户标签ID列表 |
| properties | \[String!\] | 需要导出的用户属性标示列表 |
| charset | String | 编码格式，如 “UTF-16LE” |

{% hint style="success" %}
其中tags和properties参数是可选的，用来获取相应的信息。

如在参数中提供了某个tag，则导出结果中会包含用户对应的该tag的相应信息。
{% endhint %}

返回值：GraphQL类型

```graphql
type SegmentUserExportJob {
    "任务id"
    id: String! 
    "任务名称"
    name: String!
    "描述信息"
    description: String 
    "任务状态"
    stage: JobStage!
    "创建者id"
    creatorId: HashId!
    "创建时间"
    createdAt: DateTime!
    "更新者id"
    updaterId: HashId
    "更新时间"
    updatedAt: DateTime
    "创建者"
    creator: String 
    "更新者"
    updater: String 
    "错误类型"
    error: Error
}

enum JobStage {
    # NONE 任务的初始状态
    # READY 任务准备执行
    # RUNNING 任务正在执行
    # DATA_READY 数据已经准备就绪
    # FINISH 任务完成
    # ERROR 任务执行失败
    NONE, READY, RUNNING, DATA_READY, FINISH, ERROR
}
```

请求示例：

```graphql
mutation SubmitSegmentUserExportJob {
  submitSegmentUserExportJob(projectId: "WlGk4Daj", segmentId: "qgQMXnD3", charset: "UTF-16LE") {
      __typename
      id
      name
      description
      stage
      creatorId
      createdAt
      updaterId
      updatedAt
      creator
      updater  
  }
} 
```

返回结果示例：JSON

```graphql
[
    {
        "data": {
            "submitSegmentUserExportJob": {
                "id": "U2VnbWVudFVzZXJFeHBvcnRKb2JEdG86eTlwbUxtUW0",
                "name": "DES-202101251129-41393863743000",
                "__typename": "SegmentUserExportJob",
                "description": null,
                "stage": "NONE",
                "creatorId": "zqQRq3Do",
                "createdAt": "2021-01-25T11:29:53.863810Z",
                "updaterId": "zqQRq3Do",
                "updatedAt": "2021-01-25T11:29:53.863810Z",
                "creator": "admin",
                "updater": "admin"
            }
        }
    }
]
```

### submitAnalysisExportJob

描述：提交统计数据导出任务

请求类型：Mutation

接口签名：submitAnalysisExportJob\(projectId: HashId!, id: HashId!, param: AnalysisExportJobParam!, charset: String\): AnalysisExportJob!

参数说明：

| **参数名称** | **参数类型** | **参数描述** |
| :--- | :--- | :--- |
| projectId | HashId! | 所属项目ID |
| id | HashId! | 资源ID |
| param | AnalysisExportJobParam! | 资源类型，支持：CHARTS\|FUNNELS\|RETENTIONS\|FREQUENCIES |
| charset | String | 编码格式，如 “UTF-16LE” |

返回值：GraphQL类型

```graphql
type AnalysisExportJob {
    "任务id"
    id: String! 
    "任务状态"
    stage: JobStage!
    "错误类型"
    error: Error
}

enum JobStage {
    # NONE 任务的初始状态
    # READY 任务准备执行
    # RUNNING 任务正在执行
    # DATA_READY 数据已经准备就绪
    # FINISH 任务完成
    # ERROR 任务执行失败
    NONE, READY, RUNNING, DATA_READY, FINISH, ERROR
}
```

请求示例：

```graphql
mutation SubmitAnalysisExportJob {
    submitAnalysisExportJob(id: "kqQewGry", param: {analysisType: CHARTS}, charset: "UTF-16LE", projectId: "WlGk4Daj") {
        id
        stage
        error {
            code
            __typename
        }
        __typename
    }
}
```

返回结果示例：JSON

```graphql
{
    "data": {
        "submitAnalysisExportJob": {
            "id": "Q0hBUlRTOjI5Y2E0MWFiYzA2NTgzYmFjMjY1ZjJlZTIwNDM2ZWNk",
            "stage": "FINISH",
            "error": {
                "code": "",
                "__typename": "Error"
            },
            "__typename": "AnalysisExportJob"
        }
    }
}
```

## Query类型接口

### userProfile

描述：查询单个用户的标签值和属性

请求类型: Query

接口签名：userProfile\(projectId: HashId!, userId: String, properties: \[String!\]\): UserProfile

参数说明：（请求参数“tags”和“properties”中须至少填写一个）

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#x53C2;&#x6570;&#x540D;&#x79F0;</b>
      </th>
      <th style="text-align:left"><b>&#x53C2;&#x6570;&#x7C7B;&#x578B;</b>
      </th>
      <th style="text-align:left"><b>&#x53C2;&#x6570;&#x63CF;&#x8FF0;</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">projectId</td>
      <td style="text-align:left">HashId!</td>
      <td style="text-align:left">&#x9879;&#x76EE;ID</td>
    </tr>
    <tr>
      <td style="text-align:left">userId</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x7528;&#x6237;ID</td>
    </tr>
    <tr>
      <td style="text-align:left">properties</td>
      <td style="text-align:left">[String!]</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237;&#x5C5E;&#x6027;&#x6807;&#x8BC6;&#x7B26;&#xFF0C;&#x5982;
          usr_sex</p>
        <p>&#x7528;&#x6237;&#x6807;&#x7B7E;&#x6807;&#x8BC6;&#x7B26;&#xFF0C;&#x5982;
          tag_payment</p>
      </td>
    </tr>
  </tbody>
</table>

{% hint style="success" %}
用户属性标识符为 usr\_ + {自定义标识符}

用户标签标识符为 {自定义标识符}，定义时强制以 tag\_ 开头
{% endhint %}

返回值：GraphQL类型

```graphql
type UserProfile {
    "用户详细信息id"
    id: String!
    "用户gid"
    userId: String!
    "属性列表"
    properties: [InsensitiveProperty]
}

type InsensitiveProperty {
    ""
    key: String!
    ""
    name: String
    ""
    value: String
}
```

请求示例：

```graphql
query userProfile {
    userProfile(projectId: "WlGk4Daj"
                , userId: "1001"
                , properties:["usr_sex","tag_payment"]) {
        id
        userId
        properties {
         key
         name
         value
        }
    }
}
```

返回结果示例：JSON

```graphql
{
    "data": {
        "userProfile": {
            "id": "1001",
            "userId": "1001",
            "properties": [
                {
                    "key": "usr_sex",
                    "name": "用户属性-性别",
                    "value": "男"
                },
                {
                    "key": "tag_payment",
                    "name": "用户标签-支付次数",
                    "value": "300"
                }
            ]
        }
    }
}
```

### segments

描述：获取用户分群列表

请求类型: Query

接口签名：segments\(projectId: HashId!\): \[Segment\]

参数说明：

| **参数名称** | **参数类型** | **参数描述** |
| :--- | :--- | :--- |
| projectId | HashId! | 项目ID |

返回值：GraphQL类型

```graphql
type Segment {
    "分群id"
    id: HashId!
    "分群名称"
    name: String!
    "分群描述信息"
    description: String
    "规则定义"
    compute: ComputeDefinition!
    "计算频率，可分为每周计算一次/每天计算一次等"
    scheduler: String!
    "创建者id"
    creatorId: HashId!
    "创建时间"
    createdAt: DateTime!
    "更新者id"
    updaterId: HashId
    "更新时间"
    updatedAt: DateTime
    "创建者"
    creator: String 
    "更新者"
    updater: String 
    "创建来源"
    createdBy: String
    ""
    detector: Detector
    "拥有者id"
    ownerId: HashId! 
}

type Detector {
    ""
    stage: DetectedStage!
    ""
    description: String
    ""
    detectedAt: DateTime
    ""
    totalUsers: Int
    ""
    usersRatio: Float
}

enum DetectedStage {
    NONE, READY, RUNNING, FINISH, ERROR
}

type ComputeDefinition {
    ""
    name: String 
    ""
    expression: String!
    ""
    directives: [ComputeDirective]! 
    ""
    drillDownAttrs: Object
    ""
    sql: String 
    ""
    dataUri: String 
}

type ComputeDirective {
    ""
    alias: String!
    "用来表示指标"
    measurement: Measurement!
    "时间"
    timeRange: String
    "表示过滤条件"
    filter: Filter
    ""
    op: String 
    ""
    attribute: String 
    ""
    aggregator: String 
    ""
    values: [String] 
}

type Measurement {
    "指标id"
    id: String!
    "指标类型"
    type: String!
    "指标的过滤条件"
    filter: Filter
    "指标名"     
    name: String
    "权限的 key/标识/动作"        
    action: String
    "表示时间，比如 7天前 day:8,1, 30天前 day:31,1, 绝对时间  abs:1603631197000,1604631197000" 
    timeRange: String
    ""   
    attribute: String
    "聚合方式，如 sum" 
    aggregator: String
    "指标权重"  
    weight: Float       
}

type Filter {
    "维度的 key"
    key: String
    "过滤的操作，比如：in, not in, like, =, !="   
    op: String
    "维度名"    
    name: String
    "维度值"    
    values: [String]
    "过滤规则/表达式"    
    exprs: [Filter]
    "维度值类型"
    valueType: String 
}
```

请求示例：

```graphql
query Segment {
    segment(id: "bVG24AQ6", projectId: "WlGk4Daj") {
        id
        name
        description
        scheduler
        creatorId
        createdAt
        createdBy
        updaterId
        updatedAt
        createdBy
        creator
        updater
        detector {
            description
            detectedAt
            stage
            totalUsers
            usersRatio
            __typename
        }
        compute {
            name
            expression
            directives {
                alias
                measurement {
                    id
                    name
                    type         
                    attribute
                    aggregator
                    __typename
                }
                op
                values
                attribute
                aggregator
                timeRange
                filter {
                    op
                    exprs {
                        key
                        op
                        name
                        values
                        valueType
                        __typename
                    }
                    __typename
                }
                __typename
            }
            __typename
        }
        __typename
    }
}
```

返回结果示例：JSON

```graphql
{
    "data": {
        "segment": {
            "id": "bVG24AQ6",
            "name": "0125-999",
            "description": "",
            "scheduler": "DAILY",
            "creatorId": "n1QVaDyR",
            "createdAt": "2021-01-25T09:03:39.246183Z",
            "createdBy": "DIRECT",
            "updaterId": "n1QVaDyR",
            "updatedAt": "2021-01-25T09:03:39.246184Z",
            "creator": "admin",
            "updater": "admin",
            "detector": {
                "description": null,
                "detectedAt": "2021-01-25T09:03:49.072Z",
                "stage": "ERROR",
                "totalUsers": 0,
                "usersRatio": 0.0,
                "__typename": "Detector"
            },
            "compute": {
                "name": "",
                "expression": "A",
                "directives": [
                    {
                        "alias": "A",
                        "measurement": {
                            "id": "vv",
                            "name": null,
                            "type": "prepared",
                            "attribute": null,
                            "aggregator": null,
                            "__typename": "Measurement"
                        },
                        "op": ">=",
                        "values": [
                            "1"
                        ],
                        "attribute": "",
                        "aggregator": "sum",
                        "timeRange": "day:31,1",
                        "filter": {
                            "op": "and",
                            "exprs": [
                                {
                                    "key": "usr_test_1117_int",
                                    "op": "not between",
                                    "name": "test_1117_int",
                                    "values": [
                                        "-999",
                                        "9"
                                    ],
                                    "valueType": "int",
                                    "__typename": "Filter"
                                },
                                {
                                    "key": "d",
                                    "op": "=",
                                    "name": "域名",
                                    "values": [
                                        "www.growingio.com"
                                    ],
                                    "valueType": "",
                                    "__typename": "Filter"
                                },
                                {
                                    "key": "usr_isPayed_ppl",
                                    "op": "=",
                                    "name": "是否付费（用户变量）",
                                    "values": [
                                        "付费版"
                                    ],
                                    "valueType": "string",
                                    "__typename": "Filter"
                                }
                            ],
                            "__typename": "Filter"
                        },
                        "__typename": "ComputeDirective"
                    }
                ],
                "__typename": "ComputeDefinition"
            },
            "__typename": "Segment"
        }
    }
}
```

### tags

描述：获取标签列表

请求类型: Query

接口签名：tags\(projectId: HashId!\): \[Tag\]

参数说明：

| **参数名称** | **参数类型** | **参数描述** |
| :--- | :--- | :--- |
| projectId | HashId! | 项目ID |

返回值：GraphQL类型

```graphql
type Tag {
    "标签id"
    id: HashId!
    "标签名称"
    name: String!
    "关键字"
    key: String!
    "标签类型"
    type: String!
    "tag描述信息"
    description: String
    "标签规则"
    computes: [ComputeDefinition]! 
    "业务类型"
    businessType: String
    "创建者id"
    creatorId: HashId!
    "创建时间"
    createdAt: DateTime!
    "更新者id"
    updaterId: HashId
    "更新时间"
    updatedAt: DateTime
    "创建者"
    creator: String 
    "更新者"
    updater: String 
    "值类型"
    valueType: ValueType
    ""
    detector: Detector
    "拥有者 id"
    ownerId: HashId 
}

type ComputeDefinition {
    ""
    name: String
    ""
    expression: String!
    ""
    directives: [ComputeDirective]!
    ""
    drillDownAttrs: Object
    ""
    sql: String
    ""
    dataUri: String
}

type ComputeDirective {
    ""
    alias: String!
    ""
    measurement: Measurement!
    ""
    timeRange: String
    ""
    filter: Filter
    ""
    op: String 
    ""
    attribute: String 
    ""
    aggregator: String 
    ""
    values: [String] 
}
```

请求示例：

```graphql
query dataCenterTags {
    dataCenterTags{
        id
        key
        name
        creator
        createdAt
        updater
        updatedAt
        __typename
    }
}
```

返回结果示例：JSON

```graphql
{
    "data": {
        "tags": [
            {
                "id": "mgGJj3GA",
                "key": "tag_payment",
                "name": "用户标签-支付次数",
                "creator": "gio_test",
                "createdAt": "2021-01-12T02:27:54.550872Z",
                "updater": null,
                "updatedAt": "2021-01-12T02:27:54.550872Z",
                "__typename": "Tag"
            },
            ......
            {
                "id": "JnG4NBQz",
                "key": "tag_last_payment",
                "name": "用户标签-最后一次支付距今日期",
                "creator": "gio_test",
                "createdAt": "2021-01-12T03:53:02.634829Z",
                "updater": null,
                "updatedAt": "2021-01-12T03:53:02.634829Z",
                "__typename": "Tag"
            }
       ]
    }
}
```

### funnelAnalyses

描述：获取漏斗分析列表

请求类型: Query

接口签名：funnelAnalyses\(projectId: HashId!\): \[FunnelAnalysis\]

参数说明：

| **参数名称** | **参数类型** | **参数描述** |
| :--- | :--- | :--- |
| projectId | HashId! | 项目ID |

返回值：GraphQL类型

```graphql
type FunnelAnalysis {
    "分析的id"
    id: HashId!
    "此条分析名称"
    name: String!
    "此分析描述信息"
    description: String 
    "指标列表"
    measurements: [Measurement]!
    "转化周期，天"
    conversionWindow: Int
    "时间"
    timeRange: String
    "目标用户"
    targetUser: TargetUser
    "过滤条件"
    filter: Filter
    "维度对比/用户对比"
    splitter: Splitter
    "是否为系统资源"
    isSystem: Boolean
    "业务类型"
    businessType: String
    "创建者id"
    creatorId: HashId!,
    "创建时间"
    createdAt: DateTime!
    "更新者id"
    updaterId: HashId 
    "更新时间"
    updatedAt: DateTime 
    "创建者"
    creator: String
    "更新者"
    updater: String 
    "拥有者"
    ownerId: HashId
}

type TargetUser {
    "目标用户id"
    id: String!
    "目标用户姓名"
    name: String 
}

type Splitter {
    ""
    key: String!
    ""
    values: [String] 
    ""
    users: [TargetUser] 
    ""
    actions: [Action] 
    ""
    splitters: [Splitter] 
    ""
    selectedValues: [String] 
    ""
    selectedIndices: [Int] 
    ""
    valueType: String 
    ""
    name: String 
}

type Action {
    ""
    measurement: Measurement
    ""
    excluded: Boolean
    ""
    eventType: String
}
```

请求示例：

```graphql
query FunnelAnalyses {
  funnelAnalyses(projectId: "WlGk4Daj") {
    id
    name
  }
}
```

返回结果示例：JSON

```graphql
{
  "data": {
    "funnelAnalyses": [
      {
        "id": "zqQR3po3",
        "name": "漏斗-维度对比"
      },
      {
        "id": "wWDrwQML",
        "name": "漏斗-过滤条件"
      },
      {
        "id": "klGvyp7E",
        "name": "看板-无过滤条件"
      },
      {
        "id": "y9pm1pme",
        "name": "豆腐豆腐"
      }
    ]
  }
}
```

### eventAnalyses

描述：获取事件分析列表

请求类型: Query

接口签名：eventAnalyses\(projectId: HashId!\): \[EventAnalysis\]

参数说明：

| **参数名称** | **参数类型** | **参数描述** |
| :--- | :--- | :--- |
| projectId | HashId! | 项目ID |

返回值：GraphQL类型

```graphql
type EventAnalysis {
    "事件分析id"
    id: HashId!
    "事件分析名称"
    name: String!
    "描述信息"
    description: String @wrapper
    "指标列表"
    measurements: [Measurement]!  
    "olap(新 chart-service) 服务的指标模型"
    metrics: [OlapMetric]!  
    "维度"
    dimensions: [String]  
    "粒度"
    granularities: [Granularity] 
    "时间"
    timeRange: String!
    "过滤条件"
    filter: Filter
    "目标用户"
    targetUser: TargetUser
    "数据最多条数"
    limit: Int @wrapper,
    "属性"
    attrs: BytesJson
    "排序方式"
    orders: [Order] 
    "维度对比/用户对比"
    splitter: Splitter
    "图表类型"
    chartType: String
    "是否为系统资源"
    isSystem: Boolean
    "业务类型"
    businessType: String
    "创建者id"
    creatorId: HashId!,
    "创建时间"
    createdAt: DateTime!
    "更新者id"
    updaterId: HashId 
    "更新时间"
    updatedAt: DateTime 
    "创建者"
    creator: String 
    "更新者"
    updater: String 
    "拥有者"
    ownerId: HashId 
}

type OlapMetric {
    "事件id。 e.g.: uc, xxxxx"
    id: String!
    "事件类型"
    type: String!
    "事件名称"
    name: String 
    "重命名"
    alias: String
    "是否是事件下边的事件级变量"
    attribute: String
    "基于哪种方式聚合. 目前只有按人聚合. 2021年01月11日13:21:04"
    subgroupAggregation: SubgroupAggregation 
    "指标的度量. e.g.: sum, total。 详见 olap 服务"
    math: String
}

type Granularity {
    ""
    id: String,
    ""
    values: [String] 
    ""
    interval: Long 
    ""
    split: Float 
    ""
    statistics: [String] 
    ""
    ranges: [Float] 
    ""
    top: Int 
    ""
    period: String 
    ""
    trend: Boolean
}
```

请求示例：

```graphql
query EventAnalyses {
  eventAnalyses(projectId: "WlGk4Daj") {
    id
    name
  }
}
```

返回结果示例：JSON

```graphql
{
  "data": {
    "eventAnalyses": [
      {
        "id": "qyD6qGKJ",
        "name": "事件分析"
      },
      {
        "id": "RqQwPpJw",
        "name": "气泡图"
      },
      {
        "id": "evp9kDOx",
        "name": "表格"
      },
      #......
      {
        "id": "WlGk4Daj",
        "name": "sql标签"
      }
    ]
  }
}
```

### retentionAnalyses

描述：获取留存分析列表

请求类型: Query

接口签名：retentionAnalyses\(projectId: HashId!\): \[RetentionAnalysis\]

参数说明：

| **参数名称** | **参数类型** | **参数描述** |
| :--- | :--- | :--- |
| projectId | HashId! | 项目ID |

返回值：GraphQL类型

```graphql
type RetentionAnalysis {
    "留存分析id"
    id: HashId!
    "此条分析名称"
    name: String!
    "此条分析描述信息"
    description: String 
    "指标列表"
    measurements: [Measurement]! 
    ""
    range: String!
    "事件类型"
    eventType: String
    "时间"
    timeRange: String!
    "目标用户"
    targetUser: TargetUser
    ""
    currentTurn: Int
    "维度对比/用户对比"
    splitter: Splitter
    "图表类型"
    chartType: String!
    "创建者id"
    creatorId: HashId!
    "创建时间"
    createdAt: DateTime!
    "更新者id"
    updaterId: HashId 
    "更新时间"
    updatedAt: DateTime 
    "创建者"
    creator: String 
    "更新者"
    updater: String 
    "拥有者"
    ownerId: HashId 
}
```

请求示例：

```graphql
query RetentionAnalyses {
  retentionAnalyses(projectId: "WlGk4Daj") {
    id
    name
  }
}
```

返回结果示例：JSON

```graphql
{
  "data": {
    "retentionAnalyses": [
      {
        "id": "zqQR3po3",
        "name": "留存-留存行为对比"
      },
      {
        "id": "wWDrwQML",
        "name": "留存-维度对比"
      },
      {
        "id": "rRGoYQml",
        "name": "留存-起始行为-过滤条件"
      },
      #......
      {
        "id": "n1QVaDyR",
        "name": "留存-无过滤条件"
      }
    ]
  }
}
```

### frequencyAnalyses

描述：获取分布分析列表

请求类型: Query

接口签名：frequencyAnalyses\(projectId: HashId!\): \[FrequencyAnalysis\]

参数说明：

| **参数名称** | **参数类型** | **参数描述** |
| :--- | :--- | :--- |
| projectId | HashId! | 项目ID |

返回值：GraphQL类型

```graphql
type FrequencyAnalysis {
    "此条分析的id"
    id: HashId!
    "此条分析的名称"
    name: String!
    "此条分析的描述信息"
    description: String
    "指标列表"
    measurements: [Measurement]!  
    "维度"
    dimensions: [String] 
    "粒度"
    granularities: [Granularity]
    "时间"
    timeRange: String!
    "过滤条件"
    filter: Filter
    "维度对比/用户对比"
    splitter: Splitter
    "目标用户"
    targetUser: TargetUser
    "图表类型"
    chartType: String
    "是否为系统资源"
    isSystem: Boolean
    "业务类型"
    businessType: String
    "创建者id"
    creatorId: HashId!
    "创建时间"
    createdAt: DateTime!
    "更新者id"
    updaterId: HashId
    "更新时间"
    updatedAt: DateTime
    "创建者"
    creator: String
    "更新者"
    updater: String
    "拥有者id"
    ownerId: HashId @resourceOwnerId
}
```

请求示例：

```graphql
query FrequencyAnalyses {
  frequencyAnalyses(projectId: "WlGk4Daj") {
    id
    name
  }
}
```

返回结果示例：JSON

```graphql
{
  "data": {
    "frequencyAnalyses": [
      {
        "id": "zqQR3po3",
        "name": "分布分析"
      },
      {
        "id": "n1QVaDyR",
        "name": "分布分析-维度对比"
      },
      {
        "id": "AbQ3bDYe",
        "name": "分布分析-无过滤条件"
      },
      {
        "id": "y9pm1pme",
        "name": "分布分析-过滤条件"
      }
    ]
  }
}
```

