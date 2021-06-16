# 旧版本兼容指南

## 事件查询

### 表模型

carbon.event\_log 为分区表，数据时效性为小时，即数据截止到上一个小时。

event\_buffer\_second\_{time} 为实时数据，正常情况 5-10秒钟 更新，time 格式为 2020100100 表示北京时间 10月1日早上8点。

| **事件类型** | **旧版** | **新版** |
| :--- | :--- | :--- |
| 访问 | gio.visit | carbon.event\_log / event\_buffer\_second\_{time} |
| 页面 | gio.page | carbon.event\_log / event\_buffer\_second\_{time} |
| 打点 | gio.custom\_event | carbon.event\_log / event\_buffer\_second\_{time} |

### 字段关系

| **字段名** | **旧版** | **新版** |
| :--- | :--- | :--- |
| 事件名 | n | event\_key |
| 事件时间 | stm | event\_time |
| 事件 id | id | event\_id |
| 事件类型 | 无 | event\_type |
| 客户端时间 | tm | client\_time |
| 匿名用户 id | u | anonymous\_user |
| 登录用户 id | un | user |
| 用户类型 | 无 | user\_type |
| GrowingIO 唯一 ID | gid | user\_id |
| 访问 session | s | user\_session |
| 项目 id | ai | account\_id |
| 平台 | b | platform |
| 域名 | d | domain |
| 来源域名 | rd | referrer\_domain |
| IP | ip | ip |
| 广告来源 | utm\_source | utm\_source |
| 广告媒介 | utm\_medium | utm\_medium |
| 广告名称 | utm\_campaign | utm\_campaign |
| 广告关键字 | utm\_term | utm\_term |
| 广告内容 | utm\_content | utm\_content |
| 搜索关键词 | kw | key\_word |
| 国家代号 | countryCode | country\_code |
| 国家名称 | countryName | country\_name |
| 地区 | region | region |
| 城市 | city | city |
| 客户端信息 | ua | user\_agent |
| 浏览器 | bw | browser |
| 浏览器版本 | bwv | browser\_version |
| 操作系统 | os | os |
| 操作系统版本 | osv | os\_version |
| 客户端版本 | cv | client\_version |
| 应用渠道 | ch | channel |
| 设备品牌 | db | devcie\_brand |
| 设备型号 | dm | device\_model |
| 设备类型 | ph | device\_type |
| 设备方向 | o | deivce\_orientation |
| 屏幕高度 | sh | screen\_height |
| 评估宽度 | sw | screen\_width |
| 经度 | lat | lat |
| 纬度 | lng | lng |
| 设备语言 | l | language |
| 爬虫 id | bot\_id | bot\_id |
| 广告 id | aid | ads\_id |
| 数据源 id | data\_source\_id | data\_source\_id |
| 事件属性 | es\_map | attributes |
| 页面 | p | attributes.path |
| 查询条件 | q | attributes.query |
| 页面标题 | tl | attributes.title |
| 来源 | rf | attributes.referrer |
| 来源页面 | rp | attributes.referrer\_path |
| 时间分区 | time | time |
| 事件类型 | 无 | type |

### 示例

查询 10.1 去重用户数

```text
//旧版本(9.0之前)

select
    count(distinct t.gid) as "去重用户数"
from 
    (
    select 
        gid 
    from gio.visit 
    where time >= '202009311600' 
        and time < '202010011600'
        
    union all
    
    select 
        gid 
    from gio.custom_event 
    where time >= '202009311600' 
        and time < '202010011600'
    ) t

//新版本(9.0及之后)

select 
    count(distinct user_id) as "去重用户数"
from carbon.event_log 
where time >= '202009311600' 
    and time < '202010011600'
```

查询某设备当前的实时打点数据

```text
//旧版本(9.0之前)

select 
    n
    ,es_map 
from gio.custom_event 
where time = '202011010000'
    and uni_key = '123'
    
//新版本(9.0及之后)

select 
    event_key
    ,attributes 
from event_buffer_second_2020110100 
where user = '123'
```

