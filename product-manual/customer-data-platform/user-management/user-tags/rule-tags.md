---
id: rule-tags
sidebar_position: 3
---

# 创建规则标签

一、在 **客户数据平台 > 用户管理 > 用户标签** 中点击 **新建用户标签** 进入用户标签创建弹窗

![](/img/用户标签-选择标签类型.png)

二、选择 **标签类型** 并填写标签基本信息

| 项 | 是否必填 | 说明 | 限制条件 |
| -- | -- | -- | -- |
| 名称 | 是 |用户标签名称 | 名称唯一，不可重复<br/>最大输入30个字符 |
| 标识符 | 是 | 用户标签标识符<br/>可用于数据库和API查询 | 名称唯一，不可重复<br/>最大输入100个字符<br/>仅允许大小写英文、数字、以及下划线，并且不能以数字开头 |
| 描述 | 否 | 用户标签的业务意义描述 | 最大输入150个字符 |
| 所属分类 | 否 | 选择自定义的用户标签分类 | 如不选择则为未分类 |

![](/img/用户标签-基本信息.png)

三、点击 **下一步** 开始定义标签规则

## 基础指标值[](#ji-chu-zhi-biao-zhi)

> 把事件的统计结果作为标签值，对用户打标。[点击查看说明](./user-tags#ji-chu-zhi-biao-zhi)

### 控件说明

| 项   | 说明  | 限制条件 |
| -- | -- | -- |
| 时间选择器 | 选择打标事件发生时间 | 无 |
| 事件选择器 | 选择打标事件 | 支持埋点事件和虚拟事件 |
| 维度+度量选择器 | 选择打标事件计算逻辑 | 支持选择字符串、整数、小数类型事件属性 |
| 过滤选择器 | 选择事件过滤条件 | 支持选择事件属性和用户属性 |

![](/img/用户标签-基础指标值.png)

#### 维度+度量选择器

系统根据不同数值类型的事件属性，支持以下度量方式：

| 维度 | 总和(度量) | 平均值(度量) | 累计占比(度量) | 去重数(度量) |
| -- | -- | -- | -- | -- |
| 次数 | ✓ |- | ✓ | - |
| 总天数 | - | - | - | - |
| 整数、小数事件属性 | ✓ | ✓ | ✓ | - |
| 字符串事件属性 | - | - | - | ✓ |

### 统计逻辑

#### 例1: 过去30天，直接访问次数总和

业务含义：使用过去30天，每个用户直接访问的次数作为标签值，对用户进行打标

![](/img/用户标签-基础指标值-例1.png)

``` sql
select
    gio_id          as gio_id
    ,count(1)       as tag_value                            -- 事件次数
from olap.event
where account_id = 'bc675c65b3b0290e'                       -- 项目ID
    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
    and event_key = '$visit'                                -- 事件标识符 
    and $referrer_type is null                              -- 事件过滤
group by gio_id
```
#### 例2: 过去30天，总访问天数

业务含义：使用过去30天，每个用户访问的总天数作为标签值，对用户进行打标

![](/img/用户标签-基础指标值-例2.png)

``` sql
select
    gio_id                      as gio_id
    ,count( distinct dt )       as tag_value                -- 事件总天数
from olap.event
where account_id = 'bc675c65b3b0290e'                       -- 项目ID
    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
    and event_key = '$visit'                                -- 事件标识符 
group by gio_id
```

#### 例3: 过去30天，订单支付金额总和

业务含义：使用过去30天，每个用户订单支付总金额作为标签值，对用户进行打标

![](/img/用户标签-基础指标值-例3.png)

``` sql
select
    gio_id                      as gio_id
    ,sum( var_payamount )       as tag_value                -- 订单支付总金额
from olap.event
where account_id = 'bc675c65b3b0290e'                       -- 项目ID
    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
    and event_key = 'payment'                               -- 事件标识符 
    and var_payamount is not null
group by gio_id
```

#### 例4: 过去30天，订单支付金额平均值

业务含义：使用过去30天，每个用户订单支付金额的平均值作为标签值，对用户进行打标

> 注1: 仅统计有效订单(金额有值)的订单金额平均值
> 注2: 计算结果保留小数点后2位有效数字

![](/img/用户标签-基础指标值-例4.png)

``` sql
select
    gio_id                                  as gio_id
    ,round( avg( var_payamount ) , 2 )      as tag_value    -- 金额平均值
from olap.event
where account_id = 'bc675c65b3b0290e'                       -- 项目ID
    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
    and event_key = 'payment'                               -- 事件标识符 
    and var_payamount is not null
group by gio_id
```

#### 例5: 过去30天，订单支付金额累计占比

业务含义：使用过去30天，每个用户3c类产品支付金额占总支付金额的占比作为标签值，对用户进行打标

> 注1: 仅统计有效订单(金额有值)
> 注2: 计算结果保留小数点后2位有效数字

![](/img/用户标签-基础指标值-例5.png)

``` sql
select
    gio_id                                  as gio_id
    ,round( sum( if( var_product_layer1 = '3c' , var_payamount , 0 ) ) / 
            sum( var_payamount ) , 2 )      as tag_value    -- 金额累计占比
from olap.event
where account_id = 'bc675c65b3b0290e'                       -- 项目ID
    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
    and event_key = 'payment'                               -- 事件标识符 
    and var_payamount is not null
group by gio_id
```

#### 例6: 过去30天，订单支付优惠券类型去重数

业务含义：使用过去30天，每个用户订单支付中使用优惠券类型去重个数作为标签值，对用户进行打标

> 注：标签计算结果中，
> 过去30天，未发生订单支付事件的用户标签值为 null
> 过去30天，发生订单支付但未使用优惠券的用户标签值为 0
> 过去30天，发生订单支付且使用优惠券的用户标签值为 1,2,3...

![](/img/用户标签-基础指标值-例6.png)

``` sql
select
    gio_id                                  as gio_id
    ,count( distinct var_coupon_type )      as tag_value    -- 优惠券类型去重数
from olap.event
where account_id = 'bc675c65b3b0290e'                       -- 项目ID
    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
    and event_key = 'payment'                               -- 事件标识符 
group by gio_id
```

## 最大值/最小值的事件属性[](#zui-da-zhi-zui-xiao-zhi-de-shi-jian-shu-xing)

> 按事件属性分组后，对发生次数或整数、小数类型事件属性求和最多或最少的分组属性值作为标签值，对用户打标。[点击查看说明](./user-tags#zui-da-zhi-zui-xiao-zhi-de-shi-jian-shu-xing)

### 控件说明

| 项   | 说明  | 限制条件 |
| -- | -- | -- |
| 时间选择器 | 选择打标事件发生时间 | 无 |
| 事件选择器 | 选择打标事件 | 支持埋点事件和虚拟事件 |
| 排序维度选择器 | 选择计算维度和排序逻辑 | 支持整数、小数类型事件属性<br/>支持最多和最少排序逻辑 |
| 分组维度选择器 | 选择分组维度 | 支持字符串类型事件属性 |
| 过滤选择器 | 选择事件过滤条件 | 支持选择事件属性和用户属性 |

![](/img/用户标签-最大值最小值.png)

### 统计逻辑

#### 例1：过去30天，购买金额最多的一级品类

业务含义：将过去30天每个用户订单支付金额总和按商品一级品类分组，使用支付金额最多的分组品类名称作为标签值，对用户进行打标

> 注1：仅从商品一级品类名称(分组维度)非空值中进行排序打标
> 注2：当多种一级品类(分组维度)支付总额并列最多时，随机返回其中某个一级品类名称

![](/img/用户标签-最大值最小值-例1.png)

```sql
select
	gio_id 								as gio_id
	,groupArray(1)(group_attribute)[1]	as tag_value
from 
(
	select
	    gio_id                          as gio_id
	    ,var_product_layer1 			as group_attribute  	-- 分组维度
	    ,sum( var_payamount )      		as order_attribute    	-- 排序维度
	from olap.event
	where account_id = 'bc675c65b3b0290e'                       -- 项目ID
	    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
	    and event_key = 'payment'                               -- 事件标识符 
        and var_product_layer1 is not null
	group by gio_id
		,var_product_layer1
	order by gio_id,order_attribute desc
)
group by gio_id
```

## 首次/末次的事件属性[](#shou-ci-mo-ci-de-shi-jian-shu-xing)

> 将事件第一次或最后一次发生的字符串类型事件属性作为标签值，对用户打标。[点击查看说明](./user-tags#shou-ci-mo-ci-de-shi-jian-shu-xing)

### 控件说明

| 项   | 说明  | 限制条件 |
| -- | -- | -- |
| 时间选择器 | 选择打标事件发生时间 | 无 |
| 事件选择器 | 选择打标事件 | 支持埋点事件和虚拟事件 |
| 逻辑选择器 | 选择计算逻辑 | 支持首次发生和末次发生 |
| 维度选择器 | 选择打标维度 | 支持距今天数、日期和字符串事件属性 |
| 过滤选择器 | 选择事件过滤条件 | 支持选择事件属性和用户属性 |

![](/img/用户标签-最初最终.png)

### 编辑限制

**首次/末次的事件属性** 支持将某个事件的发生时距今天数(小数)、发生时的具体日期(日期)和发生时的事件属性(字符串)作为标签值，对用户打标。且已保存标签支持在分析工具、群体画像等应用中作为维度过滤和维度拆解使用。为保证标签在应用中平稳使用，标签编辑时禁止修改标签的数值类型。因此编辑标签时具有以下限制：

| 当前选择 | 修改-距今天数 | 修改-日期 | 修改-事件属性 |
| -- | -- | -- | -- |
| 距今天数 | ✓ | - | - |
| 日期 | - | ✓ | - |
| 事件属性 | - | - | ✓ |

### 统计逻辑

#### 例1：过去30天，首次订单支付距今天数

业务含义：使用过去30天，每个用户首次发生订单支付距今天数作为标签值，对用户进行打标

![](/img/用户标签-首次末次-例1.png)

```sql
select
	gio_id 									as gio_id
	,groupArray(1)(target_atttribute)[1]	as tag_value
from 
(
	select
	    gio_id                          	as gio_id
	    ,dt 								as order_attribute
	    ,dateDiff( 'day' , dt , today())	as target_atttribute
	from olap.event
	where account_id = 'bc675c65b3b0290e'                       -- 项目ID
	    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
	    and event_key = 'payment'                               -- 事件标识符 
	order by gio_id,dt
)
group by gio_id
```

#### 例2：过去30天，末次订单支付日期

业务含义：使用过去30天，每个用户末次发生订单支付的具体日期作为标签值，对用户进行打标

![](/img/用户标签-首次末次-例2.png)

```sql
select
	gio_id 									as gio_id
	,groupArray(1)(target_atttribute)[1]	as tag_value
from 
(
	select
	    gio_id                          	as gio_id
	    ,dt 								as order_attribute
	    ,dt	                                as target_atttribute
	from olap.event
	where account_id = 'bc675c65b3b0290e'                       -- 项目ID
	    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
	    and event_key = 'payment'                               -- 事件标识符 
	order by gio_id,dt desc
)
group by gio_id
```

#### 例3：过去30天，首次使用的优惠券类型

业务含义：使用过去30天，每个用户发生订单支付时，首次使用的优惠券类型作为标签值，对用户进行打标

> 注1：仅从优惠券类型非空值中进行排序打标，即有使用优惠券的用户
> 注2：以天粒度排序，如果一天内用户使用多个优惠券，随机返回其中某个优惠券名称

![](/img/用户标签-首次末次-例3.png)

```sql
select
	gio_id 									as gio_id
	,groupArray(1)(target_atttribute)[1]	as tag_value
from 
(
	select
	    gio_id                          	as gio_id
	    ,dt 								as order_attribute
	    ,var_conpon_type	                as target_atttribute
	from olap.event
	where account_id = 'bc675c65b3b0290e'                       -- 项目ID
	    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
	    and event_key = 'payment'                               -- 事件标识符 
        and var_conpon_type is not null
	order by gio_id,dt
)
group by gio_id
```

## 列表类的事件属性[](#lie-biao-lei-de-shi-jian-shu-xing)

> 将事件的全部事件属性列表作为标签值，对用户打标。[点击查看说明](./user-tags#lie-biao-lei-de-shi-jian-shu-xing)

### 控件说明

| 项   | 说明  | 限制条件 |
| -- | -- | -- |
| 时间选择器 | 选择打标事件发生时间 | 无 |
| 事件选择器 | 选择打标事件 | 支持埋点事件和虚拟事件 |
| 维度选择器 | 选择打标维度 | 支持字符串事件属性 |
| 过滤选择器 | 选择事件过滤条件 | 支持选择事件属性和用户属性 |

![](/img/用户标签-列表.png)

### 统计逻辑

#### 例1：过去30天，使用的全部优惠券类型

业务含义：使用过去30天，每个用户使用的全部优惠券类型(去重)作为标签值，对用户进行打标

> 注1：仅筛选使用优惠券的订单
> 注2：优惠券类型去重

![](/img/用户标签-列表-例1.png)

```sql
select
	gio_id 									as gio_id
	,groupArray(target_atttribute)	        as tag_value
from 
(
	select
	    gio_id                          	as gio_id
	    ,var_conpon_type	                as target_atttribute
	from olap.event
	where account_id = 'bc675c65b3b0290e'                       -- 项目ID
	    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
	    and event_key = 'payment'                               -- 事件标识符 
        and var_conpon_type is not null
	order by gio_id,var_conpon_type
)
group by gio_id
```

## 分层标签[](#fen-ceng-biao-qian)

### 控件说明

### 统计逻辑



