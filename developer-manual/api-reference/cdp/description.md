# 接口说明

## 简介

GrowingIO 提供的接口统一使用 GraphQL 格式，下面是 GraphQL 接口的请求信息：

| Method | Path | Request Body | Response Body |
| :--- | :--- | :--- | :--- |
| POST | /graphql | application/json | application/json |

GraphQL 接口区分 Query 和 Mutation 两类，其中 Query 请求用于查询数据，Mutation 请求用于操作/修改数据。

目前 GrowingIO 系统提供以下请求方法：

| **请求类型** | **API** | **接口描述** |
| :--- | :--- | :--- |
| Mutation | submitTagUserExportJob | 提交导出标签用户任务 |
| Mutation | submitSegmentUserExportJob | 提交导出用户分群任务 |
| Mutation | submitAnalysisExportJob | 提交统计数据导出任务 |
| Query | projects | 获取项目信息 |
| Query | jobResult | 根据任务ID查询任务结果 |
| Query | userProfile | 查询单个用户的标签值或属性 |
| Query | segments | 获取用户分群列表 |
| Query | tags | 获取标签列表 |
| Query | funnelAnalyses | 获取漏斗分析列表 |
| Query | eventAnalyses | 获取事件分析列表 |
| Query | retentionAnalyses | 获取留存分析列表 |
| Query | frequencyAnalyses | 获取分布分析列表 |

## 系统自定义GraphQL标量

在数据导出相关的API中，使用了一些系统自定义的GraphQL标量，如下所示：

**HashId**: OP平台中的对象 \(如项目、标签等\) 拥有的一个独特的ID，以长度为8个字符的字符串表示，包含大小写英文字母与阿拉伯数字。

**DateTime**: 符合RFC 3339规范的日期时间表示形式。

**BytesJson**: 返回一个JSON。

## Mutation类型接口

### submitTagUserExportJob

描述：提交导出标签用户任务

请求类型：Mutation

接口签名：submitTagUserExportJob\(tagId: HashId!, properties: \[String!\], charset: String, detailExport: Boolean\): TagUserExportJob!

参数说明：

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
      <td style="text-align:left">tagId</td>
      <td style="text-align:left">HashId!</td>
      <td style="text-align:left">&#x8981;&#x5BFC;&#x51FA;&#x7684;&#x7528;&#x6237;&#x6807;&#x7B7E;&#x7684;ID</td>
    </tr>
    <tr>
      <td style="text-align:left">properties</td>
      <td style="text-align:left">[String!]</td>
      <td style="text-align:left">&#x9700;&#x8981;&#x5BFC;&#x51FA;&#x7684;&#x7528;&#x6237;&#x5C5E;&#x6027;&#x6807;&#x793A;</td>
    </tr>
    <tr>
      <td style="text-align:left">charset</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x7F16;&#x7801;&#x683C;&#x5F0F;&#xFF0C;&#x5982; &#x201C;UTF-16LE&#x201D;</td>
    </tr>
    <tr>
      <td style="text-align:left">detailExport</td>
      <td style="text-align:left">Boolean</td>
      <td style="text-align:left">
        <p>&#x5F53;detailExport&#x4E3A;True&#x65F6;&#xFF0C;&#x4E3A;&#x670D;&#x52A1;&#x7AEF;&#x63A5;&#x53E3;&#x8C03;&#x7528;&#x65F6;&#x9009;&#x7528;&#xFF0C;&#x5BFC;&#x51FA;&#x683C;&#x5F0F;&#x4E3A;&#x8BE6;&#x60C5;&#xFF0C;</p>
        <p>False&#x4E3A;&#x524D;&#x7AEF;&#x63A5;&#x53E3;&#x8C03;&#x7528;&#x65F6;&#x9009;&#x7528;&#xFF0C;&#x8FD4;&#x56DE;&#x7ED3;&#x679C;&#x4E3A;&#x7B80;&#x6D01;&#x683C;&#x5F0F;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>

返回值：GraphQL类型

```graphql
type TagUserExportJob {
    "导出操作任务的id"
    id: String! 
    "任务名"
    name: String!
    "任务描述"
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

type Error {
    "错误码"
    code: String   
    "错误信息" 
    message: String   
}
```

请求示例：

```graphql
mutation SubmitTagUserExportJob {
  submitTagUserExportJob(tagId: "mgGJj3GA", charset: "UTF-16LE", detailExport: false) {
      id
      name
      __typename
      description
      stage
      creatorId
      createdAt
      updaterId
      updatedAt   
  }
} 
```

返回结果示例：JSON

```graphql
{
    "data": {
        "submitTagUserExportJob": {
            "id": "VGFnVXNlckV4cG9ydEpvYkR0bzp3ZURxOWVERQ",
            "name": "DET-202101250901-32498440381000",
            "__typename": "TagUserExportJob",
            "description": null,
            "stage": "NONE",
            "creatorId": "zqQRq3Do",
            "createdAt": "2021-01-25T09:01:38.440443Z",
            "updaterId": "zqQRq3Do",
            "updatedAt": "2021-01-25T09:01:38.440443Z"
        }
    }
}
```

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













