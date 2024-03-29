---
description: 本页面介绍如何集成本Java SDK并以类型安全的方法调用来使用GraphQL API。
---

# Java SDK for GraphQL

## 简介

GrowingIO 提供 Java SDK 接口供开发者使用，更多详情，请查阅 [GitHub](https://github.com/growingio/growingio-graphql-javasdk)。

## 添加依赖

### maven

```java
<dependency>
    <groupId>io.growing</groupId>
    <artifactId>growingio-graphql-javasdk_2.12</artifactId>
    <version>${last-version}</version>
</dependency>
```

###  gradle

```java
compile group: 'io.growing', name: 'growingio-graphql-javasdk_2.12', version: '${last-version}'
```

###  sbt

```java
libraryDependencies += "io.growing" %% "growingio-graphql-javasdk" % "${last-version}"
```

##  调用API

这里仅列举 “请求列表” 中的六个常用接口的示例，返回数据格式请参考 [GraphQL接口说明](description/project.md#xi-tong-zi-ding-yi-graphql-biao-liang)。

#### 准备：

```java
final static GrowingioApi growingioApi = GrowingioApi.apply("http://gdp-dev.growingio.com/graphql", "Authorization", "token");
```

| **API** | **接口描述** |
| :--- | :--- |
| submitTagUserExportJob | 提交导出标签用户任务 |
| submitSegmentUserExportJob | 提交导出用户分群任务 |
| jobResult | 根据任务ID查询任务结果 |
| userProfile | 查询单个用户的标签值或属性 |
| segments | 获取用户分群列表 |
| tags | 获取标签列表 |

### submitTagUserExportJob

```java
TagUserExportJobDto tagUserExportJobDto = growingioApi.submitTagUserExportJob("rRGoVRpm", Collections.emptyList(), "UTF-16LE", false);
System.out.println(tagUserExportJobDto);
```

### submitSegmentUserExportJob

```java
SegmentUserExportJobDto segmentUserExportJobDto = growingioApi.submitSegmentUserExportJob("projectId", "J1GlNzQj", Collections.emptyList(), Collections.emptyList(), "UTF-16LE");
System.out.println(segmentUserExportJobDto);
```

### jobResult

```java
JobResultDto jobResultDto = growingioApi.jobResult(tagUserExportJobDto.getId());
System.out.println(jobResultDto);
```

### userProfile

```java
UserProfileDto userProfileDto = growingioApi.userProfile("projectId", "23945", Collections.emptyList(), Collections.emptyList());
System.out.println(userProfileDto);
```

### segments

```java
List<SegmentDto> segmentDtos = growingioApi.segments("projectId");
System.out.println(segmentDtos); 
```

### tags

```java
List<TagDto> tags = growingioApi.tags("projectId");
System.out.println(tags);
```

