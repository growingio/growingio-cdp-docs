---
description: VIVO推送通道是由VIVO官方提供的系统级推送通道。在VIVO手机上，推送消息能够通过VIVO的系统通道抵达终端，并且无需打开应用就能够收到推送。
---

# vivo推送通道集成指南

### 1. 获取VIVO推送密钥

1. 打开[VIVO开放平台](https://dev.vivo.com.cn/home)。
2. 注册/登录开发者账号。
3. 在VIVO中新建应用。注意「应用包名」需跟您在GrowingIO推送填写的包名保持一致。

{% hint style="info" %}
更多详情请参照[VIVO开发文档](https://dev.vivo.com.cn/documentCenter/doc/233)
{% endhint %}

### 2. 在app build.gradle添加VIVO通道SDK依赖

```java
dependencies {
    ...
    //由于推送底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖
    implementation 'com.squareup.okhttp3:okhttp:3.12.1'
    //推送SDK依赖
    implementation 'com.growingio.android:gtouch:$gtouch_version'
    //VIVO推送SDK依赖
    implementation 'com.growingio.android.gpush:gpush-vivo-adapter:$gtouch_version'
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

                GPUSH_VIVO_APP_ID  : "VIVO推送的AppId",
                GPUSH_VIVO_APP_KEY : "VIVO推送的AppKey",
            ]
            ......
        }
        ......
 }
```

### 4. 代码混淆

```java
-dontwarn com.vivo.push.**
-keep class com.vivo.push.**{*;}
-keep class com.growingio.android.sdk.gpush.vivo.VivoPushAdapterReceiver{*;}
```

### 5. 配置服务端AppID，AppKey和AppSecret

![](../../../../../.gitbook/assets/image%20%28298%29.png)

### 6. 厂商通道测试方法\(通用\)

1. 将集成好的App（测试版本）安装在一台VIVO测试机上，并且运行App
2. 保持App在前台运行，尝试扫码测试推送消息
3. 如果应用收到消息，将App退到后台，并且杀掉所有App进程
4. 再次进行测试推送消息，如果能够收到推送，则表明厂商通道集成成功

### 7. 兼容性

如果您的app已经集成了个推VIP或极光VIP版本的推送SDK，我们的android sdk也能兼容。

为了和个推兼容，我们将厂商通道独立打包，以VIVO推送通道为例，我们打包两个SDK：gpush-vivo-adapter和gpush-vivo-sdk。如果是从未接过个推、极光等VIP版本的用户可以直接添加VIVO推送通道依赖。

```java
implementation 'com.growingio.android.gpush:gpush-vivo-adapter:$gtouch_version'
```

如果是个推、极光等VIP版本的用户可以将vivo官方SDK包gpush-vivopush-sdk 排除出去。

```java
implementation ('com.growingio.android.gpush:gpush-vivo-adapter:$gtouch_version'){
      exclude(group: 'com.growingio.android.gpush' , module: 'gpush-vivo-sdk')
}
```



