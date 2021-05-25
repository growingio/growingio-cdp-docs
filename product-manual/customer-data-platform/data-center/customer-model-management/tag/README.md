---
description: 对标签进行定义和管理
---

# 用户标签

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

目前GrowingIO提供了 **五种** **规则标签** 模型 和 **SQL标签**，规则标签分别为

* 基础指标值：建用户完成事件的次数、人数、天数等指标作为标签值
* 最大值/最小值的事件属性：将用户完成事件按某个属性分组排序后，使用最多或最少的事件属性作为标签值
* 首次/末次的事件属性：将用户完成事件最初或最终的事件属性、具体时间、距今天数等作为标签值
* 列表类的事件属性：将用户完成事件的全部时间属性列表作为标签值
* 分层标签：根据规则自定义用户分层，并且将分层名称作为标签值

![](../../../../../.gitbook/assets/image%20%28539%29.png)

## 界面说明

在 **客户数据平台 &gt; 用户管理 &gt; 用户标签** 中可以看到 **用户标签详情页**。在 用户标签详情页 中支持

* 按四级分类结构查看用户标签
* 查看用户标签基本信息，包含名称、描述、定义规则、统计数据等
* 新建、编辑、下载、删除用户标签

{% hint style="warning" %}
在客户数据平台中 创建的标签，需要通过 项目管理 &gt;  数据授权 ，将标签分配到项目中使用。 [点此查看](https://app.gitbook.com/@growingio/s/op/~/drafts/-MO-IZPJyPUe03vlfMC_/v/v20201200/product-manual/qi-ye-guan-li-hou-tai/project-manage/data-authorization)
{% endhint %}

![&#x7528;&#x6237;&#x6807;&#x7B7E;&#x8BE6;&#x60C5;&#x9875;](../../../../../.gitbook/assets/image%20%28541%29.png)

在 用户标签详情页 中点击 **查看全部标签** 后，可以看到 **用户标签列表页**。在 用户标签列表页 中支持

* 新建、编辑用户标签分类
* 按四级分类结构查看用户标签
* \(批量\)删除、移动用户标签 和 新建、编辑用户标签

{% hint style="warning" %}
在客户数据平台中 创建的标签，需要通过 项目管理 &gt;  数据授权 ，将标签分配到项目中使用。 [点此查看](https://app.gitbook.com/@growingio/s/op/~/drafts/-MO-IZPJyPUe03vlfMC_/v/v20201200/product-manual/qi-ye-guan-li-hou-tai/project-manage/data-authorization)
{% endhint %}

![&#x7528;&#x6237;&#x6807;&#x7B7E;&#x5217;&#x8868;&#x9875;](../../../../../.gitbook/assets/image%20%28556%29.png)

## 常见问题

### 1. 用户标签 和 用户属性 的区别是什么？

GrowingIO的模型中定义用户属性为通过客观身份\( 如 设备ID、手机号、邮箱号、APP登陆ID、CRM会员ID \)上传的用户画像信息\( 如 性别、年龄、会员等级、用户偏好 等 \)，用户属性上传后会通过ID-Mapping功能识别该客观身份对应的GrowingIO系统用户\(gio\_id\)，并将用户属性赋予该用户。

对比用户属性，GrowingIO的模型中定义用户标签为通过GrowingIO识别打通\( gio\_id \)的用户行为和用户属性，根据GrowingIO提供的计算模型对用户打标，并将计算结果值赋予该用户。

![](../../../../../.gitbook/assets/image%20%28557%29.png)

{% hint style="success" %}
GrowingIOID融合功能，详见 [用户模型](../../../../../introduction/user-model/)。
{% endhint %}

