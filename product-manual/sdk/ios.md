---
description: 无埋点 SDK 具备自动采集基本的用户行为事件，比如点击和页面浏览等行为数据。
---

# iOS SDK

{% hint style="success" %}
Xcode 9.0

ARC

iOS 8.0以上
{% endhint %}

## Cocoapods集成

在你的Podfile文件中添加

```text
pod 'GrowingAnalytics-cdp/Autotracker'
```

* Ex: 如果你是2.x版本迁移3.x版本的老用户，还需要导入

```text
pod 'GrowingAnalytics-upgrade/Autotracker-upgrade-2to3-cdp'
```

## 添加 URL Scheme

URL Scheme 是您在 GrowingIO 平台创建应用时生成的该应用的唯一标识。把 URL Scheme 添加到您的项目，以便使用Mobile Debug等功能时唤醒您的应用。

选择工程 -&gt; Target -&gt; Info -&gt; URL Types -&gt; 添加您的Url Scheme 即可

> 你需要在GrowingIO网站上先创建你的App应用，获取Url Scheme

## SDK初始化配置

1.导入头文件`"GrowingAutotracker.h"`请将以下 `GrowingTracker.startWithConfiguration`加在您的`AppDelegate` 的 `application:didFinishLaunchingWithOptions:` 方法中  
代码示例:

```text
// Config GrowingIO
// 参数需要从GrowingIO网站上，创建新应用，或从已知应用中获取 
// YourProjectId eg:0a1b4118dd954ec3bcc69da5138bdb96
// YourServerHost eg:http://106.75.81.105:8080
// YourDatasourceId eg: 11223344aabbcc
GrowingTrackConfiguration *configuration = [GrowingTrackConfiguration configurationWithProjectId:@"YourProjectId"];
configuration.dataCollectionServerHost = @"YourProjectId";
configuration.dataSourceId = @"YourDatasourceId";
[GrowingAutotracker startWithConfiguration:configuration launchOptions:launchOptions];
```

* Ex: 如果你是2.x版本迁移3.x版本的老用户，还需要在此之前调用\[Growing upgrade\]，非老版本迁移用户请忽略：

```text
//导入Growing.h
[Growing upgrade];
GrowingTrackConfiguration *configuration = [GrowingTrackConfiguration configurationWithProjectId:@"YourProjectId"];
configuration.dataCollectionServerHost = @"YourProjectId";
configuration.dataSourceId = @"YourDatasourceId";
[GrowingAutotracker startWithConfiguration:configuration launchOptions:launchOptions];
```

2.在appDelegate.m文件中实现urlSchme跳转以及DeepLink跳转的代理方法

```text
// url scheme跳转
- (BOOL)application:(UIApplication *)application
            openURL:(NSURL *)url
  sourceApplication:(NSNSString *)sourceApplication
         annotation:(id)annotation {

    return NO;
}

// universal Link执行
- (BOOL) application:(UIApplication *)application
continueUserActivity:(NSUserActivity *)userActivity
  restorationHandler:(void (^)(NSArray<id <UIUserActivityRestoring>> *_Nullable))restorationHandler {
    return YES;
}
```

3.若使用了iOS 13的 UIScene，请在你指定的SceneDelegate中设置如下

```text
- (void)scene:(UIScene *)scene continueUserActivity:(NSUserActivity *)userActivity {
}

- (void)scene:(UIScene *)scene openURLContexts:(NSSet<UIOpenURLContext *> *)URLContexts {
}
```

> 上述代理方法空实现即可，SDK会自动加入处理代码

## SDK 初始化配置项

| API | 参数类型 | 是否必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| `projectId` | `NSNSString` | 是 | `nil` | 官网的中您的项目ID |
| `urlScheme` | `NSNSString` | 是 | `nil` | 官网的中您的相应APP的UrlScheme |
| `dataSourceId` | `NSNSString` | 是 | `nil` | 官网的中您的相应APP的DataSourceId |
| `dataCollectionServerHost` | `NSNSString` | 是 | `nil` | 您部署服务的后端Host |
| `uploadExceptionEnable` | `BOOL` | 否 | `YES` | 收集SDK内部异常上报服务端 |
| `debugEnabled` | `BOOL` | 否 | `NO` | 调试模式，会打印SDK log，抛出错误异常，在线上环境务必关闭 |
| `cellularDataLimit` | `NSUInteger` | 否 | `10` | 每天发送数据的流量限制，单位MB |
| `dataUploadInterval` | `NSTimeInterval` | 否 | `15` | 数据发送的间隔，单位秒 |
| `sessionInterval` | `NSTimeInterval` | 否 | `30` | 每次访问会话的最大时长，单位秒 |
| `dataCollectionEnabled` | `BOOL` | 否 | `YES` | 是否采集数据 |
| `impressionScale` | `float` | 否 | `0` | 元素曝光事件中的比例因子,范围 \[0-1\] |

## 常用API

### 数据采集开关

打开或关闭数据采集`dataCollectionEnabled`

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `enabled` | `BOOL` | `YES`打开数据采集，`NO`关闭数据采集 |

**示例**

```text
[[GrowingAutotracker sharedInstance] setDataCollectionEnabled:YES];
```

### 设置登录用户ID

当用户登录之后调用`setLoginUserId` API，设置登录用户ID

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `userId` | `NSNSString` | 长度限制大于0且小于等于1000，如果大于长度1000将只截取前1000长度 |

