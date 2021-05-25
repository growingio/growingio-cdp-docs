---
description: 事物的性质和人的特征
---

# 属性模型

## 简介

属性是用于描述一个事物与性质的关系。事物与属性是不可分的，事物都是有属性的事物，属性也都是事物的属性。脱离了事物谈属性，属性也失去了它应有的色彩和意义。

GrowingIO系统中支持三种事物模型，分别为事件模型、物品模型和用户模型，其对应的属性如下：

| 事物模型 | 属性类型 |
| :--- | :--- |
| 事件模型 | 预定义属性、事件属性 |
| 物品模型 | 物品属性 |
| 用户模型 | 用户信息、用户属性 |

根据描述的事物不同，事物的属性也千差万别。我们拿以下场景举例：

在电商业务中，我们经常会关注订单支付成功这一行为。为了更清晰的描述这一行为，谁在什么时间做什么什么事情，我们会用以下几个属性描述订单支付成功事件。

| 属性 | 属性值 |
| :--- | :--- |
| 时间 | 2015-05-01 |
| 用户ID | 3325103 |
| 订单ID | 62531631501961032 |
| 订单支付金额 | 2999.00 |
| 是否使用优惠券 | 是 |
| 优惠券名称 | 新人大礼包 |

为了满足不同事物的属性描述，我们支持四种属性类型，分别为字符串、整数、小数和日期。根据事物的差异，上述属性分别支持以下几种属性类型：

| 属性 | 字符串 | 整数 | 小数 | 日期 |
| :--- | :--- | :--- | :--- | :--- |
| 预定义属性 | -- | -- | -- | -- |
| 事件属性 | ✔️ | ✔️ | ✔️ |  |
| 物品属性 | ✔️ |  |  |  |
| 用户信息 | -- | -- | -- | -- |
| 用户属性 | ✔️ | ✔️ |  | ✔️ |

> 事件属性仅支持非负整数和非负小数

{% hint style="warning" %}
注意：创建属性时可选择属性类型，创建成功后属性类型不可更改
{% endhint %}

## 属性说明

| 属性名称 | 说明 |
| :--- | :--- |
| 预定义属性 | 系统预置的事件属性，SDK配置成功后自动采集 |
| 事件属性 | 自定义配置的事件属性 |
| 物品属性 | 自定义配置的物品属性 |
| 用户信息 | 系统预置的用户属性，需要主动上传数据 |
| 用户属性 | 自定义配置的用户属性 |

## 属性管理

GrowingIO系统支持对[事件属性](../product-manual/customer-data-platform/data-center/event-management/event-property.md)、[物品属性](../product-manual/customer-data-platform/data-center/item/item-manage.md)和[用户属性](../product-manual/customer-data-platform/data-center/customer-model-management/customer-property/)的创建、编辑和查看功能，详情请点击对应文字链接。

[预定义属性](../product-manual/customer-data-platform/data-center/event-management/preset-property.md)和[用户信息](../product-manual/customer-data-platform/data-center/customer-model-management/customer-identification.md)为系统预置信息，仅支持查看，详情请点击对应文字链接。

## 属性关联

事件属性和物品属性创建成功后，需要主动关联事件，关联成功后才能在事件中使用相应的事件属性和物品属性。

{% hint style="warning" %}
注意：如果事件没有关联或取消关联事件属性或物品属性，即使数据正常上传也无法解析，且不支持计算对应属性的统计数据
{% endhint %}

用户属性创建成功后无需额外配置即可在系统中使用。

配置方法：[事件属性](../product-manual/customer-data-platform/data-center/event-management/manual.md#chuang-jian-shi-jian)、[物品属性](../product-manual/customer-data-platform/data-center/event-management/manual.md#chuang-jian-shi-jian)

## 数据格式

GrowingIO支持多种语言的SDK，不同语言的SDK上报数据和导入数据都使用统一的数据格式。不同属性类型的数据格式说明如下：

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
      <td style="text-align:left">&apos;GrowingIO&apos;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6574;&#x6570;</td>
      <td style="text-align:left">&#x4EE5;&#x5B57;&#x7B26;&#x683C;&#x5F0F;&#x4F20;&#x5165;</td>
      <td style="text-align:left">&apos;1234567&apos;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5C0F;&#x6570;</td>
      <td style="text-align:left">
        <p>&#x4EE5;&#x5B57;&#x7B26;&#x683C;&#x5F0F;&#x4F20;&#x5165;&#xFF0C;</p>
        <p>&#x5C0F;&#x6570;&#x70B9;&#x540E;&#x6700;&#x591A;&#x5305;&#x542B;&#x56DB;&#x4F4D;&#x6709;&#x6548;&#x6570;&#x5B57;</p>
      </td>
      <td style="text-align:left">&apos;3.1415&apos;</td>
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
</table>

如上传数据不符合上述格式要求，GrowingIO系统会对部分数据类型上传的数据进行强制格式转换，具体说明如下：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5C5E;&#x6027;&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x8F6C;&#x5316;&#x89C4;&#x5219;</th>
      <th style="text-align:left">&#x793A;&#x4F8B;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x6574;&#x6570;</td>
      <td style="text-align:left">&#x4E0A;&#x4F20;&#x6570;&#x636E;&#x4E3A;&#x5C0F;&#x6570;&#x65F6;&#xFF0C;&#x6309;&#x9AD8;&#x65AF;&#x53D6;&#x6574;&#x5904;&#x7406;&#xFF0C;&#x4EC5;&#x4FDD;&#x7559;&#x6574;&#x6570;&#x90E8;&#x5206;</td>
      <td
      style="text-align:left">
        <p>&#x4E0A;&#x4F20;: 9.99</p>
        <p>&#x5B58;&#x50A8;: 9</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5C0F;&#x6570;</td>
      <td style="text-align:left">&#x4E0A;&#x4F20;&#x6570;&#x636E;&#x4E3A;&#x9AD8;&#x7CBE;&#x5EA6;&#x5C0F;&#x6570;(&#x8D85;&#x56DB;&#x4F4D;)&#x65F6;&#xFF0C;&#x6309;&#x56DB;&#x820D;&#x4E94;&#x5165;&#x4FDD;&#x7559;&#x56DB;&#x4F4D;&#x5C0F;&#x6570;</td>
      <td
      style="text-align:left">
        <p>&#x4E0A;&#x4F20;: 3.1415926</p>
        <p>&#x5B58;&#x50A8;: 3.1416</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x65E5;&#x671F;</td>
      <td style="text-align:left">&#x4E0A;&#x4F20;&#x6570;&#x636E;&#x4E3A;&#x6574;&#x6570;&#x6216;&#x5C0F;&#x6570;&#x65F6;&#xFF0C;&#x6309;&#x6BEB;&#x79D2;&#x65F6;&#x95F4;&#x6233;&#x8F6C;&#x6210;&#x65E5;&#x671F;&#x683C;&#x5F0F;&#x5B58;&#x50A8;</td>
      <td
      style="text-align:left">
        <p>&#x4E0A;&#x4F20;: 1588262400</p>
        <p>&#x5B58;&#x50A8;: 1970-01-19</p>
        </td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
注意：日期属性如按时间戳格式上传时，需使用毫秒级时间戳\(13位\)；如上传秒级时间戳\(10位\)时存储时间会发生错误
{% endhint %}

