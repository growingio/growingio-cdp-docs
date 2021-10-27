---
id: mp-ios-push-sdk
sidebar_position: 3
---

# 推送 SDK（iOS）

推送SDK最低兼容iOS 8.0 系统。

**GrowingTouchCoreKit.framework触达基础依赖库 GrowingTouchCoreUI.bundle UI页面图 GrowingPushKit.framework 触达推送库 GrowingCDPPushExtensionKit.framework 图片推送和iOS 10以上统计后台通知的到达率**


## 集成SDK[](#yi-ji-cheng-sdk)

### 集成GrowingIO iOS **CDP** 数据采集SDK[](#1-ji-cheng-growingio-ios-cdp-shu-ju-cai-ji-sdk)

推送 SDK 依赖于数据数据采集 SDK

版本要求最低1.2.3，如已集成请跳过

参考 [iOS SDK](https://growingio.github.io/growingio-sdk-docs/docs/ios/base/Getting_Started)


### 添加支持用户运营扫码的代码[](#tian-jia-zhi-chi-yong-hu-yun-ying-sao-ma-de-dai-ma)

> 在 AppDelegate 中添加

因为您代码的复杂程度以及iOS SDK的版本差异，有时候 [Growing handleUrl:url] 并没有被调用。请在各个平台上调试这段代码，确保当App被URL scheme唤醒之后，该函数能被调用到。

```swift
-  (BOOL)application:(UIApplication  *)application openURL:(NSURL  *)url sourceApplication:(NSString  *)sourceApplication annotation:(id)annotation

{

 // 如果没有触发handleUrl 扫码弹窗 和扫码注册推送不生效

 if  ([Growing handleUrl:url])  // 请务必确保该函数被调用

 {

 return  YES;

 }

 return  NO;

}
```


### 集成用户运营SDK[](#2-ji-cheng-yong-hu-yun-ying-sdk)

GrowingPushKit 和 GrowingCDPPushExtensionKit 都需要集成 ！ GrowingPushKit 和 GrowingCDPPushExtensionKit 都需要集成 ！！ GrowingPushKit 和 GrowingCDPPushExtensionKit 都需要集成 ！！！且不同target

下载地址[http://assets.giocdn.com/cdp/ios/CDPTouch1.4.7.zip](http://assets.giocdn.com/cdp/ios/CDPTouch1.4.7.zip)​

* 下载最新的iOS GrowingTouch SDK包，并将其中的GrowingTouchCoreKit.framework、GrowingTouchCoreUI.bundle以及GrowingPushKit.framework 添加到iOS工程中
    
![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC4y_fzXidyXlx3J-dz%2F-MC4zf6RuSFL-IvM8s2g%2Fimage.png?alt=media&token=c3a22d88-91f6-4b98-ac50-86eb09c4ec5d)

* **添加扩展 Notification Service Extension** ，在 File -> New -> Target 中选择箭头所指，即可建立扩展GIOEdemoServiceExtension，
    
    * 请将 Notification Service Extension 中的 Deployment Target 设置为 **10.0**。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC4y_fzXidyXlx3J-dz%2F-MC4zrJzMWgmWfU1cFot%2Fimage.png?alt=media&token=d3b75acf-8d23-4e89-bd73-81a062f68e36)

* 将其中的**GrowingCDPPushExtensionKit.framework**包将之添到扩展**Notification Service Extension**
    
![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC4y_fzXidyXlx3J-dz%2F-MC5--REJDn80V5v8L01%2Fimage.png?alt=media&token=0e4de0ab-0ded-40dc-a35e-669902684173)

* 确保扩展GrowingCDPPushExtensionKit引入成功，other link flags选项有添加`$(inherited)` 和`-ObjC` 添加编译参数，并注意大小写：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MDILJrV6oEz9XPU1RZb%2F-MDILYd4BY5K51IyUK15%2Fimage.png?alt=media&token=ce352e20-85ee-450b-98a0-2398d4b6b7fc)

