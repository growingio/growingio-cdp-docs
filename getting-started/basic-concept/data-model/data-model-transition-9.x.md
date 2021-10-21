---
id: data-model-transition-9.x
sidebar_position: 3
---

# 旧版本兼容指南 \- 9.x版本

## 事件查询[](#shi-jian-cha-xun)

表模型[](#biao-mo-xing)

carbon.event_log 为分区表，数据时效性为小时，即数据截止到上一个小时。

event\_buffer\_second_{time} 为实时数据，正常情况 5-10秒钟 更新，time 格式为 2020100100 表示北京时间 10月1日早上8点。

| **事件类型** | **旧版** | **新版** |
| --- | --- | --- |
| 访问  | gio.visit | carbon.event\_log / event\_buffer\_second\_{time} |
| 页面  | gio.page | carbon.event\_log / event\_buffer\_second\_{time} |
| 打点  | gio.custom_event | carbon.event\_log / event\_buffer\_second\_{time} |

## 字段关系[](#zi-duan-guan-xi)

| **字段名** | **旧版** | **新版** |
| --- | --- | --- |
| 事件名 | n   | event_key |
| 事件时间 | stm | event_time |
| 事件 id | id  | event_id |
| 事件类型 | 无   | event_type |
| 客户端时间 | tm  | client_time |
| 匿名用户 id | u   | anonymous_user |
| 登录用户 id | un  | user |
| 用户类型 | 无   | user_type |
| GrowingIO 唯一 ID | gid | user_id |
| 访问 session | s   | user_session |
| 项目 id | ai  | account_id |
| 平台  | b   | platform |
| 域名  | d   | domain |
| 来源域名 | rd  | referrer_domain |
| IP  | ip  | ip  |
| 广告来源 | utm_source | utm_source |
| 广告媒介 | utm_medium | utm_medium |
| 广告名称 | utm_campaign | utm_campaign |
| 广告关键字 | utm_term | utm_term |
| 广告内容 | utm_content | utm_content |
| 搜索关键词 | kw  | key_word |
| 国家代号 | countryCode | country_code |
| 国家名称 | countryName | country_name |
| 地区  | region | region |
| 城市  | city | city |
| 客户端信息 | ua  | user_agent |
| 浏览器 | bw  | browser |
| 浏览器版本 | bwv | browser_version |
| 操作系统 | os  | os  |
| 操作系统版本 | osv | os_version |
| 客户端版本 | cv  | client_version |
| 应用渠道 | ch  | channel |
| 设备品牌 | db  | devcie_brand |
| 设备型号 | dm  | device_model |
| 设备类型 | ph  | device_type |
| 设备方向 | o   | deivce_orientation |
| 屏幕高度 | sh  | screen_height |
| 评估宽度 | sw  | screen_width |
| 经度  | lat | lat |
| 纬度  | lng | lng |
| 设备语言 | l   | language |
| 爬虫 id | bot_id | bot_id |
| 广告 id | aid | ads_id |
| 数据源 id | data\_source\_id | data\_source\_id |
| 事件属性 | es_map | attributes |
| 页面  | p   | attributes.path |
| 查询条件 | q   | attributes.query |
| 页面标题 | tl  | attributes.title |
| 来源  | rf  | attributes.referrer |
| 来源页面 | rp  | attributes.referrer_path |
| 时间分区 | time | time |
| 事件类型 | 无   | type |

## 示例[](#shi-li)

查询 10.1 去重用户数

```sql
-- 旧版本(9.0之前)

SELECT

  COUNT(DISTINCT t.gid) AS "去重用户数"

FROM (SELECT

  gid

FROM gio.visit

WHERE time >= '202009311600'

AND time < '202010011600'

UNION ALL

SELECT

  gid

FROM gio.custom_event

WHERE time >= '202009311600'

AND time < '202010011600') t
​

-- 新版本(9.0及之后)

SELECT

  COUNT(DISTINCT user_id) AS "去重用户数"

FROM carbon.event_log

WHERE time >= '202009311600'

AND time < '202010011600'
```

查询某设备当前的实时打点数据

```sql
//旧版本(9.0之前)

SELECT

  n,
  es_map

FROM gio.custom_event

WHERE time = '202011010000'

AND uni_key = '123'

-- 新版本(9.0及之后)


SELECT

  event_key,
  attributes

FROM event_buffer_second_2020110100

WHERE user = '123'
```
