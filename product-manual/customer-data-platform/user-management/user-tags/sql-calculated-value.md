---
id: sql-calculated-value
sidebar_position: 4
---

# 创建SQL标签

在使用SQL标签前，推荐您阅读[数据模型](/getting-started/basic-concept/data-model)文档。

一、在 **客户数据平台 > 用户管理 > 用户标签** 中点击 **新建用户标签** 进入用户标签创建弹窗

![](/img/用户标签-选择标签类型.png)

二、选择 **SQL标签** 并填写标签基本信息

| 项 | 是否必填 | 说明 | 限制条件 |
| -- | -- | -- | -- |
| 名称 | 是 |用户标签名称 | 名称唯一，不可重复<br/>最大输入30个字符 |
| 标识符 | 是 | 用户标签标识符<br/>可用于数据库和API查询 | 名称唯一，不可重复<br/>最大输入100个字符<br/>仅允许大小写英文、数字、以及下划线，并且不能以数字开头 |
| 描述 | 否 | 用户标签的业务意义描述 | 最大输入150个字符 |
| 所属分类 | 否 | 选择自定义的用户标签分类 | 如不选择则为未分类 |

![](/img/用户标签-基本信息.png)

三、点击 **下一步** 开始定义SQL规则

# 控件说明

| 项 | 是否必填 | 说明 | 限制条件 |
| -- | -- | -- | -- |
| 数值类型 | 是 | SQL标签输出结果数值类型 | 支持选择字符串、整数、小数、集合 |
| SQL规则 | 是 | SQL计算规则 | (见SQL校验规则) |

> 注：已保存的SQL标签支持在分析工具、群体画像等应用中作为维度过滤和维度拆解使用。为保证标签在应用中平稳使用，标签编辑时禁止修改标签的数值类型。

![](/img/用户标签-SQL标签.png)

# 校验规则

保存校验

* 库表校验：SQL标签仅支持使用 **event** 和 **user** 表，使用需要指定库名 **olap**

* 格式校验：SQL标签标准返回参数为 **gio_id** 和 **tag_value**

* 数值类型校验：SQL输出结果(tag_value)和所选数值类型应保持一致

存储校验

* 用户校验：SQL标签计算结果存储时会校验 **gio_id 合法性**，仅会保留系统已识别的gio_id

# 格式示例

```sql
select
    gio_id          as gio_id
    ,usr_gender     as tag_value
from olap.user
where usr_gender is not null
```

# 语法说明

SQL标签使用 [clickhouse SQL 语法](https://clickhouse.com/docs/zh/sql-reference/functions/)

# 应用场景

## 例1：过去7天订单支付金额总和

```sql
select
    gio_id 
    ,sum( var_payAmount_var ) as tag_value
from olap.event
where event_key = 'payOrderSuccess'
    and dateDiff( 'day' , dt , today () ) between 1 and 7
    and var_payAmount_var is not null
group by gio_id
```

## 例2：过去30天浏览次数Top 3的商品名称

```sql
--- 方法一(推荐) ---
select
    gio_id
    ,groupArray(3)(var_goodsName_var) as tag_value
from 
(
select
    gio_id 
    ,var_goodsName_var
    ,count(1) as pv
from olap.event
where event_key = 'goodsDetailPageView'
    and dateDiff( 'day' , dt , today () ) between 1 and 30
group by gio_id
    ,var_goodsName_var
order by gio_id
    ,count(1) desc 
    ,var_goodsName_var
)
group by gio_id

--- 方法二 ---
select
    gio_id
    ,groupUniqArray(var_goodsName_var) as tag_value
from 
(
select
    gio_id 
    ,var_goodsName_var
    ,count(1) as pv
    ,row_number() over ( partition by gio_id order by count(1) desc, var_goodsName_var ) as num
from olap.event
where event_key = 'goodsDetailPageView'
    and dateDiff( 'day' , dt , today () ) between 1 and 30
group by gio_id
    ,var_goodsName_var
)
where num <= 3
group by gio_id
```

## 例3：过去90天最后一次订单支付具体日期

```sql
--- 方法一(推荐) ---
select
    gio_id 
    ,argMax( dt , dt ) as tav_value
from olap.event
where event_key = 'payOrderSuccess'
    and dateDiff( 'day' , dt , today () ) between 1 and 90
group by gio_id

--- 方法二 ---
select
    gio_id
    ,groupArray(1)(dt)[1] as tag_value
from 
(
    select
        gio_id 
        ,dt
    from olap.event
    where event_key = 'payOrderSuccess'
    and dateDiff( 'day' , dt , today () ) between 1 and 90
    order by gio_id
        ,dt desc
)
group by gio_id
```

## 例4：过去90天最后一次订单支付距今天数

```sql
--- 方法一(推荐) ---
select
    gio_id 
    ,dateDiff( 'day' , argMax( dt , dt ) , today() )  as tav_value
from olap.event
where event_key = 'payOrderSuccess'
    and dateDiff( 'day' , dt , today () ) between 1 and 90
group by gio_id

--- 方法二 ---
select
    gio_id
    ,dateDiff( 'day' , groupArray(1)(dt)[1] , today() ) as tag_value
from 
(
    select
        gio_id 
        ,dt
    from olap.event
    where event_key = 'payOrderSuccess'
        and dateDiff( 'day' , dt , today () ) between 1 and 90
    order by gio_id
        ,dt desc
)
group by gio_id
```

# 常用语法

## 数值类型转化

### toString

```sql
select toString(123)
```

| toString(123) |
| -- | 
| 123 |

### toDate

```sql
select toDate('2021-12-31')
```

| toDate('2021-12-31') |
| -- | 
| 2021-12-31 |

### toFloat64

```sql
select toFloat64('3.1415926')
```

| toFloat64('3.1415926') |
| -- | 
| 3.1415926 |

## 日期函数

### dateDiff

```sql
select dateDiff( 'day' , toDate('2021-01-01') , toDate('2021-12-31') )
```

| dateDiff( 'day' , toDate('2021-01-01') , toDate('2021-12-31') |
| -- | 
| 364 |

## 聚合函数

### groupArray

* 多行转一行

```sql
select 
    gio_id
    ,groupArray(tag_value)
from 
(
    select 1 as gio_id, 'a' as tag_value
    union all 
    select 1 as gio_id, 'b' as tag_value
    union all 
    select 2 as gio_id, 'c' as tag_value
    union all 
    select 2 as gio_id, 'a' as tag_value
)
group by gio_id
```

| gio_id | groupArray(tag_value) |
| -- | -- |
| 1 | ['a','b'] |
| 2 | ['c','a'] |

* 多行转一行，每个用户取第一条

```sql
select 
    gio_id
    ,groupArray(tag_value)[1]
from 
(
    select 1 as gio_id, 'a' as tag_value
    union all 
    select 1 as gio_id, 'b' as tag_value
    union all 
    select 2 as gio_id, 'c' as tag_value
    union all 
    select 2 as gio_id, 'a' as tag_value
)
group by gio_id
```

| gio_id | groupArray(tag_value)[1] |
| -- | -- |
| 1 | a |
| 2 | c |