**示例**

```text
[[GrowingAutotracker sharedInstance] setLoginUserId:@"112333445"];
```

### 清除登录用户ID

当用户登出之后调用`cleanLoginUserId`，清除已经设置的登录用户ID。

**示例**

```text
[[GrowingAutotracker sharedInstance] cleanLoginUserId];
```

### 设置用户的地理位置

设置用户当前的地理位置`setLocation`，基于WGS-84坐标。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `latitude` | `double` | 地理坐标点纬度 |
| `longitude` | `double` | 地理坐标点经度 |

**示例**

```text
[[GrowingAutotracker sharedInstance] setLocation:39.9 longitude:116.36];
```

### 清除用户的地理位置

清除用户当前的地理位置`cleanLocation`。

**示例**

```text
[[GrowingAutotracker sharedInstance] cleanLocation];
```

### 设置自定义事件

发送一个自定义事件`trackCustomEvent`。在添加所需要发送的事件代码之前，需要在事件管理用户界面配置事件以及事件级变量。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `eventName` | `NSNSString` | 事件名，事件标识符 |
| `attributes` | `NSDictionary<NSNSString, NSNSString>` | 事件发生时所伴随的维度信息 |
| `itemKey` | `NSNSString` | 事件发生关联的物品模型Key |
| `itemId` | `NSNSString` | 事件发生关联的物品模型ID |

**示例**

```text
[[GrowingAutotracker sharedInstance] trackCustomEvent:@"resourceItemTest" itemKey:@"testkey" itemId:@"testid" withAttributes:@{@"ok":@"false"}];
```

### 设置登录用户变量

以登录用户的身份定义用户属性变量`setLoginUserAttributes`，用于用户信息相关分析。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `attributes` | `NSDictionary<NSNSString, NSNSString>` | 用户属性信息 |

**示例**

```text
[[GrowingAutotracker sharedInstance] setLoginUserAttributes:@{@"fff":@"xxx"}];
```

### 获取设备ID

获取设备id`getDeviceId`，又称为匿名用户id，SDK 自动生成用来定义唯一设备。 如果没有初始化SDK 或者关闭采集开关可能返回值为nil，且可能有IO操作。

**示例**

```text
[[GrowingAutotracker sharedInstance] getDeviceId];
```

### 设置页面别名

给页面设置一个别名`setPageAlias`。

属性说明：

UIViewController分类声明的属性，设置需要在viewDidAppear执行之前。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `growingPageAlias` | `NSString` | 页面别名 |

**示例**

```text
- (void)viewDidLoad {
  [super viewDidLoad];
  ...
  self.growingPageAlias = @"xxxx";
  ...
}
```

### 设置忽略的页面

被设置忽略的页面`ignorePage`，不再触发无埋点的page事件。

属性说明：

UIViewController分类声明的属性，设置需要在viewDidAppear执行之前

参数说明：

| 属性 | 属性类型 | 说明 |
| :--- | :--- | :--- |
| `growingPageIgnorePolicy` | `GrowingIgnorePolicy` | 1. `GrowingIgnoreSelf` 只忽略自己 2. `GrowingIgnoreChildren` 只忽略该页面的子页面 3. `GrowingIgnoreAll` 忽略所有，包括自己和该页面的子页面 |

**示例**

```text
- (void)viewDidLoad {
  [super viewDidLoad];
  ...
  self.growingPageIgnorePolicy = GrowingIgnoreChildren;
  ...
}
```

### 设置忽略的View

被设置忽略的VIew`ignoreView`，不再触发点击、曝光等任何事件，被忽略的WebView也不会采集Hybrid的事件。

属性说明：

UIView 分类声明的属性，设置需要在viewDidAppear执行之前

参数说明：

| 属性 | 属性类型 | 说明 |
| :--- | :--- | :--- |
| `growingViewIgnorePolicy` | `GrowingIgnorePolicy` | 1. `GrowingIgnoreSelf` 只忽略自己 2. `GrowingIgnoreChildren` 只忽略该页面的子页面 3. `GrowingIgnoreAll` 忽略所有，包括自己和该页面的子页面 |

**示例**

```text
view.growingViewIgnorePolicy = GrowingIgnoreSelf;
```

### 设置采集View的曝光事件

当被设置的View出现在屏幕内时将触发曝光事件`trackViewImpression`。

方法说明：

UIView分类方法

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `eventName` | `NSString` | 曝光的事件名 |
| `attributes` | `NSDictionary<NSString, NSString>` | 曝光的事件属性 |

**示例**

```text
[self.view growingTrackImpression:@"xxxx" attributes:@{@"111":@"222"}];
```

### 停止采集View的曝光事件

停止采集View的曝光事件`stopTrackViewImpression`。

方法说明：

UIView分类方法

**示例**

```text
[self.view growingStopTrackImpression];
```

### 设置View唯一Tag

给View设置唯一的Tag`setUniqueTag`，方便点击等事件确定唯一的View，一般用于动态布局的场景。

属性说明：

UIView 分类声明的属性

| 属性 | 属性类型 | 说明 |
| :--- | :--- | :--- |
| `growingUniqueTag` | `NSString` | 需要设置的Tag |

**示例**

```text
self.view.growingUniqueTag = @"我是一个特别的view";
```

