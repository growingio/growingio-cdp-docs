---
description: 小米推送通道是由小米官方提供的系统级推送通道。在小米手机上，推送消息能够通过小米的系统通道抵达终端，并且无需打开应用就能够收到推送。
---

# 小米推送通道集成指南



### 1. 获取小米推送秘钥

根据[小米开放平台](https://dev.mi.com/console/appservice/push.html)指引开通小米开发者账号,然后注册应用并获取小米推送的秘钥。

认证小米开发者：

![](../../../../../.gitbook/assets/image%20%28309%29.png)

获取小米推送秘钥：

![](../../../../../.gitbook/assets/image%20%28304%29.png)

### 2. 在app build.gradle添加小米通道SDK依赖

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

> $gtouch\_version 为最新SDK版本号，现最新的版本号为请参考[SDK更新日志](https://growingio.gitbook.io/op/v/v20200701/developer-manual/sdkintegrated/mp/gtouchsdk-releasenotes)。

### 3. 配置AppID和AppKey

```java
android {
        ......
        defaultConfig {
            manifestPlaceholders = [
                PACKAGE_NAME        : "您的APP包名",

                GPUSH_XIAOMI_APP_ID : "小米推送的AppId",
                GPUSH_XIAOMI_APP_KEY: "小米推送的AppKey",
            ]
            ......
        }
        ......
}
```

### 4. 代码混淆

```java
-keep class com.xiaomi.**{*;}

-keep public class * extends com.xiaomi.mipush.sdk.PushMessageReceiver
```

### 5. 配置服务端AppID和AppSecret

![](../../../../../.gitbook/assets/image%20%28303%29.png)

在应用配置界面输入您APP的AppID和AppSecret

### 6. 厂商通道测试方法

1. 将集成好的App（测试版本）安装在一台小米测试机上，并且运行App
2. 保持App在前台运行，尝试扫码测试推送消息
3. 如果应用收到消息，将App退到后台，并且杀掉所有App进程
4. 再次进行测试推送消息，如果能够收到推送，则表明厂商通道集成成功

### 7. 兼容性

如果您的App已经集成了个推VIP或极光VIP版本的推送SDK，我们的Android SDK也能兼容。

为了和个推兼容，我们将厂商通道独立打包。以小米推送通道为例，我们打包两个SDK：gpush-mipush-sdk和gpush-xiaomi-adapter。如果是从未接过个推、极光等VIP版本的用户可以直接添加小米推送通道依赖。

```java
implementation 'com.growingio.android.gpush:gpush-xiaomi-adapter:$gtouch_version'
```

如果是个推、极光等VIP版本的用户可以将小米官方SDK包gpush-mipush-sdk 排除出去。

```java
implementation ('com.growingio.android.gpush:gpush-xiaomi-adapter:$gtouch_version'){
      exclude(group: 'com.growingio.android.gpush' , module: 'gpush-mipush-sdk')
}
```

