---
id: enterprise-roles
sidebar_position: 2
---

# 企业角色

## 简介

企业角色是区分系统使用者对“企业管理后台＆客户数据平台”的权力和责任。
一个角色，就相当于一个功能权限包。角色将决定成员在该项目中的功能权限，即该成员可否使用某项功能。


企业角色和成员是“1对1”的关系，每个成员都具有一个企业角色，即为，该用户对“企业管理功能＆客户数据平台”的权限。

## 功能说明

**企业角色关联的成员**

可查看企业角色下相关的企业成员。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25447572/1641454827747-f64d0f53-7b65-4083-9c1f-05bdd0a9106c.png#clientId=u0b852a38-7d3c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=372&id=u00f201b3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=743&originWidth=1823&originalType=binary&ratio=1&rotation=0&showTitle=false&size=92554&status=done&style=none&taskId=uf36fd29a-51cc-40c9-8c3f-e5d427d03be&title=&width=911.5)


**企业对应的权限**

可查看企业角色对应的权限。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25447572/1641454863598-fe7b1c8d-65c0-4f23-9e58-8ba5701ac28b.png#clientId=u0b852a38-7d3c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=486&id=ud8498b87&margin=%5Bobject%20Object%5D&name=image.png&originHeight=972&originWidth=1313&originalType=binary&ratio=1&rotation=0&showTitle=false&size=78722&status=done&style=none&taskId=u0cb0751c-9fdd-4f0a-95b0-5aed12cf75d&title=&width=656.5)


### 系统预置企业角色介绍

GrowingIO 在**企业**中，帮助用户预置了 5 个系统角色：拥有者、超级管理员、数据管理员、企业成员、外部成员。系統預置角色不支持编辑角色信息、修改角色权限、删除角色等操作。

**拥有者**

- 拥有者是系統唯一的。 
- 拥有者有最高权限的角色。一般来说是管理人员，管理成员们在 **企业管理、客户数据平台 **中可以做什么，不能做什么。

**超級管理员**

- 超级管理员可以辅助拥有者做管理工作的角色。
- 超级管理员拥有企业管理后台与客户数据平台的所有权限。

**数据超級管理员**

- 数据管理员主要负责 客户数据平台的管理与维护 ，负责定议数据 、接入数据源。 
- 推荐团队内部DBA、数据工程师担任此角色。

**企业成员**

- 可查看企业管理相关权限** ，**但无法进行企业管理操作。 
- 无法访问客户数据平台，推荐给各业务人员设置此角色。
- 推荐给各业务人员，或无需做数据管理的同事设置此角色。

**外部成员**

- 无访问企业管理后台与客户数据平台。推荐给各企业外部人员设置此角色。



### 企业角色的操作说明

| 操作 | 作用 |
| --- | --- |
| 添加成员至角色 | 将成员添加至当前角色 |
| 修改企业角色 | 将当前角色下的成员，修改为其他角色 |
 
#### 添加成员至角色

操作流程： 点击添加成员 > 弹窗选择成员 > 点击确定。


![image.png](https://cdn.nlark.com/yuque/0/2022/png/25447572/1641455054647-9ea07d26-4c3f-42a0-8f94-3a1793120c0b.png#clientId=ub1725114-a0dd-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=460&id=uadd44988&margin=%5Bobject%20Object%5D&name=image.png&originHeight=920&originWidth=1785&originalType=binary&ratio=1&rotation=0&showTitle=false&size=166554&status=done&style=none&taskId=u2638ce75-6743-493c-bd14-0c489428123&title=&width=892.5)

权限控制：仅拥有者、超级管理员 拥有企业角色的权限
​

#### 修改企业角色

操作流程： 点击修改企业角色 > 弹窗选择企业角色> 点击确定。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25447572/1641455166758-a26e4bf1-0d5a-4a0f-8634-c993d593ecb3.png#clientId=ub1725114-a0dd-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=477&id=ufa7e40c0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=953&originWidth=1349&originalType=binary&ratio=1&rotation=0&showTitle=false&size=113041&status=done&style=none&taskId=u10da1306-b553-457f-b09d-99a6c5f58c5&title=&width=674.5)


![image.png](https://cdn.nlark.com/yuque/0/2022/png/25447572/1641455123554-a102b0d6-c165-4e5c-b54d-e7646bd99928.png#clientId=ub1725114-a0dd-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=435&id=udc7dad8d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=869&originWidth=1436&originalType=binary&ratio=1&rotation=0&showTitle=false&size=119656&status=done&style=none&taskId=u3f94d119-10a6-4b2c-9724-fe6c1186334&title=&width=718)


权限控制：仅拥有者、超级管理员 拥有企业角色的权限
