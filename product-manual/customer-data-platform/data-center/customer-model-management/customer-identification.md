---
description: 在GrowingIO平台识别用户身份
---

# 用户ID

## 简介

GrowingIO使用 gio\_id\( 即 event 表中的 gioid \)来对每一个识别的用户进行唯一标识，gio\_id 是基于 客观用户身份\( 如 登录用户ID、设备ID \)按照一定规则生成。

{% hint style="success" %}
推荐您阅读[用户模型](https://github.com/growingio/growingio-cdp-docs/tree/4189247e398f09fdb26bde8d37ab423fc1bc3e3c/introduction/user-model/README.md)文档，了解 GrowingIO 如何标记用户。
{% endhint %}

在 用户ID 模块，您可以查看GrowingIO支持识别的客观用户身份，如用户ID\( 登录用户ID\)、UUID\( 设备ID\)。

![](../../../../.gitbook/assets/image%20%28498%29.png)

### 唯一身份ID

唯一身份ID是一种准确识别用户身份的ID体系，通常为您业务系统中的会员ID\(登录用户ID\)。GrowingIO系统会置信该身份体系并与其保持一一映射关系。即一个会员ID的值唯一对应一个gio\_id的值；一个gio\_id的值也唯一对应一个会员ID的值。

### 弱身份ID

弱身份ID是一种弱识别的用户身份体系，通常为设备ID。通常的业务场景有：

* 一个用户使用多台设备\( 浏览器、手机、ipad etc.\)
* 多个用户使用同一台设备

GrowingIO系统中，弱身份ID与gioid的映射关系支持多对一映射，即同一个用户可以使用多台设备。但同一时刻，一个弱身份ID的值只能对应唯一一个gio\_id的值。