请保证扩展的target 最低版本 iOS**10.0**

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC4y_fzXidyXlx3J-dz%2F-MC5-MFjBfLF05zeEqKW%2Fimage.png?alt=media&token=071e8fee-4dfe-43c1-973c-6bae0c44dcc1)


## 编写集成代码 重要配置[](#er-bian-xie-ji-cheng-dai-ma-zhong-yao-pei-zhi)

###  AppDelegate 写入 **推送设备的deviceToken上传**[](#1-appdelegate-xie-ru-tui-song-she-bei-de-devicetoken-shang-chuan)

用户自行实现通知注册请求授权后，在 AppDelegate 的 deviceToken 代理方法中调用API，传入获取到的 deviceToken，请确保能获取 deviceToken，否则无法接收通知消息。 #import <UserNotifications/UserNotifications.h>

```swift
#import <UserNotifications/UserNotifications.h>

​

-  (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {

 [GrowingTouch registerDeviceToken:deviceToken];

}
```

通知注册请求授权码可参考如下：

```swift
-  (void)registerRemoteNotification {

 if  (@available(iOS 10,*))  {

 UNUserNotificationCenter *center =  [UNUserNotificationCenter currentNotificationCenter];

 center.delegate =  self;

 [center requestAuthorizationWithOptions:(UNAuthorizationOptionAlert | UNAuthorizationOptionSound )

 completionHandler:^(BOOL granted, NSError * _Nullable error)  {

 if  (granted)  {

 dispatch_async(dispatch\_get\_main_queue(),  ^{ 

 [[UIApplication sharedApplication] registerForRemoteNotifications];

 });

 }

 }];

 }  else  if  ([[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)])  {

 UIUserNotificationType type = UIUserNotificationTypeAlert | UIUserNotificationTypeBadge | UIUserNotificationTypeSound;

 UIUserNotificationSettings *settings =  [UIUserNotificationSettings settingsForTypes:type

categories:nil];

 [[UIApplication sharedApplication] registerUserNotificationSettings:settings];

 [[UIApplication sharedApplication] registerForRemoteNotifications];

 }

}
```


### 扩展中写入，**Notification Service Extension**扩展的后台通知回执接口调用 `handleNotificationRequest: withCompletion:`[](#2-kuo-zhan-zhong-xie-ru-notification-service-extension-kuo-zhan-de-hou-tai-tong-zhi-hui-zhi-jie-kou-tiao-yong-handlenotificationrequest-withcompletion)

在 iOS10 提供的扩展 Notification Extension Service 中通知接收方法中调用通知消息回执接口，代码示例如下：(**注意不是写在AppDelegate中,是写在你新建的扩展里面**)

还要设置一下AccountID dataSourceID Trackhost

```swift
#import <GrowingCDPPushExtensionKit/GrowingPushExtensionKit.h>

​

-  (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void  (^)(UNNotificationContent * _Nonnull))contentHandler {

 self.contentHandler = contentHandler;

 self.bestAttemptContent =  [request.content mutableCopy];

 // 设置AccountID 和 dataSourceID

 [GrowingPushExtensionKit startWithAccountId:@"AccountId" dataSourceId:@"datasourceID "];

 // 设置Trackhost，埋点上报地址

 [GrowingPushExtensionKit setTrackerHost:@"your track host"];

 [GrowingPushExtensionKit handleNotificationRequest:request

 withCompletion:^(NSArray<UNNotificationAttachment *>  * _Nullable attachments, NSArray<NSError *>  * _Nullable errors)  {

 // Modify the notification content here...

 self.bestAttemptContent.attachments = attachments;  // 设置附件

 self.contentHandler(self.bestAttemptContent);

 }];

}
```


### 推送消息自定义协议的处理 clickMessageWithCompletionHandler:[](#3-tui-song-xiao-xi-zi-ding-yi-xie-yi-de-chu-li-clickmessagewithcompletionhandler)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC4y_fzXidyXlx3J-dz%2F-MC51EH8N_RR2Q34dEOz%2Fimage.png?alt=media&token=e5171170-a525-4702-8531-929318ef10ca)

