# SQL标签

## 简介

GrowingIO支持通过SQL自定义用户标签，如需了解基础数据模型请点击链接“[数据模型](https://docs.growingio.com/op/introduction/data-model/)”进行查看。

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
// 过去7天订单支付次数
select 
    user_id         as userId
    ,count(1)       as tagValue
from carbon.event
where time between daysAgo(7) and daysAgo(1)
    and event_key = 'payOrderSuccess'
group by 1
```

### 动态时间范围

如果您的数据计算时间范围是动态变化的，如“过去7天订单支付次数“，每天计算标签时都会根据当天\(计算时间\)





标签的每次计算都存在一个计算的“基准时间”。

若您的数据范围是动态变化的，例如：每天标签更新时，都会使用相对时间是“昨日”的数据进行计算；这时就需要使用动态时间来表示数据的时间范围。

示例：

```text
/* 需修改语句中的 event 为自己的业务字段 */

SELECT DISTINCT user_id AS id, distinct_id AS distinct_id, '1' AS value
FROM events
WHERE date BETWEEN '[baseTime]' AND '[baseTime]'
    AND event = 'login'

/* 假设当前日期为 2019-06-20，那么标签规则的基准时间为 2019-06-19，于是 [baseTime] 代表昨日 2019-06-19， */
/* 每次标签数据更新时，都会使用相对时间是昨日的数据进行计算 */
```

CopyCODE

注意：SQL 创建标签时，暂时不支持使用当前日期作为 baseTime。

'\[baseTime\]' 实际上表示的为“昨日”

'\[baseTime\]' - INTERVAL '6' DAY 表示为“过去第 7 天”  
  






