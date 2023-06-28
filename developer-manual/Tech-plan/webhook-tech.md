---
id: webhook-tech
sidebar_position: 1
---

# 自定义触点接入

## 简介

智能运营提供自定义触点（即 webhook） 能力，可用于支持任何自研或第三方提供的潜在触发行为，例如短信服务、发公众号模板消息、发优惠券/积分权益等等。经过较为轻量的 REST API 开发对接，即可快速支持非智能运营内置的触发方式。

## 工作流程

![图 1](/img/430fbbbc423d6c4707b528a6d4d648e98b7eab85c778a70642748e3e92d140eb.png)

**从数据中心获取用户数据：**

作为整个分析云平台的基础，为服务提供数据支持。营销活动开始后，智能运营会从数据中心读取满足触发条件用户的数据。

**智能运营发送 Webhook 请求：**

智能运营获取到用户数据后，经过筛选过滤和组装以后，通过 HTTP 请求的方式将数据发送到您自身的 HTTP Endpoint。

**HTTP Endpoint 接收请求：**

HTTP Endpoint 接收到来自智能运营的请求后，首先校验请求的有效性，然后对数据进行处理，最后调用 Whatever System 下游渠道进行用户触达操作。

**Webhook 请求的触达结果：**

HTTP Endpoint 的触达结果返回方式分为同步返回和异步查询两种。

- 同步返回触达结果是在智能运营发送 Webhook 请求到 HTTP Endpoint，请求的返回结果中包含触达结果；
- 异步返回触达结果的方式适合下游接口不能实时返回触达结果，或者对触达结果明细有要求的场景。智能运营会通过定时查询的方式，调用 Webhook 自定义触点中配置的获取回执地址，HTTP Endpoint 可以提前调用下游接口获取触达结果并保存，或者在智能运营查询回执时，主动调用下游接口查询触达结果，并将最终结果返回到智能运营。

**智能运营上报触达结果**

智能运营服务会把营销活动中的触达结果上报到数据中心，上报的数据可以用于后续的统计计算、行为圈群等。

## webhook 自定义触点配置和使用

### 触点配置

功能路径：智能运营—设置—触点管理—自定义触点
![图 2](/img/7eb7422e12e81d2398dc58c6bd1b99ba16f0d2bd14e3ed6df23fe51d521c155e.png)

点击列表右上角【添加触点】弹出添加弹窗，可进行基本信息以及发送参数配置。
![图 3](/img/fcbbb3d5c0193e154b667f5e124c1fec01ebf68db75ede33dbfb5bba56badb49.png)

### 触点使用

在营销画布策略器的触达渠道中，可以选择配置的自定义触点。
![图 4](/img/f76b6cacec9e608fa2dba6ff615dba335454cf10f50ddf911418ad805dab492c.png)

## webhook 自定义触点概述

自定义触点（即 Webhook）是一种基于 HTTP POST 请求的发布/订阅模式，可以实现不同服务之间的实时通信。

### Webhook 请求

为了提升触发效率，Webhook 自定义触点默认批量发送，如果下游接口不支持批量触发，可以在触点配置中把批次设置为**1**。

请求参数中包含时间戳（timeStamp）、签名（sign）、请求流水号（orderNo）和用户信息（dataList.dynamicData）以及模板信息（dataList.temData）

#### 请求参数示例

```
{
 	"timeStamp":1664590280000,  # 时间戳
	"orderNo":"1f1d0ea0c457453ab3c80ed376e5c66c", # 订单号（全局唯一）
	"sign":"D8FDEEF30F4264B264D9386415F1F992", #签名（MD5(token&timeStamp&orderNo)转大写），用于验证请求的有效性
	"dataList":[{
       "gid":123, # 用户id，用户在分析云平台的唯一标识
		"temData":{"startDate":"2022-10-01","endDate":"2022-10-07","title":"会员01生日优惠券","amount":100},  # 模板参数
		"dynamicData":{"memberId":"01","phone":"13012345678"} # 用户信息，根据自定义触点中配置的参数传输
	},{
       "gid":124, # 用户id，用户在分析云平台的唯一标识
		"temData":{"startDate":"2022-10-01","endDate":"2022-10-07","title":"会员02生日优惠券","amount":100}, # 模板参数
		"dynamicData":{"memberId":"02","phone":"13023456789"} # 用户信息，根据自定义触点中配置的参数传输
	}]
}
```