推送功能默认提供打开APP、打开网页、打开APP内部页面三种功能，如果该三种功能还是满足不了您的需求，您可以在SDK提供的以下方法回调中自定义自己的跳转逻辑。

```swift
//  点击消息跳转用户自定义

+  (void)clickMessageWithCompletionHandler:(void  (^)(NSDictionary *params))completionHandler;
```


## 注意事项[](#san-zhu-yi-shi-xiang)

由于iOS的远程推送通知在各个版本上有一定的改动，为了统计数据更加准确，需要针对不同的系统分别做相应的处理


### iOS 10以下的系统[](#1-ios-10-yi-xia-de-xi-tong)

针对 Remote Notifications 系统提供了以下2个通知接收方法，如果您的应用支持iOS 10 以下的系统，请至少实现如下2个方法中的任意一个，建议实现方法2

```swift
//  1、早期的方法，iOS 10 以后废弃，依然可以使用

-  (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo NS\_DEPRECATED\_IOS(3_0,  10_0）；

​

//  2、上述方法的替代方法

-  (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void  (^)(UIBackgroundFetchResult result))completionHandler NS\_AVAILABLE\_IOS(7_0)；
```


### iOS 10及以上系统[](#2-ios-10-ji-yi-shang-xi-tong)

对于iOS 10 及以上的系统，请通过 **UNUserNotificationCenter** 请求通知授权并设置代理，并同时实现如下2个通知代理接收方法

```swift
-  (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void  (^)(UNNotificationPresentationOptions options))completionHandler；

-  (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler ;
```


###  如何在当前项目中添加 Notification Service Extension[](#3-ru-he-zai-dang-qian-xiang-mu-zhong-tian-jia-notification-service-extension)

针对 iOS 10.0 以上的系统，为了能支持图片推送和统计后台通知的到达率，可添加 **Notification Service Extension** 类型的 target ，调用指定的 API，具体参见“重要配置”中的第2条，在当前项目中添加 **Notification Service Extension** 步骤如下：

在 File -> New -> Target 中选择箭头所指，即可建立

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC52JJRHtwQxFLSbzc2%2Fimage.png?alt=media&token=82eaf562-d8fd-40c6-8c1c-3fd2f54157c2)


## 常见问题[](#si-chang-jian-wen-ti)

### 推送跳转App原生界面[](#1-tui-song-tiao-zhuan-app-yuan-sheng-jie-mian)

特别需要注意以下两点：

（1）如果点击跳转的原生界面是通过Objective-C开发的控制器，例如控制器名称为 InAppViewController ，传递参数为key1、key2，则推送Web 页面配置如下：

* **推送Web页面配置如下：**

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC52agxViaw23nTztFh%2Fimage.png?alt=media&token=a47464b1-f75f-4158-8d3f-587d70a5b0d4)

此时生成的跳转链接为`InAppViewController?key1=value1&key2=value2` ，点击自动跳转到原生界面InAppViewController，并携带两个参数。

在InAppViewController可以通过提前定义属性，获取参数

```swift
@interface InAppViewController : UIViewController

@property  (nonatomic, copy) NSString *key1;

@property  (nonatomic, copy) NSString *key2;

@end
```

（2）如果跳转的原生界面是通过swift开发的控制器，需要按照以下步骤进行接入。

例如跳转的原生界面是SFViewController.swift，示例项目工程为 TestDemo，在SFViewController.swift中可以通过提前定义属性，用于获取参数

```swift
class  SFViewController:  UIViewController  {

 @objc  var key1:  String?

 @objc  var key2:  String?

 override  func  viewDidLoad()  {

 super.viewDidLoad() 

 // Do any additional setup after loading the view.

 }

}
```

