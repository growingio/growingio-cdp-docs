# 平台级接口

## 概览

| **请求类型** | **API** | **接口描述** |
| :--- | :--- | :--- |
| Mutation | submitTagUserExportJobByKey | 提交导出标签用户任务 |
| Query | projects | 获取项目信息 |
| Query | jobResult | 根据任务ID查询任务结果 |
| Query | dataCenterUserProfile | 查询数据中心级别用户标签值或属性 |
| Query | dataCenterTags | 获取数据中心级别标签列表 |

## Mutation类型接口

### submitTagUserExportJobByKey

描述：提交导出标签用户任务

请求类型：Mutation

submitTagUserExportJobByKey\(parameter: TagUserExportJobByKeyInput!\): TagUserExportJob!

{% hint style="success" %}
该接口仅在13.4及以上版本提供，支持根据自定义标识符\(tagKey\)导出用户标签。

旧版本接口为 [submitTagUserExportJob](version-management.md#submittaguserexportjob)
{% endhint %}

参数说明：

| 参数名称 | 参数类型 | 参数描述 |
| :--- | :--- | :--- |
| tagKey | String! | 标签key |
| exportFileName | String | 导出文件名称，不带后缀 |
| properties | \[String!\] | 需要导出的用户属性标示 |
| charset | String | 编码格式，如 “UTF-16LE” |
| detailExport | Boolean |  |

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
mutation submitTagUserExportJobByKey {
  submitTagUserExportJobByKey(parameter: {tagKey: "tag_544"}) {
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
    "submitTagUserExportJobByKey": {
      "id": "VGFnVXNlckV4cG9ydEpvYkR0bzpXbEdra2pHYQ",
      "name": "DET-202104130903-32639610000000",
      "__typename": "TagUserExportJob",
      "description": null,
      "stage": "NONE",
      "creatorId": "ExQWOQ79",
      "createdAt": "2021-04-13T09:03:59.610Z",
      "updaterId": "J1GlEDjl",
      "updatedAt": null
    }
  }
}
```

## Query类型接口

### projects

描述：获取项目信息

请求类型: Query

接口签名：projects: \[Project!\]

返回值：GraphQL类型

```graphql
type Project {
    "项目id"
    id: HashId!
    "项目名称"                            
    name: String!
    "项目描述信息"                          
    description: String
    "创建者"                    
    creator: String
    "创建者id"                        
    creatorId: HashId!
    "创建时间"                     
    createdAt: DateTime!
    "项目拥有者"                   
    owner: String
    "项目拥有者id"                          
    ownerId: HashId!
    "项目成员列表"                       
    projectMembers: [ProjectMember!]
    "项目角色列表"       
    projectRoles: [ProjectRole!]   
    "项目成员数量"
    projectMemberCount: Int!        
}

type ProjectMember {
    "成员信息"
    member: Member
    "该成员担任的角色"                         
    role: ProjectRole
    "加入项目的时间"
    joinedAt: DateTime
    "上次访问的时间" 
    lastVisitAt: DateTime
}

type ProjectRole {
    "角色id"
    id: HashId
    "角色名称"
    name: String
    "角色描述"
    description: String
    "具备该角色的成员列表"
    members: [Member!] 
    "角色权限列表"
    permissions: [Permission!] 
    "是否为系统资源"
    isSystem: Boolean
    "是否为root角色"
    isRoot: Boolean
    "是否为技术支持"
    isTechSupport: Boolean
}

type Permission {
    "权限id"
    id: HashId
    "权限的 key/标识/动作"
    action: String
    "权限名称"
    name: String
}

type Member {
    "成员id"
    id: HashId!
    "成员名称"
    name: String 
    "创建方式：ldap, origin, oauth2, cas"
    source: String!
    "头像"
    avatar: String 
    "email地址"
    email: String 
    "创建时间"
    createdAt: DateTime!
    "手机号码"
    phoneNumber: String 
    "直属部门"
    directDepartment: Department 
    "唯一标识"
    identity: String
    "可访问的项目列表"
    enterableProjects: [Project!]
    "数据中心角色"
    dataCenterRole: DataCenterRole!
    "上次访问时间"
    lastVisitAt: DateTime
    "创建人"
    creator: String
}

type Department {
    "部门id"
    id: HashId!
    "部门名称"
    name: String!
    "父部门 id"
    parentId: String!
    "子部门列表"
    departments: [Department!] 
    "部门成员列表"
    members: [Member!]
    "部门成员数量"
    memberCount: Int!
}

type DataCenterRole {
    "数据中心角色id"
    id: HashId
    "角色名称"
    name: String
    "角色描述"
    description: String
    "具备该角色的成员"
    members: [Member!] 
    "该角色具备的权限"
    permissions: [Permission!] 
    "是否为系统资源"
    isSystem: Boolean
    "是否为root角色"
    isRoot: Boolean
    "是否为技术支持"
    isTechSupport: Boolean
}
```

请求示例：

```graphql
query Projects {
  projects {
    id
    name
  }
}
```

返回结果示例：JSON

```graphql
{
    "data": {
        "projects": [
            {
                "id": "xNQXmjpM",
                "name": "graphQ 测试项目"
            }
        ]
    }
}
```

### jobResult

描述：利用任务ID获取任务结果

请求类型: Query

接口签名：jobResult\(id: String!\): JobResult

参数说明：

| **参数名称** | **参数类型** | **参数描述** |
| :--- | :--- | :--- |
| id | String! | 任务ID |

返回值：GraphQL类型

```graphql
type JobResult {
    "任务结果id"
    id: HashId!
    "任务状态"
    stage: JobStage!
    "资源uri"
    uris: [String!] 
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
query JobResult {
  jobResult(id: "U2VnbWVudFVzZXJFeHBvcnRKb2JEdG86bWVROHduRG4") {
    __typename
    id
    stage
    uris
  }
}
```

返回结果示例：JSON

```graphql
{
    "data": {
        "jobResult": {
            "__typename": "JobResult",
            "id": "meQ8wnDn",
            "stage": "FINISH",
            "uris": [
                "/jobs/results/DES-202101251109-40191580841000/下载文件.csv"
            ]
        }
    }
}
```

{% hint style="success" %}
下载地址为：{平台链接} + '/download?file=' + uris

如数据平台链接为“[xxx.growingio.cn](https://dev1.growingio.cn/download?file=/jobs/results/DES-202101280404-14677315748000/%E4%B8%8B%E8%BD%BD%E7%94%A8%E6%88%B7%E5%88%97%E8%A1%A8.csv)”，则下载地址为：

xxx.growingio.cn/download?file=/jobs/results/DES-202101251109-40191580841000/下载文件.csv
{% endhint %}

### dataCenterUserProfile

描述：获取用户标签或属性（数据中心级别），如果userId在数据端为无效或不存在，则返回空。

请求类型: Query

接口签名：dataCenterUserProfile\(userId: String!, tags: \[HashId!\], properties: \[String!\]\): UserProfile

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
      <td style="text-align:left">userId</td>
      <td style="text-align:left">String!</td>
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
type dataCenterUserProfile {
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
query dataCenterUserProfile {
    dataCenterUserProfile( userId: "1001", properties: ["usr_sex","tag_payment"]) {
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
        "dataCenterUserProfile": {
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

### dataCenterTags

描述：获取标签列表

请求类型: Query

接口签名：dataCenterTags\(\): \[Tag\]

参数说明：无参数

返回值：GraphQL类型

```graphql
type Tag {
    "标签id"
    id: HashId!
    "标签名称"
    name: String!
    "标签标识符"
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

