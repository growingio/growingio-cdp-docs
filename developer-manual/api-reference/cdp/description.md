# 接口说明

GrowingIO 提供的接口统一使用 GraphQL 格式，下面是 GraphQL 接口的请求信息：

| Method | Path | Request Body | Response Body |
| :--- | :--- | :--- | :--- |
| POST | /graphql | application/json | application/json |

GraphQL 接口区分 Query 和 Mutation 两类，其中 Query 请求用于查询数据，Mutation 请求用于操作/修改数据。

