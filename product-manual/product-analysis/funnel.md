---
id: funnel
sidebar_position: 5
---

# 漏斗分析

## 简介[](#jian-jie)

漏斗分析是一套流程式的数据分析模型，通过将用户行为起始的各个行为节点作为分析模型节点，来衡量每个节点的转化效果，是转化分析的重要工具。

核心功能包括：

* 漏斗步骤自定义，展示每步人数、转化率，以及总转化率；
    
* 自定义时间区间，查看特定时间内的相关漏斗转化；
    
* 自定义转化周期，定义不同周期下的漏斗转化
    
* 提供属性维度拆分，维度包括但不限于：访问来源、浏览器、浏览器版本、操作系统、城市、地区、国家名称、广告来源、广告名称、广告内容、广告关键字、广告媒介，以及20个自定义的用户属性维度；
    
* 支持选择不同分群用户，进行漏斗步骤的对比。
    
* 自定义漏斗转化时长分布，查看转化用户对应的转化时长分布情况。
    
## 功能边界和约束[](#gong-neng-bian-jie-he-yue-shu)

支持所有埋点事件作为漏斗步骤进行分析，不支持无埋点事件。

支持创建20个步骤的漏斗。

## 功能说明[](#gong-neng-shuo-ming)

### 转化的定义[](#zhuan-hua-de-ding-yi)

转化定义：

用户进入漏斗后，在规定的时间范围，按照分析者规定的行为，规定顺序完成了目标事件即为转化。

由此看来完成转化有三个方面： 规定的时间，规定的行为，规定的行为顺序，缺一不可。

下面举一些例子：

假设用户在规定时间内依次完成ABCD 则为转化，那么

* ABCD：用户按照规定的路径完成了转化。常见真实场景如 访问 注册 安装SDK；访问 听歌 购买会员
    
* ABCBCBCCD：用户反复多次后完成转化。常见真实场景如 表单注册，产品购买时在详情页和下单页反复后完成购买。
    
* ABCABCD： 用户重新开始完成了转化。常见真实场景如用户购买时发现明天购买更便宜，明天重新开始购买。
    
* ABCED：用户除了进行规定步骤还做了其他操作完成了转化。常见真实场景如C和D之前看是否看demo，来看demo的作用。
    
* ABCF：用户没有完成转化，在C流失。常见真实场景如发现产品太贵，去其他平台上看价格。
    
* ABCBF：用户没有完成转化，在节点B 流失。常见真实场景如回到上级页面后发现不符合需求，离开漏斗。
    
* ABC...D （... 代表转化了，但没在规定时间完成）： 用户虽然按照顺序完成了转化，但未在规定时间内完成。常见真实场景如试用期14天，十四天内成单给与九折优惠，超过14天没有奖金。
    
* AD：未转化
    
* ABABCDBCABCD：用户完成了两次转化
    
## 创建漏斗分析[](#chuang-jian-lou-dou-fen-xi)

一、在左侧导航栏选择“**分析模型 > 漏斗分析**"，进入漏斗分析列表页。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2Fsync%2Fc7ca813cedca48da9c7e5bf95aee8db8bb4bea23.png?alt=media)

二、单击右侧列表上方"**新建漏斗分析"**，进入**创建漏斗分析**页面。

三、依据以下步骤配置漏斗。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2Fsync%2F729be50337589fc51c609377a8e3e248313c1883.png?alt=media)

| 项   | 说明  |
| --- | --- |
| 1-事件选择 | 至少选择2个步骤，单击确定后展示漏斗视图。 |
| 2-事件过滤 | 单击已选步骤右侧的 ![](/img/-Lo08UtW7H58ehFKeZ4g-Ltde2dMkj6vvIsEg0mZ-LtdfDNBSgq16S3kCwqjE6BC8FE69697.png) ，配置当前步骤单独的过滤条件。 |
| 3-转化窗口期 | 指用户从漏斗第一步到完成之后每一步需要在转化周期时长内完成记作转化，否则记作流失。默认是“ 1 天”，最长支持 90 天。 比如，转化周期设置为7天，是指用户完成漏斗第一步之后，需要在后续的 7 天内完成漏斗的最后一步才计为转化，否则会记为流失。 |
| 4-目标用户 | 默认是“全部用户”，可以切换至“新用户”及用户创建的用户分群。 |
| 5-维度对比 | 维度对比：针对某个维度，对比不同维度值的漏斗表现。**例如**：我们可以对比「浏览器」维度，Chrome 和 Safari 的注册流表现是否有明显差异。Chrome 和 Safari 是「浏览器」维度的 2 个不同的值。可以看到两个浏览器在注册每一步的不同表现和整体转化率的不同表现，并且可以在右侧视图区域切换「趋势」对比它们的趋势情况。 |
| 6-用户对比 | 对比两个不同的用户群体的转化情况。**例如**：某电商平台尝试唤醒近期不活跃的用户，并将用户分成 2 组，其中1 组发了满减优惠券，另外 1 组发了立减优惠券，想要2组领取了优惠券之后的转化情况；此时可以创建 2 个用户分群：「领取了满减券的用户」(2010人)和 「领取了立减券的用户」(1080人)，在漏斗用户对比时选择这 2 个用户分群并调整时间范围到用户领取优惠券之后的一段时间，就可以对比 2 个不同用户分群的转化情况了。 |
| 7-漏斗展示 | 可选择漏斗图或趋势图。漏斗图按筛选条件展示每一步骤的整体转化率；趋势图在筛选条件范围内展示每一步骤在每天的转化率。 |
| 8-时间 | 时间是指用户进入漏斗的时间范围，也就是完成漏斗第一步的时间。默认是“过去 14 天”，可以在此处切换成“今天”或者过去的一段时间。此处时间限定的是漏斗第一步，也就是用户进入转化漏斗的时间范围。 |
| 9-全局过滤 | 针对整个漏斗的全局过滤，比如浏览器＝Chrome。 |
| 10-图表对比 | 可在图表处展示不同维度对比和用户对比数据，最多可勾选2个。 |

