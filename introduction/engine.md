---
description: 14.0版本起，引入Clickhouse开源软件作为存储计算的核心引擎，结合自研高性能算法，进一步提升查询效率。
---

# 计算引擎

> 本文档仅提供Clickhouse引擎部分常用函数便于数据排查之用，更多函数请参阅Clickhouse官网。

## 常用函数

### 字符串函数

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x51FD;&#x6570;</th>
      <th style="text-align:left">&#x7528;&#x9014;</th>
      <th style="text-align:left">&#x4E3E;&#x4F8B;</th>
      <th style="text-align:left">&#x7ED3;&#x679C;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">length(str)</td>
      <td style="text-align:left">&#x8FD4;&#x56DE;&#x5B57;&#x7B26;&#x4E32;&#x7684;&#x957F;&#x5EA6;</td>
      <td
      style="text-align:left">length(&apos;abc&apos;)</td>
        <td style="text-align:left">&#x8FD4;&#x56DE;3</td>
    </tr>
    <tr>
      <td style="text-align:left">concat(s1,s2....)</td>
      <td style="text-align:left">&#x5C06;&#x5B57;&#x7B26;&#x4E32;&#x62FC;&#x63A5;</td>
      <td style="text-align:left">concat(&apos;ab&apos;,&apos;c&apos;)</td>
      <td style="text-align:left">&#x8FD4;&#x56DE;abc</td>
    </tr>
    <tr>
      <td style="text-align:left">lower(str)</td>
      <td style="text-align:left">&#x5C06;&#x5B57;&#x7B26;&#x4E32;&#x8F6C;&#x4E3A;&#x5C0F;&#x5199;</td>
      <td
      style="text-align:left">lower(&apos;ABc&apos;)</td>
        <td style="text-align:left">&#x8FD4;&#x56DE;abc</td>
    </tr>
    <tr>
      <td style="text-align:left">upper(str)</td>
      <td style="text-align:left">&#x5C06;&#x5B57;&#x7B26;&#x4E32;&#x8F6C;&#x4E3A;&#x5927;&#x5199;</td>
      <td
      style="text-align:left">upper(&apos;abC&apos;)</td>
        <td style="text-align:left">&#x8FD4;&#x56DE;ABC</td>
    </tr>
    <tr>
      <td style="text-align:left">substring(str, offset, length)</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;&#x622A;&#x53D6;</td>
      <td style="text-align:left">substring(&apos;abc&apos;, 1, 2)</td>
      <td style="text-align:left">&#x8FD4;&#x56DE;ab</td>
    </tr>
    <tr>
      <td style="text-align:left">like(str,patten)</td>
      <td style="text-align:left">&#x6A21;&#x7CCA;&#x5339;&#x914D;</td>
      <td style="text-align:left">
        <p>like(&apos;abc&apos;,&apos;%a%&apos;)</p>
        <p>like(&apos;abc&apos;,&apos;%z%&apos;)</p>
      </td>
      <td style="text-align:left">
        <p>&#x8FD4;&#x56DE;1</p>
        <p>&#x8FD4;&#x56DE;0</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>replace(str,patten</p>
        <p>,replacement)</p>
      </td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;&#x66FF;&#x6362;</td>
      <td style="text-align:left">replace(&apos;abc&apos;,&apos;a&apos;,&apos;z&apos;)</td>
      <td style="text-align:left">&#x8FD4;&#x56DE;zbc</td>
    </tr>
  </tbody>
</table>

### 数学函数

| 函数 | 用途 | 举例 | 结果 |
| :--- | :--- | :--- | :--- |
| pow\(x, y\) | 返回x的y次方 | pow\(2, 3\) | 返回8 |
| sqrt\(x\) | 对x开平方 | sqrt\(4\) | 返回2 |
| cbrt\(x\) | 对x开立方 | cbrt\(8\) | 返回2 |

### 舍入函数

| 函数 | 用途 | 举例 | 结果 |
| :--- | :--- | :--- | :--- |
| round\(x\[, N\]\) | 四舍五入 | round\(12.67, 1\) | 返回12.7 |
| floor\(x\[, N\]\) | 向下取数 | floor\(12.67,1\) | 返回12.6 |
| ceil\(x\[, N\]\) | 向上取数 | ceil\(12.67,1\) | 返回12.7 |

