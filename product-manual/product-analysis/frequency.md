---
id: frequency
sidebar_position: 8
---

# 分布分析

## 简介[](#jian-jie)

产品优化和运营是一个动态的过程，我们需要不断监测数据，调整产品设计或运营方法，然后继续监测效果。

分布分析功能，主要用来了解不同区间事件发生频次，不同事件计算变量加和，以及不同页面浏览时长等区间的用户数量分布。

主要功能包括：

* 事件指标的统计描述：最大值、最小值、平均值、25 分位、中位数、75 分位数；
    
* 提供统计描述指标的时间趋势；
    
* 自动根据指标的数值范围，对用户进行区间拆分，支持 10 层以内，15 层以内，25 层以内，以及自定义区间。
    
* 提供不同维度的分布对比；
    
* 提供不同用户群的分布对比。
    

## 功能说明[](#gong-neng-shuo-ming)

### 创建分布分析[](#chuang-jian-fen-bu-fen-xi)

一、在顶部导航栏选择“**分析 > 产品分析 \> 分布分析**"，进入分布分析看板。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3eplYl4s7kWXaewYEO%2F-M3erBuyHh9i5HJCjHtB%2Fimage.png?alt=media&token=00dd39f3-08da-4cd5-b7e8-b6813fadf229)

分布分析看板

二、单击左侧列表上方"**新建分析 \> 分布分析"**或单击事件分析看板中“**+”**，进入**创建分布分析**页面。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3eplYl4s7kWXaewYEO%2F-M3esOxhBnAqAuE_9oSZ%2Fimage.png?alt=media&token=d9f98d08-563f-4e92-a9c6-a2364d027177)

创建分布分析页面

| 项   | 说明  |
| --- | --- |
| 1-事件选择 | 需要使用分布分析的事件或指标。 |
| 2-目标用户 | 目标用户是设定要观测的目标用户人群。 |
| 3-维度对比 | 对事件进行维度细分。 |
| 4-用户对比 | 对比不同的目标用户群体的事件分布。 |
| 5-全局过滤 | 默认不加过滤，是针对整个分布分析的全局过滤。 |
| 7-分布展示 | 支持分布图和趋势图，详见视图介绍。视图​ |
| 8-统计口径 | 支持绝对值和百分比。 |
| 9-分布区间 | 支持10层以内、15层以内、25层以内、自定义区间。 |

三、选择参数后，右侧即可实时展示分析图表。

四、单击右上角保存，完成一个分布分析的创建。


### 视图介绍[](#shi-tu-jie-shao)

趋势图

分布图

趋势图

趋势图展现了事件发生次数的“最大值、最小值、平均值、中位数、25 分位值和 75 分位值”几个关键数据指标的变化趋势，可以帮助用户快速掌握目标事件的整体分布趋势。

拿下图示的“订单支付金额”来示意：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3em46U5qQ9giyLz-2e%2F-M3en2W-rL1ZAlojxPRm%2Fimage.png?alt=media&token=4c250907-e97b-4f34-869f-d58291ddccd5)

​

* 最大值：当日订单支付金额的最大值
    
* 最小值：当日订单支付金额的最小值
    
* 平均值：当日订单支付金额的平均值
    
* 25分位：订单支付金额按从小到大排序，前25%的订单支付金额小于等于多少
    
* 中位数：订单支付金额按从小到大排序，前50%的订单支付金额小于等于多少
    
* 75分位：订单支付金额按从小到大排序，前75%的订单支付金额小于等于多少
    

分布图

用户分布图根据您所选择的用户群、时间和事件，帮您进行事件频次的分组和分组后的用户数统计。

分布算法中，会先找到分布中的分布极值。如果直接按照 10等分或者 5 等分进行拆分，很可能会遇到没有办法找到频次少的分布值。优先找到5分位、95分位的值，然后在5分位至95分位的数值范围内对数据区间进行等分，则会根据数据特征自动分层。

拿下图示的“活跃天数”来示意：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3em46U5qQ9giyLz-2e%2F-M3enhFwQZi2eelmVyao%2Fimage.png?alt=media&token=d124628f-edb6-4f2f-b7f4-a602443691a7)

* 第一个柱表示的含义是：时间范围内(过去7天)，目标用户群 (**全部用户)，**用户活跃天数从小到大排序，前5%的用户活跃天数范围和用户量。
    
* 最后一个柱表示的含义是：时间范围内(过去7天)，目标用户群 (**全部用户)，**用户活跃天数从小到大排序，后5%的用户活跃天数范围和用户量。
    
* 在排除**活跃天数非常少**和**活跃天数非常多**的**用户**后，帮助您了解按照页面浏览量几等分后，相应值的区间内有多少用户量。
    

生成用户分群或下载用户ID[](#sheng-cheng-yong-hu-fen-qun-huo-xia-zai-yong-hu-id)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MDIN0ScxdJLg7ZtVis_%2F-MDIztl20PGxNTvw2I8s%2Fimage.png?alt=media&token=29b58e90-4df8-421d-b5b7-7cffd033cf83)

在分布分析的分布图中，单击用户量所在列的单元格即可出现以下效果，选择创建分群快速创建当前区间的用户分群或者下载用户ID。

### 分布分析看板[](#fen-bu-fen-xi-kan-ban)

分布分析看板与分析看板的管理方式相同，请参考看板管理。