其中 dataList 参数是一个 List，当有多个用户满足条件时，发送的 webhook 请求参数中会包含多个对象。

### Webhook 回执

Webhook 请求的回执主要用于营销活动的数据统计，方便对活动执行效果进行分析，另外最终触达数据也会上报到数据中心，用于后续的分析和处理。

上报的事件为**智能运营-渠道触达**，事件标识符$ma_channel_touch。

回执方式分为同步回执和异步回执，可在触点配置时根据系统情况进行选择。
![图 5](/img/91cde4e7bef604e1ef0e666d661df8d5a677cf19ada8c20bfbb78468d9769786.png)

#### 同步回执

同步回执是 HTTP Endpoint 对营销活动 http 请求的响应数据，在接口正常响应的情况下，应该返回请求状态（code）、信息描述（message）、请求流水号（orderNo）和用户的最终触达结果列表（sendStatusList）。

**请求响应示例**

```
{
	"code":0, # 返回码（0-成功，除了0之外的其他值都认为失败，下游系统自行定义）
   "message":"", # 失败原因（成功不返回）
	"orderNo":"1f1d0ea0c457453ab3c80ed376e5c66c", #订单号
   "sendStatusList":[{
       "gid":123, #用户唯一标识
       "status": "TOU_SUCC", #触达状态，TOU_SUCC-成功，TOU_FAIL-失败
       "errorMsg": ""  #失败描述，触达成功可以不返回
     }, {
       "gid":124, #用户唯一标识
       "status": "TOU_FAIL", #触达状态，TOU_SUCC-成功，TOU_FAIL-失败
       "errorMsg": "用户信息有误" #失败描述，触达成功可以不返回
     }
   ]
}
```

#### 异步回执

在下游接口不能及时返回最终结果的情况下，可以配置异步回执和异步查询超时时间，智能运营会通过定时任务 5 分钟查询一次，超过超时时间未查询到结果则视为触达失败，异步回执也需要提供 HTTP Endpoint。

异步回执的请求参数中包含时间戳（timeStamp）、订单号（orderNo）和验证签名（sign），请求响应的格式与同步回执的格式一致。

**请求参数示例**

```
{
	"timeStamp":1664590280000, # 时间戳
	"orderNo":"1f1d0ea0c457453ab3c80ed376e5c66c",  #订单号，需要与webhook请求的传参保持一致
	"sign":"D8FDEEF30F4264B264D9386415F1F992" # 签名，与Webhook请求的签名规则一致
}
```

**请求响应示例**

```
{
	"code":0, # 返回码（0-成功，除了0之外的其他值都认为失败，下游系统自行定义）
    "message":"", # 失败原因（成功不返回）
	"orderNo":"1f1d0ea0c457453ab3c80ed376e5c66c", #订单号
    "sendStatusList":[{
        "gid":123, #用户唯一标识
        "status": "TOU_SUCC", #触达状态，TOU_SUCC-成功，TOU_FAIL-失败
        "errorMsg": ""  #失败描述，触达成功可以不返回
      }, {
        "gid":124, #用户唯一标识
        "status": "TOU_FAIL", #触达状态，TOU_SUCC-成功，TOU_FAIL-失败
        "errorMsg": "用户信息有误" #失败描述，触达成功可以不返回
      }
    ]
}
```

## webhook 自定义触点开发

### 触点触达接口

**API 名称：** 自定义触点触达

**API 描述：** 当用户满足策略条件后，智能运营系统会调用该接口，把对应的用户参数和模板参数传送到您自定义的 webhook 接口

**请求类型：** POST

**请求参数：**

| 名称                 | 类型             | 必填 | 描述                                                                                                                                          | 示例值                                                                         |
| -------------------- | ---------------- | ---- | --------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| timeStamp            | ava.lang.Long    | 是   | 时间戳                                                                                                                                        | 1627538679006                                                                  |
| orderNo              | java.lang.String | 是   | 请求标识（全局唯一）                                                                                                                          | 1f1d0ea0c457453ab3c80ed376e5c66c                                               |
| sign                 | java.lang.String | 否   | 签名<br/>MD5(token&timeStamp&orderNo)转大写<br/>token：通过自定义触点页面配置                                                                 | 1D8FDEEF30F4264B264D9386415F1F992                                              |
| dataList             | java.lang.List   | 是   | 批量发送用户属性信息以及模版参数内容[{dynamicData:{...}, temData:{...}}]<br/>具体包含哪些用户信息以及模版参数内容取决于页面上自定义触点的配置 |                                                                                |
| dataList.gid         | java.lang.Long   | 是   | 用户的 gid                                                                                                                                    | 123                                                                            |
| dataList.dynamicData | Object           | 是   | 用户属性<br/>根据页面配置的用户属性生成对象<br/>注：若作为用户属性进行配置，则属性数据不能在数据中心进行脱敏加密                              | {"usr*$basic_name":"01","usr* $basic_mobile":"13025057829"}                    |
| dataList.temData     | Object           | 是   | 模板参数<br/>根据页面配置的模板参数生成对象                                                                                                   | {"startDate":"2022-10-01","endDate":"2022-10-07","title":"会员 02 生日优惠券"} |

