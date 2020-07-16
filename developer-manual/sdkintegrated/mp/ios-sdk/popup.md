# 弹窗 SDK（iOS）

弹窗SDK最低兼容iOS 8.0 系统。

\*\*\*\*

库简介

> **GrowingTouchCoreKit.framework 运营基础库  
> GrowingTouchCoreUI.bundle UI页面图  
> GrowingTouchKit.framework 运营弹窗库  
> GrowingTouchBannerKit.framework 运营banner库**

## 一. 集成SDK

### 1. 集成GrowingIO iOS CDP埋点SDK\(如已集成跳过\)

[https://growingio.gitbook.io/cdp/developer-manual/sdkintegrated/cdp/ios-sdk](https://growingio.gitbook.io/cdp/developer-manual/sdkintegrated/cdp/ios-sdk)

### 2. 集成运营SDK

 手动集成SDK  
下载最新的iOS GrowingTouch SDK包，并将其中的GrowingTouchCoreKit.framework、GrowingTouchCoreUI.bundle以及GrowingTouchKit.framework 添加到iOS工程中。下载链接：[http://assets.giocdn.com/cdp/ios/GrowingIO-iOS-CDP-1.2.0-1.3.0.zip](http://assets.giocdn.com/cdp/ios/GrowingIO-iOS-CDP-1.2.0-1.3.0.zip)

![](../../../../.gitbook/assets/image%20%28110%29.png)

### 3. 初始化SDK

在 AppDelegate 中导入 `import <GrowingTouchCoreKit/GrowingTouchCoreKit.h>` 并添加初始化方法，且保证在埋点 SDK 初始化代码 `[Growing startWithAccountId:@"ACCOUNT_ID" dataSourceId:@"DATASOURCE_ID"]`后

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    ...
    // 启动GrowingIO
    [Growing startWithAccountId:@"YOUR_ACCOUNT_ID"  dataSourceId:@"YOUR_DATASOURCE_ID"]; //替换为您的项目ID
    
    // 启动GrowingTouch，设置弹窗请求地址，一般与访问页面域名一致
    [GrowingTouch setServerHost:@"http://test.xxx.com"];
    [GrowingTouch start];
}

```

{% hint style="info" %}
请注意调用顺序，需要在 \[Growing startWithAccountId\] 函数调用后，再调用 \[GrowingTouch start\] 函数。
{% endhint %}

## 二. 重要配置

### 1. 设置弹窗SDK开关 setEventPopupEnable

设置弹窗 SDK 的开关，默认是“YES”。因为每个 App 的实现方式不同，如果默认状态下弹窗在闪屏页或 启动页就会弹出，可以通过在初始化 SDK 设置 “NO” 来解决这个问题，当 App 的内容页打开时再进行弹窗：

```objectivec
+ (void)setEventPopupEnable:(BOOL)enable;
```

**参数说明**

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;&#x540D;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">enable</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x5F00;&#x5173;&#x5F39;&#x7A97;SDK&#x3002;</p>
        <ul>
          <li>&#x5F00;&#x542F;YES</li>
          <li>&#x5173;&#x95ED;NO</li>
        </ul>
        <p>&#x9ED8;&#x8BA4;&#x503C;YES</p>
      </td>
    </tr>
  </tbody>
</table>

**代码示例**

```objectivec
[GrowingTouch setEventPopupEnable:YES];
```

### 2. 设置Debug模式 setDebugEnable

查看GTouch日志，能够查看GrowingTouch打印的日志，如果需要的话，可以在初始化SDK地方添加配置。

```objectivec
+ (void)setDebugEnable:(BOOL)enable;
```

**参数说明**

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;&#x540D;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">enable</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x5F00;&#x542F;&#x5F39;&#x7A97;&#x65E5;&#x5FD7;&#x3002;</p>
        <ul>
          <li>&#x5F00;&#x542F;YES</li>
          <li>&#x5173;&#x95ED;NO</li>
        </ul>
        <p>&#x9ED8;&#x8BA4;&#x503C;NO</p>
      </td>
    </tr>
  </tbody>
</table>

**代码示例**

```swift
[GrowingTouch setDebugEnable:YES];
```

### 3. 设置显示超时时间 setEventPopupShowTimeout

埋点事件的产生到弹窗完全显示的超时时间，如网络情况可能会影响到弹窗的加载时间，或者两个弹窗埋点事件先后触发，前面一个弹窗的显示时间过长导致后面的弹窗事件超时等等。

```objectivec
+ (void)setEventPopupShowTimeout:(long long)millis;
```

**参数说明**

| **参数名** | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| millis | long long | 是 | 埋点事件的产生到弹窗完全显示的超时时间，单位ms。0&lt;=有效值&lt;=100000，默认值5000 |

**代码示例**

```swift
[GrowingTouch setEventPopupShowTimeout:8000];
```

### 4. 弹窗的事件监听 setEventPopupDelegate

通过监听获取时间和参数，您可以根据事件和参数以及您的业务场景执行相关的交互。

```objectivec
+ (void)setEventPopupDelegate:(id <GrowingTouchEventPopupDelegate>)delegate;
```

**参数说明**

```objectivec
@protocol GrowingTouchEventPopupDelegate <NSObject>
@optional
/**
 * 弹窗显示成功
 *
 * @param trackEventId 埋点事件名称
 * @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)
 */
- (void)onEventPopupLoadSuccess:(NSString *)trackEventId eventType:(NSString *)eventType;

/**
 * 弹窗加载失败
 *
 * @param trackEventId 埋点事件名称
 * @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)
 * @param error 发生的错误
 */
- (void)onEventPopupLoadFailed:(NSString *)trackEventId eventType:(NSString *)eventType withError:(NSError *)error;

/**
 * 用户点击了弹窗的有效内容。弹窗SDK现在只提供跳转APP内部界面和H5界面两种处理方式。
 * 您可以在这里接管跳转事件，处理需要跳转的url。您也可以自定义Url协议，实现更多业务和交互功能。
 *
 * @param trackEventId 埋点事件名称
 * @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)
 * @param openUrl 跳转的url
 * @return true：点击事件被消费，弹窗SDK不再处理；false：由弹窗SDK处理点击事件
 */
- (BOOL)onClickedEventPopup:(NSString *)trackEventId eventType:(NSString *)eventType openUrl:(NSString *)openUrl;

/**
 * 用户关闭了弹窗
 *
 * @param trackEventId 埋点事件名称
 * @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)
 */ 
- (void)onCancelEventPopup:(NSString *)trackEventId eventType:(NSString *)eventType;

/**
 * 弹窗显示超时
 *
 * @param trackEventId 埋点事件名称
 * @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)
 */
- (void)onTrackEventTimeout:(NSString *)trackEventId eventType:(NSString *)eventType;
@end

/**
 * 触达弹窗控制器视图将要显示
*/
- (void)eventPopupViewWillAppear;

/**
 * 触达弹窗控制器视图已经显示
*/
- (void)eventPopupViewDidAppear;

/**
 * 触达弹窗控制器视图将要消失
*/
- (void)eventPopupViewWillDisappear;

/**
 * 触达弹窗控制器视图已经消失
*/
- (void)eventPopupViewDidDisappear;
```

**代码示例**

```objectivec
@implementation AppDelegate

 - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
     // Override point for customization after application launch.
     [Growing startWithAccountId:@"xxxxxxxxxxxxxxxx"];
     [GrowingTouch setEventPopupDelegate:self];
     [GrowingTouch start];
     return YES;
}

 - (void)onEventPopupLoadSuccess:(NSString *)trackEventId eventType:(NSString *)eventType {
     NSLog(@"%s trackEventId = %@, eventType = %@", __func__, trackEventId, eventType);
}

 - (void)onEventPopupLoadFailed:(NSString *)trackEventId eventType:(NSString *)eventType withError:(NSError *)error {
     NSLog(@"%s trackEventId = %@, eventType = %@", __func__, trackEventId, eventType);
}

 - (BOOL)onClickedEventPopup:(NSString *)trackEventId eventType:(NSString *)eventType openUrl:(NSString *)openUrl {
     NSLog(@"%s trackEventId = %@, eventType = %@", __func__, trackEventId, eventType);
     return NO;
}

 - (void)onCancelEventPopup:(NSString *)trackEventId eventType:(NSString *)eventType {
     NSLog(@"%s trackEventId = %@, eventType = %@", __func__, trackEventId, eventType);
}

 - (void)onTrackEventTimeout:(NSString *)trackEventId eventType:(NSString *)eventType {
     NSLog(@"%s trackEventId = %@, eventType = %@", __func__, trackEventId, eventType);
}
```



## 三.API介绍

**+ \(void\)enableEventPopupAndGenerateAppOpenEvent;**

打开弹窗 SDK 并触发 AppOpen 事件。如果担心弹窗 SDK 在 APP 启动页或者闪屏页显示弹窗，您可以选择在初始化关闭弹窗，然后在您 App的内容页打开时再打开弹窗开关。但是单纯调用 \[GrowingTouch setEventPopupEnable:YES\]; 只会打开弹窗 SDK 开关，并不会触发 AppOpen 事件。如果调用上述API 则会打开弹窗开关，同时触发一个 AppOpen 事件。

**+ \(BOOL\)isEventPopupShowing;**

弹窗是否正在显示

## 四. 常见问题

### 1. 弹窗跳转App原生界面

特别需要注意以下两点：

（1）如果点击跳转的原生界面是通过Objective-C开发的控制器，例如控制器名称为 InAppViewController ，传递参数为key1、key2，则弹窗页面配置如下：

* **弹窗Web页面配置如下：**

![](../../../../.gitbook/assets/image%20%2851%29.png)

其中「自定义参数」意思是输入任何您自己的scheme（自定义协议），比如： myapp://productdetails/itemabc ，然后在onclick事件回调中解析出来就行了，解析自定义协议地址的话，onClick\(\)方法需返回true。

此时生成的跳转链接为`InAppViewController?key1=value1&key2=value2` ，点击自动跳转到原生界面InAppViewController，并携带两个参数。

在InAppViewController可以通过提前定义属性，获取参数

```swift
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

