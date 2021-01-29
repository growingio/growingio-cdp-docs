# 操作指南

## 用户标签导出

### 1.获取项目id

为了导出或下载需要的标签，我们需要先选择具体的项目，获取项目ID，相关API为 **projects** 。

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

如果要导出某条标签，以ID为“mgGJj3GA”的标签为例 \( 相关API为：**submitTagUserExportJob** \)，通过接口提交一个导出特定标签的任务并返回一个任务对象\(GraphQL类型\)。

请求：

```graphql
mutation SubmitTagUserExportJob {
  submitTagUserExportJob(tagId: "mgGJj3GA", charset: "UTF-16LE", detailExport: false) {
      id
      name
  }
} 
```

返回：

```graphql
{
    "data": {
        "submitTagUserExportJob": {
            "id": "VGFnVXNlckV4cG9ydEpvYkR0bzp3V0RyNzdRTQ",
            "name": "DET-202101270900-32426198185000",
        }
    }
}
```

获取该任务的信息后，通过 **jobResult** 接口请求任务结果：

```graphql
query JobResult {
  jobResult(id: "VGFnVXNlckV4cG9ydEpvYkR0bzp3V0RyNzdRTQ") {
    id
    stage
    uris
  }
}
```

得到任务结果：

```graphql
{
  "data": {
    "jobResult": {
      "id": "wWDr77QM",
      "stage": "FINISH",
      "uris": [
        "/jobs/results/DET-202101270900-32426198185000/下载标签.csv"
      ]
    }
  }
}
```

