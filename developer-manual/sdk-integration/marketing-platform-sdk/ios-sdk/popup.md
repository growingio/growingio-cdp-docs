---
id: mp-ios-popup-sdk
sidebar_position: 2
---

# 弹窗 SDK（iOS）

弹窗SDK最低兼容iOS 8.0 系统。

库简介

> GrowingTouchCoreKit.framework 运营基础库
> GrowingTouchCoreUI.bundle UI页面图
> GrowingTouchKit.framework 运营弹窗库
> GrowingTouchBannerKit.framework 运营banner库

## 集成SDK[](#yi-ji-cheng-sdk)

### 集成GrowingIO iOS CDP数据采集SDK[](#1-ji-cheng-growingio-ios-cdp-shu-ju-cai-ji-sdk)

:::info
弹窗 SDK 依赖于数据数据采集 SDK

版本要求最低1.2.3，如已集成请跳过
:::

参考 [iOS SDK](/op/v/2.0/developer-manual/sdkintegrated/client-sdk-3.0/ios-sdk)


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

### 集成运营SDK[](#2-ji-cheng-yun-ying-sdk)

手动集成SDK 下载最新的iOS GrowingTouch SDK包，并将其中的GrowingTouchCoreKit.framework、GrowingTouchCoreUI.bundle以及GrowingTouchKit.framework 添加到iOS工程中。下载链接：[http://assets.giocdn.com/cdp/ios/CDPTouch1.4.7.zip](http://assets.giocdn.com/cdp/ios/CDPTouch1.4.7.zip)​

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4mOetDAxVVM8YCSlJs%2F-M4mOmcb0LHDIZj_s540%2Fimage.png?alt=media&token=ba7ac106-deb9-444b-b087-3e5b7033fc4b)


### 初始化SDK[](#3-chu-shi-hua-sdk)

在 AppDelegate 中导入 `import <GrowingTouchCoreKit/GrowingTouchCoreKit.h>` 并添加初始化方法，且保证在 GrowingIO 采集SDK 启动代码后

```swift
-  (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

 ...

 // 启动GrowingIO采集SDK代码

 // 启动GrowingTouch，该方法需放在采集SDK之后；设置弹窗请求地址，一般与访问页面域名一致

 [GrowingTouch setServerHost:@"http://test.xxx.com"];

 [GrowingTouch start];

}
```

请注意调用顺序，需要在 GrowingIO 采集SDK 启动代码调用后，再调用 [GrowingTouch start] 函数。


## 重要配置[](#er-zhong-yao-pei-zhi)

### 设置弹窗SDK开关 setEventPopupEnable[](#1-she-zhi-dan-chuang-sdk-kai-guan-seteventpopupenable)

设置弹窗 SDK 的开关，默认是“YES”。因为每个 App 的实现方式不同，如果默认状态下弹窗在闪屏页或 启动页就会弹出，可以通过在初始化 SDK 设置 “NO” 来解决这个问题，当 App 的内容页打开时再进行弹窗：

+  (void)setEventPopupEnable:(BOOL)enable;

**参数说明**

| 参数名 | 类型  | 必填  | 说明  |
| --- | --- | --- | --- |
| enable | bool | 是   | 开关弹窗SDK。<br></br>* 开启YES<br></br>* 关闭NO<br></br>默认值YES |

**代码示例**

```swift
[GrowingTouch setEventPopupEnable:YES];
```


### 设置Debug模式 setDebugEnable[](#2-she-zhi-debug-mo-shi-setdebugenable)

查看GTouch日志，能够查看GrowingTouch打印的日志，如果需要的话，可以在初始化SDK地方添加配置。

```swift
+  (void)setDebugEnable:(BOOL)enable;
```

**参数说明**

| 参数名 | 类型  | 必填  | 说明  |
| --- | --- | --- | --- |
| enable | bool | 是   | 开启弹窗日志。<br></br>* 开启YES<br></br>* 关闭NO<br></br>默认值NO |

**代码示例**

```swift
[GrowingTouch setDebugEnable:YES];
```


### 设置显示超时时间 setEventPopupShowTimeout[](#3-she-zhi-xian-shi-chao-shi-shi-jian-seteventpopupshowtimeout)

埋点事件的产生到弹窗完全显示的超时时间，如网络情况可能会影响到弹窗的加载时间，或者两个弹窗埋点事件先后触发，前面一个弹窗的显示时间过长导致后面的弹窗事件超时等等。

```swift
+  (void)setEventPopupShowTimeout:(long  long)millis;
```

