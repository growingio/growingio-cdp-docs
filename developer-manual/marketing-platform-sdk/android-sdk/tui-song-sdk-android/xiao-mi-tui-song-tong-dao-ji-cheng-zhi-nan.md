---
id: mp-push-sdk-android-xiaomi
sidebar_position: 6
---

# 小米推送通道集成指南

小米推送通道是由小米官方提供的系统级推送通道。在小米手机上，推送消息能够通过小米的系统通道抵达终端，并且无需打开应用就能够收到推送。


## 获取小米推送秘钥[](#1-huo-qu-xiao-mi-tui-song-mi-yue)

根据[小米开放平台](https://dev.mi.com/console/appservice/push.html)指引开通小米开发者账号,然后注册应用并获取小米推送的秘钥。

认证小米开发者：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MDJ-ZKn0jRNemBrFmfQ%2F-MDJ4NORXdKxkIIqMWkS%2Fimage.png?alt=media&token=56995b6d-6f10-4567-b19a-ab463e3ab399)

获取小米推送秘钥：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MDJ-ZKn0jRNemBrFmfQ%2F-MDJ4RvtKGyDZJtnZu_x%2Fimage.png?alt=media&token=63b153ae-ab1c-4175-b501-c9ce46336316)


## 在app build.gradle添加小米通道SDK依赖[](#2-zai-app-buildgradle-tian-jia-xiao-mi-tong-dao-sdk-yi-lai)

```java
dependencies {

 ...

 //由于推送底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖

 implementation 'com.squareup.okhttp3:okhttp:3.12.1'

 //推送SDK依赖

 implementation 'com.growingio.android:gtouch:$gtouch_version'

 //小米推送SDK依赖

 implementation 'com.growingio.android.gpush:gpush-xiaomi-adapter:$gtouch_version'

}
```

> $gtouch_version 为最新SDK版本号，现最新的版本号为请参考[SDK更新日志](https://growingio.gitbook.io/op/v/v20200701/developer-manual/sdkintegrated/mp/gtouchsdk-releasenotes)。


## 配置AppID和AppKey[](#3-pei-zhi-appid-he-appkey)

```java
android {

 ......

 defaultConfig {

 manifestPlaceholders =  [

 PACKAGE_NAME :  "您的APP包名",

​

 GPUSH\_XIAOMI\_APP_ID :  "小米推送的AppId",

 GPUSH\_XIAOMI\_APP_KEY:  "小米推送的AppKey",

 ]

 ......

 }

 ......

}
```


## 代码混淆[](#4-dai-ma-hun-xiao)

```java
-keep class  com.xiaomi.**{*;}

-keep public  class  *  extends  com.xiaomi.mipush.sdk.PushMessageReceiver
```


## 配置服务端AppID和AppSecret[](#5-pei-zhi-fu-wu-duan-appid-he-appsecret)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MDJ-ZKn0jRNemBrFmfQ%2F-MDOps9ww8gHXoAA198p%2Fimage.png?alt=media&token=c89eba06-e57c-4786-969b-f3418d87cb2f)

在应用配置界面输入您APP的AppID和AppSecret


## 厂商通道测试方法[](#6-chang-shang-tong-dao-ce-shi-fang-fa)

1.  将集成好的App（测试版本）安装在一台小米测试机上，并且运行App
    
2.  保持App在前台运行，尝试扫码测试推送消息
    
3.  如果应用收到消息，将App退到后台，并且杀掉所有App进程
    
4.  再次进行测试推送消息，如果能够收到推送，则表明厂商通道集成成功
    

## 兼容性[](#7-jian-rong-xing)

如果您的App已经集成了个推VIP或极光VIP版本的推送SDK，我们的Android SDK也能兼容。

为了和个推兼容，我们将厂商通道独立打包。以小米推送通道为例，我们打包两个SDK：gpush-mipush-sdk和gpush-xiaomi-adapter。如果是从未接过个推、极光等VIP版本的用户可以直接添加小米推送通道依赖。

```java
implementation 'com.growingio.android.gpush:gpush-xiaomi-adapter:$gtouch_version'
```

如果是个推、极光等VIP版本的用户可以将小米官方SDK包gpush-mipush-sdk 排除出去。

```java
implementation ('com.growingio.android.gpush:gpush-xiaomi-adapter:$gtouch_version'){

 exclude(group:  'com.growingio.android.gpush'  , module:  'gpush-mipush-sdk')

}
```
