---
id: ios-sdk-faq
sidebar_position: 6
---

常见问题
====

推送流程介绍[](#ios_1)


--------------------

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5mMJ9jEBiG9kGcQJG%2F-MC5n4PKo-ASnPAcQD7a%2Fimage.png?alt=media&token=ea40405d-40ae-4d07-bba8-d3b9e50b188e)

简要说明iOS客户端实现推送流程的步骤：

* 第一步：要求客户端设备与APNs建立TSL连接，APNs需要验证设备的有效性；
    
* 第二步：客户端App向APNs请求推送消息用的Token；(SDK 内部实现)
    
* 第三步：客户端App将从APNs获取的Token注册到服务器分群信息中；（SDK内部实现）
    
* 第四步：通过用户运营创建分群推送消息，然后服务器再去请求APNs下发消息；
    
* 第五步：APNs服务器接收到服务器的推送消息请求后，根据Token来将推送的消息下发到指定的设备；
    
* 第六步：收到推送，上报推送送达信息，点击推送，跳转对应落地页
    

1\. 测试扫码打开app 没有预览弹窗或者没有上传推送设备信息[](#ios_1-1)


------------------------------------------------

确认一下 依赖的数据采集SDK是否是**1.2.3**以上 handleUrl 有没有调用到 Xcode 的控制台打印可看 **集成SDK版本 GrowingIO version: 1.2.3 !!! Thank you very much for using GrowingIO Touch. SDK version 1.4.1**

2\. iOS 扫码测试推送收不到推送消息？[](#2-ios-sao-ma-ce-shi-tui-song-shou-bu-dao-tui-song-xiao-xi)


----------------------------------------------------------------------------------------

推送必备条件：集成推送SDK，app开启推送， app环境与推送证书对应一致。

确认集成步骤是否缺失

确认app是否开启推送

确认证书与包名都正确

确认推送环境选择生产环境 和开发环境正确

确认证书没有过期 图片推送没收到，确认GrowingPushExtensionKit已集成，确认图片可下载，手动填写图片地址的链接是https

**3.安装app当天测试推送能推送到,但是分群推送推不到**[](#3-an-zhuang-app-dang-tian-ce-shi-tui-song-neng-tui-song-dao-dan-shi-fen-qun-tui-song-tui-bu-dao)


---------------------------------------------------------------------------------------------------------------------------------------

莫慌，因为分群T+1 ，推送令牌等信息还没有写入分群，请在第二天测试推送分群

**4.SDK最低兼容iOS系统。**[](#4sdk-zui-di-jian-rong-ios-xi-tong)


-------------------------------------------------------------

最低兼容iOS 8.0 系统。

**5.官网推送证书配置常见疑问**[](#5-guan-wang-tui-song-zheng-shu-pei-zhi-chang-jian-yi-wen)


-----------------------------------------------------------------------------------

官网推送证书过期，更新后是否需要打包 App 重新上架？ 不需要 官网推送证书的有效期是否可以设置？ 不能，该有效期是 Apple 决定的，自生成起有效期 1 年。 Apple 的生产推送证书允许用于开发环境的推送， 开发者可以上传生产证书到开发环境配置中，即可在官网推送平台处选择开发环境做推送。

6\. **iOS Token（推送令牌） 失效的原因？**[](#6-ios-token-tui-song-ling-pai-shi-xiao-de-yuan-yin)


-----------------------------------------------------------------------------------------

* 系统注销或者是应用被卸载。
    
* 用户在新的设备上安装 App。
    
* 用户从 backup 中恢复设备。
    
* 用户重新安装 OS。
    

7\. 证书验证[](#7-zheng-shu-yan-zheng)


--------------------------------------

Knuff 一款 iOS 苹果远程推送测试程序 。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-Mit8mmaK_qThkD6BLTv%2F-Mit8zlg39bdbO4Cp_Gs%2Fimage.png?alt=media&token=45163f40-dcba-46b5-adf9-107df42546f8)

地址：[https://github.com/KnuffApp/Knuff/releases/tag/v1.3](https://github.com/KnuffApp/Knuff/releases/tag/v1.3) iOS端接收到推送的通知有延迟 ？ 苹果开发环境有时推送通知延迟，可以基于第三方推送工具(Pusher)，测试通知推送，查看是否有延迟；
