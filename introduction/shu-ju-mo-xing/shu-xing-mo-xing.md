# 属性模型

## 简介

在GrowingIO的属性模型中，根据不同的使用场景需要，我们支持四种不同的属性类型，分别为字符串、整数、小数和日期。目前用户属性、事件属性和物品属性分别支持以下几种属性类型：

|  | 字符串 | 整数 | 小数 | 日期 |
| :--- | :--- | :--- | :--- | :--- |
| 用户属性 | ✔️ | ✔️ |  | ✔️ |
| 事件属性 | ✔️ | ✔️ | ✔️ |  |
| 物品属性 | ✔️ |  |  |  |

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
      <td style="text-align:left">yyyy-mm-dd &#x6216; &#x65F6;&#x95F4;&#x6233;(&#x6BEB;&#x79D2;)</td>
      <td
      style="text-align:left">2040-05-01 &#x6216; 2219414400000</td>
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

（横行为创建属性类型，纵列为导入数值格式）













