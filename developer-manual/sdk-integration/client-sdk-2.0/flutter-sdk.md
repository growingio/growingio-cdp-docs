# Flutter SDK

## 集成 SDK <a id="ji-cheng-php-sdk"></a>

直接从 [GitHub](https://github.com/growingio/flutter-growingio-sdk-tracker-plugin) 获取 SDK 的源码并集成到项目中。

## **添加依赖** <a id="tian-jia-yi-lai"></a>

以工程`flutter_app`为例，在`pubspec.yaml`文件中添加依赖

```text
dependencies:
  growingio_sdk_tracker_plugin:
    git:
      ref: master
      url: https://github.com/growingio/flutter-growingio-sdk-tracker-plugin.git
```

然后执行 `flutter pub get` 指令

## iOS 工程配置 <a id="ios-gong-cheng-pei-zhi"></a>

sdk需要初始化操作，否则会`异常退出`

在`AppDelegate`文件中添加初始化sdk代码，例如如下所示：

```text
#import "AppDelegate.h"
#import "GeneratedPluginRegistrant.h"
#import <GrowingAnalytics/GrowingTracker.h>
#import <GrowingAnalytics/GrowingTrackConfiguration.h>
@implementation AppDelegate

- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  GrowingTrackConfiguration *configuration = [GrowingTrackConfiguration configurationWithProjectId:@"0a1b4118dd954ec3bcc69da5138bdb96"];
  configuration.debugEnabled = YES;
    
  [GrowingTracker startWithConfiguration:configuration launchOptions:launchOptions];
  [GeneratedPluginRegistrant registerWithRegistry:self];
  // Override point for customization after application launch.
  return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

@end
```

使用Xcode，选择`Targets->Info->URL Types`配置好相关的`url scheme`

## Android工程配置 <a id="android-gong-cheng-pei-zhi"></a>

* 新建一个`MyApplication`继承自`FlutterApplication`

```text
package com.example.flutter_app;

import com.growingio.android.sdk.track.TrackConfiguration;
import com.growingio.android.sdk.track.GrowingTracker;
import io.flutter.app.FlutterApplication;

public class MyApplication extends FlutterApplication {
    private static TrackConfiguration sConfiguration;
    @Override
    public void onCreate() {
        super.onCreate();


        if (sConfiguration == null) {
            sConfiguration = new TrackConfiguration("bfc5d6a3693a110d", "growing.d80871b41ef40518")
                    .setUploadExceptionEnabled(false)
                    .setDebugEnabled(true)
                    .setOaidEnabled(false);
        }
        GrowingTracker.startWithConfiguration(this, sConfiguration);
    }
}

```

* 并修改 `AndroidManifest.xml`文件中`android:name`字段

```text
<application
        android:name="com.example.growingio_sdk_tracker_plugin_example.MyApplication" //修改这里
        ...
```

* 在`app`下的`build.gradle`添加配置参数

```text
android {
    compileSdkVersion 29

    lintOptions {
        disable 'InvalidPackage'
    }

    defaultConfig {
        // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
        applicationId "com.example.flutter_app"
        minSdkVersion 17   //提示：这里可能版本小于17，修改为17可以避免报错
        targetSdkVersion 29
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
	resValue("string", "growingio_project_id", "9926fc6c1189e2fb") //这里是你的工程id
	resValue("string", "growingio_url_scheme", "growing.da7e6c2879469314") //这里是你的url scheme
```

* 在`app`下的`build.gradle`中添加 `GrowingIO Tracker SDK`

```text
dependencies {
    implementation 'com.growingio.android:tracker:latest.release' //可以指定你需要的版本 >3.0.0
}
```

之后，运行你的app，即可进行正常埋点。

