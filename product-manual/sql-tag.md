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







