# 推送 SDK（iOS）

推送SDK最低兼容iOS 8.0 系统。

**GrowingTouchCoreKit.framework触达基础依赖库  
GrowingTouchCoreUI.bundle UI页面图  
GrowingPushKit.framework 触达推送库  
GrowingPushExtensionKit.framework  图片推送和iOS 10以上统计后台通知的到达率**

## 一. 集成SDK

### 1. 集成GrowingIO iOS **CDP** 埋点SDK  \(版本要求最低1.2.3\)

    

### 2. 集成用户运营SDK

GrowingPushKit 和 GrowingPushExtensionKit 都需要集成 

* 下载最新的iOS GrowingTouch SDK包，并将其中的GrowingTouchCoreKit.framework、GrowingTouchCoreUI.bundle以及GrowingPushKit.framework 添加到iOS工程中

![](../../../../.gitbook/assets/image%20%28225%29.png)



* **添加扩展 Notification Service Extension** ，在 File -&gt; New -&gt; Target 中选择箭头所指，即可建立扩展GIOEdemoServiceExtension，

  * 请将 Notification Service Extension 中的 Deployment Target 设置为 **10.0**。

![](../../../../.gitbook/assets/image%20%28230%29.png)

* 将其中的**GrowingPushExtensionKit.framework**包将之添到扩展**Notification Service Extension**

![](../../../../.gitbook/assets/image%20%28227%29.png)

* 确保扩展GrowingPushExtensionKit引入成功，other link flags选项有添加`$(inherited)`  和`-ObjC` 添加编译参数，并注意大小写：

![](../../../../.gitbook/assets/image%20%28226%29.png)

请保证扩展的target  最低版本 iOS**10.0**  


![](../../../../.gitbook/assets/image%20%28231%29.png)

## 二. 编写集成代码 重要配置

### **1.** AppDelegate 写入 **推送设备的deviceToken上传**

用户自行实现通知注册请求授权后，在 AppDelegate 的 deviceToken 代理方法中调用API，传入获取到的 deviceToken，请确保能获取 deviceToken，否则无法接收通知消息。  
  \#import &lt;UserNotifications/UserNotifications.h&gt;

```objectivec
#import <UserNotifications/UserNotifications.h>

- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    [GrowingTouch registerDeviceToken:deviceToken];
}
```

通知注册请求授权码可参考如下：

```objectivec
- (void)registerRemoteNotification {
    if (@available(iOS 10,*)) {
        UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
        center.delegate = self;
        [center requestAuthorizationWithOptions:(UNAuthorizationOptionAlert | UNAuthorizationOptionSound )
                              completionHandler:^(BOOL granted, NSError * _Nullable error) {
                                  if (granted) {
                 dispatch_async(dispatch_get_main_queue(), ^{         
                                          [[UIApplication sharedApplication] registerForRemoteNotifications];
                                      });
                                  }
                              }];
    } else if ([[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        UIUserNotificationType type =  UIUserNotificationTypeAlert | UIUserNotificationTypeBadge | UIUserNotificationTypeSound;
        UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:type
categories:nil];
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
    }
}
```

### 2. 扩展中写入，**Notification Service Extension**扩展的后台通知回执接口调用 `handleNotificationRequest: withCompletion:`

在 iOS10 提供的扩展 Notification Extension Service 中通知接收方法中调用通知消息回执接口，代码示例如下：\(**注意不是写在AppDelegate中,是写在你新建的扩展里面**\)

还要设置一下AccountId  dataSourceId  Trackhost

```objectivec
#import <GrowingPushExtensionKit/GrowingPushExtensionKit.h>

- (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler {
    self.contentHandler = contentHandler;
    self.bestAttemptContent = [request.content mutableCopy];
      [GrowingPushExtensionKit startWithAccountId:@"AccountId" dataSourceId:@"datasourceID "];
      [GrowingPushExtensionKit setTrackerHost:@"your track host"];
      [GrowingPushExtensionKit handleNotificationRequest:request
                                        withCompletion:^(NSArray<UNNotificationAttachment *> * _Nullable attachments, NSArray<NSError *> * _Nullable errors) {
        
        // Modify the notification content here...
        self.bestAttemptContent.attachments = attachments;   // 设置附件
        self.contentHandler(self.bestAttemptContent);
    }];
}
```

### 3. 推送消息自定义协议的处理 clickMessageWithCompletionHandler:

![](../../../../.gitbook/assets/image%20%28229%29.png)

推送功能默认提供打开APP、打开网页、打开APP内部页面三种功能，如果该三种功能还是满足不了您的需求，您可以在SDK提供的以下方法回调中自定义自己的跳转逻辑。

```objectivec
//  点击消息跳转用户自定义
+ (void)clickMessageWithCompletionHandler:(void (^)(NSDictionary *params))completionHandler;
```

## **三.注意事项**

由于iOS的远程推送通知在各个版本上有一定的改动，为了统计数据更加准确，需要针对不同的系统分别做相应的处理

### **1. iOS 10以下的系统**

针对 Remote Notifications 系统提供了以下2个通知接收方法，如果您的应用支持iOS 10 以下的系统，请至少实现如下2个方法中的任意一个，建议实现方法2

```objectivec
//  1、早期的方法，iOS 10 以后废弃，依然可以使用
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo NS_DEPRECATED_IOS(3_0, 10_0）；

//  2、上述方法的替代方法
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))completionHandler NS_AVAILABLE_IOS(7_0)；
```

### **2. iOS 10及以上系统**

对于iOS 10 及以上的系统，请通过 **UNUserNotificationCenter** 请求通知授权并设置代理，并同时实现如下2个通知代理接收方法



```objectivec
- (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler；

- (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler ;
```