**返回参数：**

| 名称                | 类型               | 必填 | 描述                                                 | 示例值                           |
| ------------------- | ------------------ | ---- | ---------------------------------------------------- | -------------------------------- |
| code                | java.lang.Integer  | 是   | 返回码<br/>0：成功，其他：失败                       | 0                                |
| message             | java.lang.String   | 否   | 失败原因（成功不返回）                               | ""                               |
| orderNo             | java.lang.String   | 是   | 消息发送请求标识                                     | 1f1d0ea0c457453ab3c80ed376e5c66c |
| sendStatusList      | List< SendStatus > | 是   | 触达状态                                             |                                  |
| sendStatus.gid      | java.lang.Long     | 是   | 入参中的 gid                                         | 123                              |
| sendStatus.status   | java.lang.String   | 是   | 状态：<br/>TOU_SUCC：触达成功<br/>TOU_FAIL：触达失败 | TOU_FAIL                         |
| sendStatus.errorMsg | java.lang.String   | 否   | 失败描述                                             | 用户信息有误                     |

**请求参数示例：**

```
{
	"timeStamp":1664590280000,
	"orderNo":"1f1d0ea0c457453ab3c80ed376e5c66c",
	"sign":"D8FDEEF30F4264B264D9386415F1F992",
	"dataList":[{
        "gid":123,
		"temData":{"startDate":"2022-10-01","endDate":"2022-10-07","title":"会员01生日优惠券","amount":100},
		"dynamicData":{"memberId":"01","phone":"13025057829"}
	},{
        "gid":124,
		"temData":{"startDate":"2022-10-01","endDate":"2022-10-07","title":"会员01生日优惠券","amount":100},
		"dynamicData":{"memberId":"02","phone":"13025057827"}
	}]
}
```

**返回参数示例：**

```
{
	"code":0,
    "message":"",
	"orderNo":"1f1d0ea0c457453ab3c80ed376e5c66c",
    "sendStatusList":[{
        "gid":123,
        "status": "TOU_SUCC",
        "errorMsg": ""
      }, {
        "gid":124,
        "status": "TOU_FAIL",
        "errorMsg": "用户信息有误"
      }
    ]
}
```

**异常示例：**

```
{
	"code":500,
    "message":"服务调用异常"
}
```

### 异步获取触达回执接口

**API 名称：** 自定义触点异步获取触达回执

**API 描述：** 如果自定义触点配置的回执策略为异步，那么智能运营系统调用自定义触点触达接口后，会再定时调用该接口异步查询触达回执（该接口也由企业提供），5 分钟查询一次，超过超时时间未查询到结果则视为触达失败。

**请求类型：** POST

**请求参数：**

| 名称      | 类型             | 必填                                                                          | 描述                              | 示例值                           |
| --------- | ---------------- | ----------------------------------------------------------------------------- | --------------------------------- | -------------------------------- |
| timeStamp | java.lang.Long   | 是                                                                            | 时间戳                            | 1627538679006                    |
| orderNo   | java.lang.String | 是                                                                            | 请求标识（全局唯一）              | 1f1d0ea0c457453ab3c80ed376e5c66c |
| sign      | java.lang.String | 签名<br/>MD5(token&timeStamp&orderNo)转大写<br/>token: 通过自定义触点页面配置 | 1D8FDEEF30F4264B264D9386415F1F992 |                                  |

**返回参数：**

