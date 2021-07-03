---
description: >-
  小程序无埋点SDK在代码埋点基础上，增加自动采集页面访问和浏览事件，页面元素的点击事件，元素值改变事件以及表单提交事件等，作为代码埋点的补充并结合对重要事件的圈选，支持特定场景的分析应用，如元素事件分析、页面热图分析等。
---

# 小程序无埋点SDK

{% hint style="info" %}
GrowingIO增长平台14.0版本以上支持无埋点应用
{% endhint %}

## 下载SDK

{% tabs %}
{% tab title="微信小程序" %}
下载地址：[https://assets.giocdn.com/sdk/cdp/3.0/gio-minp.js](https://assets.giocdn.com/sdk/cdp/3.0/gio-minp.js)
{% endtab %}
{% endtabs %}

##  代码集成

见[小程序SDK](./)

## 用户隐私字段屏蔽

从用户隐私安全考虑，SDK支持在初始化阶段设置需要屏蔽的用户隐私相关的字段，以便于不再采集和上报。

### 屏蔽范围

| 字段 | 含义 | 备注 |
| :--- | :--- | :--- |
| deviceBrand | 设备品牌 | 如HONOR |
| deviceModel | 设备型号 | 如BMH-AN10 |
| deviceType | 设备类型 | 如Weixin-Android |
| screenHeight | 设备屏幕尺寸 - 高度 | 2400 |
| screenWidth | 设备屏幕尺寸 - 宽度 | 1080 |
| IP | 用户的客户端IP地址 |  |

### 屏蔽方法

SDK初始化时，设置ignoreFields参数包含屏蔽范围中的字段即可。

{% tabs %}
{% tab title="微信小程序" %}
```text
gio('init', 'your projrctId','your datasourceID','your appId', {
    ignoreFields: ['deviceBrand', 'deviceModel','deviceType', 'screenHeight', 'screenWidth']
})
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
IP字段过滤

SDK不采集用户的客户端IP信息，GrowingIO收到的IP数据是从http请求中获取的，屏蔽方法使用 0.0.0.0 覆盖 header中的X-G-Real-IP，此配置可添加在负载均衡侧。
{% endhint %}









