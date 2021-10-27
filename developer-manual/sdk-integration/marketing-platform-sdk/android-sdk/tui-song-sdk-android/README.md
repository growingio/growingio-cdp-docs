---
id: mp-push-sdk-android
sidebar_position: 1
---

# 推送 SDK（Android）
​
:::info
最低兼Android版本4.2 API 17
:::

推送SDK会根据运营人员对用户的分组情况，下发弹窗和推送消息。

各个厂商通道的详细接入文档见目录栏「厂商通道」。

## 集成SDK[](#yi-ji-cheng-sdk)

### 集成GrowingIO Android无埋点SDK[](#1-ji-cheng-growingio-android-wu-mai-dian-sdk)

:::info
推送 SDK 依赖于数据数据采集 SDK

版本要求最低1.2.3，如已集成请跳过
:::

参考 [Android SDK](/op/v/2.0/developer-manual/sdkintegrated/client-sdk-3.0/android-sdk) ​


### 添加依赖[](#2-tian-jia-yi-lai)

#### 在project级别的build.gradle的allprojects->repositories添加华为推送SDK的maven仓库[](#21-zai-project-ji-bie-de-buildgradle-de-allprojectsrepositories-tian-jia-hua-wei-tui-song-sdk-de-maven-cang-ku)

如果没有开通华为推送通道可以不用添加该仓库，跳过该步骤。

```java
allprojects {

 repositories {

 google()

 jcenter()

 mavenLocal()

 // 华为仓库

 maven { url 'http://developer.huawei.com/repo/'  }

 }

}
```


#### 在module级别的build.gradle添加SDK依赖[](#22-zai-module-ji-bie-de-buildgradle-tian-jia-sdk-yi-lai)

``` java
dependencies {

 ...

 //由于推送底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖

 implementation 'com.squareup.okhttp3:okhttp:3.12.1'

 //推送SDK依赖

 implementation 'com.growingio.android:gtouch:$gtouch_version'

 //华为推送SDK依赖，如果没有开通华为推www送通道可以不用添加该依赖

 implementation 'com.growingio.android.gpush:gpush-huawei-adapter:$gtouch_version'

 //魅族推送SDK依赖，如果没有开通魅族推送通道可以不用添加该依赖

 implementation 'com.growingio.android.gpush:gpush-meizu-adapter:$gtouch_version'

 //小米推送SDK依赖，如果没有开通小米推送通道可以不用添加该依赖

 implementation 'com.growingio.android.gpush:gpush-xiaomi-adapter:$gtouch_version'

 //OPPO推送SDK依赖，如果没有开通OPPO推送通道可以不用添加该依赖

 implementation 'com.growingio.android.gpush:gpush-oppo-adapter:$gtouch_version'

 //vivo推送SDK依赖，如果没有开通vivo推送通道可以不用添加该依赖

 implementation 'com.growingio.android.gpush:gpush-vivo-adapter:$gtouch_version'

}
```

> $gtouch_version 为最新SDK版本号，现最新的版本号为请参考[SDK更新日志](/op/v/2.0/developer-manual/sdkintegrated/mp/gtouchsdk-releasenotes)。


### 配置AppID和AppKey[](#3-pei-zhi-appid-he-appkey)

在module级别的build.gradle里配置AppID和AppKey。

根据您APP的实际情况配置不同厂家渠道

``` java
android {

 ......

 defaultConfig {

 manifestPlaceholders =  [

 PACKAGE_NAME  :  "您的APP包名",

​

 GPUSH_XIAOMI_APP_ID  :  "小米推送的AppId",

 GPUSH_XIAOMI_APP_KEY:  "小米推送的AppKey",

​

 GPUSH_HUAWEI_APP_ID  :  "华为推送的AppId(华为推送不需要AppKey)",

​

 GPUSH_MEIZU_APP_ID  :  "魅族推送的AppId",

 GPUSH_MEIZU_APP_KEY  :  "魅族推送的AppKey",

​

 GPUSH_VIVO_APP_ID  :  "VIVO推送的AppId",

 GPUSH_VIVO_APP_KEY  :  "VIVO推送的AppKey",

​

 GPUSH_OPPO_APP_ID  :  "OPPO推送的AppId",

 GPUSH_OPPO_APP_KEY  :  "OPPO推送的AppKey",

 GPUSH_OPPO_APP_SECRET  :  "OPPO推送的AppSecret",

 ]

 ......

 }

 ......

}
```


### 添加权限[](#4-tian-jia-quan-xian)

集成推送SDK需在AndroidManifest.xml 中添以下权限

