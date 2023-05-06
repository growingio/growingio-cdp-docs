---
id: tracking-deeplink
sidebar_position: 2
---

# 深度链接

深度链接适用于促活、唤回场景，对于 App 已安装，希望通过广告推广促进用户打开 App 或召回老客户，可通过该方式来创建深度链接（DeepLink）来促使用户回到您的 App 中。

## 相关配置

在使用 GrowingIO 的深度链接功能时，首选需要完成以下配置：

APP 端 SDK 升级到以下版本：

- Android 3.4.6
- iOS 3.4.7

在正确集成 GrowingIO 提供的 SDK ，以及 URL Scheme 的配置后，即可开始使用 GrowingIO 提供的 DeepLink 深度链接功能。

SDK 端配置：

- iOS 端
- Android 端

为获得更好的用户使用体验，GrowingIO 同时建议您在 iOS 下开启 Universal Links 、在 Android 下开启 App Links ，该两项技术为 Apple 与 Google 提供的原生方案，使用该技术将在其系统生态中将获得更流畅的跳转体验。

- Universal Links 配置：​[深度链接配置](../acquisition-configuration#深度链接配置)
- App Links 配置：​[深度链接配置](../acquisition-configuration#深度链接配置)

## 新建深度链接

1. 在顶部导航栏选择“获客追踪>深度链接”，进入深度链接列表。

![图 1](/img/pic_1677211751668_tracking-deeplink.png)

2. 单击右上角的新建深度链接，进入新建深度链接页面。

![图 2](/img/pic_1677211797713_tracking-deeplink.png)

3. 配置参数后单击确定，展示创建好的深度链接。

## 查看数据指标

您可以查看有多少新用户通过延迟深度链接在 App 中到达了您设定的活动场景。

1. 在顶部导航栏选择获客分析 > 获客看板。
2. 选择您的 App 应用。
3. 在下方的推广日报模块单击自定义列，勾选延迟场景还原即可查看延迟深度链接的数据。
