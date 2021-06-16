# iOS SDK

## **添加依赖**

1. 获取iOS SDK以下包并解压，由GrowingIO提供。
2. 将[Growing.h](http://assets.giocdn.com/cdp/ios/GrowingIO-iOS-PublicHeader-1.2.7.zip)、[GrowingCDPCoreKit.framework](http://assets.giocdn.com/cdp/ios/GrowingIO-iOS-CDPCoreKit-1.2.7.zip) 添加到iOS工程中；记得勾选“Copy item if needed“。
3. 在工程项目中添加以下库文件：

> 添加库依赖的位置在项目设置 Target &gt; 选项卡General &gt; Linked Frameworks and Libraies。

| 库名称 | 说明 |
| :--- | :--- |
| Foundation.framework | 基础依赖库 |
| CoreTelephony.framework | 用于读取运营商 |
| SystemConfiguration.framework | 用于判断网络状态 |
| AdSupport.framework | 用于来源管理激活匹配 |
| libsqlite3.tbd | 存储日志 |
| CoreLocation.framework | 用于读取地理位置信息（如果您的App有权限） |

添加编译参数，并注意大小写。

![](../../../.gitbook/assets/image%20%28161%29.png)

### **添加URL Scheme**

添加URL Scheme到项目中，以便唤醒您的程序。

![](../../../.gitbook/assets/image%20%2812%29.png)

## **初始化配置**

> 在AppDelegate 中引入\#import "Growing.h"并添加初始化方法。

```objectivec
#import "Growing.h"
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // 启动GrowingIO
    [Growing startWithAccountId:@"您的项目ID" dataSourceId:@"您的数据源ID"];  // 替换为您的项目ID和数据源ID
    // 其他配置,设置埋点上报地址
    [Growing setTrackerHost:@"http://test.xxx.com"];
    
    // 开启Growing调试日志 可以开启日志 
    // [Growing setEnableLog:YES];
}
```

## 添加支持用户运营扫码的代码 <a id="handleurl"></a>

> 在 AppDelegate 中添加

{% hint style="warning" %}
因为您代码的复杂程度以及iOS SDK的版本差异，有时候 \[Growing handleUrl:url\] 并没有被调用。请在各个平台上调试这段代码，确保当App被URL scheme唤醒之后，该函数能被调用到。
{% endhint %}

```swift
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation
{
    
// 如果没有触发handleUrl 扫码弹窗 和扫码注册推送不生效
 if ([Growing handleUrl:url]) // 请务必确保该函数被调用
  {
      return YES;
  }
  return NO;
 
}
```

常用示例：

若您在 AppDelegate 中实现了以下一个或多个方法，请在已实现的函数中，调用`[Growing handleUrl:]`

```swift
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(nullable NSString *)sourceApplication annotation:(id)annotation
- (BOOL)application:(UIApplication *)application handleOpenURL:(NSURL *)url
- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<NSString*, id> *)options
```

若以上所有方法均未实现，请实现以下方法并调用`[Growing handleUrl:]`

```swift
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(nullable NSString *)sourceApplication annotation:(id)annotatio
```

## **重要配置**

App Store 提交注意事项‌

如果您添加了库**AdSupport.framework**，GrowingIO则会启用 IDFA，所以在向 App Store 提交应用时，需要：‌

* 对于问题 **Does this app use the Advertising Identifier \(IDFA\)**，选择 **YES**。
* 对于选项**Attribute this app installation to a previously served advertisement**，打勾。
* 对于选项**Attribute an action taken within this app to a previously served advertisement**，打勾。

> **为什么 GrowingIO 使用 IDFA?**
>
> GrowingIO 使用 IDFA 来做来源管理激活设备的精确匹配，让你更好的衡量广告效果。如您不希望启用IDFA，可以选择不引入 AdSupport.framework**。**

#### 关于权限获取

* 对于iOS 14之前，你无需主动获取 `广告标识IDFA` 的权限
* 对于iOS 14之后，你需要使用如下方法来开启你的 `广告标识IDFA` 的权限

1. Plist 文件中添加 `NSUserTrackingUsageDescription`

   ```text
   <key>NSUserTrackingUsageDescription</key>
   <string>GrowingIO测试demo 需要使用你的广告标识信息以用于数据追踪分析</string> //描述内容请根据App修改
   ```

2. 导入框架 `#import <AppTrackingTransparency/AppTrackingTransparency.h>`
3. 调用获取权限代码

   ```text
       if (@available(iOS 14, *)) {
           // iOS14及以上版本需要先请求权限
           [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status) {
               switch (status) {
                   case ATTrackingManagerAuthorizationStatusDenied:
                       //用户拒绝向App授权
                       break;
                   case ATTrackingManagerAuthorizationStatusAuthorized:
                       //用户同意向App授权
                       break;
                   case ATTrackingManagerAuthorizationStatusNotDetermined:
                       //用户未做选择或未弹窗
                       break;
                   case ATTrackingManagerAuthorizationStatusRestricted:
                       //用户在系统级别开启了限制广告追踪
                       break;
                   default:
                       break;
               }
           }];
       }
   ```

## **API**

### **初始化配置API**

GrowingIO 初始化配置项均在 AppDelegate.m 文件中的 didFinishLaunchingWithOptions 方法中SDK初始化代码块中设置，下面将分类并描述含义。

<table>
  <thead>
    <tr>
      <th style="text-align:left">API</th>
      <th style="text-align:left">&#x9ED8;&#x8BA4;&#x503C;</th>
      <th style="text-align:left">&#x662F;&#x5426;&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>startWithAccountId:AccountId</p>
        <p>dataSourceId:dataSourceId</p>
      </td>
      <td style="text-align:left">&#x65E0;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x521D;&#x59CB;&#x5316;&#x65B9;&#x6CD5;&#xFF0C;AccountID&#x4E3A;&#x9879;&#x76EE;id&#xFF1B;</p>
        <p>dataSourceId&#x4E3A;&#x6570;&#x636E;&#x6E90;ID&#xFF0C;&#x9ED8;&#x8BA4;&#x91C7;&#x6837;&#x7387;&#x4E3A;100%&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>startWithAccountId:AccountId</p>
        <p>dataSourceId:dataSourceId</p>
        <p>withSampling:sampling</p>
      </td>
      <td style="text-align:left">&#x65E0;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x521D;&#x59CB;&#x5316;&#x65B9;&#x6CD5;&#xFF0C;AccountID&#x4E3A;&#x9879;&#x76EE;id&#xFF1B;</p>
        <p>dataSourceId&#x4E3A;&#x6570;&#x636E;&#x6E90;ID&#xFF1B;sampling&#x4E3A;&#x91C7;&#x6837;&#x7387;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>

代码示例：

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    [Growing startWithAccountId:@"YOUR_ACCOUNT_ID" dataSourceId:@"YOUR_DATASOURCE_ID"];
    //输出调试日志
    [Growing setEnableLog:YES];
    return YES；
}
```

### **SDK功能API**

> GrowingIO所有API 都需要在主线程调用。

| API | 说明 |
| :--- | :--- |
| sdkVersion | 获取当前GrowingIO SDK版本号。 |
| setEnableLog | 采集日志开关，setEnableLog=YES时会输出调试日志。 |
| getEnableLog | 获取采集日志开关的当前状态。 |
| setZone | 设置zone信息，即时区信息。 |
| getDeviceId | 获取当前设备ID。 |
| getVisitUserId | 获取当前访问用户ID。 |
| getSessionId | 获取当前访问ID。 |
| setTrackerHost | 设置数据收集平台服务器地址。 |

### **数据采集API**

| API | 默认值 | 说明 |
| :--- | :--- | :--- |
| setAspectMode | 无 | 设置数据采集模式，有GrowingAspectModeSubClass 和GrowingAspectModeDynamicSwizzling 两种。 |
| setFlushInterval | 15s | 设置、获取发送数据的事件间隔，默认设置15s。 |
| setDailyDataLimit | 10485KB | 设置每天使用数据网络（2G、3G、4G）上传的数据量的上限，默认值10485KB（10MB）。 |
| getDailyDataLimit | 无 | 获取每天使用数据网络（2G、3G、4G）上传的数据量的上限，默认值10485KB（3MB）。 |
| disableDataCollect | 无 | 设置GDPR生效。 |
| enableDataCollect | 无 | 设置GDPR失效。 |
| setEnableLocationTrack | Yes | 设置是否采集地理位置的统计信息，默认采集。 |
| getEnableLocationTrack | 无 | 获取是否采集地理位置。 |

## **常用API**

### **设置登录用户ID**

当用户登录之后调用 setUserId ，设置登录用户ID。

```objectivec
// setUserId API原型
+ (void)setUserId:(NSString *)userId;
```

| 参数名称 | 类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| userId | string | 是 | 登录用户的用户ID。 |

> Tips :
>
> 如果您的App每次用户升级版本时无需重新登录的话，为防止用户本地缓存被清除导致的无法被识别为登录用户，建议在用户每次升级App版本后初次访问时重新调用上述setUserId方法。

### **清除登录用户ID**

当用户登出之后调用clearUserId ，清除已经设置的登录用户ID。

```objectivec
// clearUserId API原型
+ (void)clearUserId;
```

### **设置自定义事件和属性**

发送一个自定义事件，在添加所需发送的时间代码之前，需要在打点管理用户界面声明事件以及事件属性。

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x662F;&#x5426;&#x5FC5;&#x987B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">eventId</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x6807;&#x8BC6;&#x7B26;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">variable</td>
      <td style="text-align:left">NSDictionary</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">
        <p>&#x4E8B;&#x4EF6;&#x53D1;&#x751F;&#x65F6;&#x6240;&#x4F34;&#x968F;&#x7684;&#x7EF4;&#x5EA6;&#x4FE1;&#x606F;&#x3002;</p>
        <p>&#x9650;&#x5236;&#xFF1A;&#x975E;&#x7A7A;&#xFF1B;variable &#x5185;&#x90E8;&#x4E0D;&#x5141;&#x8BB8;&#x542B;&#x6709;</p>
        <p>NSDictionary&#x6216;&#x8005;NSArray&#xFF1B;</p>
        <p>key &#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;50&#xFF0C;value
          &#x957F;&#x5EA6;&#x9650;</p>
        <p>&#x5236;&#x5C0F;&#x7B49;&#x4E8E;200&#xFF0C;&#x503C;&#x4E0D;&#x80FD;&#x4E3A;&#x7A7A;&#x4E32;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&quot;&quot;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">itemId</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x7269;&#x54C1;&#x6A21;&#x578B;&#x552F;&#x4E00;&#x6807;&#x8BC6;&#x5C5E;&#x6027;&#xFF0C;&#x5982;&#x201C;order_id&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">itemKey</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x7269;&#x54C1;&#x6A21;&#x578B;&#x552F;&#x4E00;&#x6807;&#x8BC6;&#x5C5E;&#x6027;&#x503C;&#xFF0C;&#x5982;&#x201C;123456&#x201D;</td>
    </tr>
  </tbody>
</table>

代码示例：

```objectivec
// track API原型
+ (void)track:(NSString *)eventId;
+ (void)track:(NSString *)eventId withVariable:(NSDictionary<NSString *, NSObject *> *)variable;
+ (void)track:(NSString *)eventId withVariable:(NSDictionary<NSString *, NSObject *> *)variable forItem:(NSString *)itemId itemKey:(NSString *)itemKey;

