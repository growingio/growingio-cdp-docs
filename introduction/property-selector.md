---
description: 对属性进行过滤的操作
---

# 属性筛选

## 简介

我们可以通过一个或多个属性筛选条件来找到想要分析的目标用户或核心关注的事件行为。比如我们希望筛选今天过生日的用户并对这群用户发送生日慰问礼物；或者筛选订单支付金额大于10元的订单，统计有效支付订单数量。

在GrowingIO的分析功能中，我们当我们看到![](../.gitbook/assets/image%20%28192%29.png)全局过滤按钮和“属性为”选项时，点击该按钮或选择属性后可以对用户或事件添加过滤条件，具体操作流程如下：

![](../.gitbook/assets/image%20%28192%29.png)全局过滤按钮

step 1: 点击按钮后弹出全局过滤弹窗

step 2: 在1处选择事件或用户维度

step 3: 在2处选择计算规则

step 4: 在3处选择筛选维度值

step 5: 点击保存

![&#x5168;&#x5C40;&#x8FC7;&#x6EE4;&#x5F39;&#x7A97;](../.gitbook/assets/image%20%28191%29.png)

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

## 筛选对象







## 筛选条件















## 筛选条件分类[![](https://manual.sensorsdata.cn/sa/_/7F000001017254FC8E5DF485619F34A0/1591948739794/images/common/link-solid.svg)](https://manual.sensorsdata.cn/sa/latest/guide_terms_attribute-7547310.html#id-.%E5%B1%9E%E6%80%A7%E7%AD%9B%E9%80%89%E6%9D%A1%E4%BB%B6%E8%AF%B4%E6%98%8Ev1.17-%E7%AD%9B%E9%80%89%E6%9D%A1%E4%BB%B6%E5%88%86%E7%B1%BB) <a id="id-.&#x5C5E;&#x6027;&#x7B5B;&#x9009;&#x6761;&#x4EF6;&#x8BF4;&#x660E;v1.17-&#x7B5B;&#x9009;&#x6761;&#x4EF6;&#x5206;&#x7C7B;"></a>

### 按目标[![](https://manual.sensorsdata.cn/sa/_/7F000001017254FC8E5DF485619F34A0/1591948739794/images/common/link-solid.svg)](https://manual.sensorsdata.cn/sa/latest/guide_terms_attribute-7547310.html#id-.%E5%B1%9E%E6%80%A7%E7%AD%9B%E9%80%89%E6%9D%A1%E4%BB%B6%E8%AF%B4%E6%98%8Ev1.17-%E6%8C%89%E7%9B%AE%E6%A0%87) <a id="id-.&#x5C5E;&#x6027;&#x7B5B;&#x9009;&#x6761;&#x4EF6;&#x8BF4;&#x660E;v1.17-&#x6309;&#x76EE;&#x6807;"></a>

筛选用户：筛选条件作用于用户表，只看符合筛选条件的那些用户；一般在用户属性上进行条件设置，或者选择用户分群获取符合分析条件的用户。

筛选事件：筛选条件作用于事件，只看符合筛选条件的事件；一般在事件属性上进行条件设置。  
  










## 筛选条件

筛选条件是指在GrowingIO中能对以上属性类型进行的筛选操作。

> for example:
>
> 用户属性中创建一个整数属性 - 年龄，我们希望在分群中筛选年龄小于18岁的用户分群
>
> 筛选条件即为选择用户属性中年龄小于18的用户

### 字符串

![&#x5B57;&#x7B26;&#x4E32;&#x5C5E;&#x6027;](../.gitbook/assets/image%20%2821%29.png)

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
      <td style="text-align:left">&#x7CBE;&#x51C6;&#x5339;&#x914D;&#xFF0C;&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x5B8C;&#x5168;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">!= &#x4E0D;&#x7B49;&#x4E8E;</td>
      <td style="text-align:left">&#x7CBE;&#x51C6;&#x5339;&#x914D;&#xFF0C;&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x4E0D;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">in &#x5728;...&#x8303;&#x56F4;&#x5185;</td>
      <td style="text-align:left">
        <p>&#x7CBE;&#x51C6;&#x5339;&#x914D;&#xFF0C;&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x5B8C;&#x5168;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x7684;&#x67D0;&#x4E2A;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
        <p>&#x5982;(&#x5C5E;&#x6027;)&#x516C;&#x53F8;&#x7C7B;&#x578B;&quot;toB&quot;
          in [&quot;toC&quot;,&quot;toB&quot;]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">not in &#x4E0D;&#x5728;&#x8303;&#x56F4;&#x5185;</td>
      <td style="text-align:left">&#x7CBE;&#x51C6;&#x5339;&#x914D;&#xFF0C;&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x4E0D;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x7684;&#x4EFB;&#x610F;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">like &#x5305;&#x542B;</td>
      <td style="text-align:left">
        <p>&#x6A21;&#x7CCA;&#x5339;&#x914D;&#xFF0C;&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x5B57;&#x6BB5;&#x5305;&#x542B;&#x8F93;&#x5165;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
        <p>&#x5982;(&#x5C5E;&#x6027;)&#x516C;&#x53F8;&#x540D;&#x79F0;&#x201C;GrowingIO&quot;&#x4E2D;&#x5305;&#x542B;&#x5B57;&#x7B26;&#x4E32;&#x201D;Growing&quot;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">not like &#x4E0D;&#x5305;&#x542B;</td>
      <td style="text-align:left">
        <p>&#x6A21;&#x7CCA;&#x5339;&#x914D;&#xFF0C;&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x5B57;&#x6BB5;&#x4E0D;&#x5305;&#x542B;&#x8F93;&#x5165;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</p>
        <p>&#x5982;(&#x5C5E;&#x6027;)&#x516C;&#x53F8;&#x540D;&#x79F0;&#x201C;GrowingIO&quot;&#x4E2D;&#x4E0D;&#x5305;&#x542B;&#x5B57;&#x7B26;&#x4E32;&#x201C;Growth&quot;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6709;&#x503C;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x503C;&#x4E0D;&#x4E3A;NULL&#x3001;&#x7A7A;&#x5B57;&#x7B26;&#x4E32;(&apos;&apos;)
        &#x6216; &#x4EFB;&#x610F;&#x4E2A;&#x7A7A;&#x683C;(&apos; &apos;)&#x65F6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6CA1;&#x503C;</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x503C;&#x4E3A;NULL&#x3001;&#x7A7A;&#x5B57;&#x7B26;&#x4E32;(&apos;&apos;)
        &#x6216; &#x4EFB;&#x610F;&#x4E2A;&#x7A7A;&#x683C;(&apos; &apos;)&#x65F6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
    </tr>
  </tbody>
</table>

> 除没值外，其他筛选条件默认在有值条件下筛选

### 整数、小数

![&#x6574;&#x6570;&#x3001;&#x5C0F;&#x6570;&#x5C5E;&#x6027;](../.gitbook/assets/image%20%28138%29.png)

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

> 除没值外，其他筛选条件默认在有值条件下筛选

### 日期

![&#x65E5;&#x671F;&#x5C5E;&#x6027;](../.gitbook/assets/image%20%2846%29.png)

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

> 除没值外，其他筛选条件默认在有值条件下筛选

**相对现在**

![&#x76F8;&#x5BF9;&#x73B0;&#x5728;](../.gitbook/assets/image%20%28135%29.png)

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

