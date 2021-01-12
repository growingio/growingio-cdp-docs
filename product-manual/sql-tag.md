# SQL标签-beta\(仅内部\)

## 简介

GrowingIO支持通过SQL自定义用户标签，如需了解基础数据模型请点击 “[数据模型](https://docs.growingio.com/op/introduction/data-model/)” 进行查看。

## SQL语句和语法说明

### SQL输出结果

输出结果必须为2列数据，每列分别为：userId 和 tagValue

其中，userId为GrowingIO采集的用户匿名ID或客户上传的登录用户ID；tagValue为标签计算结果。

标签计算结果数值类型支持字符串、整数、日期、集合

{% hint style="success" %}
注意userId和tagValue严格区分大小写和输出顺序
{% endhint %}

{% hint style="success" %}
日期类型标签输出格式仅支持毫秒时间戳
{% endhint %}

示例: 

```text
// 2021年1月1日订单支付次数
select 
    user_id         as userId
    ,count(1)       as tagValue
from carbon.event
where time = '202012311600'
    and event_key = 'payOrderSuccess'
group by 1
```

![&#x8F93;&#x51FA;&#x7ED3;&#x679C;](../.gitbook/assets/image%20%28470%29.png)

{% hint style="success" %}
event表中 time 字段为UTC时间分区，精确到天级别。

即日期为 date 的数据对应的UTC时间分区为 \( date - 1 \) + '1600'。

查询event数据时，为提高查询效率建议优先使用time分区作为SQL查询条件。
{% endhint %}

### 动态时间范围

如果您的数据计算时间范围是动态变化的，如“过去7天订单支付次数“，这时就需要使用动态时间来表示数据的时间范围。GrowingIO提供预置函数 daysAgo\( input \) 支持筛选动态时间。

| 参数 | 数值类型 | 说明 |
| :--- | :--- | :--- |
| input | int | daysAgo\( n \)为过去第n天，即daysAgo\( 0 \)为今天，daysAgo\( 1 \)为昨天。 |

{% hint style="success" %}
如参数部分输入小数，则默认会截取整数部分作为参数输入值。

即daysAgo\( 1.75 \) = daysAgo\( 1 \)
{% endhint %}

示例: 

```text
// 过去7天订单支付次数
select 
    user_id         as userId
    ,count(1)       as tagValue
from carbon.event
where time between daysAgo( 7 ) and daysAgo( 1 )
    and event_key = 'payOrderSuccess'
group by 1
```

### 常见问题



## 常用SQL标签

### 1）过去7天订单支付成功事件发生次数

您可以在 “**客户数据平台 &gt; 数据 &gt; 埋点事件**" 中查看 “**订单支付成功**“ 事件的标识符，即payOrderSuccess。

```text
select 
    user_id                 as userId
    ,count(1)               as tagValue
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
group by 1
```

### 2）过去7天订单支付成功事件发生天数

```text
select 
    user_id                               as userId
    ,count( distinct time )               as tagValue
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
group by 1
```

> 注：time为UTC时间分区，精确到天

### 3）过去7天订单支付成功事件实际支付金额总和

您可以在 “**客户数据平台 &gt; 数据 &gt; 事件属性**" 中查看 “**实际支付金额**“ 事件属性的标识符，即payAmount\_var。

```text
select 
    user_id                                          as userId
    ,int(round(sum( attributes.payAmount_var ),0))   as tagValue
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
    and attributes.payAmount_var is not null
group by 1
```

{% hint style="success" %}
event中事件属性可能存在null值，在计算数值型事件属性求和时需要筛选事件属性不为空的数据。如需了解ETL规则请点击 “[属性模型“](https://docs.growingio.com/op/introduction/property-model) 进行查看。
{% endhint %}

{% hint style="success" %}
目标SQL标签仅支持整数类型，不支持小数类型，因此创建结果需要区取整才能保存标签创建规则。
{% endhint %}

### 4）过去7天订单支付成功事件实际支付金额单笔平均值

```text
select 
    user_id 											                            as userId
    ,int(round(sum( attributes.payAmount_var ) / count(1),0))	as tagValue
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
    and attributes.payAmount_var is not null
group by 1
```

{% hint style="warning" %}
目标SQL标签仅支持整数类型，不支持小数类型，因此创建结果需要区取整才能保存标签创建规则。对于平均值标签输出结果需要四舍五入仅保留整数部分。
{% endhint %}

注意，该计算结果与基础指标标签中平均值计算结果存在差异，主要原因为基础指标标签计算平均值时分母\(订单支付成功事件次数\)没有过滤null值数据。

基础指标计算方法如下：

```text
with pay_times as 
(
select 
    user_id 						as userId
    ,count(1)                       as pay_times
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
group by 1
)
,pay_amount as 
(
select 
    user_id 							as userId
    ,sum( attributes.payAmount_var ) 	as pay_amount
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
    and attributes.payAmount_var is not null
group by 1
)


select
	pt.userId 									                    as userId
	,int(round( pa.pay_amount / pt.pay_times ,0 )) 	as tagValue
from pay_times pt 
	join pay_amount pa on pt.userId = pa.userId 
```









