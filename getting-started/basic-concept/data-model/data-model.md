---
id: data-model
sidebar_position: 1
--- 

# 数据模型

## 简介[](#jian-jie)


GrowingIO采集的原始行为数据分为四种不同类型，分别为访问（visit）、页面（page）、埋点（custom_event）和行为（action）。

* 访问（visit）： 代表用户开启了一个新的访问会话，访问行为的生命周期与会话（session）绑定，新的session代表一个新的访问。
    
* 页面浏览（page）：代表用户的一次页面浏览，SDK采集以及发送浏览事件中的数据。
    
* 埋点（custom_event）： 代表用户触发了客户埋的点发送的事件。事件触发的时间以及发送的行为数据信息都由客户指定。
    
* 行为（action）： 代表用户操作了页面上的某些元素发送的行为，包括点击了按钮、修改了数据框的内容等等。
    

过去，GrowingIO数据平台将上述四种行为数据存储至多张表中，这种模型导致后续的统计逻辑非常复杂。为了串联多种行为数据，我们在查询时进行了多表关联计算，因此导致部分极端场景下数据计算结果不一致的问题偶有发生。另外，该种数据模型数据比较分散，没有统一的接口，不易与其他组件进行对接。

在[9.0版本](/op/v/2.0/update-log#v-2020-9-0-2020-nian-9-yue-30-ri-fa-bu)后，我们将多种行为数据统一抽象为EVENT模型，即四种行为数据统一到一张表中。该种模型简化了平台计算逻辑，并且通过Thrift Server方便GrowingIO数据平台与其他组件进行对接，进而提升开发效率和降低维护成本。

最新的数据模型同时具备了提供实时数据的能力，行为数据从触点触发再到客户可以观察到，时间间隔一般在10秒以内。

## 客户操作手册[](#ke-hu-cao-zuo-shou-ce)

GrowingIO CDP为客户安装了Zeppelin，客户可以通过Zeppelin SQL解释器查询数据平台中的数据库、数据表和表中数据。

**SQL语法：**

查询所有的数据库：show databases

查询数据库中的数据表：show tables in {database_name}

查询数据表结构：desc {database\_name}.{table\_name}

查询数据表创建语句：show create table {database\_name}.{table\_name}

查询表分区：select partition from system.parts where database='{database_name}' and table='{table_name_}'

查询数据表数据： select {field} from {database\_name}.{table\_name}

## 数据表[](#shu-ju-biao)


事件表：event

用户表：user

用户融合表：user_merged

## 事件表（event）：[](#shi-jian-biao-event)

GrowingIO通过SDK实时采集或文件批量导入的行为数据，统一存放在event表中。

事件表按照日期分区，数据的时效性为实时，即行为数据从触发采集到入库可查的时间间隔一般在10秒内。

在事件表中，您可以查询事件采集上报的全部信息。由于字段繁多，通过前缀将不同角度的字段分组提升查询体验，共分三组：

* 事件标识符、发生时间、用户ID等[基础信息](/op/v/2.0/getting-started/basic-concept/data-model#ji-chu-xin-xi)，字段无前缀
    
* 城市、浏览器、设备类型等[预定义属性](/op/v/2.0/getting-started/basic-concept/data-model#yu-ding-yi-shu-xing)，字段统一使用 $ 符号前缀
    
* 埋点上报的[自定义属性](/op/v/2.0/getting-started/basic-concept/data-model#zi-ding-yi-shu-xing)，字段统一使用 var_ 作为前缀
    

> 虽然事件表的字段按照前缀做了分组，但它们都在事件表内。

### 数据字段[](#shu-ju-zi-duan)

#### 基础信息[](#ji-chu-xin-xi)

| 字段名 | 字段类型 | 含义及示例 |
| --- | --- | --- |
| event_key | String | 事件标识符。示例：visit事件=$visit、页面浏览事件=$page、自定义事件如paySuccess等 |
| event_type | String | 事件类型。示例：visit、page、custom_event等 |
| event_time | DateTime | 事件上报时间，毫秒。示例：2021-06-01 23:59:20.912<br></br>注：分析应用等场景的核心字段 |
| client_time | DateTime | 事件发生时间，毫秒。示例：2021-06-01 23:59:20.912<br></br>注：仅用在访问时长和页面时长里 |
| event_id | String | 事件ID |
| anonymous_user | String | 访问用户ID |
| user | String | 登录用户ID |
| user_key | String | 用户身份类型。示例：$basic_userId |
| gio_id | UInt | id-service为用户生成的自增序号，是分析中统计用户量等指标的关键字段 |
| session | String | 会话标识，标记一个访问 |
| account_id | String | 账户ID（GrowingIO产品部署时自动生成，默认唯一值） |
| dt  | Date | 事件上报的日期。示例：2021-06-01 |
| attributes | Map | 事件属性集。示例：{"city":"beijing","color":"red"} |

event_id是对重复数据去重处理的主要参数之一。它的生成机制随事件类型的不同而各异。

* 访问事件：通过session字段加密生成
    
* 页面浏览事件：通过session、event_time和path字段加密生成
    
* 自定义事件：通过event_key、event_time、_anonymous_user、user、attributes等加密生成
    
#### 预定义属性[](#yu-ding-yi-shu-xing)

| 字段名 | 字段类型 | 含义及示例 |
| --- | --- | --- |
| $platform | String | 平台标识，示例：Web |
| $domain | String | 域名或包名 |
| $path | String | 页面路径 |
| $referrer_domain | String | 来源域名或包名 |
| $referrer_path | String | 上一个页面路径 |
| $query | String | 页面query参数 |
| $xpath | String | 元素在页面中的位置 |
| $text_value | String | 元素对应的文本名 |
| $href | String | 元素对应的链接 |
| $index | String | 元素在列表中的位置，0开始 |
| $url_scheme | String | 集成应用标识 |
| $browser | String | 浏览器名称 |
| $browser_version | String | 浏览器版本 |
| $user_agent | String | 浏览器 agent 详细信息 |
| $os | String | 操作系统名称 |
| $os_version | String | 操作系统版本 |
| $sdk_version | String | SDK版本号 |
| $client_version | String | 客户端版本（仅移动端有效） |
| $channel | String | 客户端渠道来源 |
| $utm_source | String | 广告来源，标识投放的网站 |
| $utm_medium | String | 广告媒介或营销媒介 |
| $utm_campaign | String | 广告名称，产品的具体广告系列名称、标语等 |
| $utm_term | String | 广告关键字，标识付费搜索关键字 |
| $utm_content | String | 广告内容，用于区分相似内容或同一广告内的链接 |
| $key_word | String | 访问来源广告关键字 |
| $device_brand | String | 设备品牌名称 |
| $device_model | String | 设备型号 |
| $device_type | String | 设备类型 |
| $device_orientation | String | 设备方向 |
| $language | String | 语言，示例：zh-cn |
| $country_code | String | 国家码，示例：CN |
| $country_name | String | 国家名称，示例：中国 |
| $region | String | 地区，示例：江苏 |
| $city | String | 城市，示例：南京 |
| $ip | String | 客户端IP地址 |
| $data\_source\_id | String | 数据源信息 |
| $page_count | UInt32 | 访问深度，即一次访问的页面浏览量 |
| $duration | UInt32 | 时长（秒）。page事件上是页面停留时长<br></br>，visit事件上是访问时长 |

> $page_count和$duration是离线计算而非实时采集的信息，时效性是T+1天。

#### 自定义属性[](#zi-ding-yi-shu-xing)

| 字段名 | 含义及示例 |
| --- | --- |
| var_{事件属性标识符} | 比如为提交订单事件定义了“订单金额”的属性，标识符为money ，它在事件表中的字段为：var_money |
| ... | ...​   |

> 自定义属性字段的生成机制：[客户数据平台](/op/v/2.0/product-manual/customer-data-platform) 中定义了新的事件属性，系统会实时触发事件表增加相应的字段，相应地当删除了某事件属性时，系统也会实时删除事件表中的该属性字段。

### 预置事件[](#yu-zhi-shi-jian)

预置事件是指不需要您代码埋点，只要您的产品集成了GrowingIO的客户端SDK，在自动采集的默认模式下，用户使用您的产品时，用户的大部分行为会默认采集上报，比如用户访问产品、浏览了页面以及点击页面的按钮等行为。一些预置事件则是GrowingIO系统离线计算得到的，以便于支持您使用跳出率、用户量等指标。

| 名称  | 标识符 | 含义及示例 |
| --- | --- | --- |
| 访问  | $visit | 用户开启新的访问会话，记录一次访问 |
| 页面浏览 | $page | 一次页面浏览 |
| 访问退出 | $exit | 一次访问结束。 注：使用会话中的最后一次页面浏览事件，T+1离线计算生成 |
| 访问跳出 | $bounce | 一次访问没有任何页面浏览即结束，T+1离线计算生成 |
| 元素点击 | $view_click | 页面上用户点击元素的事件，比如点击了“查看详情”的按钮 |
| 元素修改 | $view_change | 页面上用户改变元素值的事件，比如修改了下拉框值 |
| 表单提交 | $form_submit | 页面上用户提交表单的事件 |
| 任意事件 | $anyevent | 事件表中的所有事件抽象得到，实时计算生成 |

> 关于任意事件
> 
> * 核心使用场景：计算用户量，通过约减数据量来获得查询性能的提升
> * 生成机制：所有事件的部分字段分组统计得到，比如event_time字段换算到小时，attributes字段仅用到path等。
    

### 查询示例[](#cha-xun-shi-li)

```sql
-- 查询2021-06-01的用户量

select count(distinct gio_id) from event where dt='2021-06-01';

​

-- 查询2021-06-01的页面浏览量

select count(1) from event where dt='2021-06-01' and event_key='$page';

​

-- 查询2021-06-01的访问量

select count(distinct session) from event where dt='2021-06-01' and event_key='$visit';

​

-- 查询2021-06-01的总访问时长

select sum($duration) from event where dt='2021-06-01' and event_key='$visit';

​

-- 查询2021-06-01的跳出次数

select count(1) from event where dt='2021-06-01' and event_key='$bounce'

​

-- 查询2021-06-01的退出次数

select count(1) from event where dt='2021-06-01' and event_key='$exit'
```

## 用户表( user )：[](#yong-hu-biao-user)

GrowingIO系统会对每一个识别的用户会进行唯一标识( 即gio_id )。在 user 表中，您可以查询全部GrowingIO识别的用户，以及用户的

* ​[用户ID](/op/v/2.0/product-manual/customer-data-platform/user/user-identifications)​
    
* ​[用户属性](/op/v/2.0/product-manual/customer-data-platform/user/user-properties)​
    
* ​[用户标签](/op/v/2.0/product-manual/user-insights/tag-analysis)​
    
* ​分群画像​
    
* 预置字段
    

### 用户ID

在 user 表中，系统会根据用户ID配置自动增加列，即每个一个身份ID唯一对应user表中的某一个数据列。

| 项   | 说明  |
| --- | --- |
| 列名  | id_{身份ID key} |
| 数据时效性 | 实时  |

### 用户属性

在 user 表中，系统会根据用户属性新建和删除自动增加和减少列，即每一个用户属性唯一对应user表中的某一个数据列。

| 项   | 说明  |
| --- | --- |
| 列名  | usr_{用户属性 key} |
| 数值类型 | 取决于用户属性数值类型 |
| 数据时效性 | 实时  |

> 包含系统预置用户属性，如
> 
> * usr_$first\_day: gio\_id生成日期
> * usr_$basic_birthday: 出生年月日
> * usr_$basic_email: 电子邮箱
> * usr_$basic_address: 地址
> * usr_$wechat_subscribeList: 关注公众号
> * usr_$basic_mobile: 手机号
> * usr_$basic_createdAt: 注册时间
> * usr_$wechat_openId: 微信 openid
> * usr_$wechat_unionId: 微信 unionid
> * usr_$wechat_nickName: 微信昵称
> * usr_$wechat_avatarUrl: 微信头像
> * usr_$wechat_city: 微信用户所在城市
> * usr_$wechat_country: 微信用户所在国家
> * usr_$wechat_province: 微信用户所在省份
> * usr_$wechat_gender: 微信用户性别
> * usr_$wechat_language: 微信语言
> * usr_$basic_gender: 性别
> * usr_$basic_name: 姓名
> * usr_$alipay_isCertified: 支付宝实名认证
> * usr_$alipay_avatar: 支付宝头像
> * usr_$alipay_isStudentCertified: 支付宝学生认证
> * usr_$alipay_userId: 支付宝用户ID
> * usr_$alipay_userType: 支付宝用户类型
> * usr_$alipay_nickName: 支付宝用户昵称
> * usr_$alipay_city: 支付宝用户所在城市
> * usr_$alipay_province: 支付宝用户所在省份
> * usr_$alipay_gender: 支付宝用户性别
> * usr_$alipay_userStatus: 支付宝用户状态

### 用户标签

在 user 表中，系统会根据用户标签新建和删除自动增加和减少列，即每一个用户标签唯一对应user表中的某一个数据列。

| 项   | 说明  |
| --- | --- |
| 列名  | tag_{用户属性 key} |
| 数值类型 | 取决于用户标签数值类型 |
| 更新机制 | 依赖用户标签更新计算 |

### 用户分群

在 user 表中，系统会根据分群画像新建和删除自动增加和减少列，即每一个分群画像唯一对应user表中的某一个数据列。

| 项   | 说明  |
| --- | --- |
| 列名  | seg_{分群画像 key} |
| 数值类型 | 整数 ( 0 , 1 ) |
| 更新机制 | 依赖分群画像更新计算 |

> 分群画像创建时不能指定标识符，系统默认自增创建标识符。

### 预置字段

account_id：系统默认字段，每一个CDP系统具有唯一字段值

is_merged：系统默认字段，ID-Mapping标记字段，被融合用户值为1，未被融合用户值为0

## 用户融合表( user_merged ):[](#yong-hu-rong-he-biao-usermerged)


ID-Mapping业务数据表，记录用户融合关系。该数据表仅包含被融合用户，数据表为更新表，用户融合后实时触发更新。

| 项   | 数值类型 | 说明  |
| --- | --- | --- |
| gio_id | int | 被融合用户ID |
| merged\_gio\_id | int | 融合后用户ID |
| account_id | string | 系统默认字段，每一个CDP系统具有唯一字段值 |
| merged_time | datetime | 融合触发时间 |
