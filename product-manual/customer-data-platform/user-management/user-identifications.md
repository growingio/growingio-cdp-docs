---
id: user-identifications
sidebar_position: 1
---

# 用户身份

在GrowingIO平台识别用户身份


## 简介[](#jian-jie)

GrowingIO使用 gio_id 来对每一个识别的用户进行唯一标识，gio_id 是基于 客观用户身份( 如 登录用户ID、设备ID )按照一定规则生成。

推荐您阅读[用户模型](https://growingio.gitbook.io/op/v/14.7/getting-started/basic-concept/user-identifications)文档，了解 GrowingIO 如何标记用户。

在 用户ID 模块，您可以查看GrowingIO支持识别的客观用户身份，如用户ID(登录用户ID)、UUID(设备ID)。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkW0P6dvbjIFcZ7_4KL%2F-MkW0tdlvzxsEq4TOZ9H%2Fimage.png?alt=media&token=bff87184-d0d8-4581-84a4-653a55f91c2f)


## 功能说明[](#gong-neng-shuo-ming)

### 唯一身份ID[](#wei-yi-shen-fen-id)

唯一身份ID是一种准确识别用户身份的ID体系，通常为您业务系统中的会员ID(登录用户ID)。GrowingIO系统会置信该身份体系并与其保持一一映射关系。即一个会员ID的值唯一对应一个 gio_id 的值；一个 gio_id 的值也唯一对应一个会员ID的值。


### 弱身份ID[](#ruo-shen-fen-id)

弱身份ID是一种弱识别的用户身份体系，通常为设备ID。通常的业务场景有：

* 一个用户使用多台设备( 浏览器、手机、ipad etc.)
    
* 多个用户使用同一台设备
    
GrowingIO系统中，弱身份ID与gio_id的映射关系支持多对一映射，即同一个用户可以使用多台设备。但同一时刻，一个弱身份ID的值只能对应唯一一个gio_id的值。
