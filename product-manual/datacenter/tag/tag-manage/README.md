---
description: 对标签进行定义和管理
---

# 标签管理

## 简介

标签是用户行为和特征的抽象与描述。

在特定业务场景下，标签可以让我们快速的了解一个用户或一群用户的特征。如在电销场景下，我们的客服人员需要了解目标用户的性别、年龄、常住城市、家庭成员数量、历史购买记录、最近浏览偏好等标签信息。这些信息可以帮助客服人员在脑海中快速形成一个鲜活的人物形象，帮助客服人员在与客户的交谈中更好的组织语言、挖掘并满足客户需求。

按照业务特征划分，标签可以分为人口属性标签、交易属性标签、兴趣偏好标签等。

按照创建方式划分，标签可以分为属性标签、计算标签、分层标签和算法标签。

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x6807;&#x7B7E;&#x5206;&#x7C7B;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
      <th style="text-align:left">&#x7279;&#x70B9;</th>
      <th style="text-align:left">&#x4E3E;&#x4F8B;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x6807;&#x7B7E;</td>
      <td style="text-align:left">&#x6839;&#x636E;&#x4F01;&#x4E1A;&#x6C89;&#x6DC0;&#x7684;&#x7528;&#x6237;&#x4FE1;&#x606F;&#x52A0;&#x5DE5;&#x8F6C;&#x6362;&#x751F;&#x6210;</td>
      <td
      style="text-align:left">&#x6570;&#x91CF;&#x5C11;&#x3001;&#x4E1A;&#x52A1;&#x4FE1;&#x606F;&#x5927;</td>
        <td
        style="text-align:left">
          <p>&#x6839;&#x636E;&#x8EAB;&#x4EFD;&#x8BC1;&#x53F7;&#x751F;&#x6210;&#x6807;&#x7B7E;&#x3002;&#x5982;</p>
          <p>&#x5E74;&#x9F84;&#x3001;&#x6027;&#x522B;&#x3001;&#x662F;&#x5426;&#x662F;&#x751F;&#x65E5;&#x3001;</p>
          <p>&#x51FA;&#x751F;&#x7701;&#x5E02;&#x7B49;</p>
          </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x8BA1;&#x7B97;&#x6807;&#x7B7E;</td>
      <td style="text-align:left">&#x6839;&#x636E;&#x7528;&#x6237;&#x7684;&#x884C;&#x4E3A;&#x548C;&#x7279;&#x5F81;&#x8BA1;&#x7B97;&#x751F;&#x6210;</td>
      <td
      style="text-align:left">&#x6570;&#x91CF;&#x591A;&#x3001;&#x4E1A;&#x52A1;&#x4FE1;&#x606F;&#x5C0F;</td>
        <td
        style="text-align:left">
          <p>&#x6839;&#x636E;&#x8D2D;&#x4E70;&#x4E8B;&#x4EF6;&#x8BA1;&#x7B97;&#x751F;&#x6210;</p>
          <p>&#x6700;&#x8FD1;&#x8D2D;&#x4E70;&#x8DDD;&#x4ECA;&#x5929;&#x6570;(R)&#x3001;</p>
          <p>&#x8D2D;&#x4E70;&#x6B21;&#x6570;(F)&#x3001;&#x8D2D;&#x4E70;&#x91D1;&#x989D;(M)</p>
          </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x89C4;&#x5219;&#x6807;&#x7B7E;</td>
      <td style="text-align:left">
        <p>&#x6839;&#x636E;&#x4E1A;&#x52A1;&#x7ECF;&#x9A8C;&#xFF0C;&#x4EBA;&#x5DE5;&#x6216;&#x534A;&#x4EBA;&#x5DE5;&#x901A;&#x8FC7;&#x89C4;&#x5219;</p>
        <p>&#x8BA1;&#x7B97;&#x751F;&#x6210;</p>
      </td>
      <td style="text-align:left">
        <p>&#x4EBA;&#x529B;&#x6210;&#x672C;&#x9AD8;&#x3001;&#x6570;&#x91CF;&#x5C11;&#x3001;</p>
        <p>&#x4E1A;&#x52A1;&#x4FE1;&#x606F;&#x5927;</p>
      </td>
      <td style="text-align:left">
        <p>&#x6839;&#x636E;RFM&#x8BA1;&#x7B97;&#x6807;&#x7B7E;&#x6309;&#x4E1A;&#x52A1;</p>
        <p>&#x9700;&#x6C42;&#x6839;&#x636E;&#x89C4;&#x5219;&#x8BB2;&#x7528;&#x6237;&#x8FDB;&#x884C;</p>
        <p>&#x5206;&#x5C42;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x7B97;&#x6CD5;&#x6807;&#x7B7E;</td>
      <td style="text-align:left">
        <p>&#x5927;&#x90E8;&#x5206;&#x4F9D;&#x8D56;&#x7B97;&#x6CD5;&#x8BA1;&#x7B97;&#xFF0C;&#x9700;&#x8981;&#x4EBA;&#x5DE5;&#x53C2;&#x4E0E;</p>
        <p>&#x8C03;&#x53C2;&#x548C;&#x4E1A;&#x52A1;&#x6548;&#x679C;&#x9A8C;&#x8BC1;</p>
      </td>
      <td style="text-align:left">
        <p>&#x8BA1;&#x7B97;&#x6210;&#x672C;&#x9AD8;&#x3001;&#x6570;&#x91CF;&#x591A;&#x3001;</p>
        <p>&#x4E1A;&#x52A1;&#x6548;&#x679C;&#x9700;&#x8981;&#x9A8C;&#x8BC1;</p>
      </td>
      <td style="text-align:left">
        <p>&#x6839;&#x636E;&#x7528;&#x6237;&#x7279;&#x5F81;&#x548C;&#x884C;&#x4E3A;</p>
        <p>&#x9884;&#x6D4B;&#x7528;&#x6237;&#x8D2D;&#x4E70;&#x610F;&#x5411;</p>
      </td>
    </tr>
  </tbody>
