---
id: kafka_data_export
sidebar_position: 2
---

# kafka 订阅

## 简介

GrowingIO 为开放架构，实时采集的用户行为数据支持订阅导出，以满足更多的使用场景，如基于用户事件触发的商品推荐、消息推送等。

同时在开放平台，您不仅开以按项目开启/关闭订阅服务，还可以设置订阅范围类型，设置 有消费数据权限的 host 白名单 ，一键复制连接信息。
![图 1](/img/01zhengti.png)  

## 功能边界或约束​
使用前提：为确保开启订阅后的分析云环境稳定运行，使用本功能前需要先对您的分析云环境进行资源评估。
  请您联系 CSM 申请使用，同时需要您提供以下信息：订阅项目范围、订阅的数据类型、以及日活用户量。

## 功能说明

功能管理入口：【开放平台】 - 【kafka订阅】

### 开启订阅
![图2](/img/02peizhixinxi.png)  

支持订阅的数据类型包括事件数据、用户属性数据、维度表数据，按项目开启订阅，与设置数据类型范围可以帮我们完成配置数据导出的最小粒度。

host 白名单，是 将 kafka 订阅权限授权给指定 host 的配置，而且网络连接配置。白名单中配置的host，也需要在网络可连通的条件下订阅数据。

### 一键复制
支持一键复制链接信息，方便您复制到自己的环境通过客户端连接上kafka。

## 数据格式

### 事件数据
| kafka 字段  | 含义                                                                                   |
| -------- | -------------------------------------------------------------------------------------- |
| String event_key; | 事件标识|
| long event_time; | 事件接收时间（毫秒时间戳）  |
| long client_time | 事件发生时间（毫秒时间戳） |
| String anonymous_user; |访问用ID  |
| String user_id; | 登录用户ID |
| String user_key; | 用户身份类型    |
| String session;    | 会话标识，标记一个访问 |
|Map<String, String> attributes;	|事件属性|
|String package;	|APP包名/Web域名/小程序APPID|
|String $platform;|	平台标识，示例：Web|
|String $referrer_domain;	|来源域名或包名|
|String $path;	|页面路径|
|String $query;	|页面query参数|
|String $key_word;	|访问来源广告关键字|
|String account_id;	|系统账户ID，由SDK集成时设置|
| String $domain;	|域名或包名|
|String $ip;	|客户端ID地址|
|String $user_agent;|浏览器 agent 详细信息|
|String $sdk_version;|	SDK版本号|
|String dataSourceId;	|数据源信息  |

```json
{
    "event_key": "$PAGE",
    "event_type": "PAGE",
    "event_time": 1679363306000,
    "client_time": 1679363306000,
    "anonymous_user": "7196f014-d7bc-4bd8-b920-757cb2375ff6",
    "user_id": "zhang88803",
    "user_key": "$basic_userId",
    "session": "d5cbcf77-b38b-4223-954f-c6a2fdc0c098",
    "account_id": "a568c548b68ae7f4",
    "attributes": {
        "$domain": "wechatapplet",
        "$client_version": "1.2.4",
        "$language": "zh_CN",
        "$platform": "Android",
        "$device_model": "Nexus 5",
        "$url_scheme": "wechatapplet/app",
        "$sdk_version": "3.3.6",
        "$index": "0",
        "$ip": "111.198.136.130",
        "$channel": "微信小程序",
        "$session": "d5cbcf77-b38b-4223-954f-c6a2fdc0c098",
        "$user_agent": "PostmanRuntime/7.32.2",
        "$path": "/home/test",
        "$device_brand": "google"
    }
}

```               

### 用户数据
| kafka 字段  | 含义                                                                                   |
| -------- | -------------------------------------------------------------------------------------- |
|String account_id;|系统账户ID，由SDK集成时设置|
|String prop_key;	|属性标识符|
|String prop_value;|	属性值|
|long send_time;	|属性接收时间|
|String user_key;|	用户身份|
|String user_id;	|登录用户ID|
|String anonymous_id;	|匿名用户ID|


```json
{
    "account_id": "a568c548b68ae7f4",
    "prop_key": "hisuservar",
    "prop_value": "hisuservar001",
    "send_time": 1683545578034,
    "user_key": "$basic_userId",
    "anonymous_id": "",
    "user_id": "his_050801"
}

```               
### 维度表数据
| kafka 字段  | 含义                                                                                   |
| -------- | -------------------------------------------------------------------------------------- |
|String account_id;	|系统账户ID，由SDK集成时设置|
|String prop_key;|	维度表字段标识符|
|String prop_value;	|维度表字段值|
|String item_key;|	维度表标识符|
|String item_value;|	维度表记录ID   |


```json
{
    "account_id": "3",
    "prop_key": "v4_flo",
    "prop_value": "34.44989",
    "item_key": "v4_lipstick",
    "item_value": "item300001"
}

```               

# 常见问题
Q：能按组订阅 Kafka 数据吗？
A：请使用默认分组 default_group 订阅项目下数据。可以通过订阅范围修改默认分组可订阅到的范围。

Q：Kafka 订阅不到数据可能的原因
A：请先检查您的机器是否有订阅权限，点击编辑，查看host 白名单配置。如您的机器已经在权限白名单中，代表您有订阅权限。此时您需要确认网络连通性，请确认通过 telnet hostname 9092 能访问 GrowingIO 部署的服务器。

