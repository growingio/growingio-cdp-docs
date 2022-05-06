---
id: tan-chuang-faq
sidebar_position: 2
---

# 弹窗 FAQ

## **弹窗流程**[](#dan-chuang-liu-cheng)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MDJ-ZKn0jRNemBrFmfQ%2F-MDPVHAr64a35zWaj1zG%2Fimage.png?alt=media&token=18d40b31-93c3-4b1b-a156-37d8519fa6ea)

### 1. 想修改已经在运行的弹窗怎么办？**[](#1-xiang-xiu-gai-yi-jing-zai-yun-hang-de-dan-chuang-zen-mo-ban)

在弹窗详情页规则右上角可以点击修改，为了降低对线上弹窗影响，需要先将线上的弹窗下线，再进去编辑页，修改条件并测试没有问题后，可以再次上线弹窗，再次上线后之前收到过的用户不会再收到。


### 2. 消息中止后再上线，之前收到过弹窗的用户还会再收到吗？[](#2-xiao-xi-zhong-zhi-hou-zai-shang-xian-zhi-qian-shou-dao-guo-dan-chuang-de-yong-hu-huan-hui-zai-shou-dao-ma)

不会。每一个弹窗有唯一ID，会在SDK做去重。不管下线几次再上线，都是记录之前收到人的信息的。


### 3. 设置了埋点事件弹窗或者用户变量弹窗，但是没有弹窗？[](#3-she-zhi-le-mai-dian-shi-jian-dan-chuang-huo-zhe-yong-hu-bian-liang-dan-chuang-dan-shi-mei-you-dan-chuang)

如果是对已经弹过的弹窗的修改成埋点事件的话，建议创建新的弹窗试下。 确认用户是否在分群内。可从用户细查确认。 确认用户满足弹窗条件，可以从mobile debugger 看下埋点事件和 用户变量是否满足，是否与后台设置的一致，大小写没有错误。


### **4. 同一用户有多个弹窗，都满足时，优先级处理？**[](#4-tong-yi-yong-hu-you-duo-ge-dan-chuang-du-man-zu-shi-you-xian-ji-chu-li)

弹窗按照更新时间顺序弹窗。在同一个触发条件，且用户同时属于这两个弹窗的目标分群，那么在同一个时间只会收到一个弹窗，即最近**更新**过的弹窗消息。web弹窗里中央，左下角，右下角三个位置的弹窗支持同时弹。我们会持续优化这个功能，欢迎提出你的需求。


### **5. 为什么活动还没上线，但是已经有了点击/展示数据？**[](#5-wei-shi-mo-huo-dong-huan-mei-shang-xian-dan-shi-yi-jing-you-le-dian-ji-zhan-shi-shu-ju)

弹窗上线前，可以先测试弹窗。此时的弹窗展示和点击数据也会上报到数据端，所以在弹窗数据页看到这部分数据。


### 6. 弹窗功能是否稳定，上线后是否影响性能，是否页面加载时间过长?[](#6-dan-chuang-gong-neng-shi-fou-wen-ding-shang-xian-hou-shi-fou-ying-xiang-xing-neng-shi-fou-ye-mian-jia-zai-shi-jian-guo-chang)

GIO弹窗功能是后台加载的，不会影响用户现有的页面加载速度。已经有不少客户在线上环境验证过，弹窗稳定性是可以保证的。


### **7\. 上线后收不到弹窗是为什么？**[](#7-shang-xian-hou-shou-bu-dao-dan-chuang-shi-wei-shi-mo)

1.  先用设备扫码测试，看是否能正常弹出。（扫码测试用的设备，必须安装了相应App，且App内成功安装了弹窗SDK）
    
2.  如果测试设备也无法弹出，请联系GIO技术支持。
    
3.  弹窗上线后，会有最多3分钟的延时，如果是第一次设置后的时间可能会久一些，如果1个小时后仍然没有收到，请联系GIO开发人员。
    
4.  如果测试能正常弹出，上线后却收不到，可能为以下原因，请一一排查：
    
* 请检查**是否关闭了埋点功能**，因为**弹窗SDK依赖埋点**功能。
    
* 你使用的设备对应的访问用户没有在所选分群中，可以再复制一个同样的弹窗，修改分群为**全部访问用户**，测试能否收到。
    
