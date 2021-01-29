# 操作指南

## 用户标签导出

### 1.获取项目id

为了导出或下载需要的标签，我们需要先选择具体的项目，获取项目ID，相关API为projects: \[Project!\]。

请求项目信息：

```graphql
query Projects {
  projects {
    id
    name
  }
}
```

返回结果：

```graphql
{
    "data": {
        "projects": [
            {
                "id": "WlGk4Daj",
                "name": "默认项目"
            }
        ]
    }
}
```

### 2.获取标签列表

这里选取默认项目，id为 "WlGk4Daj" ，接下来获取标签列表：

```graphql
query Tags {
  tags(projectId: "WlGk4Daj") {
    id
    name
  }
}
```

得到结果：

```graphql
{
  "data": {
    "tags": [
        {
          "id": "mgGJj3GA",
          "name": "标签1"
        },
        {
          "id": "zZDb1jG9",
          "name": "标签2"
        },
        {
          "id": "JnG4NBQz",
          "name": "标签3"
        }
        # 省略......
        {
          "id": "V0G5aXGA",
          "name": "标签n"
        }
    }
}
```

### 3.导出所需标签

如果要导出某条标签，以ID为“mgGJj3GA”的标签为例，相关API为：submitTagUserExportJob\(tagId: HashId!, properties: \[String!\], charset: String, detailExport: Boolean\): TagUserExportJob!，该接口提交一个导出特定标签的任务并返回一个任务对象\(GraphQL类型\)。

请求：

  