选择需要的参数后，右侧即可实时展示分析图表。

四、单击右上角保存，完成一个漏斗分析的创建。

### 转化漏斗步骤[](#zhuan-hua-lou-dou-bu-zhou)

默认展示转化漏斗步骤图。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2Fsync%2Fd2f8574a06a4b7b32181926837fae0813cf6bf31.png?alt=media)

| 项   | 说明  |
| --- | --- |
| 单位(用户量) | GrowingIO 的漏斗基于用户行为分析，漏斗每一步的数据统计的是“**用户数**”，也就是每一步有多少用户完成；如果同1个用户在选定的时间范围完成了某个步骤 2 次，算作 1。 |
| 步骤(时序) | ​在转化周期内漏斗第一步和第二步为例：常规顺序：如果用户先完成第一步又完成第二步，则第二步用户量 +1 ；非常规顺序：用户先完成第二步再完成第一步* 今日数据：在同一小时内完成，则第二步用户量 +1；不在同一小时完成，第二步用户+0 * 今日前数据：在同一天内完成，则第二步用户量 +1；不在同一天完成，第二步用户+0 |
| 11-下钻分群 | 漏斗步骤分为转化区域和未转化区域，点击转化区域选择「创建分群」可以选择转化用户分群，点击未转化区域选择「创建分群」 |
| 12-下载用户ID | 点击转化区域，可以选择下载转化用户列表，点击转化区域，可以选择下载未转化用户列表 |

转化漏斗趋势[](#zhuan-hua-lou-dou-qu-shi)

点击右上角下拉菜单，可以查看漏斗转化趋势。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2Fsync%2F831d00d3ccf979228686e3f3951b9d3a78a5e769.png?alt=media)

图表中展示了漏斗整体转化率随时间的变化趋势。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2Fsync%2Fc4dc4819230fa0ce6464a9d2724770131798d597.png?alt=media)

您还可以通过维度拆解查看不同维度值的对比转化趋势，如：对比“城市“维度下北京和上海的转化率。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2Fsync%2F3b7865780f7807f7793c9769f8918d7311577319.png?alt=media)

### 转化时长分布[](#zhuan-hua-shi-chang-fen-bu)

点击右上角下拉菜单，可以查看漏斗的转化时长分布。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MguCrq45Rloh-hnJ5f-%2F-MguEMKE_rPdFJgdwg1p%2Fimage.png?alt=media&token=e0a3bcc0-4ad1-4307-a63c-e6389b0769e4)

点击转化时长分布，可以看到漏斗转化时长分布情况：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MguCrq45Rloh-hnJ5f-%2F-MguFn4XoghuvsR7ThbB%2Fimage.png?alt=media&token=0eb3b0cb-a79a-42b3-8cf0-0a7595dd685f)

点击全部步骤，在下拉列表可以看到漏斗任意步骤的转化时长分布情况：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MguCrq45Rloh-hnJ5f-%2F-MguGjCeWA4cK0pZ_jtw%2Fimage.png?alt=media&token=8bc38a5d-25e3-4d1a-aacc-f5487452049c)

选择维度拆解可以看到不同维度下漏斗的转化时长分布情况

你可以看到不同维度下转化时长的分布情况，我们特别对中位数所在位置做了标注。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-Mi4T87yAZ1Ec4eKB-g3%2F-Mi4ZxpXLJHVnYlC0Dyl%2Fimage.png?alt=media&token=f4b2da4c-cdb0-4565-83f2-e3ef8e4a48cd)

占比的含义：某间隔下这个纬度值对应的用户数除以维度值对应的用户数。如上图 0~2小时的北京的占比是62.1% 代表 北京维度下 有62.1%的人数在 0~2 小时完成了转化。

### 转化时长趋势[](#zhuan-hua-shi-chang-qu-shi)

选择转化时长趋势可以看到任意步骤的漏斗转化时长均值的趋势和中位数趋势。

全部步骤的均值趋势 ：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MguCrq45Rloh-hnJ5f-%2F-MguHfUYQ2gDUsSY-b0n%2Fimage.png?alt=media&token=39c77d23-db38-4391-84bf-bcdfb3fdc414)

全部步骤的转化时长中位数：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MguCrq45Rloh-hnJ5f-%2F-MguHuZkjCj9qTJAaeEQ%2Fimage.png?alt=media&token=b2764312-a066-4b5e-9154-913fbbad5930)

## 常见问题[](#chang-jian-wen-ti)

1. 漏斗分析中的数据延迟[](#1-lou-dou-fen-xi-zhong-de-shu-ju-yan-chi)

数据需要传输时间，从您传输数据到在漏斗中可用会有一定的延迟，成功发送打点事件 1 小时后，可以在漏斗分析中使用该事件创建漏斗；