第1步：编译运行当前示例项目工程TestDemo（实际过程中应为对应的项目工程名称）

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC52uPeAYdm6U5m9jTZ%2Fimage.png?alt=media&token=2fa9458a-a157-42e6-925d-c9167342427e)

第2步：运行成功之后，在Products文件夹下，选中 TestDemo.app 后 Show in Finder

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC532PsGX1fa8FBxiKA%2Fimage.png?alt=media&token=dc01a8aa-3a9e-4fd1-924d-a5a92d26c4ce)

第3步：可以看到在Products文件夹同级补录下，有一个名为Intermediates.noindex 的文件夹，依次进入 TestDemo.build -> Debug-iphoneos(或Debug-iphonesimulator) -> TestDemo.build -> DerivedSources 文件夹下

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC538aaZ9YJaXjtGZFs%2Fimage.png?alt=media&token=02088e8d-a387-4b6c-a944-3eb75a478a7a)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC53CE5mEuJukEBOwF9%2Fimage.png?alt=media&token=960232bc-44c9-4a82-84f7-1520e415fe52)

第4步：当前文件下有一个名为 TestDemo-Swift.h 的文件，双击打开在该文件中查找 SFViewController，发现该类声明的上方有一句 SWIFT\_CLASS("\_TtC8TestDemo16SFViewController")

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC53LUt9IOREvUCGDLp%2Fimage.png?alt=media&token=0c4e5faa-4a6a-4294-9008-8ae3469ef436)

_TtC8TestDemo16SFViewController 即为原生界面SFViewController.swift转换后的类名， Web 页面配置如下：

**推送Web页面配置如下：**

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC53T7LIH-Fn9VJYzjm%2Fimage.png?alt=media&token=3bbf89fe-c119-4d4f-80b7-1e3a9f6c73b2)


## 如何判断iOS push集成成功[](#wu-ru-he-pan-duan-ios-push-ji-cheng-cheng-gong)

1.扫码测试推送成功跳转对应页面，代表GrowingPushKit集成成功 2.创建图片测试推送,收到图片推送，代表GrowingPushExtensionKit集成成功


## 工程项目的推送设置以及证书配置[](#liu-gong-cheng-xiang-mu-de-tui-song-she-zhi-yi-ji-zheng-shu-pei-zhi)

### 项目配置[](#1-xiang-mu-pei-zhi)

在项目工程中打开后台推送权限设置，如下图所示

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC55PLQhk-GqF5quhkP%2Fimage.png?alt=media&token=bf7ce79e-1ae0-4dd5-a6fb-348e88fbf454)

打开推送开关Push Notifications，如下图所示

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC55XrDhYWHyLGqU-oX%2Fimage.png?alt=media&token=83d7293e-fadd-4dde-b13e-401b281ac9c9)

### 创建App ID[](#2-chuang-jian-app-id)

> 如果之前已经创建了App ID可跳过这一步。

登录苹果开发者账号，点击如下图红色箭头区域，进入证书配置页面。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC55fgSDLV3-TRIDtp-%2Fimage.png?alt=media&token=1e7cd9ba-b1f8-4536-a1f0-07852a3bb92d)

选中“Identifiers”，并且对应的是“App IDs”

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC55mqPekPrJahgwu3v%2Fimage.png?alt=media&token=8ae2d978-b59c-462d-9cbc-f17981b427fb)

选中对应的平台（Platform），输入对应的描述（Description）、Bundle ID

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC55vRLSt0OI161skpv%2Fimage.png?alt=media&token=a8e1e7bd-e6e8-4a8e-86a1-5ce1d1ef5a58)

打开推送功能，选中如下图所示，点击右上角“continue”按钮，执行下一步

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC561GZyXS8lHybbZ-D%2Fimage.png?alt=media&token=bde24005-2cfe-4ecc-8a19-49e6ccb76eff)

确定信息无误后，点击右上角“Register”进行注册

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC5692xccb4hHgWCsRd%2Fimage.png?alt=media&token=320432ea-7320-4776-a550-a8a62df65677)