``` xml
<!-- 【必须】 小米、华为，魅族和Vivo推送SDK所需权限 -->

<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"  />

<uses-permission android:name="android.permission.READ_PHONE_STATE"  /> 

<uses-permission android:name="android.permission.GET_TASKS"  /> 

<uses-permission android:name="android.permission.VIBRATE"/> 

<!-- 【必须】 Oppo推送SDK需额外权限 -->

<uses-permission android:name="com.colors.mcs.permission.RECIEVE_MCS_MESAGE"  />
```


### 初始化SDK[](#5-chu-shi-hua-sdk)

请将以下`GrowingTouch.startWithConfig`加在您的Application 的 `onCreate` 方法中，且保证在GrowingIO 采集SDK 启动代码后

``` java
public  class  MyApplication extends Application  {

 @Override

 public void onCreate()  {

 super.onCreate();

 // GrowingIO 采集SDK 启动代码

 // GrowingIO 推送SDK 启动代码

 GrowingTouch.startWithConfig(this,  new  GTouchConfig()

 .setPushEnable(true)

 .setDebugEnable(BuildConfig.DEBUG)

 );

 }

}
```

请注意调用顺序，需要在 GrowingIO 采集SDK 启动代码调用后，再调用 `GrowingTouch.startWithConfig` 函数。


### 代码混淆[](#6-dai-ma-hun-xiao)

如果您启用了代码混淆，请务必在您的proguard-rules.pro文件里加入下面的代码：

``` java
#GrowingIO

-keep class  com.growingio.**  {

 *;

}

-dontwarn com.growingio.**

-keepnames class  * extends android.view.View

-keepnames class  * extends android.app.Fragment

-keepnames class  * extends android.support.v4.app.Fragment

-keepnames class  * extends androidx.fragment.app.Fragment

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

​

#Xiaomi  Push

-dontwarn com.xiaomi.**

-keep class  com.xiaomi.**{*;}

-keep public  class  * extends com.xiaomi.mipush.sdk.PushMessageReceiver

#Huawei  Push

-ignorewarnings

-keepattributes *Annotation*

-keepattributes Exceptions

-keepattributes InnerClasses

-keepattributes Signature

-keepattributes SourceFile,LineNumberTable

-keep class  com.hianalytics.android.**{*;}

-keep class  com.huawei.updatesdk.**{*;}

-keep class  com.huawei.hms.**{*;}

-keep class  com.huawei.android.hms.agent.**{*;}

​

#Meizu  Push

-dontwarn com.meizu.cloud.pushsdk.**

-keep class  com.meizu.cloud.pushsdk.**{*;}

​

#OPPO  Push

-keep public  class  * extends android.app.Service

​

#vivo Push

-dontwarn com.vivo.push.**

-keep class  com.vivo.push.**{*;}

-keep class  com.growingio.android.sdk.gpush.vivo.VivoPushAdapterReceiver{*;}
```


## 重要配置[](#er-zhong-yao-pei-zhi)

### 设置推送开关 setPushEnable[](#1-she-zhi-tui-song-kai-guan-setpushenable)

设置推送消息的开关

setPushEnable(boolean pushEnable)

**参数说明**

| **参数名** | 类型  | 必填  | 说明  |
| --- | --- | --- | --- |
| enable | boolean | 是   | 开关推送功能<br></br>* true开启<br></br>* false关闭<br></br>默认为true |

**代码示例**

``` java
GrowingTouch.startWithConfig(this,  new  GTouchConfig()

 .setPushEnable(true)

 ...

 );

```


### 设置Debug模式（只在调试时使用，上线请务必关闭） **setDebugEnable**[](#2-she-zhi-debug-mo-shi-zhi-zai-tiao-shi-shi-shi-yong-shang-xian-qing-wu-bi-guan-bi-setdebugenable)

查看数据采集发送日志，能够在Android Studio中通过Logcat查看GrowingTouch打印的数据发送日志，在 APP 的 Application onCreate 初始化SDK地方添加配置。

``` java
setDebugEnable(boolean debugEnable)
```

**参数说明**

| **参数名** | 类型  | 必填  | 说明  |
| --- | --- | --- | --- |
| debugEnable | boolean | 是   | 开启推送日志<br></br>* true开启<br></br>* false关闭<br></br>默认false |

**代码示例**

``` java
GrowingTouch.startWithConfig(this,  new  GTouchConfig()

 //BuildConfig.DEBUG 这样配置就不会上线忘记关闭

 .setDebugEnable(BuildConfig.DEBUG)

 ...

 );
```


### 推送消息的自定义处理[](#3-tui-song-xiao-xi-de-zi-ding-yi-chu-li)

推送功能默认提供 **打开APP、打开网页、打开APP内部页面** 、**跳转自定义地址**四种功能，如果前三种功能满足不了您的需求，可以在创建一个跳转自定义地址的推送后， 代码里自定义一个**BroadcastReceiver**类，用于自定义处理各种消息的响应。例如自定义一个BroadcastReceiver，用于消费跳转自定义协议的推送。

