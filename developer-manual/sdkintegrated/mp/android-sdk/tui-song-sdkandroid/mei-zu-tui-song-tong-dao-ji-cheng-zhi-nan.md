---
description: 魅族推送通道是由魅族官方提供的系统级推送通道。在魅族手机上，推送消息能够通过魅族的系统通道抵达终端，并且无需打开应用就能够收到推送。
---

# 魅族推送通道集成指南

### 1. 获取魅族推送秘钥

1. 打开[魅族推送官网](https://open.flyme.cn/open-web/views/push.html)
2. 注册/登录开发者账号。（如果您是新注册账号，进行实名认证大约需要2天左右时间，具体请咨询魅族侧）
3. 在魅族推送平台（[http://push.meizu.com）](http://push.meizu.com%29/) 中新建应用。注意「应用包名」需跟您在GrowingIO 推送填写的包名保持一致

注：更多详情请参照[魅族开发文档](http://open.res.flyme.cn/fileserver/upload/file/201709/a271468fe23b47408fc2ec1e282f851f.pdf)

### 2. 在app build.gradle添加魅族通道SDK依赖

```java
dependencies {
    ...
    //由于推送底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖
    implementation 'com.squareup.okhttp3:okhttp:3.12.1'
    //推送SDK依赖
    implementation 'com.growingio.android:gtouch:$gtouch_version'
    //魅族推送SDK依赖
    implementation 'com.growingio.android.gpush:gpush-meizu-adapter:$gtouch_version'
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

                GPUSH_MEIZU_APP_ID  : "魅族推送的AppId",
                GPUSH_MEIZU_APP_KEY : "魅族推送的AppKey",
            ]
            ......
        }
        ......
}
```

### 4. 代码混淆

```java
-dontwarn com.meizu.cloud.pushsdk.**

-keep class com.meizu.cloud.pushsdk.**{*;}
```

### 5. 配置服务端AppID和AppSecret

![](../../../../../.gitbook/assets/image%20%28311%29.png)

### 6. 设置推送消息回执

在魅族推送APP配置界面配置回执，以便于我们GrowingIO更好的统计推送数据

![](../../../../../.gitbook/assets/image%20%28316%29.png)

其中回执地址：

```text
https://messages.growingio.com/v1/callback/meizu
```

### 7. 厂商通道测试方法\(通用\)

1. 将集成好的App（测试版本）安装在一台魅族测试机上，并且运行App
2. 保持App在前台运行，尝试扫码测试推送消息
3. 如果应用收到消息，将App退到后台，并且杀掉所有App进程
4. 再次进行测试推送消息，如果能够收到推送，则表明厂商通道集成成功



