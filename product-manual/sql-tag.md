# SQL标签-beta\(仅内部\)

## 简介

GrowingIO支持通过SQL自定义用户标签，如需了解基础数据模型请点击 “[数据模型](https://docs.growingio.com/op/introduction/data-model/)” 进行查看。

## 创建SQL标签

一、在 **客户数据平台** 选择 “**数据 &gt; 标签 &gt; 标签管理**" ，进入标签管理页面。

二、单击右上角 **新建标签**、进入**新建标签**页面。

三、切换到 **SQL标签** 选项，进入SQL标签创建页面。

四、输入标签名称和SQL规则，点击保存创建SQL标签。

{% hint style="success" %}
在完成了配置，我们即可开始在GrowingIO使用该SQL标签。
{% endhint %}

![](../.gitbook/assets/image%20%28471%29.png)

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

### 5）过去7天订单支付成功事件实际支付金额中使用满减券的支付金额占比

```text
select 
    user_id 						as userId
    ,round( sum( if( attributes.couponName_var = '满减券',attributes.payAmount_var , 0 ) )
    		/ sum( attributes.payAmount_var ) 
    	, 4 ) 						as tagValue
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
    and attributes.payAmount_var is not null
group by 1
```

{% hint style="warning" %}
SQL标签仅支持整数类型，不支持小数类型，因此不支持金额占比等SQL标签。
{% endhint %}

### 6）过去7天商品详情页浏览最多的一级品类

```text
with catalog_pv_sum as  
( 					
select 
    user_id 											  as userId
    ,attributes.firstCat_var				as catalog
    ,count(1)											  as pv
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'goodsDetailPageView'
group by 1,2
)
,catalog_pv_max as 							
(
select
	userId 									as userId
	,max(pv)								as pv_max
from catalog_pv_sum
group by 1
)
,catalog_max as 
(
select
	cps.userId 								as userId
	,cps.catalog 							as catalog
from catalog_pv_sum cps 
	join catalog_pv_max cpm on cps.userId = cpm.userId 
		and cps.pv = cpm.pv_max
)

select
	userId 								    			as userId
	,collect_set( catalog )					as tagValue
from catalog_max
group by 1
```

{% hint style="success" %}
由于一个用户可能存在多个品类浏览并列第一，因此输出结果为集合。
{% endhint %}

{% hint style="warning" %}
目前对于SQL标签输出结果并未做唯一性校验，如果输出结果中一个用户存在多行\(多值\)情况，那么系统会默认选取排序靠前的结果值进行存储。
{% endhint %}

### 7）过去7天订单支付成功事件最近一次发生的具体日期\(‘YYYY-MM-DD'\)

```text
select 
    user_id     			        as userId
    ,max( event_time ) 		    as tagValue
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
group by 1
```

{% hint style="success" %}
event\_time为GrowingIO服务器接收数据时间\(UTC时间，相比北京时间慢8个小时\)，数据格式为毫秒时间戳。您在做日期相关计算时仅需对原始event\_time进行加工计算，存储格式仍为毫秒时间戳，无需转化为天。GrowingIO前端在展示和计算时，会默认将数据转化为北京时间，并转化为'YYYY-MM-DD'格式进行前端展示。
{% endhint %}

### 8）过去7天订单支付成功事件最近一次发生距今的时间间隔

```text
select 
    user_id                                     as userId
    ,datediff( current_date() 
        , max( event_time + 8*3600*1000 ))      as tagValue
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
group by 1
```

### 9）过去7天商品详情页浏览的全部一级分类

```text
with catalog_view as 
(
select 
    user_id 								        as userId
    ,attributes.firstCat_var				as tagValue
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'goodsDetailPageView'
group by 1,2
)

select
	userId 									        as userId
	,collect_set( tagValue )				as tagValue
from catalog_view 
group by 1
```

### 10）分层标签1

定义规则：过去7天所有支付的用户中，支付金额大于200元的用户为‘高价值’用户；其余用户为‘低价值’用户。

```text
with payment as 
(
select 
    user_id 								as userId
    ,sum( attributes.payAmount_var ) 		as tagValue
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
    and cast( attributes.payAmount_var as double ) is not null
group by 1
)

select
	userId 											as userId 
	,if( tagValue > 200 , '高价值' , '低价值' ) 		as tagValue
from payment
```

### 11）分层标签2

> 基于用户属性和用户标签计算SQL标签

定义规则：在所有“有过交易行为”（用户属性）的用户中，最近7天有订单交易的用户（用户标签）为‘近期有交易’用户；其余为‘有交易’用户。

您可以在 “**客户数据平台 &gt; 数据 &gt; 用户属性**" 中查看 “**用户是否购买**“ 用户属性的标识符，即IfUserBuy\_ppl，并在user\_props表中查看用户属性。

{% hint style="success" %}
user\_props中dim为用户属性标识符，查询自定义用户属性时需要加上前缀 'usr\_'
{% endhint %}

{% hint style="success" %}
user\_props中的gid做以下处理后，

    cast\( reverse\( gid \) as int \)

对应event表中的user\_id
{% endhint %}

您可以在zeppelin中通过以下命令查询标签的tag\_id

```text
%insight
select 
	key
from computes
where id in
	(
	select 
		compute_id
	from tags_computes
	where tag_id in
		(
		select 
			id
		from tags
		where name = '{标签名称}'
		)
	)
```

并在 user\_tag\_rule\_values 中根据已获取的tag\_id查看每个用户标签值。

{% hint style="success" %}
user\_tag\_rule\_values中的gid做以下处理后，

    cast\( reverse\( gid \) as int \)

对应event表中的user\_id
{% endhint %}

```text
with user_props_value as 
(
select
	cast( reverse( gid ) as int ) 	as userId
	,DVALUE													as user_props_value
from user_props 
where dim = 'usr_IfUserBuy_ppl'
)
,tag_value as 
(
select
	cast( reverse(gid) as int ) 	as userId
	,tag_value 						as tag_value
from user_tag_rule_values
where tag_id = 'd6f6ef930082e703e8a1bc9e563dff4d'
)

select
	u.userId
	,if( t.tag_value is not null , '近期有交易' , '有交易' ) as tagValue
	,u.user_props_value 
	,t.tag_value
from user_props_value u
	left join tag_value t on u.userId = t.userId
```

### 12）分层标签3

> 基于分位数构建用户分层

定义规则：过去30天，订单支付事件实际支付金额总和小于10元的用户为“羊毛”用户；头20%的用户为“高价值“用户；头80%至20%的用户为”中价值“用户；末尾20%的用户为”低价值“用户。

```text
with pay_amount as 
(
select 
    user_id                                          as userId
    ,round(sum( attributes.payAmount_var ),0)   	 as tagValue
    ,1 												 as join_index 
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
    and attributes.payAmount_var is not null
group by 1
)
,pay_percentile as 
(
select
	percentile( tagValue , 0.2 )					 as pct_2
	,percentile( tagValue , 0.8 )					 as pct_8
	,1 												 as join_index 
from pay_amount
)

select
	pa.userId 										 as userId
	,case when pa.tagValue < 10 then '羊毛'
		when pa.tagValue > pp.pct_8 then '高价值'
		when pa.tagValue > pp.pct_2 then '中价值'
		else '低价值' end 							 as tagValue 
from pay_amount pa 
	join pay_percentile pp on pa.join_index = pp.join_index 
```

{% hint style="success" %}
SQL关联时不支持使用 1 =  1，需要在pay\_amount和pay\_percentile中分别构建关联列join\_index，并使用该列进行两个表关联查询。
{% endhint %}

### 13）分层标签4

定义规则：将分层标签中“中价值”和”低价值“用户统称”低价值“，“高价值”用户分层保留。

![](../.gitbook/assets/image%20%28480%29.png)

分层标签存储结构：

![](../.gitbook/assets/image%20%28479%29.png)

```text
%insight
with tags_info as 
(
select 
        compute_id
        ,compute_name
from tags_computes
where tag_id in
        (
        select id
        from tags
        where name = '规则：分层标签4'
        )
)


select 
        c.key                           as tag_key 
        ,t.compute_name                 as tag_value
from computes c
        join tags_info t on c.id = t.compute_id
```

Output:

![](../.gitbook/assets/image%20%28481%29.png)

```text
with tags as      // 虚拟表
(
select 
    tag_key
    ,tag_value
from ( values
                ( '939ba107f55c0f23990ed977e177dfe8' , '高价值' )
                ,( 'e1819181b5be6085dcbecdac8747af03' , '中价值' )
                ,( '47c930018c16c75fc4da47c4c506662f' , '低价值' )
        ) as t(tag_key,tag_value)
)


select
        cast( reverse(u.gid) as int )                        as userId
        ,case t.tag_value when '高价值' then '高价值'
                when '中价值' then '低价值'
                when '低价值' then '低价值'
        end                                                                         as tagValue
from USER_TAG_RULE_VALUES u 
        join tags t on u.tag_value = t.tag_key
```

### 14）用户活跃时段1

定义规则：过去30天，用户在 8:00 - 22:00 之间活跃天数最多的时段\(小时\)。且活跃天数必须大于等于3天，如果存在多个活跃时段取最早的活跃时段。

```text
with act_hour as 
(
select 
    user_id         															as userId
    ,hour( from_unixtime( event_time/1000 + 8*3600 , 'YYYY-MM-DD HH:MM:SS') ) 	as act_hour 
    ,count( distinct time )														as num
	,row_number() over (partition by user_id 
		order by count( distinct time ) desc 
			,hour( from_unixtime( event_time/1000 + 8*3600 , 'YYYY-MM-DD HH:MM:SS') )  
			)																	as rank_num 												
from carbon.event
where time between daysAgo( 30 ) and daysAgo( 1 )
	and hour( from_unixtime( event_time/1000 + 8*3600 , 'YYYY-MM-DD HH:MM:SS') ) >= 8 
	and hour( from_unixtime( event_time/1000 + 8*3600 , 'YYYY-MM-DD HH:MM:SS') ) <= 22
group by 1,2
having count( distinct time ) >= 3 
)

select
	userId 				as userId 
	,act_hour 			as tagValue
from act_hour
where rank_num = 1
```

### 15）用户活跃时段2

定义规则:  过去30天，将活跃时段分为\[0,4\),\[4,8\),\[8,12\),\[12,16\),\[16,20\),\[20,24\)六个时段，每个时段从0开始对应,一直到5，返回用户最活跃的时段序号，如存在多个则同时返回多个活跃时段。

```text
with raw_data as 
(
select 
    user_id         															as userId
    ,hour( from_unixtime( event_time/1000 + 8*3600 , 'YYYY-MM-DD HH:MM:SS') ) 	as act_hour 
    ,time 																		as act_date						
from carbon.event
where time between daysAgo( 30 ) and daysAgo( 1 )
)
,act_hour as 
(
select
	userId 								as userId 
	,case when act_hour < 4 then 0
		when act_hour < 8 then 1
		when act_hour < 12 then 2 
		when act_hour < 16 then 3
		when act_hour < 20 then 4
		else 5 end 						as act_time 
	,count( distinct act_date )			as num
from raw_data 
group by 1,2
)
,act_max as
(
select
	userId 								as userId 
	,max( num )							as num_max
from act_hour
group by 1
)
,act_hour_max as 
(
select
	ah.userId 							as userId 
	,ah.act_time 						as act_time 
from act_hour ah 
	join act_max am on ah.userId = am.userId 
		and ah.num = am.num_max
)

select
	userId 								as userId 
	,collect_set( act_time )			as tagValue
from act_hour_max
group by 1
```