``` java
public  class  PushMessageReceiver extends GPushMessageReceiver  {

 private  static  final  String  TAG  =  "PushMessageReceiver";

 /**

 \* 推送注册成功

 \* 

 \* @param context BroadcastReceiver的onReceive回调中的Context对象

 \* @param channel 推送通道，如华为、小米等

 \* @param pushToken 注册的推送Token

 */

 @Override

 public void onRegister(Context context,  PushChannel channel,  String pushToken)  {

 Log.e(TAG,  "onRegister: channel = "  + channel.getChannelName()  +  ", pushToken = "  + pushToken);

 }

 /**

 \* 推送注销成功

 *

 \* @param context BroadcastReceiver的onReceive回调中的Context对象

 */

 @Override

 public void onUnregister(Context context)  {

 Log.e(TAG,  "onUnregister: ");

 }

​

 /**

 \* 推送消息被点击

 \* 

 \* @param context BroadcastReceiver的onReceive回调中的Context对象

 \* @param pushMessage 推送的消息体

 */

 @Override

 public void onNotificationMessageClicked(Context context,  GPushMessage pushMessage)  {

 Log.e(TAG,  "onNotificationMessageClicked: "  + pushMessage.toString());

 }

}
```

将自定义的BroadcastReceiver注册到AndroidManifest.xml文件中

``` xml
<receiver

 android:name="您的包名.PushMessageReceiver"

 android:enabled="true">

 <intent-filter>

 <action android:name="com.growingio.push.intent.action.MESSAGE"  />

 </intent-filter>

</receiver>
```


### 设置推送SDK异常上传开关 setUploadExceptionEnable[](#4-she-zhi-tui-song-sdk-yi-chang-shang-chuan-kai-guan-setuploadexceptionenable)

推送SDK会收集SDK内部异常上报服务端，方便开发更好的追踪推送SDK的问题，和完善推送SDK的功能。如果您不想帮助我们推送产品完善功能，或者和您的crash收集框架有冲突，您可以选择关闭此功能。

``` java
setUploadExceptionEnable(boolean uploadExceptionEnable)
```

**参数说明**

| **参数名** | 类型  | 必填  | 说明  |
| --- | --- | --- | --- |
| uploadExceptionEnable | boolean | 是   | 开关SDK异常上传功能<br></br>* true开启<br></br>* false关闭<br></br>默认值true |

**代码示例**

``` java
 GrowingTouch.startWithConfig(this,  new  GTouchConfig()

 .setUploadExceptionEnable(true)

 ...

 );
```


## API介绍( GrowingTouch.class )[](#san-api-jie-shao-growingtouchclass)

### void registerPush()[](#1-void-registerpush)

注册消息推送功能


### void unRegisterPush()[](#2-void-unregisterpush)

注销消息推送功能

注意执行此方法会使设备发给厂商通道的推送令牌发生变化，导致厂商通道那边有脏数据，一定时间内会降低送达率。


## 其他[](#si-qi-ta)

### 推送消息跳转原生Activity界面[](#1-tui-song-xiao-xi-tiao-zhuan-yuan-sheng-activity-jie-mian)

若推送跳转链接为 com.growingio.gtouch.InAppPageActivity?key1=value1&key2=value2 那么会打开原生界面 InAppPageActivity，并携带两个参数。

对应的推送页面配置如下图所示：

其中「自定义参数」意思是输入任何您自己的scheme（自定义协议），

比如： myapp://productdetails/itemabc ，然后在onclick事件回调中解析出来就行了

* **推送页面配置截图如下：**
    
在InAppPageActivity可以通过intent获取参数

``` java
@Override

protected void onCreate(Bundle savedInstanceState)  {

 super.onCreate(savedInstanceState);

 setContentView(R.layout.activity_in_app_page);

 Intent intent =  getIntent();

 Log.e(TAG,  "onCreate: key1 = "  + intent.getStringExtra("key1"));

 Log.e(TAG,  "onCreate: key2 = "  + intent.getStringExtra("key2"));

}
```


### okhttp 版本要求[](#2-okhttp-ban-ben-yao-qiu)

需要升级到3.12.1，推送使用了新版的方法，否则会报错。

### 集成推送后,原有应用将变为多进程应用[](#3-ji-cheng-tui-song-hou-yuan-you-ying-yong-jiang-bian-wei-duo-jin-cheng-ying-yong)

请注意规避类似如下问题

* Android9.0 禁止多个进程共享同一个WebView数据目录,参见[https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28#framework-security-changes](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28#framework-security-changes)​
    

​

​

​

​

​