### 日期函数

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x51FD;&#x6570;</th>
      <th style="text-align:left">&#x7528;&#x9014;</th>
      <th style="text-align:left">&#x4E3E;&#x4F8B;</th>
      <th style="text-align:left">&#x7ED3;&#x679C;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">now()</td>
      <td style="text-align:left">&#x5F53;&#x524D;&#x65F6;&#x95F4;</td>
      <td style="text-align:left">now()</td>
      <td style="text-align:left">&#x8FD4;&#x56DE;2021-06-01 00:00:00</td>
    </tr>
    <tr>
      <td style="text-align:left">today()</td>
      <td style="text-align:left">&#x4ECA;&#x65E5;&#x65E5;&#x671F;</td>
      <td style="text-align:left">today()</td>
      <td style="text-align:left">&#x8FD4;&#x56DE;2021-06-01</td>
    </tr>
    <tr>
      <td style="text-align:left">yesterday()</td>
      <td style="text-align:left">&#x6628;&#x65E5;&#x65E5;&#x671F;</td>
      <td style="text-align:left">yesterday()</td>
      <td style="text-align:left">&#x8FD4;&#x56DE;2021-05-31</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>formatDateTime(Time</p>
        <p>, Format[, Timezone])</p>
      </td>
      <td style="text-align:left">&#x65F6;&#x95F4;&#x683C;&#x5F0F;&#x5316;</td>
      <td style="text-align:left">formatDateTime(now(),&apos;%Y-%m-%d&apos;)</td>
      <td style="text-align:left">&#x8FD4;&#x56DE;2021-06-01</td>
    </tr>
    <tr>
      <td style="text-align:left">dateDiff(t1,t2,unit)</td>
      <td style="text-align:left">&#x8BA1;&#x7B97;&#x4E24;&#x4E2A;&#x65F6;&#x95F4;&#x5DEE;&#x503C;</td>
      <td
      style="text-align:left">
        <p>dateDiff(&apos;day&apos;,yesterday(),today())</p>
        <p>dateDiff(&apos;hour&apos;,yesterday(),today())</p>
        <p>dateDiff(&apos;minute&apos;,yesterday(),today())</p>
        <p>dateDiff(&apos;second&apos;,yesterday(),today())</p>
        </td>
        <td style="text-align:left">
          <p>&#x8FD4;&#x56DE;1</p>
          <p>&#x8FD4;&#x56DE;24</p>
          <p>&#x8FD4;&#x56DE;1440</p>
          <p>&#x8FD4;&#x56DE;86400</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">addDays(t,n)</td>
      <td style="text-align:left">&#x589E;&#x52A0;&#x65E5;&#x671F;</td>
      <td style="text-align:left">addDays(today(),1)</td>
      <td style="text-align:left">&#x8FD4;&#x56DE;2021-06-02</td>
    </tr>
  </tbody>
</table>

​

**formatDateTime常用修饰符**

| 修饰符 | 描述 | 示例 |
| :--- | :--- | :--- |
| %Y | 年 | 2021 |
| %m | 月份（01-12\) | 06 |
| %d | 月中的一天（01-31\) | 01 |
| %H | 24小时格式（00-23\) | 00 |
| %M | 分钟\(00-59\) | 00 |
| %S | 秒 \(00-59\) | 00 |

​​

### 聚合函数

| 函数 | 用途 |
| :--- | :--- |
| count | 计数 |
| sum | 求和 |
| avg | 求平均 |
| min | 求最小值 |
| max | 求最大值 |



### 类型转换函数

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x51FD;&#x6570;</th>
      <th style="text-align:left">&#x7528;&#x9014;</th>
      <th style="text-align:left">&#x4E3E;&#x4F8B;</th>
      <th style="text-align:left">&#x7ED3;&#x679C;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">toString</td>
      <td style="text-align:left">
        <p>&#x5C06;&#x6570;&#x503C;&#x578B;&#x3001;&#x5B57;&#x7B26;&#x578B;&#x3001;&#x65E5;&#x671F;&#x7B49;</p>
        <p>&#x8F6C;&#x5316;&#x4E3A;&#x5B57;&#x7B26;&#x578B;</p>
      </td>
      <td style="text-align:left">toString(today())</td>
      <td style="text-align:left">&#x8FD4;&#x56DE;2021-06-01</td>
    </tr>
    <tr>
      <td style="text-align:left">toDate</td>
      <td style="text-align:left">&#x5C06;&#x5B57;&#x7B26;&#x578B;&#x8F6C;&#x5316;&#x4E3A;&#x65E5;&#x671F;</td>
      <td
      style="text-align:left">toDate(&apos;2021-06-01&apos;)</td>
        <td style="text-align:left">&#x8FD4;&#x56DE;2021-06-01</td>
    </tr>
    <tr>
      <td style="text-align:left">toInt64</td>
      <td style="text-align:left">&#x5C06;&#x5B57;&#x7B26;&#x578B;&#x8F6C;&#x5316;&#x4E3A;&#x6574;&#x578B;</td>
      <td
      style="text-align:left">toInt64(&apos;12&apos;)</td>
        <td style="text-align:left">&#x8FD4;&#x56DE;12</td>
    </tr>
  </tbody>
</table>

### 其他函数

| 函数 | 用途 | 举例 | 结果 |
| :--- | :--- | :--- | :--- |
| if\(cond,then,else\) | 条件输出 | if\(1 &gt; 2,'OK','NO'\) | 返回NO |