// track API调用示例一
[Growing track:@"registerSuccess"];

// track API调用示例二 - 事件属性
[Growing track:@"registerSuccess" withVariable:@{@"gender":@"male", @"age":@"21"}];

// track API调用示例三 - 物品模型
[Growing track:@"registerSuccess" withVariable:@{@"gender":@"male", @"age":@"21"} forItem:@"order_id" itemKey:@"123456"];
```

### **发送用户事件**

发送一个自定义的用户事件。

| 参数名称 | 类型 | 是否必填 | 说明 |
| :--- | :--- | :--- | :--- |
| attributes | NSDictionary&lt;NSString \*,id&gt;\* | 是 | 用户事件携带的其他信息。 |

```objectivec
// setUserAttributes API原型
+ (void)setUserAttributes:(NSDictionary<NSString *, id>*)attributes;
//代码示例
NSDictionary *dict = @{@"age" : 18, @"name": @"growingIO"};
[Growing setUserAttributes:dict];
```

\*\*\*\*

### **发送自定义Page 事件 （数据采集SDK &gt;=1.2.0）** <a id="page"></a>

| 参数名称 | 类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| pageName | string | 是 | **page**事件标识符。 |

```objectivec
/**
 发送自定义Page事件

 @param pageName : 页面名称, pageName为正常中英文数字组合的字符串, 长度<=1000, 请不要含有 "'|\*&$@/', 等特殊字符
 */
+ (void)trackPage:(NSString *)pageName;

//代码示例
   [Growing trackPage:@"TestPageEvent"];
   
  
```

### 加载了H5内嵌页SDK gio\_hybrid\_cdp.js的页面。自动采集H5**（数据采集SDK &gt;=1.2.0）** <a id="bridgeforwebview"></a>

| 参数名称 | 类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| webView | WKWebView | 是 | WKWebView |

```objectivec
+ (void)bridgeForWKWebView:(WKWebView *)webView;
//代码示例
    WKWebView *webView = [[WKWebView alloc] initWithFrame:self.view.frame];
    [Growing bridgeForWKWebView:webView];
```

{% hint style="info" %}
需要在 webview 初始化后调用
{% endhint %}