### 创建本地CRS证书[](#3-chuang-jian-ben-di-crs-zheng-shu)

打开MAC电脑上的钥匙串访问，点击窗口左上角的“钥匙串访问”中的“证书助理”，选择“从证书颁发机构请求证书…”

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC56GoUtm5iAW4CfWU1%2Fimage.png?alt=media&token=0281e08a-0f12-447f-8793-cea87893456d)

将证书选择为“存储到磁盘”，输入任意合法的邮箱地址后即可将证书保存到本地目录路径下

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC56NsvUY64zCbxEQPs%2Fimage.png?alt=media&token=18b1d69c-278c-4d86-9aff-702a7c3d87ed)


### 创建推送证书[](#4-chuang-jian-tui-song-zheng-shu)

登录苹果开发者账号，点击下图红色箭头指示区域

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC56VRS4BaLnGmkjqK7%2Fimage.png?alt=media&token=a4c499e0-f6f4-4508-980e-a2e5e90953f8)

点击加号“+”，创建证书

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC56XkcdA4-cv6tX-44%2F-MC56oZqScnJewCcb6i6%2Fimage.png?alt=media&token=9fed35f5-5ec4-4f5c-b13d-ff487013afa0)

选择“Services”下创建推送证书，其中红色箭头指示的为创建开发调试环境下的推送证书，蓝色箭头指示的为创建生产环境以及开发调试下的推送证书，这里

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC56vjCNQAU-iph3Ek1%2F-MC5991p9mEjaHPvwg0W%2Fimage.png?alt=media&token=04b49852-7195-4f14-9357-5ffc6536091f)

这里假如创建的是开发环境的推送证书，选中红色箭头对应的圆圈，点击右上角的“continue”按钮，进入下一步，选择项目对应的“App ID”，点击右上角的“continue”按钮，进入下一步

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC56vjCNQAU-iph3Ek1%2F-MC59F4UkeYRoV4RknKx%2Fimage.png?alt=media&token=d0864ce5-4467-4ca2-b088-6184f0087614)

选择本地的“CRS”文件，点击右上角的“continue”按钮，进入下一步，即可生成对应项目开发环境下的推送证书，点击右上角的“Download”按钮，将证书下载到本地，选中刚才下载的证书，双击安装。


### 导出推送证书p12[](#5-dao-chu-tui-song-zheng-shu-p12)

打开MAC电脑上的钥匙串访问，找到刚才安装的推送证书，选中右击导出该证书

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC56vjCNQAU-iph3Ek1%2F-MC59NVDYr3KRxeC71cx%2Fimage.png?alt=media&token=c3eec922-b967-48c1-a1c4-372cabecc33e)

设置证书的本地存储路径，选择导出证书的格式为个人信息交换( .p12 )，设置证书密码

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC56vjCNQAU-iph3Ek1%2F-MC59Uce7xIqvklqfid_%2Fimage.png?alt=media&token=810f8b3c-e28e-428a-b70b-424e678b8d86)


### 上传证书[](#6-shang-chuan-zheng-shu)

登录网站， 确保已经成功集成了触达推送SDK，在产品配置中的“应用配置”中

选择需要配置的推送证书的环境，输入对应的“BundleID”，选中本地导出的p12的推送证书，输入密码并保存。


## 推送有效性检测[](#qi-tui-song-you-xiao-xing-jian-ce)

如果在GrowingIO上测试推送时，无法收到推送消息时，请先按照如下几个步骤进行自行排查

1、工程配置，确保打开推送配置以及勾选远程推送 Remote notifications

2、通知授权注册并在token回调方法中调用GIO接口，上传token 通知授权注册请求，一般在程序启动方法中请求