**参数说明**

| **参数名** | 类型  | 必填  | 说明  |
| --- | --- | --- | --- |
| millis | long long | 是   | 埋点事件的产生到弹窗完全显示的超时时间，单位ms。0<=有效值<=100000，默认值5000 |

**代码示例**

```swift
[GrowingTouch setEventPopupShowTimeout:8000];
```


### 弹窗的事件监听 setEventPopupDelegate[](#4-dan-chuang-de-shi-jian-jian-ting-seteventpopupdelegate)

通过监听获取时间和参数，您可以根据事件和参数以及您的业务场景执行相关的交互。

```swift
+  (void)setEventPopupDelegate:(id <GrowingTouchEventPopupDelegate>)delegate;
```

**参数说明**

```swift
@protocol GrowingTouchEventPopupDelegate <NSObject>

@optional

/**

 \* 弹窗显示成功

 *

 \* @param trackEventId 埋点事件名称

 \* @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)

 */

-  (void)onEventPopupLoadSuccess:(NSString *)trackEventId eventType:(NSString *)eventType;

​

/**

 \* 弹窗加载失败

 *

 \* @param trackEventId 埋点事件名称

 \* @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)

 \* @param error 发生的错误

 */

-  (void)onEventPopupLoadFailed:(NSString *)trackEventId eventType:(NSString *)eventType withError:(NSError *)error;

​

/**

 \* 用户点击了弹窗的有效内容。弹窗SDK现在只提供跳转APP内部界面和H5界面两种处理方式。

 \* 您可以在这里接管跳转事件，处理需要跳转的url。您也可以自定义Url协议，实现更多业务和交互功能。

 *

 \* @param trackEventId 埋点事件名称

 \* @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)

 \* @param openUrl 跳转的url

 \* @return true：点击事件被消费，弹窗SDK不再处理；false：由弹窗SDK处理点击事件

 */

-  (BOOL)onClickedEventPopup:(NSString *)trackEventId eventType:(NSString *)eventType openUrl:(NSString *)openUrl;

​

/**

 \* 用户关闭了弹窗

 *

 \* @param trackEventId 埋点事件名称

 \* @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)

 */ 

-  (void)onCancelEventPopup:(NSString *)trackEventId eventType:(NSString *)eventType;

​

/**

 \* 弹窗显示超时

 *

 \* @param trackEventId 埋点事件名称

 \* @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)

 */

-  (void)onTrackEventTimeout:(NSString *)trackEventId eventType:(NSString *)eventType;

@end

​

/**

 \* 触达弹窗控制器视图将要显示

*/

-  (void)eventPopupViewWillAppear;

​

/**

 \* 触达弹窗控制器视图已经显示

*/

-  (void)eventPopupViewDidAppear;

​

/**

 \* 触达弹窗控制器视图将要消失

*/

-  (void)eventPopupViewWillDisappear;

​

/**

 \* 触达弹窗控制器视图已经消失

*/

-  (void)eventPopupViewDidDisappear;
```

**代码示例**

```swift
@implementation AppDelegate

​

 -  (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

 // Override point for customization after application launch.

 [Growing startWithAccountId:@"xxxxxxxxxxxxxxxx"];

 [GrowingTouch setEventPopupDelegate:self];

 [GrowingTouch start];

 return YES;

}

​

 -  (void)onEventPopupLoadSuccess:(NSString *)trackEventId eventType:(NSString *)eventType {

 NSLog(@"%s trackEventId = %@, eventType = %@",  __func__, trackEventId, eventType);

}

​

 -  (void)onEventPopupLoadFailed:(NSString *)trackEventId eventType:(NSString *)eventType withError:(NSError *)error {

 NSLog(@"%s trackEventId = %@, eventType = %@",  __func__, trackEventId, eventType);

}

​

 -  (BOOL)onClickedEventPopup:(NSString *)trackEventId eventType:(NSString *)eventType openUrl:(NSString *)openUrl {

 NSLog(@"%s trackEventId = %@, eventType = %@",  __func__, trackEventId, eventType);

 return NO;

}

​

 -  (void)onCancelEventPopup:(NSString *)trackEventId eventType:(NSString *)eventType {

 NSLog(@"%s trackEventId = %@, eventType = %@",  __func__, trackEventId, eventType);

}

​

 -  (void)onTrackEventTimeout:(NSString *)trackEventId eventType:(NSString *)eventType {

 NSLog(@"%s trackEventId = %@, eventType = %@",  __func__, trackEventId, eventType);

}
```
​

