---
description: 对物品进行声明和管理
---

# 物品管理

## 简介

如果您的业务中存在物品\(如商品、保险产品、课程 etc.\)，需要分析人对物品的偏好或分析物品特征时，可以使用GrowingIO提供的物品模型来创建和管理物品。物品模型支持通过文件上传的方式导入物品信息，相对于事件属性SDK埋点方式，文件上传可以规避大量的技术埋点工作。

> GrowingIO中对于物品的定义：
>
> 以商品为例，满足以下点特征可以使用物品模型。
>
> 1. 每一个商品具有唯一识别标识，即商品ID\(product\_id\)。
> 2. 不同商品具有共有的属性特征，如供应商、商品型号、商品颜色 etc.；且商品特征的个数相对稳定，不会频繁增加或减少。
> 3. 单一商品的属性值不会频繁变更，一天内商品属性值不会发生变化。

## 创建物品

一、在顶部导航栏选择“**数据 &gt; 物品 &gt; 物品管理**“，进入物品管理页面。

![&#x7269;&#x54C1;&#x7BA1;&#x7406;&#x9875;&#x9762;](../../../.gitbook/assets/image%20%288%29.png)

二、单击右上角**添加物品**，进入**新建物品**页面。

![Step 1: &#x65B0;&#x5EFA;&#x7269;&#x54C1;](../../../.gitbook/assets/image%20%281%29.png)

| 参数 | 说明 |
| :--- | :--- |
| 名称 | 输入物品名称，如商品、保险产品、课程 etc.。 |
| 描述 | 物品的描述。 |

![Step 2: &#x8BBE;&#x7F6E;&#x552F;&#x4E00;&#x8BC6;&#x522B;&#x5C5E;&#x6027;](../../../.gitbook/assets/image%20%2818%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x540D;&#x79F0;</td>
      <td style="text-align:left">&#x8F93;&#x5165;&#x7269;&#x54C1;&#x552F;&#x4E00;&#x8BC6;&#x522B;&#x5C5E;&#x6027;&#x7684;&#x540D;&#x79F0;&#xFF0C;&#x5982;&#x5546;&#x54C1;ID&#x3001;&#x4FDD;&#x9669;&#x4EA7;&#x54C1;ID&#x3001;&#x8BFE;&#x7A0B;ID
        etc.&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6807;&#x8BC6;&#x7B26;</td>
      <td style="text-align:left">
        <p>&#x8F93;&#x5165;&#x7269;&#x54C1;&#x552F;&#x4E00;&#x8BC6;&#x522B;&#x5C5E;&#x6027;&#x7684;&#x6807;&#x8BC6;&#x7B26;&#xFF0C;&#x5982;product_id&#x3001;insurance_id&#x3001;lecture_id
          etc.&#x3002;</p>
        <p>&#x6B64;&#x53D8;&#x91CF;&#x5728;&#x4EE3;&#x7801;&#x4E2D;&#x7684;&#x6807;&#x8BC6;&#xFF0C;&#x4EC5;&#x5141;&#x8BB8;&#x5927;&#x5C0F;&#x5199;&#x82F1;&#x6587;&#x3001;&#x6570;&#x5B57;&#x3001;&#x4E0B;&#x5212;&#x7EBF;&#xFF0C;&#x5E76;&#x4E14;&#x4E0D;&#x80FD;&#x4EE5;&#x6570;&#x5B57;&#x5F00;&#x5934;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x7C7B;&#x578B;</td>
      <td style="text-align:left">&#x7269;&#x54C1;&#x552F;&#x4E00;&#x5C5E;&#x6027;&#x7684;&#x5B57;&#x7B26;&#x7C7B;&#x578B;&#xFF0C;&#x9ED8;&#x8BA4;&#x4E3A;&#x5B57;&#x7B26;&#x4E32;&#xFF0C;&#x4E0D;&#x53EF;&#x66F4;&#x6539;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x63CF;&#x8FF0;</td>
      <td style="text-align:left">&#x7269;&#x54C1;&#x552F;&#x4E00;&#x8BC6;&#x522B;&#x5C5E;&#x6027;&#x7684;&#x63CF;&#x8FF0;&#x3002;</td>
    </tr>
  </tbody>
</table>三、填写完成后，单击完成，完成一个物品的创建。

{% hint style="info" %}
物品创建成功后自动跳转到物品详情页，在物品详情页可以创建和管理物品属性。
{% endhint %}

## 创建物品属性

一、在物品管理页面点击物品名称，进入物品详情页。

![&#x7269;&#x54C1;&#x7BA1;&#x7406;&#x9875;&#x9762;](../../../.gitbook/assets/image%20%2843%29.png)

![&#x7269;&#x54C1;&#x8BE6;&#x60C5;&#x9875;](../../../.gitbook/assets/image%20%28118%29.png)

二、单击右上角**添加物品属性**，进入**新建物品属性**页面。

![&#x65B0;&#x5EFA;&#x7269;&#x54C1;&#x5C5E;&#x6027;](../../../.gitbook/assets/image%20%287%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x540D;&#x79F0;</td>
      <td style="text-align:left">&#x8F93;&#x5165;&#x7269;&#x54C1;&#x5C5E;&#x6027;&#x540D;&#x79F0;&#xFF0C;&#x5982;&#x4F9B;&#x5E94;&#x5546;&#x3001;&#x5546;&#x54C1;&#x989C;&#x8272;&#x3001;&#x5546;&#x54C1;&#x578B;&#x53F7;
        etc.&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6807;&#x8BC6;&#x7B26;</td>
      <td style="text-align:left">
        <p>&#x8F93;&#x5165;&#x5C5E;&#x54C1;&#x5C5E;&#x6027;&#x6807;&#x8BC6;&#x7B26;&#x3002;</p>
        <p>&#x6B64;&#x53D8;&#x91CF;&#x5728;&#x4EE3;&#x7801;&#x4E2D;&#x7684;&#x6807;&#x8BC6;&#xFF0C;&#x4EC5;&#x5141;&#x8BB8;&#x5927;&#x5C0F;&#x5199;&#x82F1;&#x6587;&#x3001;&#x6570;&#x5B57;&#x3001;&#x4E0B;&#x5212;&#x7EBF;&#xFF0C;&#x5E76;&#x4E14;&#x4E0D;&#x80FD;&#x4EE5;&#x6570;&#x5B57;&#x5F00;&#x5934;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x7C7B;&#x578B;</td>
      <td style="text-align:left">&#x7269;&#x54C1;&#x5C5E;&#x6027;&#x7684;&#x5B57;&#x7B26;&#x7C7B;&#x578B;&#xFF0C;&#x9ED8;&#x8BA4;&#x4E3A;&#x5B57;&#x7B26;&#x4E32;&#xFF0C;&#x4E0D;&#x53EF;&#x66F4;&#x6539;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x63CF;&#x8FF0;</td>
      <td style="text-align:left">&#x7269;&#x54C1;&#x5C5E;&#x6027;&#x7684;&#x63CF;&#x8FF0;&#x3002;</td>
    </tr>
  </tbody>
</table>三、填写完成后，单击确定，完成一个物品属性的创建。

{% hint style="info" %}
物品和物品属性创建成功后，需关联事件与对应的物品属性。
{% endhint %}

## 关联事件与物品

> 一个事件仅能关联唯一一个物品。

一、新建事件时关联物品

在事件管理页面新建事件时，可单击**关联物品属性**选择物品。

![&#x65B0;&#x5EFA;&#x4E8B;&#x4EF6;&#x9875;&#x9762;](../../../.gitbook/assets/image%20%28105%29.png)

二、已创建事件关联物品

在事件管理页面单击事件进入QuickView页面，下拉到底部单击**关联物品属性**选择物品。

![&#x4E8B;&#x4EF6; - QuickView&#x754C;&#x9762;](../../../.gitbook/assets/image%20%2834%29.png)

{% hint style="success" %}
在完成了以上配置，以及物品数据上传和正确的代码实施后。我们即可以在对应的事件中使用物品及相关的物品属性。
{% endhint %}

## 使用物品和物品属性

在完成以上配置后，可在配置了物品的事件维度选择器中使用物品属性。

![&#x7EF4;&#x5EA6;&#x9009;&#x62E9;&#x5668;](../../../.gitbook/assets/image%20%2898%29.png)

## 物品管理页面

在物品管理页面可以查看物品的名称、描述、创建人、更新日期、创建日期。

您也可以对物品进行以下操作：

**搜索：**您可以在页面中列表上方的搜索框按物品名称来搜索物品。

**QuickView：**单击任一物品，您可以在右侧弹出的物品详情中，查看物品的基本信息。

**编辑：**在QuickView界面单击物品的参数进行修改，修改后单击保存。

**删除：**单击单条物品右侧的 ![](https://docs.growingio.com/.gitbook/assets/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的物品。

**批量操作**：在列表中使用复选框选择多个物品，可以进行批量删除。

## 物品属性管理页面

在物品属性管理页面可以查看物品属性的名称、标识符、类型、创建人、创建日期。

> 物品属性列表第一行默认为唯一标识，不可更改。

您也可以对物品属性进行以下操作：

**搜索：**您可以在页面中列表上方的搜索框按物品属性名称和标识符来搜索物品属性。

**QuickView：**单击任一物品属性，您可以在右侧弹出的物品属性详情中，查看物品属性的基本信息。

**编辑：**在QuickView界面单击物品属性的参数进行修改，修改后单击保存。

**删除：**单击单条物品属性右侧的 ![](https://docs.growingio.com/.gitbook/assets/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的物品属性。

**批量操作**：在列表中使用复选框选择多个物品属性，可以进行批量删除。

## 常见问题

### 1. 商品金额能不能设置成物品属性？

商品金额一天内有可能发生多次变化，如抢购活动、新手活动 etc.。对于一天内发生多次变化的属性应使用SDK埋方式上传，不能设置成物品属性。

