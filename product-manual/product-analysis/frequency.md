# 分布分析

## 简介

产品优化和运营是一个动态的过程，我们需要不断监测数据，调整产品设计或运营方法，然后继续监测效果。

分布分析功能，主要用来了解不同区间事件发生频次，不同事件计算变量加和，以及不同页面浏览时长等区间的用户数量分布。

主要功能包括：

* 事件指标的统计描述：最大值、最小值、平均值、25 分位、中位数、75 分位数；
* 提供统计描述指标的时间趋势；
* 自动根据指标的数值范围，对用户进行区间拆分，支持 10 层以内，15 层以内，25 层以内，以及自定义区间。
* 提供不同维度的分布对比；
* 提供不同用户群的分布对比。

## 创建分布分析

一、在顶部导航栏选择“**分析 &gt; 产品分析 &gt; 分布分析**"，进入分布分析看板。

![&#x5206;&#x5E03;&#x5206;&#x6790;&#x770B;&#x677F;](../../.gitbook/assets/image%20%2885%29.png)

二、单击左侧列表上方"**新建分析 &gt; 分布分析"**或单击事件分析看板中“**+”**，进入**创建分布分析**页面。

![&#x521B;&#x5EFA;&#x5206;&#x5E03;&#x5206;&#x6790;&#x9875;&#x9762;](../../.gitbook/assets/image%20%2834%29.png)

| 项 | 说明 |
| :--- | :--- |
| 1-事件选择 | 需要使用分布分析的事件或指标。 |
| 2-目标用户 | 目标用户是设定要观测的目标用户人群。 |
| 3-维度对比 | 对事件进行维度细分。 |
| 4-用户对比 | 对比不同的目标用户群体的事件分布。 |
| 5-全局过滤 | 默认不加过滤，是针对整个分布分析的全局过滤。 |
| 7-分布展示 | 支持分布图和趋势图，详见视图介绍。[视图]() |
| 8-统计口径 | 支持绝对值和百分比。 |
| 9-分布区间 | 支持10层以内、15层以内、25层以内、自定义区间 |

三、选择要参数后，右侧即可实时展示分析图表。

四、单击右上角保存，完成一个分布分析的创建。

## 视图介绍

{% tabs %}
{% tab title="趋势图" %}
趋势图展现了事件发生次数的“最大值、最小值、平均值、中位数、25 分位值和 75 分位值”几个关键数据指标的变化趋势，可以帮助用户快速掌握目标事件的整体分布趋势。

拿下图示的“订单支付金额”来示意：

![](../../.gitbook/assets/image%20%2859%29.png)



* 最大值：当日订单支付金额的最大值 
* 最小值：当日订单支付金额的最小值 
* 平均值：当日订单支付金额的平均值
* 25分位：订单支付金额按从小到大排序，前25%的订单支付金额小于等于多少
* 中位数：订单支付金额按从小到大排序，前50%的订单支付金额小于等于多少
* 75分位：订单支付金额按从小到大排序，前75%的订单支付金额小于等于多少
{% endtab %}

{% tab title="分布图" %}
用户分布图根据您所选择的用户群、时间和事件，帮您进行事件频次的分组和分组后的用户数统计。

分布算法中，会先找到分布中的分布极值。如果直接按照 10等分或者 5 等分进行拆分，很可能会遇到没有办法找到频次少的分布值。优先找到5分位、95分位的值，然后在5分位至95分位的数值范围内对数据区间进行等分，则会根据数据特征自动分层。

拿下图示的“活跃天数”来示意：

![](../../.gitbook/assets/image%20%2813%29.png)

* 第一个柱表示的含义是：时间范围内\(过去7天\)，目标用户群 \(**全部用户\)，**用户活跃天数从小到大排序，前5%的用户活跃天数范围和用户量。
* 最后一个柱表示的含义是：时间范围内\(过去7天\)，目标用户群 \(**全部用户\)，**户活跃天数从小到大排序，后5%的用户活跃天数范围和用户量。
* 在排除**活跃天数非常少**和**活跃天数非常多**的**用户**后，帮助您了解按照页面浏览量几等分后，相应值的区间内有多少用户量。
{% endtab %}
{% endtabs %}

## 生成用户分群或下载用户ID

![](../../.gitbook/assets/image%20%28289%29.png)

在分布分析的分布图中，单击用户量所在列的单元格即可出现以下效果，选择创建分群快速创建当前区间的用户分群或者下载用户ID。

## 分布分析看板

分布分析看板与分析看板的管理方式相同，请参考看板管理。

