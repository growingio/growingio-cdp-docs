---
id: data-model-transition-13.x
sidebar_position: 2
---

# 旧版本兼容指南 - 13.x版本
=================

## 数据表[](#shu-ju-biao)


============================

行为模型：CARBON.EVENT_LOG

查询时请使用时间和类型分区加速查询速度。如需查询当前小时实时数据，可查询 HBASE 表，表名为 EVENT\_BUFFER\_SECOND_{day}_{hour} ，比如北京时间 2020.10.1 上午 8点，对应的是 EVENT\_BUFFER\_SECOND_2020100100。

用户属性模型：USER_PROPS

物品模型：CARBON.ITEM

标签模型：TAG\_RULE\_RESULTS（标签角度）、USER\_TAG\_RULE_VALUES（用户角度）

## 行为模型(Event)[](#hang-wei-mo-xing-event)

|     |     |     |
| --- | --- | --- |
| **原始数据字段** | **类型** | **备注** |
| event_key | string | 事件标识符： 访问事件 → $visit，页面事件 → $page，埋点事件 → 埋点事件标识符 |
| event_time | bigint | 事件接收时间: 服务端接收时间为准，精确到毫秒。 |
| event_id | string | 事件唯一标识符：GrowingIO系统生成，不同事件类型生成id逻辑不同。 |
| event_type | string | 事件类型：visit、page、custom_event |
| client_time | bigint | 事件发生时间：精确到毫秒 |
| anonymous_user | string | 访问用户标识符 |
| user | string | 用户标识符：如果登录用户为空，则为访问用户，否则为登录用户 |
| user_type | string | 用户类型：标识user对应的是登录用户还是访问用户 |
| user_id | int | 用户：登录用户、访问用户生成的ID |
| user_session | string | 访问会话标识符 |
| account_id | string | 项目标识符：通过 url 路径解析 |
| platform | string | 事件发送平台 |
| domain | string | 事件应用域名 |
| referrer_domain | string | 访问来源域名 |
| ip  | string | IP地址，通过 http 请求自动获取 |
| utm_source | string | 广告来源：utm所有字段从query中解析 |
| utm_medium | string | 广告媒介：utm所有字段从query中解析 |
| utm_campaign | string | 广告名称：utm所有字段从query中解析 |
| utm_term | string | 广告关键字：utm所有字段从query中解析 |
| utm_content | string | 广告内容：utm所有字段从query中解析 |
| key_word | string | 搜索关键字：从query中解析 |
| country_code | stirng | 国家代码：地理位置信息从ip/gps(lat, lng)中解析 |
| country_name | string | 国家名称：地理位置信息从ip/gps(lat, lng)中解析 |
| region | string | 省份：地理位置信息从ip/gps(lat, lng)中解析 |
| city | string | 城市：地理位置信息从ip/gps(lat, lng)中解析 |
| user_agent | string | 客户端信息：通过 http 请求自动获取 |
| browser | string | 浏览器 ：从user_agent中解析 |
| browser_version | string | 浏览器版本： 从user_agent中解析 |
| os  | string | 操作系统：移动端通过 SDK 上传，web 端从user_agent中解析 |
| os_version | string | 操作系统版本：移动端通过 SDK 上传，web 端从user_agent中解析 |
| client_version | string | 客户端版本 |
| channel | string | 渠道来源 |
| devcie_brand | string | 设备品牌：移动端通过 SDK 上传，web 端从user_agent中解析 |
| device_model | string | 设备型号 |
| device_type | string | 设备类型 |
| deivce_orientation | string | 设备方向 |
| screen_height | string | 屏幕高度 |
| screen_width | string | 屏幕宽度 |
| lat | string | 经度  |
| lng | string | 维度  |
| language | string | 语言  |
| bot_id | string | 爬虫标识，如果大于-1说明为爬虫数据 |
| ads_id | string | 广告 id，私有化版本未支持 |
| data\_source\_id | string | 数据源ID |
| attributes | map<string, string> |行为属性 : 多个字段 map json string。1.访问事件，页面事件：path，query，title，referrer，refferrer_path 2.埋点事件: itemKey，itemOriginalId，itemId，关联的事件级变量 3.点击事件：pageShowTimestamp，textValue，xpath，index，hyperlink 4.表单提交事件：pageShowTimestamp，xpath，index 5.输入元素内容改变事件 pageShowTimestamp，textValue，xpath，index |
| time | string | 时间分区列，UTC 时区，精确到小时，如 202010010000 为北京时间 10月1日早上8点 |
| type | string | 同 event_type，分区列 |