* 已经点击过该弹窗，所以该弹窗不会再出现。
    
* 触发条件没有匹配，建议重新编辑弹窗，试下选择弹窗触发条件为「打开app」的时候弹出。过十来秒后退出APP后台，重新启动app。
    
* 重新冷启动APP，查看日志是否有类似下面内容，如果**popupWindows/PopupWindowEvent** 字段不为**null**表示弹窗正确获取到了，如果为**null**表示该设备不在群组中。
    
iOS

```
GTouch.GTouchManager: Load touch event config success, eventConfig is <GTouchEventConfig: self.splashs=(null), self.popupWindows=(

 "&lt;GrowingPopupWindowEvent: self.id=452, self.state=activated, self.content=https://statics.growingio.com/pages/20190410/1114/1554862553584/1554862553584-popupWindow.html?url_scheme=growing.4458a0c50d7fd57c, self.priority=1, self.updateAt=1554862553666, self.rule=<GrowingRule: self.action=appOpen, self.type=system, self.startAt=1176171353583, self.endAt=1933553753583, self.limit=5&gt;>"

), self.idMappings=&lt;GrowingIdMappings: self.bu=2787622, self.bcs=248881&gt;>
```

Android

```
D/GTouch.GTouchManager: Loading touch event config success result is TouchEventConfig{idMappings=IdMappings{bu=976846, bcs=137554}, splashs=\[\], popupWindows=\[PopupWindowEvent{id=297, state='null', content='https://statics.growingio.com/pages/20190328/3/1553767879538/1553767879538-popupWindow.html?url_scheme=growing.638b52710867187c', priority=1, updateAt=1553767879559, rule=Rule{action='appOpen', type='system', startAt=1175076679537, endAt=1932459079537, limit=1}}\]}
```

或者重新冷启动APP，通过抓包软件获取类似[https://xxxx.xxxx.com/marketing/automation/v3/your\_project\_id/notifications?url_scheme=xxxxx](https://messages.growingio.com/v1/xxxxxx/notifications?url_scheme=xxxxx) 的url的响应包，其中响应 json 中 popupWindows 字段不为 null 表示弹窗正确获取到了，如果为null表示该设备不在群组中。


### **8. 扫码测试时唤醒了app，但是没有弹出弹窗?**[](#8-sao-ma-ce-shi-shi-huan-xing-le-app-dan-shi-mei-you-dan-chu-dan-chuang)

如果 SDK 没有问题，刷新下二维码页面，然后试试杀死 app 后台进程，再次扫码唤醒。


### 9. 为什么目标分群人数会和实际展示的人数略有差异？[](#9-wei-shi-mo-mu-biao-fen-qun-ren-shu-hui-he-shi-ji-zhan-shi-de-ren-shu-lve-you-cha-yi)

* 用户网络环境差，导致加载弹窗资源超时或者失败。
    
* 在极少数机型上面WebView会初始化失败，所以弹窗无法弹出。
    
* 分群是每天早上更新，有可能部分用户上午活跃，弹窗是下午上线，但这部分用户下午并没有打开过App。
    

### 10. 是否Scheme必须配置正确，才能弹出弹窗?[](#10-shi-fou-scheme-bi-xu-pei-zhi-zheng-que-cai-neng-dan-chu-dan-chuang)

是的，Scheme是用于标示产品，没有产品无法过滤弹窗

### 11. Scheme要在哪里获取 ？[](#11-scheme-yao-zai-na-li-huo-qu)

**在数据 -** 「数据源管理」- 点开「具体的应用」-

在右侧栏可以看到应用的scheme


### 12. 选择了某个分群作为弹窗的目标人群，但该分群中只有部分人收到了弹窗，为什么？[](#12-xuan-ze-le-mou-ge-fen-qun-zuo-wei-dan-chuang-de-mu-biao-ren-qun-dan-gai-fen-qun-zhong-zhi-you-bu-fen-ren-shou-dao-le-dan-chuang-wei-shi-mo)

1.  这些用户的APP需要升级到了有弹窗SDK的App版本。
    
2.  因为网络环境或者手机版本兼容性等问题，可能有极少数用户是弹不出来的。
    

### 13. 我的App有闪屏广告，如何能在闪屏结束后再弹出弹窗？[](#13-wo-de-app-you-shan-ping-guang-gao-ru-he-neng-zai-shan-ping-jie-shu-hou-zai-dan-chu-dan-chuang)

appOpen是App从后台到前台，第一个activity onStarted 的时候触发，如果把握不准appOpen的时机，建议自定义事件（埋点），可以更精准的控制弹窗弹出的时机。

如下图，选择触发时机为您的打点时间，可以更精准的控制。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MDJ-ZKn0jRNemBrFmfQ%2F-MDP_IOyE4qLZtbtzETb%2Fimage.png?alt=media&token=7dca201c-9ae0-4434-be8f-521d7665c40d)

