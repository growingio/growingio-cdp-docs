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

  
  




