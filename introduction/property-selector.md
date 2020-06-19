---
description: 对属性进行过滤的操作
---

# 属性筛选

## 简介

我们可以通过一个或多个属性筛选条件来找到想要分析的目标用户或核心关注的事件行为。比如我们希望筛选今天过生日的用户并对这群用户发送生日慰问礼物；或者筛选订单支付金额大于10元的订单，统计有效支付订单数量。

在GrowingIO的分析功能中，我们当我们看到![](../.gitbook/assets/image%20%28193%29.png)全局过滤按钮和“属性为”选项时，点击该按钮或选择属性后可以对用户或事件添加过滤条件，具体操作流程如下：

![](../.gitbook/assets/image%20%28193%29.png)全局过滤按钮

step 1: 点击按钮后弹出全局过滤弹窗

step 2: 在1处选择事件或用户维度

step 3: 在2处选择计算规则

step 4: 在3处选择筛选维度值

step 5: 点击保存

![&#x5168;&#x5C40;&#x8FC7;&#x6EE4;&#x5F39;&#x7A97;](../.gitbook/assets/image%20%28192%29.png)

{% hint style="warning" %}
注意：

1. 如需添加多个过滤条件可点击“添加过滤条件”按钮
2. 最多支持添加5个过滤条件
3. 过滤结果会按"且"逻辑处理多个过滤条件，即同时满足每条过滤条件
{% endhint %}

属性为

step 1: 在1处选择事件或用户维度

step 2: 在2处选择计算规则

step 3: 在3处选择筛选维度值

![&#x5C5E;&#x6027;&#x4E3A;](../.gitbook/assets/image%20%28190%29.png)

## 筛选条件

### 字符串

![&#x5B57;&#x7B26;&#x4E32;&#x7B5B;&#x9009;&#x6761;&#x4EF6;](../.gitbook/assets/image%20%28198%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7B5B;&#x9009;&#x6761;&#x4EF6;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">= &#x7B49;&#x4E8E;</td>
      <td style="text-align:left">
        <p>&#x7CBE;&#x51C6;&#x5339;&#x914D;&#xFF0C;</p>
        <p>&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x5B8C;&#x5168;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">!= &#x4E0D;&#x7B49;&#x4E8E;</td>
      <td style="text-align:left">
        <p>&#x7CBE;&#x51C6;&#x5339;&#x914D;&#xFF0C;</p>
        <p>&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x4E0D;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">in &#x5728;...&#x8303;&#x56F4;&#x5185;</td>
      <td style="text-align:left">
        <p>&#x7CBE;&#x51C6;&#x5339;&#x914D;&#xFF0C;</p>
        <p>&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x5B8C;&#x5168;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x7684;&#x67D0;&#x4E2A;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">not in &#x4E0D;&#x5728;&#x8303;&#x56F4;&#x5185;</td>
      <td style="text-align:left">
        <p>&#x7CBE;&#x51C6;&#x5339;&#x914D;&#xFF0C;</p>
        <p>&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x4E0D;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x7684;&#x4EFB;&#x610F;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">like &#x5305;&#x542B;</td>
      <td style="text-align:left">
        <p>&#x6A21;&#x7CCA;&#x5339;&#x914D;&#xFF0C;</p>
        <p>&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x5B57;&#x6BB5;&#x5305;&#x542B;&#x8F93;&#x5165;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">not like &#x4E0D;&#x5305;&#x542B;</td>
      <td style="text-align:left">
        <p>&#x6A21;&#x7CCA;&#x5339;&#x914D;&#xFF0C;</p>
        <p>&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x5B57;&#x6BB5;&#x4E0D;&#x5305;&#x542B;&#x8F93;&#x5165;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6709;&#x503C;</td>
      <td style="text-align:left">
        <p>&#x5C5E;&#x6027;&#x503C;&#x4E0D;&#x4E3A;NULL&#x3001;&#x7A7A;&#x5B57;&#x7B26;&#x4E32;&#x6216;&#x4EFB;&#x610F;&#x4E2A;&#x7A7A;&#x683C;&#x65F6;</p>
        <p>&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6CA1;&#x503C;</td>
      <td style="text-align:left">
        <p>&#x5C5E;&#x6027;&#x503C;&#x4E3A;NULL&#x3001;&#x7A7A;&#x5B57;&#x7B26;&#x4E32;&#x6216;&#x4EFB;&#x610F;&#x4E2A;&#x7A7A;&#x683C;&#x65F6;</p>
        <p>&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
      </td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
注意：除没值外，其它筛选条件均默认在有值条件下进行筛选，即值不为NULL、空字符串或仅包含任意多个空字符
{% endhint %}

### 整数和小数

![&#x6574;&#x6570;&#x548C;&#x5C0F;&#x6570;&#x7B5B;&#x9009;&#x6761;&#x4EF6;](../.gitbook/assets/image%20%28196%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7B5B;&#x9009;&#x6761;&#x4EF6;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">= &#x7B49;&#x4E8E;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x6570;&#x503C;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x6570;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">!= &#x4E0D;&#x7B49;&#x4E8E;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x6570;&#x503C;&#x4E0D;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x6570;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">&lt; &#x5C0F;&#x4E8E;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x6570;&#x503C;&#x5C0F;&#x4E8E;&#x8F93;&#x5165;&#x6570;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">&lt;= &#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x6570;&#x503C;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x6570;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">&gt; &#x5927;&#x4E8E;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x6570;&#x503C;&#x5927;&#x4E8E;&#x8F93;&#x5165;&#x6570;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">&gt;= &#x5927;&#x4E8E;&#x7B49;&#x4E8E;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x6570;&#x503C;&#x5927;&#x4E8E;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x6570;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">between &#x533A;&#x95F4;</td>
      <td style="text-align:left">
        <p>&#x5C5E;&#x6027;&#x6570;&#x503C;&#x4ECB;&#x4E8E;&#x8F93;&#x5165;&#x6570;&#x503C;&#x533A;&#x95F4;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
        <p>&#x5982;&#x8F93;&#x5165;&#x503C;&#x4E3A;10&#x5230;100&#x65F6;&#xFF0C;&#x7EDF;&#x8BA1;&#x533A;&#x95F4;&#x4E3A;[10,100]
          (&#x5305;&#x542B;&#x8FB9;&#x754C;&#x503C;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6709;&#x503C;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x503C;&#x4E0D;&#x4E3A;NULL&#x65F6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6CA1;&#x503C;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x503C;&#x4E3A;NULL&#x65F6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
注意：除没值外，其它筛选条件均默认在有值条件下进行筛选，即值不为NULL
{% endhint %}

### 日期

![&#x65E5;&#x671F;&#x7B5B;&#x9009;&#x6761;&#x4EF6;](../.gitbook/assets/image%20%28199%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7B5B;&#x9009;&#x6761;&#x4EF6;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">= &#x7B49;&#x4E8E;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x65E5;&#x671F;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x65E5;&#x671F;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">!= &#x4E0D;&#x7B49;&#x4E8E;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x65E5;&#x671F;&#x4E0D;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x65E5;&#x671F;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">&lt; &#x5728;&#x67D0;&#x5929;&#x4E4B;&#x524D;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x65E5;&#x671F;&#x5C0F;&#x4E8E;&#x8F93;&#x5165;&#x65E5;&#x671F;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">&lt;= &#x5728;&#x67D0;&#x5929;&#x4E4B;&#x524D;(&#x5305;&#x542B;&#x5F53;&#x5929;)</td>
      <td
      style="text-align:left">&#x5C5E;&#x6027;&#x65E5;&#x671F;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x65E5;&#x671F;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">&gt; &#x5728;&#x67D0;&#x5929;&#x4E4B;&#x540E;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x65E5;&#x671F;&#x5927;&#x4E8E;&#x8F93;&#x5165;&#x65E5;&#x671F;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">&gt;= &#x5728;&#x67D0;&#x5929;&#x4E4B;&#x540E;(&#x5305;&#x542B;&#x5F53;&#x5929;)</td>
      <td
      style="text-align:left">&#x5C5E;&#x6027;&#x65E5;&#x671F;&#x5927;&#x4E8E;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x65E5;&#x671F;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">between &#x533A;&#x95F4;</td>
      <td style="text-align:left">
        <p>&#x5C5E;&#x6027;&#x65E5;&#x671F;&#x4ECB;&#x4E8E;&#x8F93;&#x5165;&#x65E5;&#x671F;&#x533A;&#x95F4;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
        <p>&#x5982;&#x8F93;&#x5165;&#x65E5;&#x671F;&#x4E3A;2020-05-01&#x548C;2020-05-05</p>
        <p>&#x7EDF;&#x8BA1;&#x533A;&#x95F4;&#x4E3A;2020-05-01(&#x5305;&#x542B;)&#x81F3;2020-05-05(&#x5305;&#x542B;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x76F8;&#x5BF9;&#x73B0;&#x5728;</td>
      <td style="text-align:left">(&#x89C1;&#x4E0B;&#x65B9;&#x8BF4;&#x660E;)</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x76F8;&#x5BF9;&#x533A;&#x95F4;</td>
      <td style="text-align:left">(&#x89C1;&#x4E0B;&#x65B9;&#x8BF4;&#x660E;)</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6709;&#x503C;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x503C;&#x4E0D;&#x4E3A;NULL&#x65F6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6CA1;&#x503C;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x503C;&#x4E3A;NULL&#x65F6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
注意：除没值外，其它筛选条件均默认在有值条件下进行筛选，即值不为NULL
{% endhint %}

**相对现在**

![&#x65E5;&#x671F;&#x7B5B;&#x9009;&#x6761;&#x4EF6; - &#x76F8;&#x5BF9;&#x73B0;&#x5728;](../.gitbook/assets/image%20%28191%29.png)

过去N天之前：表示当前日期 - N + 1 天\(不包含这天\)之前的所有日期

> 当前日期：2020年5月10日
>
> 筛选条件：过去5天之前
>
> 计算结果：2020年5月6日之前的所有日期，不包含2020年5月6日

过去N天之内：表示当前日期 - N + 1 天\(包含这天\)之内的所有日期

> 当前日期：2020年5月10日
>
> 筛选条件：过去5天之内
>
> 计算结果：2020年5月6日至2020年5月10日之间的所有日期，包含2020年5月6日和2020年5月10日

未来N天之内：表示当前日期 + N - 1 天\(包含这天\)之内的所有日期

> 当前日期：2020年5月10日
>
> 筛选条件：未来5天之内
>
> 计算结果：2020年5月10日至2020年5月14日之间的所有日期，包含2020年5月10日和2020年5月14日

未来N天之后：表示当前日期 + N - 1 天\(不包含这天\)之后的所有日期

> 当前日期：2020年5月10日
>
> 筛选条件：未来5天之后
>
> 计算结果：2020年5月14日之后的所有日期，不包含2020年5月14日





























相对现在在过去n天之前：表示无穷小时间点到当前日期减n天，即 \(无穷小时间 , 当前日期 - n\)

> 如现在时间是5月5日，过去2天之前即为5月3日\(包含\)之前

相对现在在过去n天之内：表示当前日期减n天到当前日期，即 \[当前日期 - n , 当前日期\]

> 如现在时间是5月5日，过去2天之内即为5月3日\(包含\)到5月5日\(包含\)之间

相对现在在未来n天之内：表示当前日期到当前日期加n天，即 \[当前日期 , 当前日期 + n\]

> 如现在时间是5月5日，未来2天之内即为5月5日\(包含\)到5月7日\(包含\)之间

相对现在在未来n天之后：表示当前日期加n天到无穷大时间，即 \[当前日期 + n , 无穷大时间\)

> 如相对时间是5月5日，未来2天之后即为5月7日\(包含\)之后

> 注：输入值为正整数 1,2,3,4 ...

**相对区间**

![&#x76F8;&#x5BF9;&#x533A;&#x95F4;](../.gitbook/assets/image%20%2814%29.png)

相对区间在过去m天至过去n天之内：表示当前日期减m天到当前日期减n天之间，即 \[当前日期 - m , 当前日期 - n\]

> 如现在时间是5月5日，过去3天至过去1天之内即为5月2日\(包含\)至5月4日\(包含\)之间

相对区间在未来m天至未来n天之内：表示当前日期加m天到当前日期加n天之间，即 \[当前日期 + m , 当前日期 + n\]

> 如现在时间是5月5日，未来2天至未来4天之内即为5月7日\(包含\)至5月9日\(包含\)之间

> 注：输入值为正整数 1,2,3,4 ...

## 使用案例

### 1. 会员到期用户运营

业务目标：会员续费率提升

目标人群：高活跃会员 且 会员即将到期

运营策略：支付订单后弹窗提醒会员续费（无优惠）

筛选方法：

1）相对时间，过去30天内活跃天数大于等于4

> 平均一周访问一次

2）相对时间，过去30天内订单支付数大于等于2

> 高活跃用户

3）相对区间，会员到期日在未来7天到14天之内

> 会员即将到期