## 物品模型(Item)[](#wu-pin-mo-xing-item)


======================================

GrowingIO平台采用独立的模型存储商品属性信息。在计算的过程中，我们采用高效的mapping算法，完美解决了维度值组合过多的问题，加速对商品指标的计算速度。

> 经典电商场景：
> 
> 一般情况下，企业内商品种类繁多。如果把商品特征（如品牌、颜色等）作为行为维度进行存储，会造成维度值组合爆炸的问题。因此GrowingIO将物品属性与其他属性分割开。

物品模型需要与埋点事件进行绑定后才能使用

| **原始数据字段** | **类型**                  | **备注**                                                                             |
|------------------|---------------------------|--------------------------------------------------------------------------------------|
| account_id       | string                    | 项目标识符                                                                           |
| send_time        | bigint                    | 数据处理时间，因为用户属性是取最后一次归因，因此以处理时间为准，不以数据发送时间为准 |
| item_key         | string                    | 物品模型 key                                                                         |
| item_value       | string                    | 物品模型 value                                                                       |
| item_id          | int                       | GrowingIO 内部使用                                                                   |
| attributes       | map&lt;string, string&gt; | 用户自定义属性                                                                       |

## 用户属性模型(UserProps)[](#yong-hu-shu-xing-mo-xing-userprops)


============================================================

用户属性是人的画像描述信息，可以作为维度对人群进行拆解。

用户属性模型相比事件模型而言要简单的多，包含who（用户标识），dim（属性名称），dvalue（属性值）, in_time（更新时间）信息。

通过用户模型可以确定某个用户在某个时间点 ‘长什么样'，方便客户更加深入地洞察某个用户。

| **原始数据字段** | **类型** | **备注**                              |
|------------------|----------|---------------------------------------|
| ai               | string   | 项目标识符                            |
| dim              | string   | 用户属性名                            |
| dvalue           | string   | 用户属性值                            |
| gid              | int      | 用户标识符，同 EVENT 模型中的 user_id |
| in_time          | bigint   | 属性值最后更新时间，精确到秒          |

## 标签模型(Tag)[](#biao-qian-mo-xing-tag)


=======================================

用户标签是人的画像描述信息，与用户属性的差别在于标签是基于GrowingIO计算能力对人进行打标。

| **原始数据字段**    | **类型**                  | **备注**     |
|---------------------|---------------------------|--------------|
| tag_id              | varchar                   | 标签id       |
| tag_value           | varchar                   | 标签值       |
| tag_type            | varchar                   | 标签类型     |
| cnt                 | bigint                    | 标签人数     |
| bitmap              | varbinary                 | 标签人bitmap |
| in_time             | bigint                    | 更新时间     |
| tag\_id, tag\_value | map&lt;string, string&gt; | 联合主键     |

从用户角度看，该用户在哪些标签人群中。

| **原始数据字段** | **类型**                  | **备注**   |
|------------------|---------------------------|------------|
| gid              | varchar                   | 用户标识符 |
| tag_id           | varchar                   | 标签id     |
| tag_value        | varchar                   | 标签值     |
| in_time          | bigint                    | 更新时间   |
| gid, tag_id      | map&lt;string, string&gt; | 联合主键   |