```swift
-  (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

 //  通知授权注册请求方法，仅供参考

 [self registerRemoteNotification];

 return YES;

}

​

/\*\* 注册 APNs */

-  (void)registerRemoteNotification {

 if  (@available(iOS 10,*))  {

 UNUserNotificationCenter *center =  [UNUserNotificationCenter currentNotificationCenter];

 center.delegate =  self;

 [center requestAuthorizationWithOptions:(UNAuthorizationOptionAlert | UNAuthorizationOptionSound )

 completionHandler:^(BOOL granted, NSError * _Nullable error)  {

 if  (granted)  {

 dispatch_async(dispatch\_get\_main_queue(),  ^{

 [[UIApplication sharedApplication] registerForRemoteNotifications];

 });

 }

 }];

 }  else  if  ([[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)])  {

 UIUserNotificationType type = UIUserNotificationTypeAlert | UIUserNotificationTypeBadge | UIUserNotificationTypeSound;

 UIUserNotificationSettings *settings =  [UIUserNotificationSettings settingsForTypes:type

 categories:nil];

 [[UIApplication sharedApplication] registerUserNotificationSettings:settings];

 [[UIApplication sharedApplication] registerForRemoteNotifications];

 }

}
```

在如下代理方法中将获取到的token上传到GIO

```swift
/\*\* 远程通知注册成功委托 */

-  (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {

 //  上传推送token

 [GrowingTouch registerDeviceToken:deviceToken];

 NSMutableString *deviceTokenString =  [NSMutableString string];

 const  char  *bytes = deviceToken.bytes;

 NSInteger count = deviceToken.length;

 for  (NSInteger i =  0; i < count; i++)  {

 [deviceTokenString appendFormat:@"%02x", bytes[i]  &  0xff];

 }

​

 NSLog(@"Token 字符串：%@", deviceTokenString);

}
```

3、本地测试推送 下载推送工具（[Knuff](https://github.com/KnuffApp/Knuff/releases/tag/v1.3) 等），导入相应的推送证书，填入上一步获取到的 token 进行本地推送，截图如下（这里以 Knuff 为例）

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-Mit97KKXXvr2LCIU2w0%2F-Mit9F2wVxPYr8wOATUn%2Fimage.png?alt=media&token=38b1a0f9-f44d-4370-8571-b6d437e24bf3)

4、iOS 10 以后的图片推送送达检测 确保项目中添加了ServiceExtension，类似如下图

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC56vjCNQAU-iph3Ek1%2F-MC5A_ppsxyXnu1-wHwA%2Fimage.png?alt=media&token=7e0bece6-a997-4355-acad-1b59cb0e89aa)

ServiceExtension的NotificationService类，在接收到推送的方法中调用GIO的API

```swift
#import <GrowingCDPPushExtensionKit/GrowingPushExtensionKit.h>

​

-  (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void  (^)(UNNotificationContent * _Nonnull))contentHandler {

 self.contentHandler = contentHandler;

 self.bestAttemptContent =  [request.content mutableCopy];

 [GrowingPushExtensionKit startWithAccountId:@"AccountId" dataSourceId:@"datasourceID "];

 [GrowingPushExtensionKit setTrackerHost:@"your track host"];

 [GrowingPushExtensionKit handleNotificationRequest:request

 withCompletion:^(NSArray<UNNotificationAttachment *>  * _Nullable attachments, NSArray<NSError *>  * _Nullable errors)  {

 // Modify the notification content here...

 self.bestAttemptContent.attachments = attachments;  // 设置附件

 self.contentHandler(self.bestAttemptContent);

 }];

}
```

* 通过推送图片，确认收到图片推送即可

**如果上述1、2、3步骤都正常，从网站上进行测试推送时，无法收到消息，请联系我们！**

注意：

* App集成GIO的推送SDK，并发布到商店后，用户只有下载并打开了新版的App才可以上报推送令牌，这台设备才能够被送达。
    
* 分群是每日凌晨计算，所以如果用户A今天是第一次打开新版的App，那么第二天才能进入分群被送达到。所以建议您第一次发送 Push 等待一天。