### **13. Android SDK 支持的最低版本是 Android 4.2，那低于这个版本的话会是什么表现？**[](#13-android-sdk-zhi-chi-de-zui-di-ban-ben-shi-android-4-2-na-di-yu-zhe-ge-ban-ben-de-hua-hui-shi-shi-mo-biao-xian)

由于 GTouch SDK 依赖埋点 SDK ，在低于 Android 4.2 的系统中，埋点 SDK 会自动关闭，这样我们的弹窗功能也会自动关闭，不会影响任何业务。

### 14. 弹窗设置了只弹出一次，为什么同一个设备或者同一个用户仍然会多次收到弹窗？[](#14-dan-chuang-she-zhi-le-zhi-dan-chu-yi-ci-wei-shi-mo-tong-yi-ge-she-bei-huo-zhe-tong-yi-ge-yong-hu-reng-ran-hui-duo-ci-shou-dao-dan-chuang)

1.  用户删除APP后重新下载了APP。
    
2.  用户同一个设备上切换了不同账号。
    
3.  用户在多台设备上登录了同一个账号。
    
4.  手机清除缓存
    
5.  有极少数用户由于手机硬盘或者系统低概率出现问题，导致弹窗数据无法正常写入到本地，导致下次弹窗仍然会弹出(基本可以忽略)。
    
### 15. 预览弹窗连续弹两次或多次？[](#15-yu-lan-dan-chuang-lian-xu-dan-liang-ci-huo-duo-ci)

您有可能在同一时间触发了两次对应的埋点事件，在预览模式下我们的sdk是触发一次对应的事件就弹一次对应的预览弹窗。

### 16. 弹窗的展示数比实际分群人数少？[](#16-dan-chuang-de-zhan-shi-shu-bi-shi-ji-fen-qun-ren-shu-shao)

* 部分用户更新了app的话，app当天采集的用户属性会被清空，导致这部分用户未能满足弹窗条件。
    
* GIO的分群人数会在每日凌晨重新计算，3-5点计算完毕。这期间基于分群发出去的弹窗还是旧分群范围，部分新范围内的用户无法命中，导致当天白天查看弹窗数据时，分群人数与弹窗展示数对不上。
    

### 17. 用户没有上报访问事件却上报弹窗展示事件？[](#17-yong-hu-mei-you-shang-bao-fang-wen-shi-jian-que-shang-bao-dan-chuang-zhan-shi-shi-jian)

* 访问事件由GIO埋点SDK上报，弹窗展示事件由GIO触达SDK上报，这是两个SDK。
    
* 埋点SDK数据上报策略默认为30秒一次，安卓用户打开APP后立马清后台的话，埋点的数据是不会上报上来的，但弹窗SDK的数据是实时上报的。所以会出现某个用户在某时间段有弹窗展示数据，但访问次数为0的情况。
    
* iOS埋点SDK一般不会有这种情况，有强制数据上报策略，避免清App后台导致数据不上报的情况。
    

### 18. 扫码预览不弹窗？[](#18-sao-ma-yu-lan-bu-dan-chuang)

* 建议刷新下网页，重新扫码。
    
* 还不行的话建议把弹窗设置成AppOpen事件触发，再扫码预览。先确认app能弹窗。
    
* 还是不行的话请立即联系我们。
    
* 小米手机扫码链接使用http唤醒不了app，浏览器有限制，需要用https。
    
* 扫码后出现null，刷新网页重新扫码
    

### 19. 弹窗自定义协议跳转获取不到openUrl？[](#19-dan-chuang-zi-ding-yi-xie-yi-tiao-zhuan-huo-qu-bu-dao-openurl)

* 换张不同图片的测试，图片加载出来会有缓存
