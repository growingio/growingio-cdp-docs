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
| 事件选择器 | 选择打标事件 | 无 |
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


## 最大值/最小值的事件属性[](#zui-da-zhi-zui-xiao-zhi-de-shi-jian-shu-xing)


## 首次/末次的事件属性[](#shou-ci-mo-ci-de-shi-jian-shu-xing)


## 列表类的事件属性[](#lie-biao-lei-de-shi-jian-shu-xing)


## 分层标签[](#fen-ceng-biao-qian)







控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaWT8g4phN_UqWQQthL%2F-MaX7r5FZlB_gIjpWI8V%2Fimage.png?alt=media&token=e75280d8-3ff0-4ff6-aa7a-86cac573c9d9)

| 项   | 说明  |
| --- | --- |
| 1.选择时间 | 如过去7天、过去30天、过去90天等 |
| 2.选择事件 | 如全局指标(访问、活跃)、埋点事件和计算指标 |
| 3.选择属性 | 如次数、天数、埋点事件的整数、小数、字符串类型事件属性 |
| 4.选择计算模型 | 如累计值、平均值、占比、去重数 |
| 5.选择事件过滤 | 选择事件过滤条件 |

由于属性的数值类型不同，支持的计算模型对应关系如下：

| 属性  | 累计值 | 平均值 | 占比  | 去重数 |
| --- | --- | --- | --- | --- |
| 次数  | ✔️  | ​   | ✔️  | ​   |
| 天数  | ✔️  | ​   | ​   | ​   |
| 整数、小数类型事件属性 | ✔️  | ✔️  | ✔️  | ​   |
| 字符串类型事件属性 | ​   | ​   | ​   | ✔️  |


#### 最大值/最小值的事件属性[](#zui-da-zhi-zui-xiao-zhi-de-shi-jian-shu-xing-1)

控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaX8gmlITGn2zTUPjta%2F-MaX955wpjSxFGygI76a%2Fimage.png?alt=media&token=8fbc6d27-1014-4ca2-8649-3cd9daeaa64e)

| 项   | 说明  |
| --- | --- |
| 1.选择时间 | 如过去7天、过去30天、过去90天等 |
| 2.选择事件 | 如全局指标(访问、活跃)和埋点事件 |
| 3.选择分组属性 | 如次数和埋点事件的整数、小数类型事件属性 |
| 4.选择计算模型 | 如最多、最少 |
| 5.选择打标属性 | 如埋点事件的字符串类型事件属性 |
| 6.选择事件过滤 | 选择事件过滤条件 |


#### 首次/末次的事件属性[](#shou-ci-mo-ci-de-shi-jian-shu-xing-1)

控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaX9FEkMV4TtU-ccU95%2F-MaX9iiMNQsxpX2ETO5e%2Fimage.png?alt=media&token=291e868d-4faa-4109-b910-f6711c2a890c)

| 项   | 说明  |
| --- | --- |
| 1.选择时间 | 如过去7天、过去30天、过去90天等 |
| 2.选择计算模型 | 如最初、最终 |
| 3.选择事件 | 如全局指标(访问、活跃)和埋点事件 |
| 4.选择属性 | 如距今天数、日期和埋点事件的字符串类型事件属性 |
| 5.选择事件过滤 | 选择事件过滤条件 |


#### 列表类的事件属性[](#lie-biao-lei-de-shi-jian-shu-xing-1)

控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaXAPPPHyRVJTXO1Z3e%2F-MaXAllgogkiDLxjhel7%2Fimage.png?alt=media&token=55832063-b163-4e10-9543-6a4bce4ac464)

| 项   | 说明  |
| --- | --- |
| 1.选择时间 | 如过去7天、过去30天、过去90天等 |
| 2.选择事件 | 如全局指标(访问、活跃)和埋点事件 |
| 3.选择属性 | 如埋点事件的字符串类型事件属性 |
| 4.选择事件过滤 | 选择事件过滤条件 |


#### 分层标签[](#fen-ceng-biao-qian-1)

控件说明:
* 用户行为
    * 做过
    * 未做过
* 用户属性
    * 用户是


![图 1](/img/9a3fa2b94ae53b6f3c33f6ae3090d485e8e318b2ec6fc83369305adf19bdb903_pic_1639999256652_2021-12-20.png)  


**SQL标签**

控件说明：‌

* 支持选择数值类型
    
* 支持写入SQL规则
    
![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiQNGh3wdzlC8uur13S%2F-MiQObm0w2zbwDsZsT_e%2Fimage.png?alt=media&token=37910440-3c54-4a19-b1a8-192d882e4eb5)