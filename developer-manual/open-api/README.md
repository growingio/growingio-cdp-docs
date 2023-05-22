---
id: open-api-overview
sidebar_position: 1
---

# Open API 概述

## 公共请求参数

公共请求参数是指每个接口都需要使用到的请求参数。如下表所示的参数均放在 HTTP 请求的头部。

| 参数          | 类型   | 说明                                                                                                                                                                                    |
| ------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authorization | string | 接口请求所需的认证码，即 Token，您可以在 GrowingIO 平台的[个人设置](../../product-manual/portal/personal)中获取一个长期有效的 Token。<br/>请求时在 header 中增加“Authorization:Bearer {Token}” |
| language      | string | 语言，默认 CH。可选：CH - 中文，US - 英文。 |                                                                                                              