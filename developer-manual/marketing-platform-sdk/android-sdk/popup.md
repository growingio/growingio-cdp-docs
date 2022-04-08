---
id: mp-android-popup-sdk
sidebar_position: 1
---

# 弹窗 SDK （Android）

:::info
最低兼容Android版本4.2 API 17

弹窗 SDK 会根据运营人员对用户的分组情况，下发弹窗消息
:::


## 集成SDK[](#yi-ji-cheng-sdk)

### 集成GrowingIO Android CDP SDK[](#1-ji-cheng-growingio-android-cdp-sdk)

:::info
弹窗 SDK 依赖于数据数据采集 SDK

版本建议使用最新版本，如已集成请跳过
:::

参考 [Android SDK](https://growingio.github.io/growingio-sdk-docs/docs/android/base) ​


### 添加依赖[](#2-tian-jia-yi-lai)

#### 2.1 在app build.gradle添加SDK依赖[](#21-zai-app-buildgradle-tian-jia-sdk-yi-lai)

```java
dependencies {

 ...

 //由于弹窗底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖

 implementation "com.squareup.okhttp3:okhttp:3.12.1"

 //弹窗SDK依赖

 implementation "com.growingio.android:gtouch:$gtouch_version"

}
```

> $gtouch_version 为最新SDK版本号，现最新的版本号为请参考[SDK更新日志](./../changelogs.md)。


### 需要的权限列表[](#3-xu-yao-de-quan-xian-lie-biao)

所需权限同埋点SDK

```xml
<uses-permission android:name="android.permission.INTERNET"  />

<!--非危险权限，不需要运行时请求，Manifest文件中添加即可-->

<uses-permission android:name="android.permission.ACCESS\_NETWORK\_STATE"  />

<uses-permission android:name="android.permission.SYSTEM\_ALERT\_WINDOW"/>

<uses-permission android:name="android.permission.ACCESS\_WIFI\_STATE"  />

<uses-permission android:name="android.permission.SYSTEM\_ALERT\_WINDOW"/>
```
​

### 初始化SDK[](#4-chu-shi-hua-sdk)

请将以下`GrowingTouch.startWithConfig`加在您的Application 的 `onCreate` 方法中，且保证在GrowingIO 采集SDK 启动代码后

```java
public  class  MyApplication  extends  Application  {

​

 @Override

 public  void  onCreate()  {

 super.onCreate();

 // GrowingIO采集SDK 启动代码

​

 //调用 弹窗SDK 启动方法 

 GrowingTouch.startWithConfig(this,  new  GTouchConfig()

 .setEventPopupShowTimeout(5000)

 .setEventPopupEnable(true)

 .setDebugEnable(BuildConfig.DEBUG)

 .setMessageHost("获取您的服务器上发出的弹窗和banner数据")

 .setEventPopupListener(new  EventPopupListener()  {

 @Override

 public  void  onLoadSuccess(String eventId, String eventType)  {

 Log.d(TAG,  "onLoadSuccess: eventId = "  + eventId +  ", eventType = "  + eventType);

 }

​

 @Override

 public  void  onLoadFailed(String eventId, String eventType,  int errorCode, String description)  {

 Log.d(TAG,  "onLoadFailed: eventId = "  + eventId +  ", eventType = "  + eventType);

​

 }

​

 @Override

 public  boolean  onClicked(String eventId, String eventType, String openUrl)  {

 Log.d(TAG,  "onClicked: eventId = "  + eventId +  ", eventType = "  + eventType);

 return  false;

 }

​

 @Override

 public  void  onCancel(String eventId, String eventType)  {

 Log.d(TAG,  "onCancel: eventId = "  + eventId +  ", eventType = "  + eventType);

​

 }

​

 @Override

 public  void  onTimeout(String eventId, String eventType)  {

 Log.d(TAG,  "onTimeout: eventId = "  + eventId +  ", eventType = "  + eventType);

 }

 })

 );

 }

}
```

请注意调用顺序，需要在 GrowingIO 采集SDK 启动代码调用后，再调用 `GrowingTouch.startWithConfig` 函数。


### 代码混淆[](#6-dai-ma-hun-xiao)

如果您启用了代码混淆，请务必在您的proguard-rules.pro文件里加入下面的代码：

```java
#GrowingIO

-keep class  com.growingio.**  {

 *;

}

-dontwarn com.growingio.**

-keepnames class  *  extends  android.view.View

-keepnames class  *  extends  android.app.Fragment

-keepnames class  *  extends  android.support.v4.app.Fragment

-keepnames class  *  extends  androidx.fragment.app.Fragment

-keep class  android.support.v4.view.ViewPager{

 *;

}

-keep class  android.support.v4.view.ViewPager$**{

 *;

}

-keep class  androidx.viewpager.widget.ViewPager{

 *;

}

-keep class  androidx.viewpager.widget.ViewPager$**{

 *;

}

​

#okhttp

-dontwarn okhttp3.**

-keep class  okhttp3.**{*;}

​

#okio

-dontwarn okio.**

-keep class  okio.**{*;}
```


## 重要配置[](#er-zhong-yao-pei-zhi)

### 设置弹窗开关[](#1-she-zhi-dan-chuang-kai-guan)

#### 1.1 setEventPopupEnable[](#1-1-seteventpopupenable)

设置弹窗的开关，可以在初始化的时候选择关闭弹窗功能，这样弹窗SDK就不会在APP的logo页和闪屏页显示弹窗，然后在APP的内容页打开时再打开弹窗开关。

setEventPopupEnable(boolean eventPopupEnable)


#### 1.2 参数说明[](#12-can-shu-shuo-ming)

| **参数名** | **类型** | **必填** | **默认值** | **说明** |
| --- | --- | --- | --- | --- |
| enable | boolean | 是   | true | 开关弹窗功能，true开启，false关闭 |


#### 1.3 代码示例[](#13-dai-ma-shi-li)

```java
GrowingTouch.startWithConfig(this,  new  GTouchConfig()

 .setEventPopupEnable(true)

 ...

 );
```


### 设置Debug模式（只在调试时使用，上线请务必关闭）[](#2-she-zhi-debug-mo-shi-zhi-zai-tiao-shi-shi-shi-yong-shang-xian-qing-wu-bi-guan-bi)

#### 2.1 setDebugEnable[](#2-1-setdebugenable)

查看数据采集发送日志，能够在Android Studio中通过Logcat查看GrowingTouch打印的数据发送日志，在 APP 的 Application onCreate 初始化SDK地方添加配置。

setDebugEnable(boolean debugEnable)


#### 2.2 参数说明[](#22-can-shu-shuo-ming)

| **参数名** | **类型** | **必填** | **默认值** | **说明** |
| --- | --- | --- | --- | --- |
| debugEnable | boolean | 是   | false | 开启弹窗日志，true开启，false关闭 |


#### 2.3 代码示例[](#23-dai-ma-shi-li)

```java
GrowingTouch.startWithConfig(this,  new  GTouchConfig()

 //BuildConfig.DEBUG 这样配置就不会上线忘记关闭

 .setDebugEnable(BuildConfig.DEBUG)

 ...

 );
```

### 设置弹窗显示超时时间[](#3-she-zhi-dan-chuang-xian-shi-chao-shi-shi-jian)

#### 3.1 setEventPopupShowTimeout[](#3-1-seteventpopupshowtimeout)

埋点事件的产生到弹窗完全显示的超时时间，如网络情况可能会影响到弹窗的加载时间，或者两个弹窗埋点事件先后触发，前面一个弹窗的显示时间过长导致后面的弹窗事件超时等等。

setEventPopupShowTimeout(long eventPopupShowTimeout)

#### 3.2 参数说明[](#32-can-shu-shuo-ming)

| **参数名** | **类型** | **必填** | **默认值** | **说明** |
| --- | --- | --- | --- | --- |
| eventPopupShowTimeout | long | 是   | 5000 | 埋点事件的产生到弹窗完全显示的超时时间,单位ms。0<=有效值<=100000 |

#### 3.3 代码示例[](#33-dai-ma-shi-li)

```java
GrowingTouch.startWithConfig(this,  new  GTouchConfig()

 .setEventPopupShowTimeout(8000)

 ...

 );
```


### 弹窗的事件监听[](#4-dan-chuang-de-shi-jian-jian-ting)

#### 4.1 setEventPopupListener[](#4-1-seteventpopuplistener)

通过监听获取事件和参数，您可以根据事件和参数以及您的业务场景执行相关的交互。

setEventPopupListener(EventPopupListener eventPopupListener)


#### 4.2 参数说明[](#42-can-shu-shuo-ming)

```java
public  interface  EventPopupListener  {

 /**

 \* 弹窗显示成功

 *

 \* @param eventId   埋点事件名称

 \* @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)

 */

 void  onLoadSuccess(String eventId, String eventType);

​

 /**

 \* 弹窗加载失败

 *

 \* @param eventId     埋点事件名称

 \* @param eventType   事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)

 \* @param errorCode   错误码

 \* @param description 错误描述

 */

 void  onLoadFailed(String eventId, String eventType,  int errorCode, String description);

​

 /**

 \* 用户点击了弹窗的有效内容。弹窗SDK现在只提供跳转APP内部界面和H5界面两种处理方式。

 \* 您可以在这里接管跳转事件，处理需要跳转的url。您也可以自定义Url协议，实现更多业务和交互功能。

 *

 \* @param eventId   埋点事件名称

 \* @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)

 \* @param openUrl   跳转的url

 \* @return true：点击事件被消费，弹窗SDK不在处理；false：由弹窗SDK处理点击事件

 */

 boolean  onClicked(String eventId, String eventType, String openUrl);

​

 /**

 \* 用户关闭了弹窗

 *

 \* @param eventId   埋点事件名称

 \* @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)

 */

 void  onCancel(String eventId, String eventType);

​

 /**

 \* 弹窗显示超时

 *

 \* @param eventId   埋点事件名称

 \* @param eventType 事件类型，system(弹窗SDK内置的事件)或custom(用户自定义的埋点事件)

 */

 void  onTimeout(String eventId, String eventType);

}
```


#### 4.3 代码示例[](#43-dai-ma-shi-li)

```java
GrowingTouch.startWithConfig(this,  new  GTouchConfig()

 .setEventPopupListener(new  EventPopupListener()  {

 @Override

 public  void  onLoadSuccess(String eventId, String eventType)  {

 Log.d(TAG,  "onLoadSuccess: eventId = "  + eventId +  ", eventType = "  + eventType);

 }

​

 @Override

 public  void  onLoadFailed(String eventId, String eventType,  int errorCode, String description)  {

 Log.d(TAG,  "onLoadFailed: eventId = "  + eventId +  ", eventType = "  + eventType);

​

 }

​

 @Override

 public  boolean  onClicked(String eventId, String eventType, String openUrl)  {

 Log.d(TAG,  "onClicked: eventId = "  + eventId +  ", eventType = "  + eventType);

 return  false;

 }

​

 @Override

 public  void  onCancel(String eventId, String eventType)  {

 Log.d(TAG,  "onCancel: eventId = "  + eventId +  ", eventType = "  + eventType);

​

 }

​

 @Override

 public  void  onTimeout(String eventId, String eventType)  {

 Log.d(TAG,  "onTimeout: eventId = "  + eventId +  ", eventType = "  + eventType);

 }

 })

 ...

 );
```

## 运行时API介绍( GrowingTouch.class )[](#san-yun-hang-shi-api-jie-shao-growingtouchclass)

### void enableEventPopupAndGenerateAppOpenEvent()[](#1-void-enableeventpopupandgenerateappopenevent)

打开弹窗并触发AppOpen事件。

应用场景时：担心弹窗SDK在APP启动的Logo页或者闪屏页显示弹窗，这时可以选择在初始化时关闭弹窗开关，然后在APP的内容页打开时再打开弹窗开关。

如果只是单纯调用`**GrowingTouch.setEventPopupEnable(true)**`只会打开弹窗开关，并不会触发AppOpen的弹窗事件。调用该API则会打开弹窗的同时触发一个AppOpen的弹窗事件。（AppOpen 对应的是触发时机选择“打开App时”）


### boolean isEventPopupShowing()[](#2-boolean-iseventpopupshowing)

弹窗是否正在显示


## 其他[](#si-qi-ta)

### 弹窗跳转原生Activity界面[](#1-dan-chuang-tiao-zhuan-yuan-sheng-activity-jie-mian)

若弹窗跳转链接为 GInApp://com.growingio.gtouch.InAppPageActivity?key1=value1&key2=value2 那么会打开原生界面 InAppPageActivity，并携带两个参数。

对应的Web弹窗页面配置如下图所示：

* **弹窗配置页面：**

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4n6bm44ny-7NmMTwSQ%2F-M4nSxsFTYb0MFuizCCD%2Fimage.png?alt=media&token=2e03ebb8-1b01-4424-a687-10a44305822a)

其中「自定义参数」意思是输入任何您自己的scheme（自定义协议），

比如： myapp://productdetails/itemabc?key1=111&key2=222 ，然后在onclick事件回调中解析出来就行了

```java
@Override

protected  void  onCreate(Bundle savedInstanceState)  {

 super.onCreate(savedInstanceState);

 setContentView(R.layout.activity\_in\_app_page);

 Intent intent =  getIntent();

 Log.e(TAG,  "onCreate: key1 = "  + intent.getStringExtra("key1"));

 Log.e(TAG,  "onCreate: key2 = "  + intent.getStringExtra("key2"));

}
```

### "打开APP时"事件触发的时机[](#2-da-kai-app-shi-shi-jian-chu-fa-de-shi-ji)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4n6bm44ny-7NmMTwSQ%2F-M4nT7FlkEwp3di-yMFH%2Fimage.png?alt=media&token=f62a9eea-1e82-4fe8-bb71-a5baafc726ab)

打开APP时，无论是冷启动还是热启动，第一个Activity的onStart生命周期的时候触发。


### okhttp 版本要求[](#3-okhttp-ban-ben-yao-qiu)

需要升级到3.12.1，弹窗使用了新版的方法，否则会报错。
