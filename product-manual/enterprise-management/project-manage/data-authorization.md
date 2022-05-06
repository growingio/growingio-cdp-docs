---
id: data-authorization
sidebar_position: 3
---

# 数据授权

## 简介[](#jian-jie)

对不同的授权不同的数据（事件、用户标签、用户属性） ，使不同项目可以使用的数据范围是被限制的，达到数据隔离的目的。

举例示意图：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MMtsNVauG-I9X8H6e_w%2F-MMtsQVw106rjldQRveS%2F2020%20Q3%20%E7%89%88%20Copy%208.png?alt=media&token=031360be-e89f-4c88-9a32-30ac669c3e24)

此情景下 ，我们分了4 个项目 ，分别为 **_健康险业务线、寿险业务线、车险业务线、客户服务部 。_**

用户属性：

* 需求上各个业务项目都需要使用用户属性的数据 ，于是授权了给4 个项目全部的用户属性 。

用户标签 ：

* 标签为整个系统整合数据后统一分配 ，但由于业务场景不同 与 数据安全的考量 ， 给业务线 RFM 、购卖意象等级等，具备銷售目的的标签 。
    
* 但由于 _**客服部门**_ 需要处理“投诉与业务”與“流失预防” ，但不负责销售行为 ，于是只授权了客户服务相关的标签 。

埋点事件：

* 由于交易KPI 的信息为企业内部高度敏感信息 ，功能内部不可跨业务线查看 交易相关数据 ，因此将不同的 业务的交易 拆分为 多个交易事件，分别授权不同的项目 。
    
> v 12.0 版本 ，不支持用户范围的授权与限制。 默认所有项目 可查看的用户范围 = 全部用户。


## 功能说明[](#gong-neng-shuo-ming)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MdH-kQRsk-7EGLrJHVq%2F-MdH09rILiCKAWD-1DpK%2Fimage.png?alt=media&token=de52be2a-2c15-4be2-857d-dafb4e903657)

| 操作  | 作用  |
| --- | --- |
| 查看项目数据范围 | 可查看项目中可用的数据 |
| 编辑用户属性、用戶标签、埋点事件、虚拟事件 授权范围 | 配置项目可用的数据 |


### 查看项目数据范围[](#cha-kan-xiang-mu-shu-ju-fan-wei)

在弹窗列表中可查看项目中可用的数据 (用户属性、用户标签、埋点事件) ，只有列表中被授权的数据可在项目中被使用与查看。

操作流程 ： 点击查看 > 打开弹窗 > 查看可用的 用户属性、用户标签、埋点事件。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHBnQw9E0sdmYDJiDL%2F-MkHBtAiMI7dZ8YT-CMn%2Fimage.png?alt=media&token=3da325d1-4a7e-45da-a2f6-40737c98f411)


### 编辑 数据源、用户范围、用户属性、用户标签、埋点事件、虚拟事件 授权范围[](#bian-ji-shu-ju-yuan-yong-hu-fan-wei-yong-hu-shu-xing-yong-hu-biao-qian-mai-dian-shi-jian-xu-ni-shi-jian-shou-quan-fan-wei)

透过授权配置，可配置不同的项目可用的不同的数据。

操作流程 ： 点击编辑 > 进入 埋点数据授权 > 选择授权方式 > 保存。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHBnQw9E0sdmYDJiDL%2F-MkHBynxJw5xZA7SmG7h%2Fimage.png?alt=media&token=7d0dc852-940f-4396-a725-15c34bae76d9)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHBnQw9E0sdmYDJiDL%2F-MkHC1x4XEDlxqxwmKkI%2Fimage.png?alt=media&token=145d5338-fea5-4fd5-954d-990c09172902)

> 授权模式：
> 
> * 全部可用 ：可以使用全部 ，当有新的 属性、标签、埋点事件时 ，自动授权项目使用。
> 
> * 全部禁用：不可以使用任何 用户属性、标签、埋点事件。 
> 
> * 自定义：可以自由定义使用 用户属性、标签、埋点事件。

> V12.0版本 用户属性 (不控制用户信息)

> 权限控制： 仅拥有者、超级管理员可配置数据授权
