# Unity SDK

## **API列表**

* Track: 发送自定义事件, 对应于cstm事件

```text
public static void Track(string eventName)
public static void Track(string eventName, Dictionary<string, object> var)
public static void Track(string eventName, Dictionary<string, object> var, String itemId, String itemKey)
```

* TrackPage: 发送自定义page事件, 对应于page事件

```text
public static void TrackPage(string pageName)
public static void TrackPage(string pageName, Dictionary<string, object> var)
```

* SetUserId: 设置登录用户ID

```text
public static void SetUserId(string userId)
```

* ClearUserId: 清除登录用户ID

```text
public static void ClearUserId()
```

* SetUserAttributes: 发送一个自定义的用户事件

```text
public static void SetUserAttributes(Dictionary<string, object> var)
```



## 集成步骤

直接从 [GitHub  ](https://github.com/growingio/growingio-unity-sdk)获取 SDK 的源码并集成到项目中。

* Android
  * 将最新版本的vds-android-agent-cdp以及对应依赖的protobuf-lite、gmonitor替换Assets/Plugins/Android目录下对应文件
  * 将Assets/Plugins/Android 下内容以及Assets/Sources 内容拷贝到对应工程目录下
  * 在Assets/Plugins/Android/AndroidManifest.xml中配置对应项目的url scheme
  * 在Assets/Sources/com/growingio/demo/App.java中配置对应启动配置
  * 将Scripts/GrowingIO放入对应工程
  * 更多细节参考[Android原生端埋点sdk](https://docs.growingio.com/op/developer-manual/sdkintegrated/cdp/android-sdk)
  * Edit/Project Settings/Player/Other Settings 中配置包名
* iOS
  * 将最新版本的GrowingCDPCoreKit.framework和Growing.h替换Assets/Plugins/iOS目录下对应文件
  * 将Assets/Plugins/iOS/GrowingIOHelper.mm 放入对应工程目录
  * 将Scripts/GrowingIO放入对应工程
  * 将Editor/BuildPostProcessor.cs放入对应工程目录\(目前依赖framework支持直接勾选, 如果希望通过勾选配置以及手动配置scheme, 请参考原生sdk文档\)
  * 在导出的Xcode工程中UnityAppController.mm文件中添加如下代码完成初始化：
  * * ```text
      #import <WebKit/WebKit.h>
      #import "Growing.h"

      - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
      {
        	...
          [Growing startWithAccountId:@"AccountId" dataSourceId:@"dataSourceId"];
          [Growing setTrackerHost:@"host"];
          [Growing setEnableLog:YES];
      }
      ```
  * 更多细节参考[iOS原生端埋点sdk](https://docs.growingio.com/op/developer-manual/sdkintegrated/cdp/ios-sdk)
  * Edit/Project Settings/Player/Other Settings 中配置Bundle Identifier

## 集成效果

* Android

![](../../../.gitbook/assets/tu-pian-%20%2811%29.png)

* iOS

![](../../../.gitbook/assets/tu-pian-%20%289%29.png)

![](../../../.gitbook/assets/tu-pian-%20%2810%29.png)