</table>

标签可以帮助我们更加全面的描述一个用户，但这并不意味着标签需要越多越好。出于计算成本和管理成本考量，我们应结合业务场景和业务需求，考虑什么样的标签能在业务操作中帮助我们更好的完成业务目标，并依据此目标进行标签的创建。

目前GrowingIO提供了五种标签计算模型，分别为累计值/平均值/占比标签、最大值/最小值的事件属性标签、最初/最终的事件属性标签、列表类的事件属性标签、分层标签。这五种标签主要用于解决计算标签和规则标签的使用场景。

## 创建标签

![&#x6807;&#x7B7E;&#x7BA1;&#x7406;&#x9875;&#x9762;](../../../../.gitbook/assets/image%20%28201%29.png)

一、在顶部导航栏选择“**数据 &gt; 标签 &gt; 标签管理**“，进入标签管理页面。

二、单击右上角**添加标签**，进入**新建标签**页面。

![&#x6807;&#x7B7E;&#x521B;&#x5EFA;&#x9875;&#x9762;](../../../../.gitbook/assets/image%20%28221%29.png)

三、根据业务需求选择需要创建的标签类型，配置完成后，单击保存，完成一个标签的创建。

{% hint style="success" %}
目前支持5种标签类型，分别为：

* [累计值/平均值占比](tag-basic.md)
* [最大值/最小值的事件属性](tag-max-nd-min.md)
* [最初/最终的事件属性](tag-first-nd-last.md)
* [列表类的事件属性](tag-list.md)
* [分层标签](tag-rule.md)
{% endhint %}

## 标签管理页面

在标签管理页面可以查看标签的名称、创建日期、创建人、最后编辑时间。

您也可以对标签进行以下操作：

**搜索：**您可以在页面中列表上方的搜索框按标签名称来搜索标签。

**查看**：单击单条标签右侧的 ![](https://docs.growingio.com/.gitbook/assets/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择查看详情，可以查看标签的基本信息和统计信息。

**编辑：**单击单条标签右侧的 ![](https://docs.growingio.com/.gitbook/assets/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择修改规则，可以修改标签计算规则。

**删除：**单击单条标签右侧的 ![](https://docs.growingio.com/.gitbook/assets/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的标签。

**批量操作**：在列表中使用复选框选择多个标签，可以进行批量删除。

