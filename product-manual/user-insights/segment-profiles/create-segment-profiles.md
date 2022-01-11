---
id: create-segment-profiles
sidebar_position: 2
---

# 创建用户群体

在 **项目 > 用户洞察 > 群体画像** 中点击 **新建群体画像** 进入群体画像创建弹窗，选择创建方式后进入群体画像创建流程。

![](/img/用户洞察-群体画像-选择新建方式.png)

## 规则创建

在 **新建群体画像** 弹窗中选择 **规则创建** 后进入规则创建弹窗。

### 控件说明

* 基础信息

| 项 | 是否必填 | 说明 | 限制条件 |
| -- | -- | -- | -- |
| 名称 | 是 | 群体画像名称 | 名称 **项目内** 唯一，不可重复<br/>最大输入30个字符 |
| 标识符 | 是 | 群体画像标识符<br/>可用于数据库和API查询 | 名称 **全局** 唯一，不可重复<br/>最大输入100个字符<br/>仅允许大小写英文、数字、以及下划线 |
| 描述 | 否 | 群体画像的业务意义描述 | 最大输入150个字符 |
| 更新频次 | 是 | 群体画像更新计算周期 | 仅支持选择每日更新和手动更新 |

![](/img/用户洞察-群体画像-规则创建-基础信息.png)

* 定义规则

群体画像支持根据 **用户行为** 和 **用户属性** 创建用户群体

> 注：最多支持10条定义规则

#### 用户行为 - 做过

| 项   | 说明  | 限制条件 |
| -- | -- | -- |
| 时间选择器 | 选择事件发生时间 | 无 |
| 事件选择器 | 选择事件 | 支持埋点事件和虚拟事件 |
| 维度+度量选择器 | 选择事件计算逻辑 | 支持选择次数总和<br/>支持选择整数、小数类型事件属性总和 |
| 行为条件选择器 | 选择事件计算结果的筛选条件 | 无 |
| 过滤选择器 | 选择事件过滤条件 | 支持选择事件属性、用户属性和用户标签 |

![](/img/用户洞察-群体画像-规则创建-定义规则.png)

#### 用户行为 - 未做过

| 项   | 说明  | 限制条件 |
| -- | -- | -- |
| 时间选择器 | 选择事件发生时间 | 无 |
| 事件选择器 | 选择事件 | 支持埋点事件和虚拟事件 |
| 过滤选择器 | 选择事件过滤条件 | 支持选择事件属性、用户属性和用户标签 |

![](/img/用户洞察-群体画像-规则创建-定义规则-未做过.png)

#### 用户属性

| 项   | 说明  | 限制条件 |
| -- | -- | -- |
| 属性选择器 | 选择用户特征 | 支持选择用户属性和用户标签 |
| 过滤选择器 | 选择用户特征过滤条件 | 无 |

![](/img/用户洞察-群体画像-规则创建-定义规则-用户属性.png)

#### 预估人数

在群体画像保存前，建议点击 **计算** 预估群体人数，以确定定义规则和业务预期是否一致。

### 统计逻辑

#### 例1：做过订单支付事件金额总和大于1万元

![](/img/用户洞察-群体画像-规则创建-例1.png)

```sql
select
	u.gio_id 								as gio_id
from 
(
	select
		gio_id 								as gio_id
	from olap.user
	where usr_$first_day is not null
) u  															-- 全量用户
join 
(
	select
	    gio_id                          	as gio_id
	    ,sum( var_payamount )				as payamount
	from olap.event
	where account_id = 'bc675c65b3b0290e'                       -- 项目ID
	    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
	    and event_key = 'payment'                             	-- 事件标识符 
	group by gio_id
	having payamount > 10000
) e on u.gio_id = e.gio_id 
```

#### 例2：未做过使用优惠券的订单支付事件

![](/img/用户洞察-群体画像-规则创建-例2.png)

以上规则计算结果包含以下用户群体：

* 过去30天未活跃(未发生任意行为)的用户

* 过去30天活跃但未发生订单支付的用户

* 过去30天活跃且发生订单支付，但未使用优惠券的用户

> 当使用未做过时，计算结果可能会包含大量“沉睡用户”，建议先进行人群预估再进行保存

```sql
select
	u.gio_id 								as gio_id
from 
(
	select
		gio_id 								as gio_id
	from olap.user
	where usr_$first_day is not null
) u  															-- 全量用户
left join 
(
	select
	    gio_id                          	as gio_id
	    ,count(1)                           as num
	from olap.event
	where account_id = 'bc675c65b3b0290e'                       -- 项目ID
	    and dateDiff( 'day' , dt , today()) between 1 and 30    -- 时间筛选
	    and event_key = 'payment'                             	-- 事件标识符 
        and var_E_ifCounpon = '是'
	group by gio_id
) e on u.gio_id = e.gio_id 
where e.num is null or e.num = 0
```

#### 例3：用户属性性别为男

![](/img/用户洞察-群体画像-规则创建-例3.png)

```sql
select
	gio_id 								    as gio_id
from olap.user
where usr_gender = '男'
```

## 文件上传创建

在 **新建群体画像** 弹窗中选择 **文件上传创建** 后进入文件上传创建弹窗。

### 控件说明



### 统计逻辑


