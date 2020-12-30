---
description: 无埋点 SDK 具备自动采集基本的用户行为事件，比如点击和页面浏览等行为数据。
---

# Android SDK

{% hint style="success" %}
Gradle编译环境：Android Studio  
适配最低Android系统版本：Android 4.2
{% endhint %}

## 添加依赖

在project级别的`build.gradle`文件中添加`autotracker-gradle-plugin`依赖。

```text
buildscript {
    repositories {
        jcenter()
        google()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:x.x.x'
        //GrowingIO 无埋点 SDK plugin
        classpath 'com.growingio.android:autotracker-gradle-plugin:3.0.0'
    }
}
```

在 module 级别的 `build.gradle` 文件中添加`com.growingio.android.autotracker`插件、`autotracker`依赖。

```text
apply plugin: 'com.android.application'
//添加 GrowingIO 插件
apply plugin: 'com.growingio.android.autotracker'

...

dependencies {
    ...

    //GrowingIO 无埋点 SDK
    implementation 'com.growingio.android:autotracker-cdp:3.0.0'

    //如果不是AndroidX项目，请添加下面依赖
    compileOnly 'androidx.appcompat:appcompat:1.2.0'

    //如果你之前集成的是3.0.0版本之前的SDK，请还需要集成upgrade，方便最小程度的迁移
    implementation 'com.growingio.android.sdk.upgrade:autotracker-upgrade-2to3-cdp:1.0.0'
```

## 添加 URL Scheme

URL Scheme 是您在 GrowingIO 平台创建应用时生成的该应用的唯一标识。把 URL Scheme 添加到您的项目，以便使用圈选等功能时唤醒您的应用。 将应用的 URLScheme 和应用权限添加到你的 AndroidManifest.xml 中的 LAUNCHER Activity 下。 代码示例：

```text
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.growingio.testdemo">
​
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
​
    <!--请注意<application/>标签中的name属性值（这里为android:name=".MyApplication"）必须为您的Application类-->
    <application
        android:name=".MyApplication"
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
            <!--请添加这里的整个 intent-filter 区块，并确保其中只有一个 data 字段-->
            <intent-filter>
                <data android:scheme="growing.您的URL Scheme" />
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
            </intent-filter>
            <!--请添加这里的整个 intent-filter 区块，并确保其中只有一个 data 字段-->
        </activity>
    </application>
</manifest>
```

## SDK初始化配置

请将以下 `GrowingAutotracker.startWithConfiguration`加在您的`Application` 的 `onCreate` 方法中  
代码示例

```text
public class MyApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        //如果你之前集成的是3.0.0版本之前的SDK，请还需要初始化upgrade，将进行本地数据的迁移。
        GrowingIO.getInstance().upgrade(this);

        //初始化无埋点SDK
        GrowingAutotracker.startWithConfiguration(this,
                new CdpAutotrackConfiguration("exampleProjectId", "exampleUrlScheme")
                        .setDataCollectionServerHost("http://myhost.com/")
                        .setDataSourceId("exampleSourceId")
                        .setChannel("XXX应用商店")
                        .setDebugEnabled(BuildConfig.DEBUG)
        );
    }
}
```

## SDK 初始化配置项

| API | 参数类型 | 是否必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| `projectId` | `String` | 是 | `null` | 官网的中您的项目ID |
| `urlScheme` | `String` | 是 | `null` | 官网的中您的相应APP的UrlScheme |
| `setDataSourceId` | `String` | 是 | `null` | 官网的中您的相应APP的DataSourceId |
| `setDataCollectionServerHost` | `String` | 是 | `null` | 您部署服务的后端Host |
| `setChannel` | `String` | 否 | `null` | APP的分发渠道 |
| `setDebugEnabled` | `boolean` | 否 | `false` | 调试模式，会打印SDK log，抛出错误异常，在线上环境务必关闭 |
| `setCellularDataLimit` | `int` | 否 | `10` | 每天发送数据的流量限制，单位MB |
| `setDataUploadInterval` | `int` | 否 | `15` | 数据发送的间隔，单位秒 |
| `setSessionInterval` | `int` | 否 | `30` | 每次访问会话的最大时长，单位秒 |
| `setDataCollectionEnabled` | `boolean` | 否 | `true` | 是否采集数据 |
| `setOaidEnabled` | `boolean` | 否 | `false` | 是否采集Android OAID，如果设置为采集的话，受OAID获取时间的限制，事件采集可能会延迟 |
| `setUploadExceptionEnabled` | `boolean` | 否 | `true` | 收集SDK内部异常上报服务端 |
| `setImpressionScale` | `float` | 否 | `0` | 元素曝光事件中的比例因子,范围 \[0-1\] |

## 常用API

### 数据采集开关

打开或关闭数据采集 `setDataCollectionEnabled`

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `enabled` | `boolean` | `true`打开数据采集，`false`关闭数据采集 |

**示例**

```text
GrowingAutotracker.get().setDataCollectionEnabled(true);
```

### 设置登录用户ID

当用户登录之后调用`setLoginUserId` API，设置登录用户ID

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `userId` | `String` | 长度限制大于0且小于等于1000，如果大于长度1000将只截取前1000长度 |

