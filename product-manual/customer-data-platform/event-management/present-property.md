---
id: present-property
sidebar_position: 4
---

# 预定义属性

SDK默认采集信息


## 简介[](#jian-jie)

预定义属性为iOS、Android、JS和小程序各端SDK默认采集信息，以及由GrowingIO进行采集信息解析派生出来的信息。预定义属性仅能查看和使用，不能编辑和删除。


## 名词解释[](#ming-ci-jie-shi)

| 名称  | 含义  | 示例  |
| --- | --- | --- |
| 时间  | 事件发生的时间（日期） | 2019-01-01 |
| 域名  | Web端理解为：“[www.growingio.com](http://www.growingio.com/)”是<br></br>​[https://www.growingio.com/about](https://www.growingio.com/about) 的域名。<br></br>App理解为应用的包名。<br></br>小程序理解为AppID。 | ​[www.growingio.com](http://www.growingio.com/)​ |
| 应用平台端 | 即应用是指什么类型的终端，包括：网页、<br></br>iOS、Android、微信小程序(MinP)、H5应用、<br></br>支付宝小程序、微信公众号等。 | Web、iOS、<br></br>Android、MinP |
| App版本 | App和小程序的版本号。 | 5.1、5.2 |
| 访问来源 | 网站的流量来源，可以是百度、谷歌、优酷等站外渠道，<br></br>也可能是直接访问该网站。可以通过设置UTM参数来确<br></br>定流量具体是哪个广告带来的。 | ​[www.baidu.com](http://www.baidu.com/)、<br></br>m.baidu.com、直接访问、<br></br>微信-其他 |
| 一级访问来源 | 为了便于分析，我们将访问来源进行了归类。分为直接<br></br>访问、搜索引擎、社交媒体、外部链接四大部分。<br></br>-直接访问：可能是用户直接在浏览器中输入了一个域名<br></br>或使用书签进行访问；<br></br>-搜索引擎：[www.baidu.com](http://www.baidu.com/)、m.baidu.com、so.com、<br></br>sogou.com 等；<br></br>-社交媒体：weibo.com、zhihu.com、linkedin.com、<br></br>facebook.com、mp.weixin.qq.com等；<br></br>-外部链接：除了社交媒体、搜索网站之外的来源。 | 直接访问、搜索引擎、<br></br>社交媒体、外部链接 |
| 搜索词 | 用户从搜索引擎进入网站所使用的搜索词，一般情况下<br></br>付费搜索的搜索词可以被解析，但由于、百度、搜狗等<br></br>搜索引擎对自然搜索词加密的原因，来自这些搜索引擎<br></br>的自然搜索词将以“xx自然流量”的形式展示。如果在值<br></br>中出现N/A，意为这部分流量不是通过搜索词访问的。 | GrowingIO、热力图、<br></br>百度自然流量、<br></br>搜狗自然流量 |
| 广告来源 | utm_source，标识投放的广告来源。 | google、baidu、<br></br>toutiao |
| 广告名称 | utm_campaign，标识投放产品的具体广告系列名称、<br></br>标语、促销代码等。 | springsale |
| 广告内容 | utm_content，用于区分相似内容或同一广告内的链接。<br></br>如果在同一封EDM中使用了两个不同的链接，就可以使<br></br>用 utm_content 设置不同的值，以便判断哪个版本的效<br></br>果更好。 | textlink |
| 广告关键字 | utm_term，标识投放的付费搜索关键字。 | running+shose |
| 广告媒介 | utm_medium，标识投放的广告媒介或营销媒介，<br></br>例如CPC、Banner和EDM。 | cpc、banner、EDM |
| 自定义<br></br>App渠道 | 自定义App渠道。在App集成SDK的时候，针对安卓用户，<br></br>设置分包渠道。<br></br>在小程序中，则自动获取小程序打开的来源。目前支持<br></br>微信中60多种统计场景。 | huawei、oppo、<br></br>vivo、xiaomi |
| 城市  | 用户访问时所在的城市，Web基于IP地址，App和小程<br></br>序基于IP地址和GPS。优先判断GPS值，GPS值缺失时，<br></br>使用IP地址。 | 北京、上海、<br></br>广东、浙江 |
| 地区  | 用户访问时所在的城市，Web基于IP地址，该维度包含<br></br>国内省级以上行政区，以及国外地区。App和小程序基<br></br>于IP地址和GPS。优先判断GPS值，GPS值缺失时，使<br></br>用IP地址。 | 北京、上海、<br></br>广东、浙江 |
| 国家代码 | 用户所在的国家的英文缩写。 | CN、US、JP、SG |
| 国家名称 | 用户所在的国家的名称。 | 中国、美国、<br></br>英国、新加坡 |
| 浏览器 | 用户所用浏览器的类型。 | Chrome、<br></br>Chrome Mobile、<br></br>Safari、IE |
| 浏览器版本 | 同浏览器，但是会按照不同的版本进行区分。 | Chrome 47.0.2526、<br></br>IE 8.0、Firefox 65.0 |
| 操作系统 | 用户所使用的操作系统。 | Mac OS X、Android、<br></br>weixin-iOS、<br></br>weixin-Android |
| 操作系统版本 | 同操作系统但是会按照不同的版本进行区分。 | Android 4.0、<br></br>Windows 8、Windows 7 |
| 屏幕大小<br></br>(高*宽) | Web端是窗口大小，移动端是屏幕大小。 | 640_360、1920_1080 |
| 操作系统<br></br>语言 | 统计不同的操作系统语言的使用情况。 | 简体中文、英文、繁体中文 |
| 设备品牌 | 设备的品牌。 | Apple、xiaomi、<br></br>huawei、oppo |
| 设备型号 | 设备的具体机型。 | iPhone X、iPhone 8 Plus、<br></br>OPPO R11 |
| 设备类型 | 设备的类型。 | 手机、平板电脑 |
| 设备方向 | 用户访问时使用的设备方向。 | 竖直、横向 |


## 功能说明[](#gong-neng-shuo-ming)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkM34qxXur5C43PN7N7%2F-MkM3vpQ0PiYvrvX14t6%2Fimage.png?alt=media&token=2235ec58-6440-446e-aba2-43d72d0f9df8)

在预定义属性管理页面可以查看预定义属性名称、标识符、含义、示例。

您也可以对预定义属性进行以下操作：

**搜索：**您可以在页面中列表上方的搜索框按预定义属性名称来搜索预定义属性。

**QuickView：**单击任一预定义属性，您可以在右侧弹出的预定义属性详情中，查看预定义属性的基本信息。


## 常见问题[](#chang-jian-wen-ti)

Q1. 是否可以统计到搜索引擎渠道的“搜索词”?

您的用户群体使用搜索引擎在搜索框中输入搜索词，通过此搜索词的返回结果访问您的网站，我们会记录用户在搜索框中输入的「搜索词」。

GrowingIO会针对百度、搜狗、谷歌、360这4个搜索引擎的搜索词进行解析。

* 谷歌的搜索词目前无法获取，包括所有浏览器。
    
* 付费的搜索词正常情况下都能被解析到 \-\-\- 未付费的搜索词对于不同的浏览器存在不同限制，当在不同的浏览器上使用上述搜索引擎搜索，能解析到的关键词会被收集，不能解析的归为“\[搜索引擎\]自然流量”。
    
* N/A表示，这部分流量不是通过搜索词访问的。
    
> 注：据[百度商业开发中心官方通知](http://dev2.baidu.com/newdev2/dist/index.html#/content/?pageType=3&productlineId=3&noticeId=323)，百度预计将于 7 月 1 日（7 月 1 日开始小流量，7 月 7 日全流量）对搜索推广流量 referer 中搜索关键词字段下线。

由于 GrowingIO 是通过解析搜索推广流量 refer url 的方式来统计本次访问搜索关键词，本次升级将会对原有的搜索关键词获取产生影响，具体表现是：「用户来源」中的「搜索词」数据无法解析，将被归为「百度自然流量」。
