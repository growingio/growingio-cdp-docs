# 用户模型

GrowingIO系统使用 **gid** 来对每个GrowingIO识别的用户进行唯一标识。目前系统支持采集匿名和登录用户\(user\_id\)，GrowingIO系统会根据匿名和登录用户的匹配关系生成 gid 唯一识别一个真实的使用用户。

### 基本概念

#### 匿名用户

匿名用户是GrowingIO对访问您的应用（包括网页、App、微信小程序等 ）用户的一种识别机制。，每一个访问您应用的用户都会在对应的设备中生成并记录一个唯一的 ID，我们称之为访问用户 ID。

对于不同平台类型的应用，GrowingIO 提供了多种识别方案，从而尽可能的实现对用户的唯一标识。

参见 [匿名用户ID生成机制](anonymous.md)

#### 登录用户

登录用户也就是注册用户，当用户访问您的产品并发生注册/登录行为时，您可以通过GrowingIO SDK 中的 API 将该用户的注册ID（或与之对应的唯一标识，可以加密处理）上传给 GrowingIO。

这个 ID 会被作为今后用户在各个地方使用您的产品的身份识别 ID。

### GrowingIO识别用户\(gid\)

GrowingIO系统默认提供ID-Mapping逻辑，帮助您打通匿名用户和登录用户唯一识别一个真实的使用用户。

#### 计算逻辑

如果一个设备\( 网站应用、APP、小程序 \)从未登录过，我们会将该设备识别为一个“用户”，此时gid为设备匿名ID；如果一个设备曾经登录过，我们会将该设备的所有行为归属于它所登录的用户ID，通过登录用户ID来唯一识别一个用户，此时gid为登录ID。

#### 常见场景

* 匿名用户首次登录后，关联用户首次登录前后产生的行为
* 用户在设备登录后，关联用户登录行为和匿名行为
* 用户跨应用使用时，关联用户多应用使用行为
* 多用户使用同一应用时，区分不同用户使用行为

### 案例

#### 案例一：关联用户匿名行为和登录行为