uris 即为要导出资源的URI。如果需要下载该文件，则在该URI之前拼接自有OP平台域名的下载路径即可，例如本文档的数据平台链接为“[xxx.growingio.cn](https://dev1.growingio.cn/download?file=/jobs/results/DES-202101280404-14677315748000/%E4%B8%8B%E8%BD%BD%E7%94%A8%E6%88%B7%E5%88%97%E8%A1%A8.csv)”， 则下载链接为：

{平台链接} + '/download?file=' + uris

即 https://xxx.growingio.cn/download?file=/jobs/results/DET-202101270900-32426198185000/下载标签.csv

## 用户分群导出

### 1.获取项目id

这里选取默认项目，id为“WlGk4Daj”

### 2.获取分群列表

在默认项目“WlGk4Daj”中，要导出用户分群需要先获取用户分群列表，使用 **segments** 接口，获取分群列表，其中segment代表一个分群。

```graphql
query Segments {
  segments(projectId: "WlGk4Daj") {
    id
    name
  }
}
```

返回分群列表：

```graphql
{
  "data": {
    "segments": [
      {
        "id": "AVpZBzpK",
        "name": "分群1",
      },
      {
        "id": "KzpNmzQk",
        "name": "分群2",
      },
      {
        "id": "V0G5yvGA",
        "name": "分群3",
      },
      {
        "id": "qgQMXnD3",
        "name": "分群4",
      },
      #......
      {
        "id": "3mpxywGO",
        "name": "分群n",
      }
    ]
  }
}
```

### 3.导出所需分群

如果要导出某个分群，以ID为“qgQMXnD3“的分群为例 \( 相关API为：**submitSegmentUserExportJob** \)，通过接口提交一个导出特定分群的任务并返回一个任务对象\(GraphQL类型\)。

```graphql
mutation SubmitSegmentUserExportJob {
  submitSegmentUserExportJob(projectId: "WlGk4Daj", segmentId: "qgQMXnD3", charset: "UTF-16LE") {
      id
      name 
  }
} 
```

获得导出任务结果：

```graphql
{
  "data": {
    "submitSegmentUserExportJob": {
      "id": "U2VnbWVudFVzZXJFeHBvcnRKb2JEdG86d1dEcjdPUU0",
      "name": "DES-202101280344-13456258654000"
    }
  }
}
```

然后根据任务id："U2VnbWVudFVzZXJFeHBvcnRKb2JEdG86d1dEcjdPUU0",使用 **jobResult** 接口获取任务执行结果：

```graphql
query MyQuery {
  jobResult(id: "U2VnbWVudFVzZXJFeHBvcnRKb2JEdG86d1dEcjdPUU0") {
    uris
    stage
    id
  }
}
```

返回结果：

```graphql
{
  "data": {
    "jobResult": {
      "uris": [
        "/jobs/results/DES-202101280344-13456258654000/下载用户列表.csv"
      ],
      "stage": "FINISH",
      "id": "wWDr7OQM"
    }
  }
}
```

uris 即为要导出资源的URI。如果需要下载该文件，则在该URI之前拼接自有OP平台域名的下载路径即可，例如本文档的数据平台链接为“[xxx.growingio.cn](https://dev1.growingio.cn/download?file=/jobs/results/DES-202101280404-14677315748000/%E4%B8%8B%E8%BD%BD%E7%94%A8%E6%88%B7%E5%88%97%E8%A1%A8.csv)”， 则下载链接为：

{平台链接} + '/download?file=' + uris

即 https://xxx.growingio.cn/download?file=/jobs/results/DES-202101280344-13456258654000/下载用户列表.csv

## 导出分析结果

目前可导出分析结果的产品分析有漏斗分析、事件分析、留存分析、分布分析，这里以导出漏斗分析结果举例说明，其余分析的导出流程相同。

### 1.获取项目id

还是选取默认项目，项目id为“WlGk4Daj”。

### 2.获取分析列表

通过 **funnelAnalyses** 接口请求所有的分析列表：

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
        "name": "漏斗1"
      },
      {
        "id": "wWDrwQML",
        "name": "漏斗2"
      },
      {
        "id": "klGvyp7E",
        "name": "漏斗3"
      },
      #......
      {
        "id": "y9pm1pme",
        "name": "漏斗n"
      }
    ]
  }
}
```

### 3.导出相应的id

如果要导出某个漏斗，以ID为“klGvyp7E“的漏斗为例 \( 相关API为：**submitAnalysisExportJob** \)，通过接口提交一个导出特定漏斗的任务并返回一个任务对象\(GraphQL类型\)。

```graphql
mutation SubmitAnalysisExportJob{
    submitAnalysisExportJob(id: "klGvyp7E", param: {analysisType: FUNNELS}, charset: "UTF-16LE", projectId: "WlGk4Daj") {
        id
        stage
    }
}
```

返回：

```graphql
{
    "data": {
        "submitAnalysisExportJob": {
            "id": "Q0hBUlRTOmJjZGJjNjViZTA4MGE4NzIyZGM0NTM0OGI2YjdjNGMz",
            "stage": "FINISH"
        }
    }
}
```

通过 **jobResult** 接口查询结果：

```graphql
query JobResult {
  jobResult(id: "Q0hBUlRTOmJjZGJjNjViZTA4MGE4NzIyZGM0NTM0OGI2YjdjNGMz") {
    id
    stage
    uris
  }
}
```

返回任务结果：

```graphql
{
  "data": {
    "jobResult": {
      "id": "J1GlEDjl",
      "stage": "FINISH",
      "uris": [
        "/jobs-results/downloads/下载漏斗.csv"
      ]
    }
  }
}
```

uris 即为要导出资源的URI。如果需要下载该文件，则在该URI之前拼接自有OP平台域名的下载路径即可，例如本文档的数据平台链接为“[xxx.growingio.cn](https://dev1.growingio.cn/download?file=/jobs/results/DES-202101280404-14677315748000/%E4%B8%8B%E8%BD%BD%E7%94%A8%E6%88%B7%E5%88%97%E8%A1%A8.csv)”， 则下载链接为：

{平台链接} + '/download?file=' + uris

即 https://xxx.growingio.cn/download?file=/jobs-results/downloads/下载漏斗.csv

