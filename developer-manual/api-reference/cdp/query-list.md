# 请求列表

目前 GrowingIO 系统提供以下请求方法：

| Type | Function Name | 说明 |
| :--- | :--- | :--- |
| Mutation | submitTagUserExportJob | 提交导出标签用户任务 |
| Mutation | submitSegmentUserExportJob | 提交导出分群用户任务 |
| Query | jobResult | 查询任务结果 |
| Query | userProfile | 查询单个用户的标签值或属性 |
| Query | tags | 获取标签列表 |
| Query | segments | 获取用户分群列表 |

## **数据结构**

请求中涉及到的数据结构有：  
  
**Error:**

```text
{
	code: String // 内部错误码
	message: String // 错误消息
}
```

**JobStage \(枚举型\):**

```text
{
	// NONE 任务初始状态
	// READY 任务准备执行
	// RUNNING 任务正在执行
	// DATA_READY 数据准备就绪
	// FINISH 任务完成
	// ERROR 任务失败
	NONE, READY, RUNNING, DATA_READY, ERROR
}
```

**TagUserExportJob:**

```text
{
	id: String
	name: String
	description: String
	stage: JobStage
	creatorId: String
	updaterId: String
	updatedAt: DateTime
	error: Error
}
```

**SegmentUserExportJob:**

```text
{
	id: String
	name: String
	description: String
	stage: JobStage
	creatorId: String
	createdAt: DateTime
	updaterId: String
	updatedAt: DateTime
	error: Error
}
```

**JobResult:**

```text
{
	id: String
	stage: JobStage
	uris: [String] // 任务输出文件目录
}
```

**Property:**

```text
{
	key: String
	name: String
	value: String
}
```

**UserProfile:**

```text
{
	id: String
	userId: String
	properties: [Property]
}
```

**Tag:**

```text
{
	id: String
	name: String
	type: String
	description: String
	creatorId: String
	createdAt: DateTime
	updaterId: String
	updatedAt: DateTime
	creator: String
	updater: String
}
```

**Segment:**

```text
{
	id: String
	name: String
	description: String
	scheduler: String
	creatorId: String
	createdAt: DateTime
	updaterId: String
	updatedAt: DateTime
}
```

## 函数

**提交标签用户导出任务**

```text
# tagId: 标签 ID
# properties: 需要导出的用户属性标示
submitTagUserExportJob(tagId: String!, properties: [String!]): TagUserExportJob!

示例：
mutation {
    submitTagUserExportJob(tagId: "ZYoXrmRq",properties: ["$basic_name","$basic_email","usr_company"]) {
        id
        name
    }
}
```

**提交分群用户导出任务**

```text
# segmentId: 用户分群 ID
# tags: 需要导出的用户标签 ID 列表
# properties: 需要导出的用户属性标示列表
submitSegmentUserExportJob(segmentId: String!, tags: [String!], properties: [String!]): SegmentUserExportJob!

示例：
mutation {
    submitSegmentUserExportJob(segmentId: "MQRe7qoq", tags: ["d4PYBjoM","gnPNYkRW","KnoqwDRk","La9BLwPn","AwoVLvR2","nxogj0Pm"], properties: ["$basic_mobile","mobile_undefined"]) {
        id
        name
    }
}
```

**查看任务结果**

```text
# id: 任务 ID
jobResult(id: String!): JobResult

示例：
query {
    jobResult(id: "Lj9yBRyD") {
        stage
        uris
    }
}
```

**查询单个用户的标签值和属性**

```text
# userId: 用户 ID
# tags: 用户标签 ID 列表
# properties: 用户属性标示列表
userProfile(userId: String, tags: [HashId!], properties: [String!]): UserProfile

示例：
query {
    userProfile(userId: "195699") {
        properties {
            key
            name
            value
        }
    }
}
```

**获取标签列表**

```text
tags: [Tag]

示例：
query {
    tags {
        id
        name
    }
}
```

**获取用户分群列表**

```text
segments: [Segment]

示例：
query {
    segments {
        id
        name
    }
}
```

**统计数据导出**

```text
# id: String [资源id]
# param: {"analysisType": "CHARTS"} [资源类型，支持CHARTS|FUNNELS|RETENTIONS|FREQUENCIES]
submitAnalysisExportJob(id: HashId!, param: AnalysisExportJobParam!): AnalysisExportResult!

式例
mutation SubmitAnalysisExportJob($id: HashId!, $param: AnalysisExportJobParam!){
    submitAnalysisExportJob(id: $id, param: $param) {
        id
        status 
        uri
    }
}

Curl 示例
curl --location --request POST 'http://cdp.growingio.com/graphql' \
--header 'Cache-Control: no-cache' \
--header 'DNT: 1' \
--header 'Host: 10.0.6.60:8086' \
--header 'Postman-Token: 90603b24-c8b2-4a2c-9b42-15ec4880089d,316e4f2f-60bb-42d5-ac0a-3f2f3f4810d3' \
--header 'Referer: http://localhost:8000/data/dataSources' \
--header 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.132 Safari/537.36' \
--header 'accept: */*' \
--header 'accept-encoding: gzip, deflate' \
--header 'Content-Type: application/json' \
--header 'Authorization: NmUxMTAwYjctYjRmMS00NjcwLWI0MTItNjBhY2U0ZmNlMmNl' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"mutation SubmitAnalysisExportJob($id: HashId!, $param: AnalysisExportJobParam!){\n    submitAnalysisExportJob(id: $id, param: $param) {\n        resourceId\n        status \n        uri\n    }\n}","variables":{"id":"y9pm11pm","param":{"analysisType":"FUNNELS"}}}'
```