![](../../.gitbook/assets/image%20%28451%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x65F6;&#x95F4;</th>
      <th style="text-align:left">&#x7528;&#x6237;&#x884C;&#x4E3A;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">
        <p><b>&#x5C0F;&#x660E;</b> &#x4F7F;&#x7528;&#x6D4F;&#x89C8;&#x5668; <b>X</b> &#x672A;&#x767B;&#x9646;&#x8BBF;&#x95EE;GrowingIO&#x5B98;&#x7F51;&#x3002;</p>
        <p>SDK&#x9996;&#x6B21;&#x8BC6;&#x522B;&#x6D4F;&#x89C8;&#x5668;&#x6839;&#x636E;cookie&#x751F;&#x6210;&#x533F;&#x540D;ID
          c1&#xFF0C;&#x672A;&#x8BC6;&#x522B;&#x5230;&#x767B;&#x5F55;ID&#x3002;</p>
        <p>&#x6B64;&#x65F6;&#x6839;&#x636E;&#x533F;&#x540D;ID c1&#x751F;&#x6210;gid
          1&#xFF0C;&#x5E76;&#x5728;Event&#x8868;&#x4E2D;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;&#x7528;&#x6237;gid
          1&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">
        <p><b>&#x5C0F;&#x660E;</b> &#x4F7F;&#x7528;&#x6D4F;&#x89C8;&#x5668; <b>X</b> &#x5728;GrowingIO&#x5B98;&#x7F51;&#x767B;&#x5F55;&#x8D26;&#x6237;u1&#x3002;</p>
        <p>SDK&#x8BC6;&#x522B;&#x533F;&#x540D;ID(cookie) c1&#x548C;&#x767B;&#x5F55;ID
          u1&#x3002;</p>
        <p>&#x6B64;&#x65F6;&#x6839;&#x636E;&#x767B;&#x5F55;ID u1&#x751F;&#x6210;gid
          2&#xFF0C;&#x5E76;&#x5728;Event&#x8868;&#x4E2D;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;&#x7528;&#x6237;gid
          2&#x3002;</p>
        <p>&#x540C;&#x65F6;&#x5728;&#x865A;&#x62DF;&#x8868;(ID-Mapping)&#x8BB0;&#x5F55;
          &#x65F6;&#x523B;2 &#x533F;&#x540D;ID c1&#x548C;&#x767B;&#x5F55;ID u1&#x7684;&#x7ED1;&#x5B9A;&#x5173;&#x7CFB;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">
        <p><b>&#x5C0F;&#x660E;</b> &#x5728;&#x6D4F;&#x89C8;&#x5668; <b>X</b> &#x4E0A;&#x9000;&#x51FA;&#x767B;&#x5F55;&#xFF0C;&#x7EE7;&#x7EED;&#x6D4F;&#x89C8;GrowingIO&#x5B98;&#x7F51;&#x3002;</p>
        <p>SDK&#x8BC6;&#x522B;&#x533F;&#x540D;ID(cookie) c1&#xFF0C;&#x672A;&#x8BC6;&#x522B;&#x5230;&#x767B;&#x5F55;ID&#x3002;</p>
        <p>&#x7531;&#x4E8E;&#x8BE5;&#x8BBE;&#x5907;&#x6700;&#x540E;&#x767B;&#x5F55;ID&#x4E3A;u1&#xFF0C;&#x6B64;&#x65F6;&#x6211;&#x4EEC;&#x8BA4;&#x4E3A;&#x8BE5;&#x533F;&#x540D;&#x884C;&#x4E3A;&#x4ECD;&#x662F;u1&#x53D1;&#x751F;&#x7684;&#xFF0C;&#x56E0;&#x6B64;&#x5728;Event&#x8868;&#x4E2D;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;&#x7528;&#x6237;gid
          2&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">
        <p><b>&#x5C0F;&#x660E;</b> &#x5728;&#x6D4F;&#x89C8;&#x5668; <b>X </b>&#x4E0A;&#x672A;&#x767B;&#x5F55;&#x72B6;&#x6001;&#x4E0B;&#x7EE7;&#x7EED;&#x6D4F;&#x89C8;GrowingIO&#x5B98;&#x7F51;&#x3002;</p>
        <p>SDK&#x8BC6;&#x522B;&#x533F;&#x540D;ID(cookie) c1&#xFF0C;&#x672A;&#x8BC6;&#x522B;&#x5230;&#x767B;&#x5F55;ID&#x3002;</p>
        <p>&#x7531;&#x4E8E;&#x8BE5;&#x8BBE;&#x5907;&#x6700;&#x540E;&#x767B;&#x5F55;ID&#x4E3A;u1&#xFF0C;&#x6B64;&#x65F6;&#x6211;&#x4EEC;&#x8BA4;&#x4E3A;&#x8BE5;&#x533F;&#x540D;&#x884C;&#x4E3A;&#x4ECD;&#x662F;u1&#x53D1;&#x751F;&#x7684;&#xFF0C;&#x56E0;&#x6B64;&#x5728;Event&#x8868;&#x4E2D;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;&#x7528;&#x6237;gid
          2&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">
        <p><b>&#x5C0F;&#x7EA2;</b> &#x4F7F;&#x7528;&#x6D4F;&#x89C8;&#x5668; <b>Y</b> &#x672A;&#x767B;&#x9646;&#x8BBF;&#x95EE;GrowingIO&#x5B98;&#x7F51;&#x3002;</p>
        <p>SDK&#x9996;&#x6B21;&#x8BC6;&#x522B;&#x6D4F;&#x89C8;&#x5668;&#x6839;&#x636E;cookie&#x751F;&#x6210;&#x533F;&#x540D;ID
          c2&#xFF0C;&#x672A;&#x8BC6;&#x522B;&#x5230;&#x767B;&#x5F55;ID&#x3002;</p>
        <p>&#x6B64;&#x65F6;&#x6839;&#x636E;&#x533F;&#x540D;ID c2&#x751F;&#x6210;gid
          3&#xFF0C;&#x5E76;&#x5728;Event&#x8868;&#x4E2D;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;&#x7528;&#x6237;gid
          3&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>

查询时间：1 - 5

计算指标：活跃用户量

![](../../.gitbook/assets/image%20%28462%29.png)

第一步：虚拟表中，时间1 - 时间5根据ID-Mapping最终归因原则匹配匿名ID和登录ID的匹配关系。

* 匿名ID: c1 - 登录ID: u1 - gid: 2

第二步：Event表中，时间1 - 时间5根据Mapping关系将匿名ID生成的gid进行映射，打通首次登陆前行为和首次登陆后行为。

* gid: 1 -&gt; gid: 2

第三步：Event表中，时间1 - 时间5根据“合并后gid"计算用户量，结果为2。

#### 

#### 案例二：同一用户多应用使用时，关联用户跨应用行为

![](../../.gitbook/assets/image%20%28461%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x65F6;&#x95F4;</th>
      <th style="text-align:left">&#x7528;&#x6237;&#x884C;&#x4E3A;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x533F;&#x540D;&#x8BBF;&#x95EE;GrowingIO&#x5B98;&#x7F51;&#xFF0C;SDK&#x751F;&#x6210;&#x533F;&#x540D;ID
          c1&#x3002;</p>
        <p>&#x6B64;&#x8BBE;&#x5907;&#x9996;&#x6B21;&#x8BC6;&#x522B;&#x4E14;&#x65E0;&#x767B;&#x5F55;ID&#xFF0C;&#x6839;&#x636E;c1&#x751F;&#x6210;gid
          1&#xFF0C;&#x5E76;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          1&#x7684;&#x7528;&#x6237;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x5728;&#x5B98;&#x7F51;&#x767B;&#x5F55;&#x8D26;&#x6237;u1&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          c1 &#x548C; &#x767B;&#x5F55;ID u1&#x3002;</p>
        <p>&#x8BE5;&#x767B;&#x5F55;ID&#x9996;&#x6B21;&#x8BC6;&#x522B;&#x751F;&#x6210;gid
          2&#xFF0C;&#x5E76;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          2&#x7684;&#x7528;&#x6237;&#x3002;</p>
        <p>&#x6B64;&#x65F6;&#x8BB0;&#x5F55;&#x65F6;&#x523B;2&#x533F;&#x540D;ID c1&#x548C;&#x767B;&#x5F55;ID
          u1&#x7684;&#x7ED1;&#x5B9A;&#x5173;&#x7CFB;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x5728;&#x5B98;&#x7F51;&#x9000;&#x51FA;&#x767B;&#x5F55;&#x8BBF;&#x95EE;&#x7F51;&#x7AD9;&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          c1&#xFF0C;&#x65E0;&#x767B;&#x5F55;ID&#x3002;</p>
        <p>&#x4F46;&#x7531;&#x4E8E;&#x8BE5;&#x8BBE;&#x5907;&#x6700;&#x540E;&#x767B;&#x5F55;ID&#x4E3A;u1&#xFF0C;&#x6B64;&#x65F6;&#x6211;&#x4EEC;&#x8BA4;&#x4E3A;&#x8BE5;&#x533F;&#x540D;&#x884C;&#x4E3A;&#x4ECD;&#x662F;u1&#x53D1;&#x751F;&#x7684;&#xFF0C;&#x56E0;&#x6B64;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          2&#x7684;&#x7528;&#x6237;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x5728;&#x5B98;&#x7F51;&#x533F;&#x540D;&#x6D4F;&#x89C8;&#x4EA7;&#x54C1;&#x8BE6;&#x60C5;&#x9875;&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          c1&#xFF0C;&#x65E0;&#x767B;&#x5F55;ID&#x3002;</p>
        <p>&#x4F46;&#x7531;&#x4E8E;&#x8BE5;&#x8BBE;&#x5907;&#x6700;&#x540E;&#x767B;&#x5F55;ID&#x4E3A;u1&#xFF0C;&#x6B64;&#x65F6;&#x6211;&#x4EEC;&#x8BA4;&#x4E3A;&#x8BE5;&#x533F;&#x540D;&#x884C;&#x4E3A;&#x4ECD;&#x662F;u1&#x53D1;&#x751F;&#x7684;&#xFF0C;&#x56E0;&#x6B64;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          2&#x7684;&#x7528;&#x6237;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>Y</b> &#x4F7F;&#x7528;&#x53E6;&#x4E00;&#x4E2A;&#x6D4F;&#x89C8;&#x5668;&#x533F;&#x540D;&#x8BBF;&#x95EE;GrowingIO&#x5B98;&#x7F51;&#xFF0C;SDK&#x751F;&#x6210;&#x533F;&#x540D;ID
          c2&#x3002;</p>
        <p>&#x6B64;&#x8BBE;&#x5907;&#x9996;&#x6B21;&#x8BC6;&#x522B;&#x4E14;&#x65E0;&#x767B;&#x5F55;ID&#xFF0C;&#x6839;&#x636E;c2&#x751F;&#x6210;gid
          3&#xFF0C;&#x5E76;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          3&#x7684;&#x7528;&#x6237;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x533F;&#x540D;&#x8BBF;&#x95EE;GrowingIO App&#xFF0C;SDK&#x751F;&#x6210;&#x533F;&#x540D;ID
          IDFA&#x3002;</p>
        <p>&#x6B64;&#x8BBE;&#x5907;&#x9996;&#x6B21;&#x8BC6;&#x522B;&#x4E14;&#x65E0;&#x767B;&#x5F55;ID&#xFF0C;&#x6839;&#x636E;IDFA&#x751F;&#x6210;gid
          4&#xFF0C;&#x5E76;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          4&#x7684;&#x7528;&#x6237;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x5728;App&#x767B;&#x5F55;&#x8D26;&#x6237;u1&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          IDFA &#x548C; &#x767B;&#x5F55;ID u1&#x3002;</p>
        <p>&#x56E0;&#x4E3A;&#x8BE5;&#x767B;&#x5F55;ID&#x4E3A;&#x5DF2;&#x8BC6;&#x522B;&#x7528;&#x6237;gid
          2&#xFF0C;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid 2&#x7684;&#x7528;&#x6237;&#x3002;</p>
        <p>&#x6B64;&#x65F6;&#x8BB0;&#x5F55;&#x65F6;&#x523B;7&#x533F;&#x540D;ID IDFA&#x548C;&#x767B;&#x5F55;ID
          u1&#x7684;&#x7ED1;&#x5B9A;&#x5173;&#x7CFB;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x5728;App&#x9000;&#x51FA;&#x767B;&#x5F55;&#x8BBF;&#x95EE;&#x7F51;&#x7AD9;&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          IDFA&#xFF0C;&#x65E0;&#x767B;&#x5F55;ID&#x3002;</p>
        <p>&#x4F46;&#x7531;&#x4E8E;&#x8BE5;&#x8BBE;&#x5907;&#x6700;&#x540E;&#x767B;&#x5F55;ID&#x4E3A;u1&#xFF0C;&#x6B64;&#x65F6;&#x6211;&#x4EEC;&#x8BA4;&#x4E3A;&#x8BE5;&#x533F;&#x540D;&#x884C;&#x4E3A;&#x4ECD;&#x662F;u1&#x53D1;&#x751F;&#x7684;&#xFF0C;&#x56E0;&#x6B64;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          2&#x7684;&#x7528;&#x6237;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>

计算：时间1 - 时间7 的 用户量 是多少？

![](../../.gitbook/assets/image%20%28458%29.png)

第一步：虚拟表中，时间1 - 时间7根据ID-Mapping最终归因原则匹配匿名ID和登录ID的匹配关系。

* 匿名ID: c1 - 登录ID: u1 - gid: 2
* 匿名ID: IFDA - 登陆ID: u1 - gid: 2

第二步：Event表中，时间1 - 时间7根据Mapping关系将匿名ID生成的gid进行映射，打通首次登陆前行为和首次登陆后行为。

* gid: 1 -&gt; gid: 2
* gid: 4 -&gt; gid: 2

第三步：Event表中，时间1 - 时间7根据“合并后gid"计算用户量，结果为2。

> 活跃用户量为2，包含gid 2\( u1, c1, IDFA \) 和 gid 3\( c2 \)
>
> 实际访问设备数为3，包含浏览器设备c1、c2和App设备IDFA
>
> 实际登陆用户数为1，包含登陆用户ID u1



#### 案例三：同一应用多用户使用时，区分不同用户使用行为

![](../../.gitbook/assets/image%20%28450%29.png)

操作步骤如下：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x65F6;&#x95F4;</th>
      <th style="text-align:left">&#x7528;&#x6237;&#x884C;&#x4E3A;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x533F;&#x540D;&#x8BBF;&#x95EE;GrowingIO&#x5B98;&#x7F51;&#xFF0C;SDK&#x751F;&#x6210;&#x533F;&#x540D;ID
          cookie&#x3002;</p>
        <p>&#x6B64;&#x8BBE;&#x5907;&#x9996;&#x6B21;&#x8BC6;&#x522B;&#x4E14;&#x65E0;&#x767B;&#x5F55;ID&#xFF0C;&#x6839;&#x636E;cookie&#x751F;&#x6210;gid
          1&#xFF0C;&#x5E76;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          1&#x7684;&#x7528;&#x6237;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x5728;&#x5B98;&#x7F51;&#x767B;&#x5F55;&#x8D26;&#x6237;u1&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          cookie &#x548C; &#x767B;&#x5F55;ID u1&#x3002;</p>
        <p>&#x8BE5;&#x767B;&#x5F55;ID&#x9996;&#x6B21;&#x8BC6;&#x522B;&#x751F;&#x6210;gid
          2&#xFF0C;&#x5E76;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          2&#x7684;&#x7528;&#x6237;&#x3002;</p>
        <p>&#x6B64;&#x65F6;&#x8BB0;&#x5F55;&#x65F6;&#x523B;2&#x533F;&#x540D;ID cookie&#x548C;&#x767B;&#x5F55;ID
          u1&#x7684;&#x7ED1;&#x5B9A;&#x5173;&#x7CFB;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x5728;&#x5B98;&#x7F51;&#x9000;&#x51FA;&#x767B;&#x5F55;&#x8BBF;&#x95EE;&#x7F51;&#x7AD9;&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          cookie&#xFF0C;&#x65E0;&#x767B;&#x5F55;ID&#x3002;</p>
        <p>&#x4F46;&#x7531;&#x4E8E;&#x8BE5;&#x8BBE;&#x5907;&#x6700;&#x540E;&#x767B;&#x5F55;ID&#x4E3A;u1&#xFF0C;&#x6B64;&#x65F6;&#x6211;&#x4EEC;&#x8BA4;&#x4E3A;&#x8BE5;&#x533F;&#x540D;&#x884C;&#x4E3A;&#x4ECD;&#x662F;u1&#x53D1;&#x751F;&#x7684;&#xFF0C;&#x56E0;&#x6B64;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          2&#x7684;&#x7528;&#x6237;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>Y</b> &#x4F7F;&#x7528;&#x76F8;&#x540C;&#x6D4F;&#x89C8;&#x5668;&#x8BBF;&#x95EE;GrowingIO&#x5B98;&#x7F51;&#xFF0C;&#x767B;&#x5F55;&#x8D26;&#x6237;u2&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          cookie&#xFF0C;&#x767B;&#x5F55;ID u2&#x3002;</p>
        <p>&#x8BE5;&#x767B;&#x5F55;ID&#x9996;&#x6B21;&#x8BC6;&#x522B;&#x751F;&#x6210;gid
          3&#xFF0C;&#x5E76;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          3&#x7684;&#x7528;&#x6237;&#x3002;</p>
        <p>&#x6B64;&#x65F6;&#x8BB0;&#x5F55;&#x65F6;&#x523B;4&#x533F;&#x540D;ID cookie&#x548C;&#x767B;&#x5F55;ID
          u2&#x7684;&#x7ED1;&#x5B9A;&#x5173;&#x7CFB;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>Y</b> &#x5728;&#x5B98;&#x7F51;&#x9000;&#x51FA;&#x767B;&#x5F55;&#x8BBF;&#x95EE;&#x7F51;&#x7AD9;&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          cookie&#xFF0C;&#x65E0;&#x767B;&#x5F55;ID&#x3002;</p>
        <p>&#x4F46;&#x7531;&#x4E8E;&#x8BE5;&#x8BBE;&#x5907;&#x6700;&#x540E;&#x767B;&#x5F55;ID&#x4E3A;u2&#xFF0C;&#x6B64;&#x65F6;&#x6211;&#x4EEC;&#x8BA4;&#x4E3A;&#x8BE5;&#x533F;&#x540D;&#x884C;&#x4E3A;&#x4ECD;&#x662F;u2&#x53D1;&#x751F;&#x7684;&#xFF0C;&#x56E0;&#x6B64;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          3&#x7684;&#x7528;&#x6237;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x533F;&#x540D;&#x8BBF;&#x95EE;GrowingIO App&#xFF0C;SDK&#x751F;&#x6210;&#x533F;&#x540D;ID
          IDFA&#x3002;</p>
        <p>&#x6B64;&#x8BBE;&#x5907;&#x9996;&#x6B21;&#x8BC6;&#x522B;&#x4E14;&#x65E0;&#x767B;&#x5F55;ID&#xFF0C;&#x6839;&#x636E;IDFA&#x751F;&#x6210;gid
          4&#xFF0C;&#x5E76;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          4&#x7684;&#x7528;&#x6237;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x5728;App&#x767B;&#x5F55;&#x8D26;&#x6237;u1&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          IDFA &#x548C; &#x767B;&#x5F55;ID u1&#x3002;</p>
        <p>&#x56E0;&#x4E3A;&#x8BE5;&#x767B;&#x5F55;ID&#x4E3A;&#x5DF2;&#x8BC6;&#x522B;&#x7528;&#x6237;gid
          2&#xFF0C;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid 2&#x7684;&#x7528;&#x6237;&#x3002;</p>
        <p>&#x6B64;&#x65F6;&#x8BB0;&#x5F55;&#x65F6;&#x523B;7&#x533F;&#x540D;ID IDFA&#x548C;&#x767B;&#x5F55;ID
          u1&#x7684;&#x7ED1;&#x5B9A;&#x5173;&#x7CFB;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x4F7F;&#x7528;&#x8BBE;&#x5907;cookie&#x533F;&#x540D;&#x8BBF;&#x95EE;GrowingIO&#x5B98;&#x7F51;&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          cookie&#xFF0C;&#x65E0;&#x767B;&#x5F55;ID&#x3002;</p>
        <p>&#x4F46;&#x7531;&#x4E8E;&#x8BE5;&#x8BBE;&#x5907;&#x6700;&#x540E;&#x767B;&#x5F55;ID&#x4E3A;u2&#xFF0C;&#x6B64;&#x65F6;&#x6211;&#x4EEC;&#x8BA4;&#x4E3A;&#x8BE5;&#x533F;&#x540D;&#x884C;&#x4E3A;&#x4ECD;&#x662F;u2&#x53D1;&#x751F;&#x7684;&#xFF0C;&#x56E0;&#x6B64;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          3&#x7684;&#x7528;&#x6237;&#x3002;</p>
        <p>( &#x6B64;&#x65F6;&#x8BB0;&#x5F55;&#x4F7F;&#x7528;&#x7528;&#x6237;&#x4E3A;gid
          3 &#x5373;&#x7528;&#x6237; <b>Y</b> &#xFF0C;&#x4F46;&#x5B9E;&#x9645;&#x4F7F;&#x7528;&#x7528;&#x6237;&#x662F;gid
          2 &#x5373;&#x7528;&#x6237; <b>X</b> )</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">9</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x5728;&#x5B98;&#x7F51;&#x767B;&#x5F55;&#x8D26;&#x6237;u1&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          cookie &#x548C; &#x767B;&#x5F55;ID u1&#x3002;</p>
        <p>&#x56E0;&#x4E3A;&#x8BE5;&#x767B;&#x5F55;ID&#x4E3A;&#x5DF2;&#x8BC6;&#x522B;&#x7528;&#x6237;gid
          2&#xFF0C;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid 2&#x7684;&#x7528;&#x6237;&#x3002;</p>
        <p>&#x6B64;&#x65F6;&#x8BB0;&#x5F55;&#x65F6;&#x523B;9&#x533F;&#x540D;ID cookie&#x548C;&#x767B;&#x5F55;ID
          u1&#x7684;&#x7ED1;&#x5B9A;&#x5173;&#x7CFB;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">10</td>
      <td style="text-align:left">
        <p>&#x7528;&#x6237; <b>X</b> &#x5728;&#x5B98;&#x7F51;&#x9000;&#x51FA;&#x767B;&#x5F55;&#x8BBF;&#x95EE;&#x7F51;&#x7AD9;&#xFF0C;&#x6B64;&#x65F6;SDK&#x8BB0;&#x5F55;&#x533F;&#x540D;ID
          cookie&#xFF0C;&#x65E0;&#x767B;&#x5F55;ID&#x3002;</p>
        <p>&#x4F46;&#x7531;&#x4E8E;&#x8BE5;&#x8BBE;&#x5907;&#x6700;&#x540E;&#x767B;&#x5F55;ID&#x4E3A;u1&#xFF0C;&#x6B64;&#x65F6;&#x6211;&#x4EEC;&#x8BA4;&#x4E3A;&#x8BE5;&#x533F;&#x540D;&#x884C;&#x4E3A;&#x4ECD;&#x662F;u1&#x53D1;&#x751F;&#x7684;&#xFF0C;&#x56E0;&#x6B64;&#x8BB0;&#x5F55;&#x8BE5;&#x4E8B;&#x4EF6;&#x5C5E;&#x4E8E;gid
          2&#x7684;&#x7528;&#x6237;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>

计算：时间1 - 时间8 的 用户量 是多少？

![](../../.gitbook/assets/image%20%28455%29.png)

第一步：时间1 - 时间8虚拟表中根据ID-Mapping最终归因原则匹配匿名ID和登录ID的匹配关系。

* 匿名ID: cookie - 登录ID: u2 - gid: 3
* 匿名ID: IDFA - 登录ID: u1 - gid: 2

第二步：在Event表中，根据Mapping关系将匿名ID生成的gid进行映射，打通首次登陆前行为和首次登陆后行为。

* gid: 1 -&gt; gid: 3
* gid: 4 -&gt; gid: 2

第三步：时间1 - 时间8根据“合并后gid"计算用户量，结果为2。

> 活跃用户量为2，包含gid 2和gid 3
>
> 实际访问设备数为2，包含浏览器设备cookie和App设备IDFA
>
> 实际登陆用户数为2，包含登陆用户ID u1、u2

