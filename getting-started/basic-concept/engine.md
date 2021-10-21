---
id: engine
sidebar_position: 5
---

# 计算引擎

## 简介[](#jian-jie)

GrowingIO使用Clickhouse开源软件作为数据存储和分析计算的核心引擎，结合自研的高性能算法，获得超高效率的应用支撑。

在数据校验、问题排查、二次开发等诸多场景中，您将会编写SQL语句直接在Clickhouse中运行。虽然Clickhouse提供了非常丰富的函数集，不过对于习惯Hive等语法的开发者或分析师来说，了解Clickhouse中标准语法和常用函数，对于快速上手是大有裨益的。

> 本文档仅提供Clickhouse引擎部分常用函数，更多资料请参阅Clickhouse官网。

## 功能说明[](#gong-neng-shuo-ming)

展示了Clickhouse常用函数

### 字符串函数[](#zi-fu-chuan-han-shu)

| 函数  | 用途  | 举例  | 结果  |
| --- | --- | --- | --- |
| length(str) | 返回字符串的长度 | length('abc') | 返回3 |
| concat(s1,s2....) | 将字符串拼接 | concat('ab','c') | 返回abc |
| lower(str) | 将字符串转为小写 | lower('ABc') | 返回abc |
| upper(str) | 将字符串转为大写 | upper('abC') | 返回ABC |
| substring(str, offset, length) | 字符串截取 | substring('abc', 1, 2) | 返回ab |
| like(str,patten) | 模糊匹配 | like('abc','%a%')<br></br>like('abc','%z%') | 返回1<br></br>返回0 |
| replace(str,patten<br></br>,replacement) | 字符串替换 | replace('abc','a','z') | 返回zbc |

### 数学函数[](#shu-xue-han-shu)

| 函数  | 用途  | 举例  | 结果  |
| --- | --- | --- | --- |
| pow(x, y) | 返回x的y次方 | pow(2, 3) | 返回8 |
| sqrt(x) | 对x开平方 | sqrt(4) | 返回2 |
| cbrt(x) | 对x开立方 | cbrt(8) | 返回2 |

### 舍入函数[](#she-ru-han-shu)

| 函数  | 用途  | 举例  | 结果  |
| --- | --- | --- | --- |
| round(x\[, N\]) | 四舍五入 | round(12.67, 1) | 返回12.7 |
| floor(x\[, N\]) | 向下取数 | floor(12.67,1) | 返回12.6 |
| ceil(x\[, N\]) | 向上取数 | ceil(12.67,1) | 返回12.7 |

### 日期函数[](#ri-qi-han-shu)

| 函数  | 用途  | 举例  | 结果  |
| --- | --- | --- | --- |
| now() | 当前时间 | now() | 返回2021-06-01 00:00:00 |
| today() | 今日日期 | today() | 返回2021-06-01 |
| yesterday() | 昨日日期 | yesterday() | 返回2021-05-31 |
| formatDateTime(Time<br></br>, Format\[, Timezone\]) | 时间格式化 | formatDateTime(now(),'%Y-%m-%d') | 返回2021-06-01 |
| dateDiff(t1,t2,unit) | 计算两个时间差值 | dateDiff('day',yesterday(),today())<br></br>dateDiff('hour',yesterday(),today())<br></br>dateDiff('minute',yesterday(),today())<br></br>dateDiff('second',yesterday(),today()) | 返回1<br></br>返回24<br></br>返回1440<br></br>返回86400 |
| addDays(t,n) | 增加日期 | addDays(today(),1) | 返回2021-06-02 |

#### formatDateTime 常用修饰符

| 修饰符 | 描述  | 示例  |
| --- | --- | --- |
| %Y  | 年   | 2021 |
| %m  | 月份（01-12) | 06  |
| %d  | 月中的一天（01-31) | 01  |
| %H  | 24小时格式（00-23) | 00  |
| %M  | 分钟(00-59) | 00  |
| %S  | 秒 (00-59) | 00  |

​​

### 聚合函数[](#ju-he-han-shu)

| 函数  | 用途  |
| --- | --- |
| count | 计数  |
| sum | 求和  |
| avg | 求平均 |
| min | 求最小值 |
| max | 求最大值 |

### 类型转换函数[](#lei-xing-zhuan-huan-han-shu)

| 函数  | 用途  | 举例  | 结果  |
| --- | --- | --- | --- |
| toString | 将数值型、字符型、日期等<br></br>转化为字符型 | toString(today()) | 返回2021-06-01 |
| toDate | 将字符型转化为日期 | toDate('2021-06-01') | 返回2021-06-01 |
| toInt64 | 将字符型转化为整型 | toInt64('12') | 返回12 |

### 其他函数[](#qi-ta-han-shu)

| 函数  | 用途  | 举例  | 结果  |
| --- | --- | --- | --- |
| if(cond,then,else) | 条件输出 | if(1 > 2,'OK','NO') | 返回NO |
