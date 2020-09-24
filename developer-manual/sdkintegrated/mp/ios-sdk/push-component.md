# 推送 SDK（iOS）



推送SDK最低兼容iOS 8.0 系统。

**GrowingTouchCoreKit.framework触达基础依赖库  
GrowingTouchCoreUI.bundle UI页面图  
GrowingPushKit.framework 触达推送库  
GrowingCDPPushExtensionKit.framework  图片推送和iOS 10以上统计后台通知的到达率**

## 一. 集成SDK

### 1. 集成GrowingIO iOS **CDP** 数据采集SDK  \(版本要求最低1.2.3\)

    详细步骤见[集成文档](https://docs.growingio.com/op/developer-manual/sdkintegrated/cdp/ios-sdk)  
    添加 handleUrl方法  [链接](https://docs.growingio.com/op/developer-manual/sdkintegrated/cdp/ios-sdk#handleurl)

### 2. 集成用户运营SDK

GrowingPushKit 和 GrowingCDPPushExtensionKit 都需要集成 ！   
GrowingPushKit 和 GrowingCDPPushExtensionKit 都需要集成 ！！   
GrowingPushKit 和 GrowingCDPPushExtensionKit 都需要集成 ！！！且不同target  
下载地址  
[http://assets.giocdn.com/cdp/ios/CDP1.2.4\_Touch1.4.1.zip](http://assets.giocdn.com/cdp/ios/CDP1.2.4_Touch1.4.1.zip)

* 下载最新的iOS GrowingTouch SDK包，并将其中的GrowingTouchCoreKit.framework、GrowingTouchCoreUI.bundle以及GrowingPushKit.framework 添加到iOS工程中

![](../../../../.gitbook/assets/image%20%28225%29.png)



* **添加扩展 Notification Service Extension** ，在 File -&gt; New -&gt; Target 中选择箭头所指，即可建立扩展GIOEdemoServiceExtension，

  * 请将 Notification Service Extension 中的 Deployment Target 设置为 **10.0**。

![](../../../../.gitbook/assets/image%20%28250%29.png)

* 将其中的**GrowingCDPPushExtensionKit.framework**包将之添到扩展**Notification Service Extension**

![](../../../../.gitbook/assets/image%20%28230%29.png)

* 确保扩展GrowingCDPPushExtensionKit引入成功，other link flags选项有添加`$(inherited)`  和`-ObjC` 添加编译参数，并注意大小写：

![](../../../../.gitbook/assets/image%20%28286%29.png)

请保证扩展的target  最低版本 iOS**10.0**  


![](../../../../.gitbook/assets/image%20%28251%29.png)

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

还要设置一下AccountID  dataSourceID  Trackhost

```objectivec
#import <GrowingCDPPushExtensionKit/GrowingPushExtensionKit.h>

- (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler {
    self.contentHandler = contentHandler;
    self.bestAttemptContent = [request.content mutableCopy];
    // 设置AccountID 和 dataSourceID
      [GrowingPushExtensionKit startWithAccountId:@"AccountId" dataSourceId:@"datasourceID "];
    // 设置Trackhost，埋点上报地址
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

![](../../../../.gitbook/assets/image%20%28242%29.png)

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

### **3. 如何在当前项目中添加**Notification Service Extension

针对 iOS 10.0 以上的系统，为了能支持图片推送和统计后台通知的到达率，可添加 **Notification Service Extension** 类型的 target ，调用指定的 API，具体参见“重要配置”中的第2条，在当前项目中添加 **Notification Service Extension** 步骤如下：

在 File -&gt; New -&gt; Target 中选择箭头所指，即可建立

![](../../../../.gitbook/assets/image%20%28244%29.png)



## 四. 常见问题

### 1. 推送跳转App原生界面

特别需要注意以下两点：

（1）如果点击跳转的原生界面是通过Objective-C开发的控制器，例如控制器名称为 InAppViewController ，传递参数为key1、key2，则推送Web 页面配置如下：

* **推送Web页面配置如下：**

![](../../../../.gitbook/assets/image%20%28254%29.png)



此时生成的跳转链接为`InAppViewController?key1=value1&key2=value2` ，点击自动跳转到原生界面InAppViewController，并携带两个参数。

在InAppViewController可以通过提前定义属性，获取参数

```objectivec
@interface InAppViewController : UIViewController
@property (nonatomic, copy) NSString *key1;
@property (nonatomic, copy) NSString *key2;
@end
```

（2）如果跳转的原生界面是通过swift开发的控制器，需要按照以下步骤进行接入。

例如跳转的原生界面是SFViewController.swift，示例项目工程为 TestDemo，在SFViewController.swift中可以通过提前定义属性，用于获取参数

```swift
class SFViewController: UIViewController {
    @objc var key1: String?
    @objc var key2: String?
    override func viewDidLoad() {
        super.viewDidLoad()  
        // Do any additional setup after loading the view.
    }
}
```

第1步：编译运行当前示例项目工程TestDemo（实际过程中应为对应的项目工程名称）

![](../../../../.gitbook/assets/image%20%28249%29.png)

第2步：运行成功之后，在Products文件夹下，选中 TestDemo.app 后 Show in Finder

![](../../../../.gitbook/assets/image%20%28243%29.png)

第3步：可以看到在Products文件夹同级补录下，有一个名为Intermediates.noindex 的文件夹，依次进入 TestDemo.build -&gt; Debug-iphoneos\(或Debug-iphonesimulator\) -&gt; TestDemo.build -&gt; DerivedSources 文件夹下

![](../../../../.gitbook/assets/image%20%28234%29.png)

![](../../../../.gitbook/assets/image%20%28237%29.png)

第4步：当前文件下有一个名为 TestDemo-Swift.h 的文件，双击打开在该文件中查找 SFViewController，发现该类声明的上方有一句 SWIFT\_CLASS\("\_TtC8TestDemo16SFViewController"\)

![](../../../../.gitbook/assets/image%20%28253%29.png)

\_TtC8TestDemo16SFViewController 即为原生界面SFViewController.swift转换后的类名， Web 页面配置如下：

**推送Web页面配置如下：**

![](../../../../.gitbook/assets/image%20%28229%29.png)

## 五. 如何判断iOS push集成成功

1.扫码测试推送成功跳转对应页面，代表GrowingPushKit集成成功  
2.创建图片测试推送,收到图片推送，代表GrowingPushExtensionKit集成成功

## 六. 工程项目的推送设置以及证书配置

### 1. 项目配置

在项目工程中打开后台推送权限设置，如下图所示

![](../../../../.gitbook/assets/image%20%28247%29.png)

打开推送开关Push Notifications，如下图所示  
****

![](../../../../.gitbook/assets/image%20%28231%29.png)

### 2. 创建App ID

> 如果之前已经创建了App ID可跳过这一步。

登录苹果开发者账号，点击如下图红色箭头区域，进入证书配置页面。

![](../../../../.gitbook/assets/image%20%28256%29.png)

选中“Identifiers”，并且对应的是“App IDs”  


![](../../../../.gitbook/assets/image%20%28235%29.png)

选中对应的平台（Platform），输入对应的描述（Description）、Bundle ID

![](../../../../.gitbook/assets/image%20%28238%29.png)

打开推送功能，选中如下图所示，点击右上角“continue”按钮，执行下一步

![](../../../../.gitbook/assets/image%20%28246%29.png)

确定信息无误后，点击右上角“Register”进行注册

![](../../../../.gitbook/assets/image%20%28255%29.png)

### 3. 创建本地CRS证书

打开MAC电脑上的钥匙串访问，点击窗口左上角的“钥匙串访问”中的“证书助理”，选择“从证书颁发机构请求证书…”

![](../../../../.gitbook/assets/image%20%28236%29.png)

将证书选择为“存储到磁盘”，输入任意合法的邮箱地址后即可将证书保存到本地目录路径下

![](../../../../.gitbook/assets/image%20%28252%29.png)

### 4. 创建推送证书

登录苹果开发者账号，点击下图红色箭头指示区域

![](../../../../.gitbook/assets/image%20%28245%29.png)

点击加号“+”，创建证书

![](../../../../.gitbook/assets/image%20%28226%29.png)

选择“Services”下创建推送证书，其中红色箭头指示的为创建开发调试环境下的推送证书，蓝色箭头指示的为创建生产环境以及开发调试下的推送证书，这里

![](../../../../.gitbook/assets/image%20%28239%29.png)

这里假如创建的是开发环境的推送证书，选中红色箭头对应的圆圈，点击右上角的“continue”按钮，进入下一步，选择项目对应的“App ID”，点击右上角的“continue”按钮，进入下一步

![](../../../../.gitbook/assets/image%20%28233%29.png)

选择本地的“CRS”文件，点击右上角的“continue”按钮，进入下一步，即可生成对应项目开发环境下的推送证书，点击右上角的“Download”按钮，将证书下载到本地，选中刚才下载的证书，双击安装。

### 5. 导出推送证书p12

打开MAC电脑上的钥匙串访问，找到刚才安装的推送证书，选中右击导出该证书

![](../../../../.gitbook/assets/image%20%28248%29.png)

设置证书的本地存储路径，选择导出证书的格式为个人信息交换\( .p12 \)，设置证书密码

![](../../../../.gitbook/assets/image%20%28240%29.png)

### 6. 上传证书

登录网站， 确保已经成功集成了触达推送SDK，在产品配置中的“应用配置”中

选择需要配置的推送证书的环境，输入对应的“BundleID”，选中本地导出的p12的推送证书，输入密码并保存。

## 七. 推送有效性检测

如果在GrowingIO上测试推送时，无法收到推送消息时，请先按照如下几个步骤进行自行排查

1、工程配置，确保打开推送配置以及勾选远程推送 Remote notifications

2、通知授权注册并在token回调方法中调用GIO接口，上传token  
通知授权注册请求，一般在程序启动方法中请求

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  
  //  通知授权注册请求方法，仅供参考
  [self registerRemoteNotification];
  return YES;
}

/** 注册 APNs */
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

在如下代理方法中将获取到的token上传到GIO

```objectivec
/** 远程通知注册成功委托 */
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    //  上传推送token
    [GrowingTouch registerDeviceToken:deviceToken];
    NSMutableString *deviceTokenString = [NSMutableString string];
    const char *bytes = deviceToken.bytes;
    NSInteger count = deviceToken.length;
    for (NSInteger i = 0; i < count; i++) {
        [deviceTokenString appendFormat:@"%02x", bytes[i] & 0xff];
    }

    NSLog(@"Token 字符串：%@", deviceTokenString);
}
```

3、本地测试推送  
下载推送工具（Pusher等），导入相应的推送证书，填入上一步获取到的token进行本地推送，截图如下（这里以Pusher为例）

![](../../../../.gitbook/assets/image%20%28228%29.png)

4、iOS 10 以后的图片推送送达检测  
确保项目中添加了ServiceExtension，类似如下图

![](../../../../.gitbook/assets/image%20%28241%29.png)

ServiceExtension的NotificationService类，在接收到推送的方法中调用GIO的API

```objectivec
#import <GrowingCDPPushExtensionKit/GrowingPushExtensionKit.h>

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

* 通过推送图片，确认收到图片推送即可

**如果上述1、2、3步骤都正常，从网站上进行测试推送时，无法收到消息，请联系我们！**

注意：

* App集成GIO的推送SDK，并发布到商店后，用户只有下载并打开了新版的App才可以上报推送令牌，这台设备才能够被送达。
* 分群是每日凌晨计算，所以如果用户A今天是第一次打开新版的App，那么第二天才能进入分群被送达到。所以建议您第一次发送 Push 等待一天。

