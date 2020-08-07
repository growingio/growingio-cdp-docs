---
description: 小米推送通道是由小米官方提供的系统级推送通道。在小米手机上，推送消息能够通过小米的系统通道抵达终端，并且无需打开应用就能够收到推送。
---

# 小米推送通道集成指南

### 1. 获取小米推送秘钥 <a id="1-huo-qu-xiao-mi-tui-song-mi-yue"></a>

根据[小米开放平台](https://dev.mi.com/console/appservice/push.html)指引开通小米开发者账号,然后注册应用并获取小米推送的秘钥。

认证小米开发者：![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-LqiImfa22AAr2Os4K3V%2F-LqiYHvsQhlpRUk-2ejq%2F3.png?alt=media&token=10ae6ec1-feb0-44d6-b8f3-79db138e975b)

获取小米推送秘钥：![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-LqiImfa22AAr2Os4K3V%2F-LqiYWzfhJYSrhiYf8dR%2F4.png?alt=media&token=5d3da45c-3eab-4ced-8d5d-54806ba3d025)

### 2. 在app build.gradle添加小米通道SDK依赖 <a id="2-zai-app-buildgradle-tian-jia-xiao-mi-tong-dao-sdk-yi-lai"></a>

```text
dependencies {    ...    //由于推送底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖    implementation 'com.squareup.okhttp3:okhttp:3.12.1'    //推送SDK依赖    implementation 'com.growingio.android:gtouch:$gtouch_version'    //小米推送SDK依赖    implementation 'com.growingio.android.gpush:gpush-xiaomi-adapter:$gtouch_version'}
```

> $gtouch\_version 为最新SDK版本号，现最新的版本号为请参考[SDK更新日志](https://docs.growingio.com/mp/developers/integrations/changelog)。

### 3. 配置AppID和AppKey <a id="3-pei-zhi-appid-he-appkey"></a>

```text
android {        ......        defaultConfig {            manifestPlaceholders = [                PACKAGE_NAME        : "您的APP包名",​                GPUSH_XIAOMI_APP_ID : "小米推送的AppId",                GPUSH_XIAOMI_APP_KEY: "小米推送的AppKey",            ]            ......        }        ......}
```

### 4. 代码混淆 <a id="4-dai-ma-hun-xiao"></a>

```text
-keep class com.xiaomi.**{*;}​-keep public class * extends com.xiaomi.mipush.sdk.PushMessageReceiver
```

### 5. 配置服务端AppID和AppSecret <a id="5-pei-zhi-fu-wu-duan-appid-he-appsecret"></a>

![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-LqiImfa22AAr2Os4K3V%2F-LqiZEHMyTOP34M7HzfG%2F5.png?alt=media&token=d78d8a2e-a6e5-4181-8436-067d5cc4b6f3)

在应用配置界面输入您APP的AppID和AppSecret

### 6. 厂商通道测试方法 <a id="6-chang-shang-tong-dao-ce-shi-fang-fa"></a>

1. 将集成好的App（测试版本）安装在一台小米测试机上，并且运行App
2. 保持App在前台运行，尝试扫码测试推送消息
3. 如果应用收到消息，将App退到后台，并且杀掉所有App进程
4. 再次进行测试推送消息，如果能够收到推送，则表明厂商通道集成成功

### 7. 兼容性 <a id="7-jian-rong-xing"></a>

如果您的App已经集成了个推VIP或极光VIP版本的推送SDK，我们的Android SDK也能兼容。

为了和个推兼容，我们将厂商通道独立打包。以小米推送通道为例，我们打包两个SDK：gpush-mipush-sdk和gpush-xiaomi-adapter。如果是从未接过个推、极光等VIP版本的用户可以直接添加小米推送通道依赖。

```text
implementation 'com.growingio.android.gpush:gpush-xiaomi-adapter:$gtouch_version'
```

如果是个推、极光等VIP版本的用户可以将小米官方SDK包gpush-mipush-sdk 排除出去。

```text
implementation ('com.growingio.android.gpush:gpush-xiaomi-adapter:$gtouch_version'){      exclude(group: 'com.growingio.android.gpush' , module: 'gpush-mipush-sdk')}
```

