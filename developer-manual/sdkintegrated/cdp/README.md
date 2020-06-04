# 数据采集 SDK

## 简介

SDK支持采集的事件类型：

| SDK类型 | VISIT\(访问\) | User\(用户变量\) | CUSTOM\_EVEN\(自定义事件\) |
| :--- | :--- | :--- | :--- |
| JS | ✅ | ✅ | ✅ |
| Android | ✅ | ✅ | ✅ |
| iOS | ✅ | ✅ | ✅ |
| Java |  | ✅ | ✅ |
| 小程序 | ✅ | ✅ | ✅ |

## 采集字段信息

* VISIT事件中的字段：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5B57;&#x6BB5;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5B57;&#x6BB5;&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">anonymous</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>&#x8BBF;&#x95EE;&#x7528;&#x6237;ID&#x3002;</p>
        <p>&#x793A;&#x4F8B;&#xFF1A;7196f014-d7bc-4bd8-b920-757cb2375ff6</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">project_key</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>GrowingIO&#x4E0B;&#x7684;&#x9879;&#x76EE;ID&#x3002;</p>
        <p>&#x793A;&#x4F8B;&#xFF1A;0a1b4118dd954ec3bcc69da5138bdb96</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">user_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x767B;&#x5F55;&#x7528;&#x6237;ID&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">gio_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">GrowingIO&#x7EDF;&#x8BA1;&#x4F7F;&#x7528;&#x7F16;&#x53F7;&#xFF0C;&#x4E0A;&#x4E00;&#x4E2A;&#x767B;&#x5F55;&#x7528;&#x6237;&#x7684;user_id&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">timestamp</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">&#x6570;&#x636E;&#x4EA7;&#x751F;&#x7684;&#x65F6;&#x95F4;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">esid</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">&#x8BF7;&#x6C42;&#x7F16;&#x53F7;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">session</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBF;&#x95EE;ID&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x7C7B;&#x578B;&#x3002;&#x793A;&#x4F8B;&#xFF1A;VISIT</td>
    </tr>
    <tr>
      <td style="text-align:left">version</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>SDK&#x7248;&#x672C;&#x3002;</p>
        <p>&#x793A;&#x4F8B;&#xFF1A;T8989_gandroid_uc0.7_6bdd1b54</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">data_source_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x6570;&#x636E;&#x6E90;ID&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">ip</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">ipv4&#x5730;&#x5740;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">context</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">&#x8BF7;&#x8BE6;&#x89C1;context&#x4E2D;&#x5305;&#x542B;&#x7684;&#x5B57;&#x6BB5;&#x3002;</td>
    </tr>
  </tbody>
</table>

| context中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| app | object | 请详见App中包含的字段解释。 |
| device | object | 请详见device中包含的字段解释。 |
| screen | object | 请详见screen中包含的字段解释。 |
| operationSystem | object | 请详见operationSystem中包含的字段解释。 |
| page | object | 请详见page中包含的字段解释。 |
| referrer | object | 请详见referrer中包含的字段解释。 |
| location | object | 请详见location中包含的字段解释。 |
| network | object | 请详见network中包含的字段解释。 |
| locale | object | 请详见locale中包含的字段解释。 |

| App中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| id | string | AppId。 |
| name | string | App名称。 |
| package | string | App包名。 |
| version | string | App版本号。 |
| url\_schema | string | url元信息。 |
| user\_agent | string | user agent。 |
| channel | string | 渠道信息。 |

<table>
  <thead>
    <tr>
      <th style="text-align:left">device&#x4E2D;&#x5305;&#x542B;&#x7684;&#x5B57;&#x6BB5;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">brand</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBE;&#x5907;&#x54C1;&#x724C;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">model</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBE;&#x5907;&#x578B;&#x53F7;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">platform</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5E73;&#x53F0;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">
        <p>&#x8BBE;&#x5907;&#x7C7B;&#x578B;&#xFF0C;&#x7528;&#x4E8E;&#x533A;&#x5206;&#x5E73;&#x677F;&#x548C;&#x624B;&#x673A;&#x3002;</p>
        <p>0&#x6807;&#x8BC6;&#x5E73;&#x677F;&#xFF1B;</p>
        <p>1&#x6807;&#x8BC6;&#x624B;&#x673A;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>