**示例**

```text
GrowingAutotracker.get().setLoginUserId("zhangsan");
```

### 清除登录用户ID

当用户登出之后调用`cleanLoginUserId`，清除已经设置的登录用户ID。

**示例**

```text
GrowingAutotracker.get().cleanLoginUserId();
```

### 设置用户的地理位置

设置用户当前的地理位置，基于WGS-84坐标

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `latitude` | `double` | 地理坐标点纬度 |
| `longitude` | `double` | 地理坐标点经度 |

**示例**

```text
GrowingAutotracker.get().setLocation(39.9, 116.3);
```

### 清除用户的地理位置

清除用户当前的地理位置

**示例**

```text
GrowingAutotracker.get().cleanLocation();
```

### 设置自定义事件

送一个自定义事件`trackCustomEvent`。在添加所需要发送的事件代码之前，需要在事件管理用户界面配置事件以及事件属性。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `eventName` | `String` | 事件名，事件标识符 |
| `attributes` | `Map<String, String>` | 事件发生时所伴随的维度信息 |
| `itemKey` | `String` | 事件发生关联的物品模型Key |
| `itemId` | `String` | 事件发生关联的物品模型ID |

**示例**

```text
GrowingAutotracker.get().trackCustomEvent("registerSuccess");

Map<String, String> map = new HashMap<>();
map.put("name", "June");
map.put("age", "12");
GrowingAutotracker.get().trackCustomEvent("registerSuccess", map);
```

### 设置登录用户属性

以登录用户的身份定义用户属性变量`setLoginUserAttributes`，用于用户信息相关分析。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `attributes` | `Map<String, String>` | 用户属性信息 |

**示例**

```text
Map<String, String> map = new HashMap<>();
map.put("gender", "male");
map.put("age", "12");
GrowingAutotracker.get().setLoginUserAttributes(map);
```

### 获取设备ID

获取设备id`getDeviceId`，又称为匿名用户id，SDK 自动生成用来定义唯一设备。 如果没有初始化SDK 或者关闭采集开关可能返回值为null，且可能有IO操作。

**示例**

```text
GrowingTracker.get().getDeviceId();
```

### 设置页面别名

给页面设置一个别名`setPageAlias`。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `page` | `Activity / Fragment` | 需要设置别名的页面对象，建议在`onCreate`生命周期中调用 |
| `alias` | `String` | 页面别名 |

**示例**

```text
GrowingAutotracker.get().setPageAlias(mActivity, "home");
```

### 设置忽略的页面

被设置忽略的页面`ignorePage`，不再触发无埋点的page事件。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `page` | `Activity / Fragment` | 需要忽略的页面对象，建议在`onCreate`生命周期中调用 |
| `policy` | `IgnorePolicy` | 1. `IGNORE_SELF` 只忽略自己 2. `IGNORE_CHILD` 只忽略该页面的子页面 3. `IGNORE_ALL` 忽略所有，包括自己和该页面的子页面 |

**示例**

```text
GrowingAutotracker.get().ignorePage(mActivity, IgnorePolicy.IGNORE_ALL);
```

### 设置忽略的View

被设置忽略的VIew`ignoreView`，不再触发点击、曝光等任何事件，被忽略的WebView也不会采集Hybrid的事件。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `view` | `View` | 需要忽略的View对象 |
| `policy` | `IgnorePolicy` | 1. `IGNORE_SELF` 只忽略自己 2. `IGNORE_CHILD` 只忽略该View的子View 3. `IGNORE_ALL` 忽略所有，包括自己和该View的子View |

**示例**

```text
GrowingAutotracker.get().ignoreView(view, IgnorePolicy.IGNORE_SELF);
```

### 设置采集View的曝光事件

当被设置的View出现在屏幕内时将触发曝光事件`trackViewImpression`。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `view` | `View` | 需要采集曝光事件的View对象 |
| `impressionEventName` | `String` | 曝光的事件名 |
| `attributes` | `Map<String, String>` | 曝光的事件属性 |

**示例**

```text
GrowingAutotracker.get().trackViewImpression(view, "buttonShowed");

Map<String, String> map = new HashMap<>();
map.put("color", "red");
map.put("name", "home");
GrowingAutotracker.get().trackViewImpression(view, "buttonShowed", map);
```

### 停止采集View的曝光事件

停止采集View的曝光事件`stopTrackViewImpression`。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `trackedView` | `View` | 需要停止采集曝光事件的View对象 |

**示例**

```text
GrowingAutotracker.get().stopTrackViewImpression(trackedView);
```

### 设置View唯一Tag

给View设置唯一的Tag`setUniqueTag`，方便点击等事件确定唯一的View，一般用于动态布局的场景。

参数说明：

| 参数 | 参数类型 | 说明 |
| :--- | :--- | :--- |
| `view` | `View` | 需要设置唯一Tag的View对象 |
| `tag` | `String` | 需要设置的Tag |

**示例**

```text
GrowingAutotracker.get().setUniqueTag(button, "homeTabButton");
```