![](../../../../.gitbook/assets/image%20%2873%29.png)

第2步：运行成功之后，在Products文件夹下，选中 TestDemo.app 后 Show in Finder

![](../../../../.gitbook/assets/image%20%2833%29.png)

第3步：可以看到在Products文件夹同级补录下，有一个名为Intermediates.noindex 的文件夹，依次进入 TestDemo.build -&gt; Debug-iphoneos\(或Debug-iphonesimulator\) -&gt; TestDemo.build -&gt; DerivedSources 文件夹下

![](../../../../.gitbook/assets/image%20%2898%29.png)

![](../../../../.gitbook/assets/image%20%2838%29.png)

第4步：当前文件下有一个名为 TestDemo-Swift.h 的文件，双击打开在该文件中查找 SFViewController，发现该类声明的上方有一句 SWIFT\_CLASS\("\_TtC8TestDemo16SFViewController"\)

![](../../../../.gitbook/assets/image%20%2884%29.png)

\_TtC8TestDemo16SFViewController 即为原生界面SFViewController.swift转换后的类名， Web 页面配置如下：

**弹窗Web页面配置如下：**

![](../../../../.gitbook/assets/image%20%2896%29.png)

### **2. “打开App时”事件触发的时机**

![](../../../../.gitbook/assets/image%20%28105%29.png)

当选择弹窗的触发时机为“打开App时”，触发场景如下：

1、启动弹窗并打开弹窗SDK开关时，后台切换到前台时触发

2、启动弹窗但关闭弹窗SDK开关时，主动调用如下方法时触发

```swift
+ (void)enableEventPopupAndGenerateAppOpenEvent;
```

\*\*\*\*

