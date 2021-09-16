---
description: 华为推送通道是由华为官方提供的系统级推送通道。在华为手机上，推送消息能够通过华为的系统通道抵达终端，并且无需打开应用就能够收到推送。
---

# 华为推送通道集成指南

* 华为推送只有在**签名发布包环境**下才可以收到推送消息
* 华为手机中的**移动推送服务**，必须升级到 2.5.3 以上版本

## 1. 获取华为推送秘钥 <a id="1-huo-qu-hua-wei-tui-song-mi-yue"></a>

1. 访问 [华为开放平台](http://developer.huawei.com/)。
2. 注册/登录开发者账号。（如果您是新注册账号，需进行实名认证）.
3. 在华为推送平台中新建应用。注意：应用包名需跟您在GIO集成的包名保持一致

## 2. **在project build.gradle的allprojects-&gt;repositories添加华为推送SDK的maven仓库** <a id="2-zai-project-buildgradle-de-allprojectsrepositories-tian-jia-hua-wei-tui-song-sdk-de-maven-cang-ku"></a>

```text
allprojects {    repositories {        google()        jcenter()        mavenLocal()        // 华为仓库        maven { url 'http://developer.huawei.com/repo/' }    }}
```

## 3. 在app build.gradle添加华为通道SDK依赖 <a id="3-zai-app-buildgradle-tian-jia-hua-wei-tong-dao-sdk-yi-lai"></a>

```text
dependencies {    ...    //由于推送底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖    implementation 'com.squareup.okhttp3:okhttp:3.12.1'    //推送SDK依赖    implementation 'com.growingio.android:gtouch:$gtouch_version'    //华为推送SDK依赖    implementation 'com.growingio.android.gpush:gpush-huawei-adapter:$gtouch_version'}
```

> $gtouch\_version 为最新SDK版本号，现最新的版本号为请参考[SDK更新日志](https://docs.growingio.com/mp/developers/integrations/changelog)。

## 4. 配置AppID <a id="4-pei-zhi-appid"></a>

```text
android {        ......        defaultConfig {            manifestPlaceholders = [                PACKAGE_NAME        : "您的APP包名",​                GPUSH_HUAWEI_APP_ID : "华为推送的AppId(华为推送不需要AppKey)",            ]            ......        }        ......}
```

## 5. 代码混淆 <a id="5-dai-ma-hun-xiao"></a>

```text
-ignorewarning​-keepattributes *Annotation*​-keepattributes Exceptions​-keepattributes InnerClasses​-keepattributes Signature​-keepattributes SourceFile,LineNumberTable​-keep class com.hianalytics.android.**{*;}​-keep class com.huawei.updatesdk.**{*;}​-keep class com.huawei.hms.**{*;}​-keep class com.huawei.android.hms.agent.**{*;}
```

## 6. 配置服务端AppID和AppSecret <a id="6-pei-zhi-fu-wu-duan-appid-he-appsecret"></a>

![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-LwW7qFJdkpsyPiAUXoG%2F-LwWK91WiRjSBM-I2t3g%2Fimage.png?alt=media&token=ae26ad07-bea7-4dc5-b6a0-a09e84e0df96)

## 7. 设置推送消息回执 <a id="7-she-zhi-tui-song-xiao-xi-hui-zhi"></a>

在华为推送APP编辑界面配置回执，以便于我们GrowingIO更好的统计推送数据![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-LqiImfa22AAr2Os4K3V%2F-LqiTmuqvoTo2uYHo-QR%2F2.png?alt=media&token=d8219105-0af7-491c-9397-305609e1a47b)

目前单击【测试回执】，会提示“https，error"，请忽略并直接单击【提交】。

其中回调地址

```text
https://messages.growingio.com/v1/callback/huawei
```

HTTPS证书

```text
-----BEGIN CERTIFICATE-----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-----END CERTIFICATE-----
```

## 8. 厂商通道测试方法 <a id="8-chang-shang-tong-dao-ce-shi-fang-fa"></a>

1. 将集成好的App（测试版本）安装在一台华为测试机上，并且运行App
2. 保持App在前台运行，尝试扫码测试推送消息
3. 如果应用收到消息，将App退到后台，并且杀掉所有App进程
4. 再次进行测试推送消息，如果能够收到推送，则表明厂商通道集成成功
5. 最好能根据官方推荐方式，先[测通华为官方推送](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/push-console)​

## 9. 兼容性 <a id="9-jian-rong-xing"></a>

如果您的app已经集成了个推VIP或极光VIP版本等其他包含了华为推送sdk的第三方推送平台SDK，我们的android sdk也能兼容。

为了和个推兼容，我们将厂商通道独立打包。以华为推送通道为例，我们打包两个SDK：gpush-hms-agent和gpush-huawei-adapter。如果是从未接过个推、极光等VIP版本的用户可以直接添加华为推送通道依赖

```text
implementation 'com.growingio.android.gpush:gpush-huawei-adapter:$gtouch_version'
```

如果是个推、极光等VIP版本的用户可以将华为官方SDK包gpush-hms-agent 排除出去。

```text
implementation ('com.growingio.android.gpush:gpush-huawei-adapter:$gtouch_version'){      exclude(group: 'com.growingio.android.gpush' , module: 'gpush-hms-agent')}
```

