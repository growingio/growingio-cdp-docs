# 数据模型

## 简介

<<<<<<< HEAD
GrowingIO采集的原始行为数据分为四种不同类型，分别为访问\(visit\)、页面\(page\)、埋点\(custom\_event\)和行为\(action\)。

* 访问\(visit\): 代表用户开启了一个新的访问会话，访问行为的生命周期与会话（session）绑定，新的session代表一个新的访问。
* 页面浏览\(page\): 代表用户的一次页面浏览，SDK采集以及发送浏览事件中的数据。
* 埋点\(custom\_event\): 代表用户触发了客户埋的点发送的事件。事件触发的时间以及发送的行为数据信息都由客户指定。
* 行为\(action\): 代表用户操作了页面上的某些元素发送的行为，包括点击了按钮，修改了数据框的内容等等。

过去，GrowingIO数据平台将上述四种行为数据存储至多张Hive表中，这种模型导致后续的统计逻辑非常复杂。为了串联多种行为数据，我们在查询时进行了多表关联计算，因此导致部分极端场景下数据计算结果不一致的问题偶有发生。另外，该种数据模型数据比较分散，没有统一的接口，不易与其他组件对接。

在[9.0版本](../../update-log.md#v-2020-9-0-2020-nian-9-yue-30-ri-fa-bu)后，我们将多种行为数据统一抽象为EVENT模型，即四种行为数据统一到一张表中。该种模型简化了平台计算逻辑，并且通过Thrift Server方便GrowingIO数据平台与其他组件进行对接，进而提升开发效率和降低维护成本。

最新的数据模型同时具备了提供实时数据的能力，行为数据从触点触发再到客户可以观察到，时间间隔可以缩小到5 ～ 10秒钟。
=======
GrowingIO采集的原始行为数据分为四种不同类型，分别为访问（visit）、页面（page）、埋点（custom\_event）和行为（action）。

* 访问（visit）： 代表用户开启了一个新的访问会话，访问行为的生命周期与会话（session）绑定，新的session代表一个新的访问。
* 页面浏览（page）：代表用户的一次页面浏览，SDK采集以及发送浏览事件中的数据。
* 埋点（custom\_event）： 代表用户触发了客户埋的点发送的事件。事件触发的时间以及发送的行为数据信息都由客户指定。
* 行为（action）： 代表用户操作了页面上的某些元素发送的行为，包括点击了按钮、修改了数据框的内容等等。

过去，GrowingIO数据平台将上述四种行为数据存储至多张表中，这种模型导致后续的统计逻辑非常复杂。为了串联多种行为数据，我们在查询时进行了多表关联计算，因此导致部分极端场景下数据计算结果不一致的问题偶有发生。另外，该种数据模型数据比较分散，没有统一的接口，不易与其他组件进行对接。

在[9.0版本](../../update-log.md#v-2020-9-0-2020-nian-9-yue-30-ri-fa-bu)后，我们将多种行为数据统一抽象为EVENT模型，即四种行为数据统一到一张表中。该种模型简化了平台计算逻辑，并且通过Thrift Server方便GrowingIO数据平台与其他组件进行对接，进而提升开发效率和降低维护成本。

最新的数据模型同时具备了提供实时数据的能力，行为数据从触点触发再到客户可以观察到，时间间隔可以缩小到5 - 10秒钟。
>>>>>>> 14.3.0-beta

## 客户操作手册

GrowingIO CDP为客户安装了Zeppelin，客户可以通过Zeppelin SQL解释器查询数据平台中的数据库、数据表和表中数据。

<<<<<<< HEAD
SQL语法：
=======
**SQL语法：**
>>>>>>> 14.3.0-beta

查询所有的数据库：show databases

查询数据库中的数据表：show tables in {database\_name}

查询数据表结构：desc {database\_name}.{table\_name}

查询数据表分区： show partitions {database\_name}.{table\_name}

查询数据表数据： select {field} from {database\_name}.{table\_name}

<<<<<<< HEAD
数据表：

行为模型：CARBON.EVENT\_LOG

查询时请使用时间和类型分区加速查询速度。如需查询当前小时实时数据，可查询 HBASE 表，表名为 EVENT\_BUFFER\_SECOND\_{day}\_{hour} ，比如北京时间 2020.10.1 上午 8点，对应的是 EVENT\_BUFFER\_SECOND\_2020100100。

用户属性模型：USER\_PROPS

物品模型：CARBON.ITEM

标签模型：TAG\_RULE\_RESULTS\(标签角度\)、USER\_TAG\_RULE\_VALUES（用户角度）

## 行为模型\(Event\)
=======
## **数据表**

事件表：event

用户表：user

用户融合表：user\_merged

## 事件表（event）：

GrowingIO系统实时采集或批量导入的行为数据，统一存放在event表中。该表为日期分区表，数据时效性为实时，即行为数据从触发到入库可查的时间一般在10秒内。

在该表中，您可以查询事件采集上报的全部信息。由于字段繁多，通过前缀将不同角度的字段分组，以避免字段冲突并提升查询体验，共分三组，它们都一张在事件表里：

* 事件标识符、发生时间、用户ID等[基础信息](./#ji-chu-xin-xi)，字段无前缀
* 城市、浏览器、设备类型等[预定义属性](./#yu-ding-yi-shu-xing)，字段统一使用 $ 符号前缀
* 埋点上报的[自定义属性](./#zi-ding-yi-shu-xing)，字段统一使用 var\_ 作为前缀

### 数据字段

#### 基础信息

| 字段名 | 字段类型 | 含义及示例 |
| :--- | :--- | :--- |
| event\_key | String | 事件标识符。visit事件$visit、访问事件$page、自定义事件如paySuccess |
| event\_type | String | 事件类型。示例：visit、page、custom\_event |
| event\_time | DateTime\(3\) | 事件发生时间，毫秒。示例：2021-06-01 23:59:20.912 |
| event\_id | String | 事件ID |
| anonymous\_user | String | 访问用户ID（SDK自动采集） |
| user | String | 登录用户ID（未上报则记为访问用户） |
| user\_type | String | 用户的账号体系类型。示例：login\_user、visit\_user |
| gio\_id | UInt | id-service生成的识别用户的唯一编号 |
| session | String | 访问标识 |
| account\_id | String | 项目ID |
| dt | Date | 日期分区。示例：2021-06-01 |

#### 预定义属性
>>>>>>> 14.3.0-beta

<table>
  <thead>
    <tr>
<<<<<<< HEAD
      <th style="text-align:left"><b>&#x539F;&#x59CB;&#x6570;&#x636E;&#x5B57;&#x6BB5;</b>
      </th>
      <th style="text-align:left"><b>&#x7C7B;&#x578B;</b>
      </th>
      <th style="text-align:left"><b>&#x5907;&#x6CE8;</b>
      </th>
=======
      <th style="text-align:left">&#x5B57;&#x6BB5;&#x540D;</th>
      <th style="text-align:left">&#x5B57;&#x6BB5;&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x542B;&#x4E49;&#x53CA;&#x793A;&#x4F8B;</th>
>>>>>>> 14.3.0-beta
    </tr>
  </thead>
  <tbody>
    <tr>
<<<<<<< HEAD
      <td style="text-align:left">event_key</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x6807;&#x8BC6;&#x7B26;&#xFF1A; &#x8BBF;&#x95EE;&#x4E8B;&#x4EF6;
        &#x2192; $visit&#xFF0C;&#x9875;&#x9762;&#x4E8B;&#x4EF6; &#x2192; $page&#xFF0C;&#x57CB;&#x70B9;&#x4E8B;&#x4EF6;
        &#x2192; &#x57CB;&#x70B9;&#x4E8B;&#x4EF6;&#x6807;&#x8BC6;&#x7B26;</td>
    </tr>
    <tr>
      <td style="text-align:left">event_time</td>
      <td style="text-align:left">bigint</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x63A5;&#x6536;&#x65F6;&#x95F4;: &#x670D;&#x52A1;&#x7AEF;&#x63A5;&#x6536;&#x65F6;&#x95F4;&#x4E3A;&#x51C6;&#xFF0C;&#x7CBE;&#x786E;&#x5230;&#x6BEB;&#x79D2;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">event_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x552F;&#x4E00;&#x6807;&#x8BC6;&#x7B26;&#xFF1A;GrowingIO&#x7CFB;&#x7EDF;&#x751F;&#x6210;&#xFF0C;&#x4E0D;&#x540C;&#x4E8B;&#x4EF6;&#x7C7B;&#x578B;&#x751F;&#x6210;id&#x903B;&#x8F91;&#x4E0D;&#x540C;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">event_type</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x7C7B;&#x578B;&#xFF1A;visit&#x3001;page&#x3001;custom_event</td>
    </tr>
    <tr>
      <td style="text-align:left">client_time</td>
      <td style="text-align:left">bigint</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x53D1;&#x751F;&#x65F6;&#x95F4;&#xFF1A;&#x7CBE;&#x786E;&#x5230;&#x6BEB;&#x79D2;</td>
    </tr>
    <tr>
      <td style="text-align:left">anonymous_user</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBF;&#x95EE;&#x7528;&#x6237;&#x6807;&#x8BC6;&#x7B26;</td>
    </tr>
    <tr>
      <td style="text-align:left">user</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x7528;&#x6237;&#x6807;&#x8BC6;&#x7B26;&#xFF1A;&#x5982;&#x679C;&#x767B;&#x5F55;&#x7528;&#x6237;&#x4E3A;&#x7A7A;&#xFF0C;&#x5219;&#x4E3A;&#x8BBF;&#x95EE;&#x7528;&#x6237;&#xFF0C;&#x5426;&#x5219;&#x4E3A;&#x767B;&#x5F55;&#x7528;&#x6237;</td>
    </tr>
    <tr>
      <td style="text-align:left">user_type</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x7528;&#x6237;&#x7C7B;&#x578B;&#xFF1A;&#x6807;&#x8BC6;user&#x5BF9;&#x5E94;&#x7684;&#x662F;&#x767B;&#x5F55;&#x7528;&#x6237;&#x8FD8;&#x662F;&#x8BBF;&#x95EE;&#x7528;&#x6237;</td>
    </tr>
    <tr>
      <td style="text-align:left">user_id</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">&#x7528;&#x6237;&#xFF1A;&#x767B;&#x5F55;&#x7528;&#x6237;&#x3001;&#x8BBF;&#x95EE;&#x7528;&#x6237;&#x751F;&#x6210;&#x7684;ID</td>
    </tr>
    <tr>
      <td style="text-align:left">user_session</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBF;&#x95EE;&#x4F1A;&#x8BDD;&#x6807;&#x8BC6;&#x7B26;</td>
    </tr>
    <tr>
      <td style="text-align:left">account_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x9879;&#x76EE;&#x6807;&#x8BC6;&#x7B26;: &#x901A;&#x8FC7; url &#x8DEF;&#x5F84;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">platform</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x53D1;&#x9001;&#x5E73;&#x53F0;</td>
    </tr>
    <tr>
      <td style="text-align:left">domain</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x5E94;&#x7528;&#x57DF;&#x540D;</td>
    </tr>
    <tr>
      <td style="text-align:left">referrer_domain</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBF;&#x95EE;&#x6765;&#x6E90;&#x57DF;&#x540D;</td>
    </tr>
    <tr>
      <td style="text-align:left">ip</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">IP&#x5730;&#x5740;&#xFF0C;&#x901A;&#x8FC7; http &#x8BF7;&#x6C42;&#x81EA;&#x52A8;&#x83B7;&#x53D6;</td>
    </tr>
    <tr>
      <td style="text-align:left">utm_source</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5E7F;&#x544A;&#x6765;&#x6E90;&#xFF1A;utm&#x6240;&#x6709;&#x5B57;&#x6BB5;&#x4ECE;query&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">utm_medium</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5E7F;&#x544A;&#x5A92;&#x4ECB;&#xFF1A;utm&#x6240;&#x6709;&#x5B57;&#x6BB5;&#x4ECE;query&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">utm_campaign</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5E7F;&#x544A;&#x540D;&#x79F0;&#xFF1A;utm&#x6240;&#x6709;&#x5B57;&#x6BB5;&#x4ECE;query&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">utm_term</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5E7F;&#x544A;&#x5173;&#x952E;&#x5B57;&#xFF1A;utm&#x6240;&#x6709;&#x5B57;&#x6BB5;&#x4ECE;query&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">utm_content</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5E7F;&#x544A;&#x5185;&#x5BB9;&#xFF1A;utm&#x6240;&#x6709;&#x5B57;&#x6BB5;&#x4ECE;query&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">key_word</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x641C;&#x7D22;&#x5173;&#x952E;&#x5B57;&#xFF1A;&#x4ECE;query&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">country_code</td>
      <td style="text-align:left">stirng</td>
      <td style="text-align:left">&#x56FD;&#x5BB6;&#x4EE3;&#x7801;&#xFF1A;&#x5730;&#x7406;&#x4F4D;&#x7F6E;&#x4FE1;&#x606F;&#x4ECE;ip/gps(lat,
        lng)&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">country_name</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x56FD;&#x5BB6;&#x540D;&#x79F0;&#xFF1A;&#x5730;&#x7406;&#x4F4D;&#x7F6E;&#x4FE1;&#x606F;&#x4ECE;ip/gps(lat,
        lng)&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">region</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x7701;&#x4EFD;: &#x5730;&#x7406;&#x4F4D;&#x7F6E;&#x4FE1;&#x606F;&#x4ECE;ip/gps(lat,
        lng)&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">city</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x57CE;&#x5E02;: &#x5730;&#x7406;&#x4F4D;&#x7F6E;&#x4FE1;&#x606F;&#x4ECE;ip/gps(lat,
        lng)&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">user_agent</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5BA2;&#x6237;&#x7AEF;&#x4FE1;&#x606F;&#xFF1A;&#x901A;&#x8FC7; http
        &#x8BF7;&#x6C42;&#x81EA;&#x52A8;&#x83B7;&#x53D6;</td>
    </tr>
    <tr>
      <td style="text-align:left">browser</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x6D4F;&#x89C8;&#x5668; &#xFF1A;&#x4ECE;user_agent&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">browser_version</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x6D4F;&#x89C8;&#x5668;&#x7248;&#x672C;&#xFF1A; &#x4ECE;user_agent&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">os</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x64CD;&#x4F5C;&#x7CFB;&#x7EDF;&#xFF1A;&#x79FB;&#x52A8;&#x7AEF;&#x901A;&#x8FC7;
        SDK &#x4E0A;&#x4F20;&#xFF0C;web &#x7AEF;&#x4ECE;user_agent&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">os_version</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x64CD;&#x4F5C;&#x7CFB;&#x7EDF;&#x7248;&#x672C;&#xFF1A;&#x79FB;&#x52A8;&#x7AEF;&#x901A;&#x8FC7;
        SDK &#x4E0A;&#x4F20;&#xFF0C;web &#x7AEF;&#x4ECE;user_agent&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">client_version</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5BA2;&#x6237;&#x7AEF;&#x7248;&#x672C;</td>
    </tr>
    <tr>
      <td style="text-align:left">channel</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x6E20;&#x9053;&#x6765;&#x6E90;</td>
    </tr>
    <tr>
      <td style="text-align:left">devcie_brand</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBE;&#x5907;&#x54C1;&#x724C;&#xFF1A;&#x79FB;&#x52A8;&#x7AEF;&#x901A;&#x8FC7;
        SDK &#x4E0A;&#x4F20;&#xFF0C;web &#x7AEF;&#x4ECE;user_agent&#x4E2D;&#x89E3;&#x6790;</td>
    </tr>
    <tr>
      <td style="text-align:left">device_model</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBE;&#x5907;&#x578B;&#x53F7;</td>
    </tr>
    <tr>
      <td style="text-align:left">device_type</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBE;&#x5907;&#x7C7B;&#x578B;</td>
    </tr>
    <tr>
      <td style="text-align:left">deivce_orientation</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BBE;&#x5907;&#x65B9;&#x5411;</td>
    </tr>
    <tr>
      <td style="text-align:left">screen_height</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5C4F;&#x5E55;&#x9AD8;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">screen_width</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5C4F;&#x5E55;&#x5BBD;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">lat</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x7ECF;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">lng</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x7EF4;&#x5EA6;</td>
    </tr>
    <tr>
      <td style="text-align:left">language</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x8BED;&#x8A00;</td>
    </tr>
    <tr>
      <td style="text-align:left">bot_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x722C;&#x866B;&#x6807;&#x8BC6;&#xFF0C;&#x5982;&#x679C;&#x5927;&#x4E8E;-1&#x8BF4;&#x660E;&#x4E3A;&#x722C;&#x866B;&#x6570;&#x636E;</td>
    </tr>
    <tr>
      <td style="text-align:left">ads_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5E7F;&#x544A; id&#xFF0C;&#x79C1;&#x6709;&#x5316;&#x7248;&#x672C;&#x672A;&#x652F;&#x6301;</td>
    </tr>
    <tr>
      <td style="text-align:left">data_source_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x6570;&#x636E;&#x6E90;ID</td>
    </tr>
    <tr>
      <td style="text-align:left">attributes</td>
      <td style="text-align:left">map&lt;string, string&gt;</td>
      <td style="text-align:left">
        <p>&#x884C;&#x4E3A;&#x5C5E;&#x6027; : &#x591A;&#x4E2A;&#x5B57;&#x6BB5;map
          json string&#x3002;</p>
        <p>1.&#x8BBF;&#x95EE;&#x4E8B;&#x4EF6;&#xFF0C;&#x9875;&#x9762;&#x4E8B;&#x4EF6;&#xFF1A;path,
          query, title, referrer, refferrer_path</p>
        <p>2.&#x57CB;&#x70B9;&#x4E8B;&#x4EF6;: itemKey, itemOriginalId, itemId,&#x5173;&#x8054;&#x7684;&#x4E8B;&#x4EF6;&#x7EA7;&#x53D8;&#x91CF;</p>
        <p>3.&#x70B9;&#x51FB;&#x4E8B;&#x4EF6;&#xFF1A;pageShowTimestamp&#xFF0C;textValue&#xFF0C;xpath&#xFF0C;index&#xFF0C;hyperlink</p>
        <p>4.&#x8868;&#x5355;&#x63D0;&#x4EA4;&#x4E8B;&#x4EF6;&#xFF1A;pageShowTimestamp&#xFF0C;xpath&#xFF0C;index</p>
        <p>5.&#x8F93;&#x5165;&#x5143;&#x7D20;&#x5185;&#x5BB9;&#x6539;&#x53D8;&#x4E8B;&#x4EF6;
          pageShowTimestamp&#xFF0C;textValue&#xFF0C;xpath&#xFF0C;index</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">time</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x65F6;&#x95F4;&#x5206;&#x533A;&#x5217;&#xFF0C;UTC &#x65F6;&#x533A;&#xFF0C;&#x7CBE;&#x786E;&#x5230;&#x5C0F;&#x65F6;&#xFF0C;&#x5982;
        202010010000 &#x4E3A;&#x5317;&#x4EAC;&#x65F6;&#x95F4; 10&#x6708;1 &#x65E5;&#x65E9;8&#x70B9;</td>
    </tr>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x540C; event_type&#xFF0C;&#x5206;&#x533A;&#x5217;</td>
=======
      <td style="text-align:left">$platform</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5E73;&#x53F0;&#x6807;&#x8BC6;&#xFF0C;&#x793A;&#x4F8B;&#xFF1A;Web</td>
    </tr>
    <tr>
      <td style="text-align:left">$domain</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x57DF;&#x540D;&#x6216;&#x5305;&#x540D;</td>
    </tr>
    <tr>
      <td style="text-align:left">$path</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x9875;&#x9762;&#x8DEF;&#x5F84;</td>
    </tr>
    <tr>
      <td style="text-align:left">$referrer_domain</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x6765;&#x6E90;&#x57DF;&#x540D;&#x6216;&#x5305;&#x540D;</td>
    </tr>
    <tr>
      <td style="text-align:left">$referrer_path</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x4E0A;&#x4E00;&#x4E2A;&#x9875;&#x9762;&#x8DEF;&#x5F84;</td>
    </tr>
    <tr>
      <td style="text-align:left">$query</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x9875;&#x9762;query&#x53C2;&#x6570;</td>
    </tr>
    <tr>
      <td style="text-align:left">$xpath</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5143;&#x7D20;&#x5728;&#x9875;&#x9762;&#x4E2D;&#x7684;&#x4F4D;&#x7F6E;</td>
    </tr>
    <tr>
      <td style="text-align:left">$text_value</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5143;&#x7D20;&#x5BF9;&#x5E94;&#x7684;&#x6587;&#x672C;&#x540D;</td>
    </tr>
    <tr>
      <td style="text-align:left">$href</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5143;&#x7D20;&#x5BF9;&#x5E94;&#x7684;&#x94FE;&#x63A5;</td>
    </tr>
    <tr>
      <td style="text-align:left">$index</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5143;&#x7D20;&#x5728;&#x5217;&#x8868;&#x4E2D;&#x7684;&#x4F4D;&#x7F6E;&#xFF0C;0&#x5F00;&#x59CB;</td>
    </tr>
    <tr>
      <td style="text-align:left">$url_scheme</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x96C6;&#x6210;&#x5E94;&#x7528;&#x6807;&#x8BC6;</td>
    </tr>
    <tr>
      <td style="text-align:left">$browser</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x6D4F;&#x89C8;&#x5668;&#x540D;&#x79F0;</td>
    </tr>
    <tr>
      <td style="text-align:left">$browser_version</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x6D4F;&#x89C8;&#x5668;&#x7248;&#x672C;</td>
    </tr>
    <tr>
      <td style="text-align:left">$user_agent</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x6D4F;&#x89C8;&#x5668; agent &#x8BE6;&#x7EC6;&#x4FE1;&#x606F;</td>
    </tr>
    <tr>
      <td style="text-align:left">$os</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x64CD;&#x4F5C;&#x7CFB;&#x7EDF;&#x540D;&#x79F0;</td>
    </tr>
    <tr>
      <td style="text-align:left">$os_version</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x64CD;&#x4F5C;&#x7CFB;&#x7EDF;&#x7248;&#x672C;</td>
    </tr>
    <tr>
      <td style="text-align:left">$sdk_version</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">SDK&#x7248;&#x672C;&#x53F7;</td>
    </tr>
    <tr>
      <td style="text-align:left">$client_version</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5BA2;&#x6237;&#x7AEF;&#x7248;&#x672C;&#xFF08;&#x4EC5;&#x79FB;&#x52A8;&#x7AEF;&#x6709;&#x6548;&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left">$channel</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5BA2;&#x6237;&#x7AEF;&#x6E20;&#x9053;&#x6765;&#x6E90;</td>
    </tr>
    <tr>
      <td style="text-align:left">$utm_source</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5E7F;&#x544A;&#x6765;&#x6E90;&#xFF0C;&#x6807;&#x8BC6;&#x6295;&#x653E;&#x7684;&#x7F51;&#x7AD9;</td>
    </tr>
    <tr>
      <td style="text-align:left">$utm_medium</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5E7F;&#x544A;&#x5A92;&#x4ECB;&#x6216;&#x8425;&#x9500;&#x5A92;&#x4ECB;</td>
    </tr>
    <tr>
      <td style="text-align:left">$utm_campaign</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5E7F;&#x544A;&#x540D;&#x79F0;&#xFF0C;&#x4EA7;&#x54C1;&#x7684;&#x5177;&#x4F53;&#x5E7F;&#x544A;&#x7CFB;&#x5217;&#x540D;&#x79F0;&#x3001;&#x6807;&#x8BED;&#x7B49;</td>
    </tr>
    <tr>
      <td style="text-align:left">$utm_term</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5E7F;&#x544A;&#x5173;&#x952E;&#x5B57;&#xFF0C;&#x6807;&#x8BC6;&#x4ED8;&#x8D39;&#x641C;&#x7D22;&#x5173;&#x952E;&#x5B57;</td>
    </tr>
    <tr>
      <td style="text-align:left">$utm_content</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5E7F;&#x544A;&#x5185;&#x5BB9;&#xFF0C;&#x7528;&#x4E8E;&#x533A;&#x5206;&#x76F8;&#x4F3C;&#x5185;&#x5BB9;&#x6216;&#x540C;&#x4E00;&#x5E7F;&#x544A;&#x5185;&#x7684;&#x94FE;&#x63A5;</td>
    </tr>
    <tr>
      <td style="text-align:left">$key_word</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x8BBF;&#x95EE;&#x6765;&#x6E90;&#x5E7F;&#x544A;&#x5173;&#x952E;&#x5B57;&#xFF08;&#x901A;&#x7528;&#x7EF4;&#x5EA6;&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left">$device_brand</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x8BBE;&#x5907;&#x54C1;&#x724C;&#x540D;&#x79F0;</td>
    </tr>
    <tr>
      <td style="text-align:left">$device_model</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x8BBE;&#x5907;&#x578B;&#x53F7;</td>
    </tr>
    <tr>
      <td style="text-align:left">$device_type</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x8BBE;&#x5907;&#x7C7B;&#x578B;</td>
    </tr>
    <tr>
      <td style="text-align:left">$device_orientation</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x8BBE;&#x5907;&#x65B9;&#x5411;</td>
    </tr>
    <tr>
      <td style="text-align:left">$language</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x8BED;&#x8A00;&#xFF0C;&#x793A;&#x4F8B;&#xFF1A;zh-cn</td>
    </tr>
    <tr>
      <td style="text-align:left">$country_code</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x56FD;&#x5BB6;&#x7801;&#xFF0C;&#x793A;&#x4F8B;&#xFF1A;CN</td>
    </tr>
    <tr>
      <td style="text-align:left">$country_name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x56FD;&#x5BB6;&#x540D;&#x79F0;&#xFF0C;&#x793A;&#x4F8B;&#xFF1A;&#x4E2D;&#x56FD;</td>
    </tr>
    <tr>
      <td style="text-align:left">$region</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5730;&#x533A;&#xFF0C;&#x793A;&#x4F8B;&#xFF1A;&#x6C5F;&#x82CF;</td>
    </tr>
    <tr>
      <td style="text-align:left">$city</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x57CE;&#x5E02;&#xFF0C;&#x793A;&#x4F8B;&#xFF1A;&#x5357;&#x4EAC;</td>
    </tr>
    <tr>
      <td style="text-align:left">$ip</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5BA2;&#x6237;&#x7AEF;IP&#x5730;&#x5740;</td>
    </tr>
    <tr>
      <td style="text-align:left">$data_source_id</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x6570;&#x636E;&#x6E90;&#x4FE1;&#x606F;</td>
    </tr>
    <tr>
      <td style="text-align:left">$page_count</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">&#x8BBF;&#x95EE;&#x6DF1;&#x5EA6;&#xFF0C;&#x5373;&#x4E00;&#x6B21;&#x8BBF;&#x95EE;&#x7684;&#x9875;&#x9762;&#x6D4F;&#x89C8;&#x91CF;</td>
    </tr>
    <tr>
      <td style="text-align:left">$duration</td>
      <td style="text-align:left">UInt32</td>
      <td style="text-align:left">
        <p>&#x65F6;&#x957F;&#xFF08;&#x79D2;&#xFF09;&#x3002;page&#x4E8B;&#x4EF6;&#x4E0A;&#x662F;&#x9875;&#x9762;&#x505C;&#x7559;&#x65F6;&#x957F;</p>
        <p>&#xFF0C;visit&#x4E8B;&#x4EF6;&#x4E0A;&#x662F;&#x8BBF;&#x95EE;&#x65F6;&#x957F;</p>
      </td>
    </tr>
  </tbody>
</table>

{% hint style="success" %}
$page\_count和$duration是离线计算而非实时采集的信息，时效性是T+1天。
{% endhint %}

#### 自定义属性

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5B57;&#x6BB5;&#x540D;</th>
      <th style="text-align:left">&#x542B;&#x4E49;&#x53CA;&#x793A;&#x4F8B;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">var_{&#x81EA;&#x5B9A;&#x4E49;&#x6807;&#x8BC6;&#x7B26;}</td>
      <td style="text-align:left">
        <p>&#x6BD4;&#x5982;&#x4E3A;&#x63D0;&#x4EA4;&#x8BA2;&#x5355;&#x4E8B;&#x4EF6;&#x5B9A;&#x4E49;&#x4E86;&#x8BA2;&#x5355;&#x91D1;&#x989D;&#xFF0C;</p>
        <p>&#x5B57;&#x6BB5;&#x4E3A;price&#xFF0C;&#x5219;&#x5728;&#x4E8B;&#x4EF6;&#x8868;&#x4E2D;&#x7684;&#x5B57;&#x6BB5;&#x4E3A;var_price</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">......</td>
      <td style="text-align:left"></td>
>>>>>>> 14.3.0-beta
    </tr>
  </tbody>
</table>

<<<<<<< HEAD
## 物品模型\(Item\)

GrowingIO平台采用独立的模型存储商品属性信息。在计算的过程中，我们采用高效的mapping算法，完美的解决了维度值组合过多的问题，加速对商品指标的计算速度。

> 经典电商场景：
>
> 一般情况下，企业内商品种类繁多。如果把商品特征\(如品牌、颜色 etc.\)作为行为维度进行存储，会造成维度值组合爆炸的问题。因此GrowingIO将物品属性与其他属性分割开。

{% hint style="success" %}
物品模型需要与埋点事件进行绑定后才能使用
{% endhint %}

| **原始数据字段** | **类型** | **备注** |
| :--- | :--- | :--- |
| account\_id | string | 项目标识符 |
| send\_time | bigint | 数据处理时间，因为用户属性是取最后一次归因，因此以处理时间为准，不以数据发送时间为准 |
| item\_key | string | 物品模型 key |
| item\_value | string | 物品模型 value |
| item\_id | int | GrowingIO 内部使用 |
| attributes | map&lt;string, string&gt; | 用户自定义属性 |

## 用户属性模型\(UserProps\)

用户属性是人的画像描述信息，可以作为维度对人群进行拆解。

用户属性模型相比事件模型而言要简单的多，包含who\(用户标识\)，dim\(属性名称\)，dvalue\(属性值\), in\_time\(更新时间\)信息。

通过用户模型可以确定某个用户在某个时间点用户 ‘长什么样'，方便客户更加深入的洞察某个用户。

| **原始数据字段** | **类型** | **备注** |
| :--- | :--- | :--- |
| ai | string | 项目标识符 |
| dim | string | 用户属性名 |
| dvalue | string | 用户属性值 |
| gid | int | 用户标识符，同 EVENT 模型中的 user\_id |
| in\_time | bigint | 属性值最后更新时间，精确到秒 |

## 标签模型\(Tag\)

用户标签是人的画像描述信息，与用户属性的差别在于标签是基于GrowingIO计算能力对人进行打标。

| **字段** | **类型** | **备注** |
| :--- | :--- | :--- |
| tag\_id | varchar | 标签id |
| tag\_value | varchar | 标签值 |
| tag\_type | varchar | 标签类型 |
| cnt | bigint | 标签人数 |
| bitmap | varbinary | 标签人bitmap |
| in\_time | bigint | 更新时间 |
| tag\_id, tag\_value | map&lt;string, string&gt; | 联合主键 |

从用户角度看，该用户在哪些标签人群中。

| **字段** | **类型** | **备注** |
| :--- | :--- | :--- |
| gid | varchar | 用户标识符 |
| tag\_id | varchar | 标签id |
| tag\_value | varchar | 标签值 |
| in\_time | bigint | 更新时间 |
| gid, tag\_id | map&lt;string, string&gt; | 联合主键 |
=======
{% hint style="success" %}
自定义属性字段的生成机制：[客户数据平台](../../product-manual/customer-data-platform/) 中定义了新的事件属性，系统会实时触发事件表增加相应的字段，相应地当删除了某事件属性时，系统也会实时删除事件表中的该属性字段。
{% endhint %}

### 查询示例

```text
-- 查询2021-06-01的用户量
select count(distinct gio_id)
from event 
where dt='2021-06-01';

-- 查询2021-06-01的页面浏览量
select count(1)
from event 
where dt='2021-06-01' and event_key='$page';

-- 查询2021-06-01的访问量
select count(distinct session)
from event 
where dt='2021-06-01' and event_key='$visit';

-- 查询2021-06-01的总访问时长
select sum($duration) 
from event 
where dt='2021-06-01' and event_key='$visit';

-- 查询2021-06-01的跳出次数
select count(1) 
from event 
where dt='2021-06-01' and event_key='$bounce'

-- 查询2021-06-01的退出次数
select count(1) 
from event 
where dt='2021-06-01' and event_key='$exit'
```

{% hint style="success" %}
$bounce和$exit是离线计算而非实时采集的事件，时效性是T+1天。$bounce表示访问后直接跳出事件，用来统计跳出次数及跳出率，$exit表示访问的最后一次页面浏览。
{% endhint %}

## 用户表\( user \)：

GrowingIO系统会对每一个识别的用户会进行唯一标识\( 即gio\_id \)。在 user 表中，您可以查询全部GrowingIO识别的用户，以及用户的

* [用户ID](../../product-manual/customer-data-platform/customer-model-management/customer-identification.md)
* [用户属性](../../product-manual/customer-data-platform/customer-model-management/customer-property/)
* [用户标签](../../product-manual/uesr-analysis/tag-analysis.md)
* [分群画像](../../product-manual/uesr-analysis/segmentations/segmentations-insights.md)
* 预置字段

用户ID:

在 user 表中，系统会根据用户ID配置自动增加列，即每个一个身份ID唯一对应user表中的某一个数据列。

| 项 | 说明 |
| :--- | :--- |
| 列名 | id\_{身份ID key} |
| 数据时效性 | 实时 |

用户属性:

在 user 表中，系统会根据用户属性新建和删除自动增加和减少列，即每一个用户属性唯一对应user表中的某一个数据列。

| 项 | 说明 |
| :--- | :--- |
| 列名 | usr\_{用户属性 key} |
| 数值类型 | 取决于用户属性数值类型 |
| 数据时效性 | 实时 |

{% hint style="success" %}
包含系统预置用户属性，如

usr\_$first\_day: gio\_id生成日期

usr\_$basic\_birthday: 出生年月日

usr\_$basic\_email: 电子邮箱

usr\_$basic\_address: 地址

usr\_$wechat\_subscribeList: 关注公众号

usr\_$basic\_mobile: 手机号

usr\_$basic\_createdAt: 注册时间

usr\_$wechat\_openId: 微信 openid

usr\_$wechat\_unionId: 微信 unionid

usr\_$wechat\_nickName: 微信昵称

usr\_$wechat\_avatarUrl: 微信头像

usr\_$wechat\_city: 微信用户所在城市

usr\_$wechat\_country: 微信用户所在国家

usr\_$wechat\_province: 微信用户所在省份

usr\_$wechat\_gender: 微信用户性别

usr\_$wechat\_language: 微信语言

usr\_$basic\_gender: 性别

usr\_$basic\_name: 姓名

usr\_$alipay\_isCertified: 支付宝实名认证

usr\_$alipay\_avatar: 支付宝头像

usr\_$alipay\_isStudentCertified: 支付宝学生认证

usr\_$alipay\_userId: 支付宝用户ID

usr\_$alipay\_userType: 支付宝用户类型

usr\_$alipay\_nickName: 支付宝用户昵称

usr\_$alipay\_city: 支付宝用户所在城市

usr\_$alipay\_province: 支付宝用户所在省份

usr\_$alipay\_gender: 支付宝用户性别

usr\_$alipay\_userStatus: 支付宝用户状态
{% endhint %}

用户标签:

在 user 表中，系统会根据用户标签新建和删除自动增加和减少列，即每一个用户标签唯一对应user表中的某一个数据列。

| 项 | 说明 |
| :--- | :--- |
| 列名 | tag\_{用户属性 key} |
| 数值类型 | 取决于用户标签数值类型 |
| 更新机制 | 依赖用户标签更新计算 |

用户分群:

在 user 表中，系统会根据分群画像新建和删除自动增加和减少列，即每一个分群画像唯一对应user表中的某一个数据列。

| 项 | 说明 |
| :--- | :--- |
| 列名 | seg\_{分群画像 key} |
| 数值类型 | 整数 \( 0 , 1 \) |
| 更新机制 | 依赖分群画像更新计算 |

{% hint style="success" %}
分群画像创建时不能指定标识符，系统默认自增创建标识符。
{% endhint %}

预置字段:

account\_id：系统默认字段，每一个CDP系统具有唯一字段值

is\_merged：系统默认字段，ID-Mapping标记字段，被融合用户值为1，未被融合用户值为0

## 用户融合表\( user\_merged \): 

ID-Mapping业务数据表，记录用户融合关系。该数据表仅包含被融合用户，数据表为更新表，用户融合后实时触发更新。

| 项 | 数值类型 | 说明 |
| :--- | :--- | :--- |
| gio\_id | int | 被融合用户ID |
| merged\_gio\_id | int | 融合后用户ID |
| account\_id | string | 系统默认字段，每一个CDP系统具有唯一字段值 |
| merged\_time | datetime | 融合触发时间 |
>>>>>>> 14.3.0-beta

