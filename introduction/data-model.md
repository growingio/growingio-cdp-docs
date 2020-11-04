# 数据模型

## 简介

GrowingIO采集的原始行为数据分为四种不同类型，分别为访问\(visit\)、页面\(page\)、埋点\(custom\_event\)和行为\(action\)。

* 访问\(visit\): 代表用户开启了一个新的访问会话，访问行为的生命周期与会话（session）绑定，新的session代表一个新的访问。
* 页面浏览\(page\): 代表用户的一次页面浏览，SDK采集以及发送浏览事件中的数据。
* 埋点\(custom\_event\): 代表用户触发了客户埋的点发送的事件。事件触发的时间以及发送的行为数据信息都由客户指定。
* 行为\(action\): 代表用户操作了页面上的某些元素发送的行为，包括点击了按钮，修改了数据框的内容等等。

过去，GrowingIO数据平台将上述四种行为数据存储至多张Hive表中，这种模型导致后续的统计逻辑非常复杂。为了串联多种行为数据，我们在查询时进行了多表关联计算，因此导致部分极端场景下数据计算结果不一致的问题偶有发生。另外，该种数据模型数据比较分散，没有统一的接口，不易与其他组件对接。

在[9.0版本](../update-log.md#v-2020-9-0-2020-nian-9-yue-30-ri-fa-bu)后，我们将多种行为数据统一抽象为EVENT模型，即四种行为数据统一到一张表中。该种模型简化了平台计算逻辑，并且通过Thrift Server方便GrowingIO数据平台与其他组件进行对接，进而提升开发效率和降低维护成本。

最新的数据模型同时具备了提供实时数据的能力，行为数据从触点触发再到客户可以观察到，时间间隔可以缩小到5 ～ 10秒钟。

## 客户操作手册

GrowingIO CDP为客户安装了Zeppelin，客户可以通过Zeppelin SQL解释器查询数据平台中的数据库、数据表和表中数据。

SQL语法：

查询所有的数据库：show databases

查询数据库中的数据表：show tables in {database\_name}

查询数据表结构：desc {database\_name}.{table\_name}

查询数据表分区： show partitions {database\_name}.{table\_name}

查询数据表数据： select {field} from {database\_name}.{table\_name}

数据表：

行为模型：CARBON.EVENT\_LOG

查询时请使用时间和类型分区加速查询速度。如需查询当前小时实时数据，可查询 HBASE 表，表名为 EVENT\_BUFFER\_SECOND\_{day}\_{hour} ，比如北京时间 2020.10.1 上午 8点，对应的是 EVENT\_BUFFER\_SECOND\_2020100100。

用户属性模型：USER\_PROPS

物品模型：CARBON.ITEM

标签模型：TAG\_RULE\_RESULTS\(标签角度\)、USER\_TAG\_RULE\_VALUES（用户角度）

## 行为模型\(Event\)

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#x539F;&#x59CB;&#x6570;&#x636E;&#x5B57;&#x6BB5;</b>
      </th>
      <th style="text-align:left"><b>&#x7C7B;&#x578B;</b>
      </th>
      <th style="text-align:left"><b>&#x5907;&#x6CE8;</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
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
    </tr>
  </tbody>
</table>

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