| screen中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| width | int | 屏幕宽度。 |
| height | int | 屏幕高度。 |
| density | int | 屏幕密度。 |
| orientation | enum | 屏幕方向。 |

| operationSystem中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| name | string | 操作系统名称。 |
| version | string | 操作系统版本。 |

| page中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| domain | string | 访问页面域名。 |
| path | string | 访问页面路径。 |
| query | string | 请求参数。 |
| title | string | 访问页面标题。 |

| referrer中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| from | string | 访问来源。 |

| location中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| longitude | double | 纬度。非自动采集，需要您调用接口设置经纬度才会上传。 |
| latitude | double | 经度。非自动采集，需要您调用接口设置经纬度才会上传。 |

| network中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| type | string | 网络类型。 |
| carrier | string | 网络载体。 |

| locale中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| language | string | 获取的页面语言。 |
| timezone | string | 时区。 |

* User事件中包含的字段：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5B57;&#x6BB5;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">anonymous</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>&#x8BBF;&#x95EE;&#x7528;&#x6237;ID&#x3002;</p>
        <p>&#x793A;&#x4F8B;&#xFF1A;7196f014-d7bc-4bd8-b920-757cb2375ff6</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">project_key</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>GrowingIO&#x4E0B;&#x7684;&#x9879;&#x76EE;ID&#x3002;</p>
        <p>&#x793A;&#x4F8B;&#xFF1A;0a1b4118dd954ec3bcc69da5138bdb96</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">user_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x767B;&#x5F55;&#x7528;&#x6237;ID&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">gio_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">GrowingIO&#x7EDF;&#x8BA1;&#x4F7F;&#x7528;&#x7F16;&#x53F7;&#xFF0C;&#x4E0A;&#x4E00;&#x4E2A;&#x767B;&#x5F55;&#x7528;&#x6237;&#x7684;user_id&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">Timestamp</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">&#x6570;&#x636E;&#x4EA7;&#x751F;&#x7684;&#x65F6;&#x95F4;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">esid</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">&#x8BF7;&#x6C42;&#x7F16;&#x53F7;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">session</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBF;&#x95EE;ID&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">attributes</td>
      <td style="text-align:left">map&lt;string,string&gt;</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x53D8;&#x91CF;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">send_time</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">&#x6570;&#x636E;&#x53D1;&#x9001;&#x51FA;&#x6765;&#x7684; &#x65F6;&#x95F4;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">data_source_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x6570;&#x636E;&#x6765;&#x6E90;ID&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">profile</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">&#x8BF7;&#x8BE6;&#x89C1;profile&#x4E2D;&#x5305;&#x542B;&#x7684;&#x5B57;&#x6BB5;&#x89E3;&#x91CA;&#x3002;</td>
    </tr>
  </tbody>
</table>

| profile中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| basic | object | 请详见basic中包含的字段解释。 |
| device | object | 请详见device中包含字段解释。 |
| wechat | object | 请详见wechat中包含的字段解释。 |
| alipay | object | 请详见alipay中包含的字段解释。 |

| basic中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| name | string | 姓名。 |
| createdAt | Timestamp | 创建时间。 |
| birthday | Timestamp | 出生日期。 |
| mobile | string | 手机号。 |
| email | string | 邮箱号。 |
| gender | enum | 性别。 |
| addresses | Array\[string\] | 通讯地址。 |

| device中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| android\_id | string | Android ID。 |
| idfa | string | IDFA |
| idfv | string | IDFV |
| imei | string | IMEI |

