---
id: application
sidebar_position: 5
---

# 应用场景








基础指标值：过去30天活跃天数​



项	说明
1.选择时间	过去30天
2.选择事件	活跃
3.选择属性	天数
4.选择计算模型	累计值
5.选择事件过滤	​
基础指标值：过去90天平均订单支付金额​



项	说明
1.选择时间	过去90天
2.选择事件	订单支付成功
3.选择属性	实际购买金额
4.选择计算模型	平均值
5.选择事件过滤	​
基础指标值：过去7天男装商品浏览次数占总商品浏览次数占比​



项	说明
1.选择时间	过去7天
2.选择事件	浏览商品详情页
3.选择属性	次数
4.选择计算模型	占比
5.占比属性	一级分类 等于 男装
最大值/最小值的事件属性：过去30天浏览次数最多的商品一级分类​



项	说明
1.选择时间	过去30天
2.选择事件	浏览商品详情页
3.选择分组属性	次数
4.选择计算模型	最多
5.选择打标属性	一级分类
6.选择事件过滤	​
首次/末次的事件属性：过去90天末次(最后一次)订单购买距今日期​



项	说明
1.选择时间	过去90天
2.选择计算模型	末次发生
3.选择事件	订单支付成功
4.选择属性	距今天数
5.选择事件过滤	​
列表类的事件属性：过去30天全部浏览的商品名称​



项	说明
1.选择时间	过去30天
2.选择事件	浏览商品详情页
3.选择属性	商品名称
4.选择事件过滤	​
分层标签：用户活跃度​

高活跃用户：过去30天累计交易金额大于1千元且活跃天数大于4天‌



中活跃用户：过去30天累计交易金额大于300元或活跃天数大于2天‌



低活跃用户：过去30天有活跃的用户



SQL标签：过去7天订单支付金额总和​

-- 埋点事件: 订单支付事件  payOrderSuccess

-- 事件属性：实际支付金额  payAmount_var

select

 gio_id 

 ,sum( var\_payAmount\_var ) as tag_value

from olap.event

where event_key = 'payOrderSuccess'

 and dateDiff( 'day' , dt , today () ) between 1 and 7

group by gio_id
Copy
SQL标签：过去30天浏览次数Top 3的商品名称​


-- 埋点事件：商品浏览事件   goodsDetailPageView

-- 事件属性：商品名称      var\_goodsName\_var

​

--- 方法一(推荐) ---

select

 gio_id

 ,groupArray(3)(var\_goodsName\_var) as tag_value

from 

(

select

 gio_id 

 ,var\_goodsName\_var

 ,count(1) as pv

from olap.event

where event_key = 'goodsDetailPageView'

 and dateDiff( 'day' , dt , today () ) between 1 and 30

group by gio_id

 ,var\_goodsName\_var

order by gio_id

 ,count(1) desc 

 ,var\_goodsName\_var

)

group by gio_id

​

--- 方法二 ---

 gio_id

 ,groupUniqArray(var\_goodsName\_var) as tag_value

from 

(

select

 gio_id 

 ,var\_goodsName\_var

 ,count(1) as pv

 ,row\_number() over ( partition by gio\_id order by count(1) desc, var\_goodsName\_var ) as num

from olap.event

where event_key = 'goodsDetailPageView'

 and dateDiff( 'day' , dt , today () ) between 1 and 30

group by gio_id

 ,var\_goodsName\_var

)

where num <= 3

group by gio_id
Copy
SQL标签：过去90天最后一次订单支付具体日期​


-- 埋点事件: 订单支付事件  payOrderSuccess

​

--- 方法一(推荐) ---

select

 gio_id 

 ,argMax( dt , dt ) as tav_value

from olap.event

where event_key = 'payOrderSuccess'

 and dateDiff( 'day' , dt , today () ) between 1 and 90

group by gio_id

​

--- 方法二 ---

select

 gio_id

 ,groupArray(1)(dt)\[1\] as tag_value

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
Copy
SQL标签：过去90天最后一次订单支付距今天数​

-- 埋点事件: 订单支付事件  payOrderSuccess

​

--- 方法一(推荐) ---

select

 gio_id 

 ,dateDiff( 'day' , argMax( dt , dt ) , today() )  as tav_value

from olap.event

where event_key = 'payOrderSuccess'

 and dateDiff( 'day' , dt , today () ) between 1 and 90

group by gio_id

​

--- 方法二 ---

select

 gio_id

 ,dateDiff( 'day' , groupArray(1)(dt)\[1\] , today() ) as tag_value

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