| 名称                | 类型              | 必填 | 描述                                                   | 示例值                           |
| ------------------- | ----------------- | ---- | ------------------------------------------------------ | -------------------------------- |
| code                | java.lang.Integer | 是   | 返回码<br/>0：成功，其他：失败                         | 0                                |
| message             | java.lang.String  | 否   | 失败原因（成功不返回）                                 |                                  |
| orderNo             | java.lang.String  | 是   | 消息发送请求标识                                       | 1f1d0ea0c457453ab3c80ed376e5c66c |
| sendStatusList      | List< SendStatus  | 是   | 触达状态                                               |                                  |
| sendStatus.gid      | java.lang.Long    | 是   | 入参中的 gid                                           | 123                              |
| sendStatus.status   | ava.lang.String   | 是   | 触达状态<br/>TOU_SUCC：触达成功<br/>TOU_FAIL：触达失败 | TOU_FAIL                         |
| sendStatus.errorMsg | java.lang.String  | 否   | 失败描述                                               | 用户信息有误                     |

**请求参数示例：**

```
{
	"timeStamp":1664590280000,
	"orderNo":"1f1d0ea0c457453ab3c80ed376e5c66c",
	"sign":"D8FDEEF30F4264B264D9386415F1F992"
}
```

**返回参数示例：**

```
{
	"code":0,
    "message":"",
	"orderNo":"1f1d0ea0c457453ab3c80ed376e5c66c",
    "sendStatusList":[{
        "gid":123,
        "status": "TOU_SUCC",
        "errorMsg": ""
      }, {
        "gid":124,
        "status": "TOU_FAIL",
        "errorMsg": "用户信息有误"
      }
    ]
}
```

**异常示例：**

```
{
	"code":500,
    "message":"服务调用异常"
}
```

### 枚举值列表接口

**API 名称：** 自定义触点枚举值列表

**API 描述：** 当配置模板参数时，参数类型选择枚举型时支持通过 API 获取枚举值，该 API 由企业提供。智能运营平台会调用该接口获取枚举值，并在运营配置策略时进行展示。

**请求类型：** POST

**请求参数：**

| 名称             | 类型              | 必填 | 描述                                                         | 示例值   |
| ---------------- | ----------------- | ---- | ------------------------------------------------------------ | -------- |
| projectId        | java.lang.Integer | 是   | 分析云项目 id                                                | 1        |
| paramDescription | java.lang.String  | 是   | 模板参数描述（即模板参数名称）                               | 跳转类型 |
| paramName        | java.lang.String  | 是   | 模板参数标识，参数值要和使用到该枚举接口对应参数标识保持一致 | jump     |

**返回参数：**

| 名称                       | 类型              | 必填 | 描述                                                                                                                                                                          | 示例值               |
| -------------------------- | ----------------- | ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| code                       | java.lang.Integer | 是   | 返回码<br/>0：成功，其他：失败                                                                                                                                                | 0                    |
| enumArgs                   | array[object]     | 是   | 枚举数组或者分类<br/>当 childEnumArgs 为空时该参数代表枚举<br/>当 childEnumArgs 不为空时该参数代表分类<br/>enumArgs.code、enumArgs.description 分别代表分类 code 和分类的描述 |                      |
| -enumArgs.code             | java.lang.String  | 是   | 枚举 code                                                                                                                                                                     | "JUMP_H5"            |
| -enumArgs.description      | java.lang.String  | 是   | 枚举描述                                                                                                                                                                      | 跳转到 h5 页面       |
| -enumArgs.childEnumArgs    | array[object]     | 否   | 枚举数组                                                                                                                                                                      |                      |
| -childEnumArgs.code        | java.lang.String  | 否   | 枚举 code                                                                                                                                                                     | JUMP_H5_mini         |
| -childEnumArgs.description | java.lang.String  | 否   | 枚举描述                                                                                                                                                                      | 跳转到小程序 h5 页面 |

支持枚举值的级联关系，最多支持 2 级。

**请求参数示例：**

```
{
  "projectId": 1,
  "paramDescription":"模板消息跳转",
  "paramName":"jump"
}
```

**返回参数示例：**

```
{
  "code":0,
  "enumArgs":[
      // 如果选择了”跳转到h5页面“最终webhook提交的参数为:"jump":"JUMP_H5"
      {"code":"JUMP_H5","description":"跳转到h5页面"},
      {"code":"JUMP_APP","description":"跳转到app"},
      {"code":"NO_JUMP","description":"无跳转"}
    ]
}
```

**异常示例：**

```
{
	"code":500,
    "message":"服务调用异常"
}
```