| wechat中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| open\_id | string | 微信的OPEN\_ID |
| union\_id | string | 微信的UNION\_ID |
| nick\_name | string | 微信昵称 |
| avatar\_url | string | 微信头像url |
| gender | string | 微信性别 |
| country | string | 微信国家 |
| province | string | 微信省份 |
| city | string | 微信城市 |
| language | string | 微信语言 |
| subscribe\_list | \[Array\] | 微信订阅号 |

| alipay中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| user\_id | string | 支付宝-用户ID |
| avatar | string | 支付宝-头像 |
| province | string | 支付宝-省份 |
| city | string | 支付宝-城市 |
| nick\_name | string | 支付宝-昵称 |
| is\_student\_certified | bool | 支付宝-是否学生认证 |
| user\_type | string | 支付宝-用户类型 |
| user\_status | string | 支付宝-用户状态 |
| is\_certified | bool | 支付宝-是否身份认证 |
| gender | string | 支付宝-性别 |

* CUSTOM\_EVENT中包含的字段：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5B57;&#x6BB5;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">anonymous</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>&#x8BBF;&#x95EE;&#x7528;&#x6237;ID&#x3002;</p>
        <p>&#x793A;&#x4F8B;&#xFF1A;7196f014-d7bc-4bd8-b920-757cb2375ff6</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">project_key</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>GrowingIO&#x4E0B;&#x7684;&#x9879;&#x76EE;ID&#x3002;</p>
        <p>&#x793A;&#x4F8B;&#xFF1A;0a1b4118dd954ec3bcc69da5138bdb96</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">user_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x767B;&#x5F55;&#x7528;&#x6237;ID&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">gio_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">GrowingIO&#x7EDF;&#x8BA1;&#x4F7F;&#x7528;&#x7F16;&#x53F7;&#xFF0C;&#x662F;&#x4E0A;&#x4E00;&#x4E2A;&#x767B;&#x5F55;&#x7528;&#x6237;&#x7684;user_id&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">timestamp</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">&#x6570;&#x636E;&#x4EA7;&#x751F;&#x7684;&#x65F6;&#x95F4;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">esid</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">&#x8BF7;&#x6C42;&#x7F16;&#x53F7;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">session</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBF;&#x95EE;ID&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">event_key</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x57CB;&#x70B9;&#x4E8B;&#x4EF6;&#x552F;&#x4E00;&#x6807;&#x8BC6;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x7C7B;&#x578B;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">data_source_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x6570;&#x636E;&#x6765;&#x6E90;ID&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">attributes</td>
      <td style="text-align:left">map&lt;string,string&gt;</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x53D8;&#x91CF;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">event_num</td>
      <td style="text-align:left">double</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x5BF9;&#x5E94;&#x7684;&#x6570;&#x503C;&#xFF0C;&#x975E;&#x6570;&#x503C;&#x7C7B;&#x578B;&#x65F6;&#x53EF;&#x4E0D;&#x586B;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">send_time</td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">&#x6570;&#x636E;&#x53D1;&#x9001;&#x51FA;&#x6765;&#x7684;&#x65F6;&#x95F4;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">context</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">&#x8BF7;&#x8BE6;&#x89C1;context&#x4E2D;&#x5305;&#x542B;&#x7684;&#x5B57;&#x6BB5;&#x89E3;&#x91CA;&#x3002;</td>
    </tr>
  </tbody>
</table>

| context中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| page | object | 请详见page中包含的字段解释。 |
| referrer | object | 请详见referrer中包含的字段解释。 |
| network | object | 请详见network中包含的字段解释。 |

| page中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| domain | string | 访问页面域名。 |
| path | string | 访问页面路径。 |
| query | string | 请求参数。 |
| title | string | 访问页面标题。 |

| referrer中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| from | string | 访问来源。 |

| network中包含的字段 | 类型 | 说明 |
| :--- | :--- | :--- |
| type | string | 网络类型。 |
| carrier | string | 网络载体。 |