## API介绍[](#san-api-jie-shao)

**\+ (void)enableEventPopupAndGenerateAppOpenEvent;**

打开弹窗 SDK 并触发 AppOpen 事件。如果担心弹窗 SDK 在 APP 启动页或者闪屏页显示弹窗，您可以选择在初始化关闭弹窗，然后在您 App的内容页打开时再打开弹窗开关。但是单纯调用 [GrowingTouch setEventPopupEnable:YES]; 只会打开弹窗 SDK 开关，并不会触发 AppOpen 事件。如果调用上述API 则会打开弹窗开关，同时触发一个 AppOpen 事件。

**\+ (BOOL)isEventPopupShowing;**

弹窗是否正在显示


## 常见问题[](#si-chang-jian-wen-ti)

### 弹窗跳转App原生界面[](#1-dan-chuang-tiao-zhuan-app-yuan-sheng-jie-mian)

特别需要注意以下两点：

（1）如果点击跳转的原生界面是通过Objective-C开发的控制器，例如控制器名称为 InAppViewController ，传递参数为key1、key2，则弹窗页面配置如下：

* **弹窗Web页面配置如下：**
    
![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4m_pKRmrAEW9BUZ6tm%2F-M4maFVCNIv4UhyoP2A9%2Fimage.png?alt=media&token=ffd8c212-c05c-487e-9bdb-b8f93e9e4460)

其中「自定义参数」意思是输入任何您自己的scheme（自定义协议），比如： myapp://productdetails/itemabc ，然后在onclick事件回调中解析出来就行了，解析自定义协议地址的话，onClick()方法需返回true。

此时生成的跳转链接为`InAppViewController?key1=value1&key2=value2` ，点击自动跳转到原生界面InAppViewController，并携带两个参数。

在InAppViewController可以通过提前定义属性，获取参数

```swift
@interface InAppViewController  :  UIViewController

@property (nonatomic, copy)  NSString  *key1;

@property (nonatomic, copy)  NSString  *key2;

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

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4maKROKUTl-cUIwle-%2F-M4maPc9ZF4vO6HXHRUt%2Fimage.png?alt=media&token=1a8b8078-996a-4bc6-8e32-2622fc0f1644)
![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4maKROKUTl-cUIwle-%2F-M4maVDSvwn0BaJVbpGS%2Fimage.png?alt=media&token=66f59993-5f68-4a55-98b9-7cec0cf915d3)

第3步：可以看到在Products文件夹同级补录下，有一个名为Intermediates.noindex 的文件夹，依次进入 TestDemo.build -> Debug-iphoneos(或Debug-iphonesimulator) -> TestDemo.build -> DerivedSources 文件夹下

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4maKROKUTl-cUIwle-%2F-M4ma_ElzRjuOkF23KFu%2Fimage.png?alt=media&token=22286439-dfd4-4422-859a-efd10b6f967e)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4maKROKUTl-cUIwle-%2F-M4mbDh79lUKLBV35Vih%2Fimage.png?alt=media&token=c9b723da-fcfc-46c8-a249-2f17cb33961a)

第4步：当前文件下有一个名为 TestDemo-Swift.h 的文件，双击打开在该文件中查找 SFViewController，发现该类声明的上方有一句 SWIFT_CLASS("_TtC8TestDemo16SFViewController")

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4maKROKUTl-cUIwle-%2F-M4mbAJ_UHKJTMWouRPP%2Fimage.png?alt=media&token=82916c47-7b0c-4b05-9a61-a8efe7f710b7)

_TtC8TestDemo16SFViewController 即为原生界面SFViewController.swift转换后的类名， Web 页面配置如下：

**弹窗Web页面配置如下：**

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4maKROKUTl-cUIwle-%2F-M4mbMYOxVU-eXA_4M_4%2Fimage.png?alt=media&token=f72765ca-5dae-4615-9be5-ad40f0c6e7ae)

### “打开App时”事件触发的时机[](#2-da-kai-app-shi-shi-jian-chu-fa-de-shi-ji)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4maKROKUTl-cUIwle-%2F-M4mb5LsPow3UOxJbFVi%2Fimage.png?alt=media&token=c7655039-da15-47e9-8faf-916672c2a881)

当选择弹窗的触发时机为“打开App时”，触发场景如下：

1、启动弹窗并打开弹窗SDK开关时，后台切换到前台时触发

2、启动弹窗但关闭弹窗SDK开关时，主动调用如下方法时触发

```swift
+  (void)enableEventPopupAndGenerateAppOpenEvent;
```
