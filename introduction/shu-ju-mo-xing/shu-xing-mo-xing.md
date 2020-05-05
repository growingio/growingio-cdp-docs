# 属性模型

## 简介

在GrowingIO的属性模型中，根据不同使用场景的需要，我们支持四种属性类型，分别为字符串、整数、小数和日期。目前用户属性、事件属性和物品属性分别支持以下几种属性类型：

|  | 字符串 | 整数 | 小数 | 日期 |
| :--- | :--- | :--- | :--- | :--- |
| 用户属性 | ✔️ | ✔️ |  | ✔️ |
| 事件属性 | ✔️ | ✔️ | ✔️ |  |
| 物品属性 | ✔️ |  |  |  |

> 事件属性仅支持非负整数和非负小数类型

## 数据格式

属性的类型由创建属性时选择的类型决定，创建后属性类型不可更改。四种属性对应导入数值格式如下：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5C5E;&#x6027;&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x683C;&#x5F0F;&#x9650;&#x5236;</th>
      <th style="text-align:left">&#x793A;&#x4F8B;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x975E;&#x7A7A;&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x2018;GrowingIO&#x2019;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6574;&#x6570;</td>
      <td style="text-align:left">&#x4EE5;&#x5B57;&#x7B26;&#x683C;&#x5F0F;&#x4F20;&#x5165;</td>
      <td style="text-align:left">&#x2018;1234567&#x2019;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5C0F;&#x6570;</td>
      <td style="text-align:left">
        <p>&#x4EE5;&#x5B57;&#x7B26;&#x683C;&#x5F0F;&#x4F20;&#x5165;&#xFF0C;</p>
        <p>&#x56DB;&#x820D;&#x4E94;&#x5165;&#x540E;&#x5C0F;&#x6570;&#x70B9;&#x540E;&#x6700;&#x591A;&#x4FDD;&#x7559;4&#x4F4D;</p>
      </td>
      <td style="text-align:left">&apos;3.1416&apos;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x65E5;&#x671F;</td>
      <td style="text-align:left">
        <p>&#x4EE5;&#x5B57;&#x7B26;&#x683C;&#x5F0F;&#x4F20;&#x5165;&#xFF0C;</p>
        <p>yyyy-mm-dd &#x6216; &#x65F6;&#x95F4;&#x6233;(&#x6BEB;&#x79D2;)</p>
      </td>
      <td style="text-align:left">
        <p>&apos;2040-05-01&apos; &#x6216;</p>
        <p>&apos;2219414400000&apos;</p>
      </td>
    </tr>
  </tbody>
</table>## 数据转换

数据导入时，如数值格式与属性创建类型不符时，会尝试进行如下转换（如无法转换则数值不会录入GrowingIO系统）

| 数值类型 | 字符串 | 整数 | 小数 | 日期 |
| :--- | :--- | :--- | :--- | :--- |
| 字符串 | 原值录入 | 原值录入 | 原值录入 | 原值录入 |
| 整数 |  | 原值录入 | 舍弃小数部分录入 |  |
| 小数 |  | 原值录入 | 原值录入 |  |
| 日期 |  |  |  | 原值录入 |

> 横行为创建属性类型，纵列为导入数值格式

## 筛选条件

筛选条件是指在GrowingIO中能对以上属性类型进行的筛选操作。

> for example:
>
> 用户属性中创建一个整数属性 - 年龄，我们希望在分群中筛选年龄小于18岁的用户分群
>
> 筛选条件即为选择用户属性中年龄小于18的用户

### 字符串

![&#x5B57;&#x7B26;&#x4E32;&#x5C5E;&#x6027;](../../.gitbook/assets/image%20%2820%29.png)

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
      <td style="text-align:left">&#x7CBE;&#x51C6;&#x5339;&#x914D;&#xFF0C;&#x53EA;&#x6709;&#x5C5E;&#x6027;&#x5B8C;&#x5168;&#x7B49;&#x4E8E;&#x8F93;&#x5165;&#x7684;&#x67D0;&#x4E2A;&#x503C;&#x65F6;&#x4E8B;&#x4EF6;&#x624D;&#x4F1A;&#x8FDB;&#x5165;&#x7EDF;&#x8BA1;&#x5206;&#x6790;</td>
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
</table>> 除没值外，其他筛选条件默认在有值条件下筛选

### 整数、小数

![&#x6574;&#x6570;&#x3001;&#x5C0F;&#x6570;&#x5C5E;&#x6027;](../../.gitbook/assets/image%20%28135%29.png)

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
</table>> 除没值外，其他筛选条件默认在有值条件下筛选

### 日期

![&#x65E5;&#x671F;&#x5C5E;&#x6027;](../../.gitbook/assets/image%20%2845%29.png)

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
</table>> 除没值外，其他筛选条件默认在有值条件下筛选

**相对现在**

![&#x76F8;&#x5BF9;&#x73B0;&#x5728;](../../.gitbook/assets/image%20%28132%29.png)

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

![&#x76F8;&#x5BF9;&#x533A;&#x95F4;](../../.gitbook/assets/image%20%2813%29.png)

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

