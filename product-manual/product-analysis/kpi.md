# KPI 分析

## 简介

KPI看板可以帮助业务负责人在 GrowingIO 平台上监控 KPI 数据，判断 KPI 是否符合预期。若数据与预期不符，用户可以借助维度拆解和下钻，迅速找到影响KPI表现的原因。

功能包括：

* 趋势对比：指标趋势，以及时间范围内的同环比计算
* 属性拆解：基于不同属性维度的拆解，如根据维度拆解变化量和变化率指标
* 维度下钻：支持基于不同属性的下钻
* 洞察：支持KPI波动主要影响因子洞察分析

**以某电商公司 KPI 看板为例子：**

我们将销售量、销售额、用户量、复购等核心业务数据放在KPI看板。您打开KPI看板后，借助大数字图，所有核心指标表现一览无余，帮您迅速了解整体表现和有异常的 KPI。

比如，我们可以看到下图中**订单支付成功人数**这个KPI出现了问题。同比下降18%、环比下降53%。

![KPI&#x770B;&#x677F;\(Demo&#x6570;&#x636E;\)](../../.gitbook/assets/image%20%2871%29.png)

此时，我们可以单击订单支付成功人数这一KPI看板，在KPI详情页了解不同维度下订单支付人数变化状况，迅速判断业务指标下降原因。KPI分析包含以下功能：

* 自定义维度拆分
* 自动业务分析

![KPI&#x5206;&#x6790;&#x8BE6;&#x60C5;&#x9875;\(Demo&#x6570;&#x636E;\)](../../.gitbook/assets/image%20%2858%29.png)

## 创建KPI分析

一、在顶部导航栏选择“**分析 &gt; 产品分析 &gt; KPI分析**"，进入KPI分析看板。

![KPI&#x5206;&#x6790;&#x770B;&#x677F;](../../.gitbook/assets/image%20%28123%29.png)

二、单击左侧列表上方“**新建分析 &gt; KPI分析"**或单击KPI分析看板中“**+”**，进入**创建KPI分析**页面。

![&#x521B;&#x5EFA;KPI&#x6307;&#x6807;&#x9875;&#x9762;](../../.gitbook/assets/image%20%282%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>&#x65F6;</p>
        <p>&#x95F4;</p>
        <p>&#x8303;</p>
        <p>&#x56F4;</p>
      </td>
      <td style="text-align:left">
        <p>&#x53EF;&#x9009;&#x62E9;&#x4ECA;&#x5929;&#x3001;&#x672C;&#x5468;&#x3001;&#x672C;&#x6708;&#x76D1;&#x63A7;KPI&#x6307;&#x6807;&#x3002;</p>
        <ul>
          <li>&#x82E5;&#x60A8;&#x9009;&#x62E9;&#x4ECA;&#x5929;&#xFF0C;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x4ECA;&#x5929;&#x7684;&#x5C0F;&#x65F6;&#x7EA7;&#x522B;&#x6570;&#x636E;&#xFF0C;&#x5982;&#x679C;&#x60A8;&#x5BF9;&#x67D0;&#x4E00;&#x4E2A;&#x6307;&#x6807;&#x7684;&#x5173;&#x6CE8;&#x5EA6;&#x662F;&#x6BCF;&#x5C0F;&#x65F6;&#x90FD;&#x4F1A;&#x770B;&#x4E00;&#x770B;&#xFF0C;&#x6216;&#x8005;&#x6BCF;&#x534A;&#x5929;&#x90FD;&#x4F1A;&#x770B;&#x4E00;&#x4E0B;&#xFF0C;&#x5EFA;&#x8BAE;&#x9009;&#x62E9;&#x4ECA;&#x5929;&#x3002;</li>
          <li>&#x82E5;&#x60A8;&#x9009;&#x62E9;&#x672C;&#x5468;&#xFF08;&#x4E0D;&#x5305;&#x62EC;&#x4ECA;&#x5929;&#xFF09;&#xFF0C;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x672C;&#x5468;&#x7684;&#x5929;&#x7EA7;&#x522B;&#x6570;&#x636E;&#xFF0C;&#x5982;&#x679C;&#x60A8;&#x5BF9;&#x67D0;&#x4E00;&#x4E2A;&#x6307;&#x6807;&#x7684;&#x5173;&#x6CE8;&#x5EA6;&#x662F;&#x6BCF;&#x5929;&#x90FD;&#x4F1A;&#x770B;&#x4E00;&#x770B;&#xFF0C;&#x5468;&#x672B;&#x4F1A;&#x505A;&#x4E00;&#x4E2A;&#x603B;&#x7ED3;&#x62A5;&#x544A;&#xFF0C;&#x5EFA;&#x8BAE;&#x9009;&#x62E9;&#x672C;&#x5468;&#x3002;</li>
          <li>&#x82E5;&#x60A8;&#x9009;&#x62E9;&#x672C;&#x6708;&#xFF08;&#x4E0D;&#x5305;&#x62EC;&#x4ECA;&#x5929;&#xFF09;&#xFF0C;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x672C;&#x6708;&#x5929;&#x7EA7;&#x522B;&#x7684;KPI&#x6570;&#x636E;&#xFF0C;&#x5982;&#x679C;&#x60A8;&#x5BF9;&#x67D0;&#x4E00;&#x4E2A;&#x6307;&#x6807;&#x7684;&#x5173;&#x6CE8;&#x5EA6;&#x662F;&#x6BCF;&#x5929;&#x6216;&#x8005;&#x6BCF;&#x5468;&#x90FD;&#x4F1A;&#x770B;&#x4E00;&#x770B;&#xFF0C;&#x6708;&#x5EA6;&#x4F1A;&#x505A;&#x4E00;&#x4E2A;&#x603B;&#x7ED3;&#x62A5;&#x544A;&#xFF0C;&#x5EFA;&#x8BAE;&#x9009;&#x62E9;&#x672C;&#x6708;&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x76EE;</p>
        <p>&#x6807;</p>
        <p>&#x7528;</p>
        <p>&#x6237;</p>
      </td>
      <td style="text-align:left">&#x8BBE;&#x7F6E;&#x76EE;&#x6807;&#x4EBA;&#x7FA4;&#xFF0C;&#x4EE5;&#x4FBF;&#x4E86;&#x89E3;&#x7279;&#x6B8A;&#x4EBA;&#x7FA4;&#x7684;KPI&#x8868;&#x73B0;&#xFF0C;&#x5982;&#x91CD;&#x65B0;&#x8D2D;&#x4E70;&#x3001;&#x65B0;&#x6CE8;&#x518C;&#x7B49;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>KPI</p>
        <p>&#x6307;</p>
        <p>&#x6807;</p>
      </td>
      <td style="text-align:left">
        <p>&#x9009;&#x62E9;KPI&#x6307;&#x6807;&#x3002;</p>
        <p>KPI &#x7531;&#x4E8B;&#x4EF6;&#x3001;&#x4E8B;&#x4EF6;&#x7684;&#x5EA6;&#x91CF;&#x65B9;&#x5F0F;&#xFF08;&#x4EBA;&#x3001;&#x6B21;&#x3001;&#x4EBA;&#x5747;&#xFF09;&#x548C;&#x8FC7;&#x6EE4;&#x6761;&#x4EF6;&#x6784;&#x6210;&#xFF0C;&#x4EE5;&#x4E0B;&#x6307;&#x6807;&#x90FD;&#x53EF;&#x4EE5;&#x662F;
          KPI&#xFF1A;&#x8D2D;&#x4E70;&#x4EBA;&#x6570;&#x3001;&#x8D2D;&#x4E70;&#x6B21;&#x6570;&#x3001;&#x5E73;&#x5747;&#x8D2D;&#x4E70;&#x6B21;&#x6570;&#x3001;&#x8D2D;&#x4E70;&#x91D1;&#x989D;&#x3001;&#x624B;&#x673A;&#x8D2D;&#x4E70;&#x91CF;&#x7B49;&#x3002;</p>
        <p>&#x4ED6;&#x53EF;&#x4EE5;&#x501F;&#x52A9;&#x4E8B;&#x4EF6; &#x201C;&#x8D2D;&#x4E70;&#x201C;&#xFF0C;&#x201C;&#x8D2D;&#x4E70;&#x201D;&#x4E8B;&#x4EF6;&#x7684;&#x5EA6;&#x91CF;&#x65B9;&#x5F0F;
          &#x4EBA;&#x3001;&#x6B21;&#x3001;&#x4EBA;&#x5747;&#xFF0C;&#x4E8B;&#x4EF6;&#x7684;&#x53D8;&#x91CF;&#xFF1A;&#x91D1;&#x989D;&#x3001;&#x54C1;&#x7C7B;&#x7B49;&#x7EC4;&#x5408;&#x6784;&#x6210;&#x3002;</p>
        <p>&#x6CE8;&#xFF1A;KPI &#x4F5C;&#x4E3A;&#x6838;&#x5FC3;&#x4E1A;&#x52A1;&#x6307;&#x6807;&#xFF0C;&#x9700;&#x8981;&#x901A;&#x8FC7;&#x4E1A;&#x52A1;&#x7EF4;&#x5EA6;&#x5BF9;&#x5176;&#x8FDB;&#x884C;&#x62C6;&#x89E3;&#xFF0C;&#x540C;&#x65F6;&#x5BF9;&#x6570;&#x636E;&#x7684;&#x51C6;&#x786E;&#x6027;&#x3001;&#x7A33;&#x5B9A;&#x6027;&#x6709;&#x8F83;&#x9AD8;&#x7684;&#x8981;&#x6C42;&#xFF0C;&#x6211;&#x4EEC;&#x66F4;&#x5EFA;&#x8BAE;&#x60A8;&#x91C7;&#x7528;&#x57CB;&#x70B9;&#x6307;&#x6807;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>

三、填写完成后单击**创建**，完成一个KPI分析的创建。

## 设置KPI目标

您可以对KPI设置目标，以便观察目标进度是否符合预期。

在KPI看板中，单击单个KPI指标框右上角的 ![](https://docs.growingio.com/.gitbook/assets/-Lo08UtW7H58ehFKeZ4g-LugKRBPNPab7MdZtndt-LugeasN0wzG5aPiGtgoKPIE79C8BE69DBFE782B9E782B9E782B9.png) 选择编辑，在编辑页面设置目标值。

![&#x8BBE;&#x7F6E;KPI&#x76EE;&#x6807;](../../.gitbook/assets/image%20%28174%29.png)

设置完成后即可在单个KPI框右下角查看目标完成度。

![](../../.gitbook/assets/image%20%2811%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x6807;&#x9898;</td>
      <td style="text-align:left">&#x6211;&#x4EEC;&#x9ED8;&#x8BA4;&#x7528;&#x4E86;&#x4E8B;&#x4EF6;&#x540D;&#x79F0;&#x6765;&#x6307;&#x4EE3;&#x6807;&#x9898;&#xFF0C;&#x60A8;&#x53EF;&#x4EE5;&#x901A;&#x8FC7;KPI&#x5355;&#x56FE;&#x53F3;&#x4E0A;&#x89D2;&#x7684;&#x64CD;&#x4F5C;&#x6309;&#x94AE;&#x8FDB;&#x884C;&#x7F16;&#x8F91;&#x3002;&#x5EFA;&#x8BAE;&#x6807;&#x9898;&#x8BBE;&#x7F6E;&#x4E00;&#x5B9A;&#x8981;&#x7B80;&#x5355;&#x660E;&#x4E86;&#xFF0C;&#x6240;&#x6709;&#x4EBA;&#x770B;&#x5230;&#x6807;&#x9898;&#x540E;&#x5C31;&#x80FD;&#x660E;&#x767D;&#x5B83;&#x7684;&#x4E1A;&#x52A1;&#x542B;&#x4E49;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x65F6;&#x95F4;</p>
        <p>&#x8303;&#x56F4;</p>
      </td>
      <td style="text-align:left">
        <p>&#x8003;&#x5BDF;KPI&#x7684;&#x8303;&#x56F4;&#xFF0C;&#x4E00;&#x822C;&#x60C5;&#x51B5;&#x4E0B;&#x516C;&#x53F8;&#x7528;&#x4ECA;&#x5929;&#x3001;&#x672C;&#x5468;&#x3001;&#x672C;&#x6708;&#x6765;&#x770B;KPI&#x7684;&#x8868;&#x73B0;&#x3002;</p>
        <p>&#x5728;&#x7F16;&#x8F91;&#x65F6;&#x60A8;&#x53EF;&#x4EE5;&#x66F4;&#x7075;&#x6D3B;&#x5730;&#x9009;&#x62E9;&#x65F6;&#x95F4;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x540C;&#x6BD4;</td>
      <td style="text-align:left">
        <p>&#x540C;&#x6BD4;&#x662F;&#x4E00;&#x4E2A;&#x4E1A;&#x52A1;&#x6982;&#x5FF5;&#xFF0C;&#x662F;&#x57FA;&#x4E8E;&#x4E1A;&#x52A1;&#x5468;&#x671F;&#x7684;&#x5B9A;&#x4E49;&#x3002;</p>
        <p>&#x5BF9;&#x6BD4;&#x89C4;&#x5219;&#xFF1A;&#x672C;&#x5468;&#x6BD4;&#x4E0A;&#x5468;&#x3001;&#x672C;&#x6708;&#x6BD4;&#x4E0A;&#x6708;&#x3001;&#x4ECA;&#x5E74;&#x6BD4;&#x53BB;&#x5E74;&#x3002;</p>
        <p>&#x5982;&#x679C;&#x4ECA;&#x5929;&#x662F;&#x5468;&#x4E09;&#xFF0C;&#x90A3;&#x4E48;&#x672C;&#x5468;&#x6BD4;&#x4E0A;&#x5468;&#x5C31;&#x662F;&#x672C;&#x5468;&#x4E00;&#x4E8C;&#x4E09;&#x7684;&#x6570;&#x636E;&#x6BD4;&#x4E0A;&#x5468;&#x4E00;&#x4E8C;&#x4E09;&#x7684;&#x6570;&#x636E;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x73AF;&#x6BD4;</td>
      <td style="text-align:left">
        <p>&#x5B9A;&#x4E49;&#x4E3A;&#x8FD9;&#x4E2A;N&#x5929;&#x6BD4;&#x4E0A;&#x4E2A;N&#x5929;&#x3002;</p>
        <p>&#x6BD4;&#x5982;&#xFF1A;&#x4ECA;&#x5929;&#x6BD4;&#x6628;&#x5929;&#xFF0C;&#x8FC7;&#x53BB;7&#x5929;&#x7684;&#x6570;&#x636E;&#x6BD4;&#x8FC7;&#x53BB;8
          -14&#x5929;&#x6570;&#x636E;&#xFF0C;&#x73AF;&#x6BD4;&#x66F4;&#x5173;&#x6CE8;&#x4E1A;&#x52A1;&#x7684;&#x8FDE;&#x7EED;&#x6027;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x76EE;&#x6807;</td>
      <td style="text-align:left">
        <p>&#x7ED9;&#x4E88;&#x6240;&#x9009;&#x65F6;&#x95F4;&#x8303;&#x56F4;&#x548C;&#x7C92;&#x5EA6;&#x7684;&#x76EE;&#x6807;&#x3002;&#x6BD4;&#x5982;&#x672C;&#x5468;&#x76EE;&#x6807;&#x3001;&#x672C;&#x6708;&#x76EE;&#x6807;&#x7B49;&#x3002;&#x5BF9;&#x4E8E;&#x6240;&#x9009;&#x65F6;&#x95F4;&#x8303;&#x56F4;&#x548C;&#x7C92;&#x5EA6;&#x7684;KPI&#x60A8;&#x53EF;&#x4EE5;&#x8BBE;&#x5B9A;&#x5BF9;&#x5E94;&#x7684;&#x76EE;&#x6807;&#x3002;</p>
        <p>&#x6CE8;&#xFF1A;&#x5F53;&#x6240;&#x9009;&#x65F6;&#x95F4;&#x8303;&#x56F4;&#x53D1;&#x751F;&#x53D8;&#x5316;&#x65F6;&#xFF0C;&#x76EE;&#x6807;&#x9700;&#x8981;&#x91CD;&#x65B0;&#x586B;&#x5199;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x76EE;&#x6807;&#x5B8C;&#x6210;&#x7387;</td>
      <td style="text-align:left">&#x5B9E;&#x9645;KPI&#x8868;&#x73B0;/&#x76EE;&#x6807;&#x503C;&#xFF0C;&#x60A8;&#x53EF;&#x4EE5;&#x501F;&#x52A9;&#x76EE;&#x6807;&#x5B8C;&#x6210;&#x7387;&#x6765;&#x8FFD;&#x8E2A;&#x8FDB;&#x7A0B;&#x662F;&#x5426;&#x7B26;&#x5408;&#x9884;&#x671F;&#x3002;</td>
    </tr>
  </tbody>
</table>

## 解读KPI分析

当您发现KPI不符合预期时，点击KPI单图进入KPI详情页，详情页将帮助您快速找到数据波动的原因。

KPI详情页构成：

![KPI&#x8BE6;&#x60C5;&#x9875;](../../.gitbook/assets/image%20%2856%29.png)

| 项 | 说明 |
| :--- | :--- |
| 1-时间范围与粒度 | 灵活选择事件与粒度。 |
| 2-用户范围 | 更改目标人群。 |
| 3-趋势图 | 趋势线图，帮助您监测 KPI 趋势与波动状况。 |
| 4-趋势图洞察 | 基于您关注的业务维度，直接呈现 KPI 变化的主要影响因子。快速理解导致数据波动的核心原因。 |
| 5-维度拆解 | 您可以按照业务维度对您的KPI进行拆解，找到 KPI 变化的影响因子。同时提供不同业务维度下的数据变化量与变化率。 |
| 6-选择下钻维度 | 单击维度列单元格可以对维度进行下钻。可以根据您的业务思路，不断拆解下钻找到最小粒度的原因。 |
| 7-展示条数 | 设置图表中展示的维度条数。 |

## KPI分析看板

KPI分析看板与分析看板的管理方式相同，请参考看板管理。

