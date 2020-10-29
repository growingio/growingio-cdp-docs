---
description: OPPO推送通道是由OPPO官方提供的系统级推送通道。在OPPO手机上，推送消息能够通过OPPO的系统通道抵达终端，并且无需打开应用就能够收到推送。
---

# OPPO推送通道集成指南

### 1. 获取OPPO推送密钥 <a id="1-huo-qu-oppo-tui-song-mi-yue"></a>

1.打开[OPPO推送平台](https://push.oppo.com/)。

2.注册/登录开发者账号。

3.在[OPPO推送平台](https://push.oppo.com/) 中新建应用。注意「应用包名」需跟您在GrowingIO推送填写的包名保持一致。

注: 更多详情请参照[OPPO开发文档](https://push.oppo.com/documents)。

### 2. 创建通道 <a id="2-chuang-jian-tong-dao"></a>

参考[OPPO推送平台开发文档](https://open.oppomobile.com/wiki/doc#id=10289),对于target API≥ 26\(Android 8.0\)的应用，必须适配通知通道，未指定通道的情况下发出的通知将无法显示。

请按照下图配置channel。![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-Lt0MoZxOFvYUG_kBSBp%2F-Lt0RsTv_-HTlqp09qVW%2F111.png?alt=media&token=304271f3-d8a7-433e-8e32-9bb7585d9832)

channel的内容如下：请不要随意改动

```text
// 需要填写的地方可以复制下方内容分组ID: GPUSH_GROUP_ID分组名称:推送消息通道ID:GPUSH_CHANNEL_ID通道名称:标准推送消息消息用途:标准推送消息
```

![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-Lt0MoZxOFvYUG_kBSBp%2F-Lt0RvRxQtKouzpL6_TA%2F222.png?alt=media&token=e92f3c6c-4155-4f60-a83f-3be85b06b12b)

### 3. 在app build.gradle添加OPPO通道SDK依赖 <a id="3-zai-app-buildgradle-tian-jia-oppo-tong-dao-sdk-yi-lai"></a>

```text
dependencies {    ...    //由于推送底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖    implementation 'com.squareup.okhttp3:okhttp:3.12.1'    //推送SDK依赖    implementation 'com.growingio.android:gtouch:$gtouch_version'    //OPPO推送SDK依赖     implementation 'com.growingio.android.gpush:gpush-oppo-adapter:$gtouch_version'    }
```

> $gtouch\_version 为最新SDK版本号，现最新的版本号为请参考[SDK更新日志](https://docs.growingio.com/mp/developers/integrations/changelog)。

### 4. 在app build.gradle配置AppID, AppKey和AppSecret <a id="4-zai-app-buildgradle-pei-zhi-appid-appkey-he-appsecret"></a>

```text
android {        ......        defaultConfig {            manifestPlaceholders = [                PACKAGE_NAME          : "您的APP包名",​                GPUSH_OPPO_APP_ID     : "OPPO推送的AppId",                GPUSH_OPPO_APP_KEY    : "OPPO推送的AppKey",                GPUSH_OPPO_APP_SECRET : "OPPO推送的AppSecret",            ]            ......        }        ......
```

### 5. 代码混淆 <a id="5-dai-ma-hun-xiao"></a>

```text
-keep public class * extends android.app.Service
```

### 6. 配置服务端AppID和**MasterSecrect** <a id="6-pei-zhi-fu-wu-duan-appid-he-mastersecrect"></a>

![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-LvOyMJ6KYe8jItZoem5%2F-LvP-KcX-UAxev01xbOk%2Fimage.png?alt=media&token=654f450d-eb6e-42a3-bf92-faa109f74d86)

MasterSecret在这里找![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-LvOwrPsqj_XMXBfxNb7%2F-LvOxASEAqu9OaB_lWAx%2Fimage.png?alt=media&token=094e0584-091a-458b-9523-996fd23c909a)

### 7. 厂商通道测试方法\(通用\) <a id="7-chang-shang-tong-dao-ce-shi-fang-fa-tong-yong"></a>

1. 将集成好的App（测试版本）安装在一台OPPO测试机上，并且运行App。
2. 保持App在前台运行，尝试扫码测试推送消息。
3. 如果应用收到消息，将App退到后台，并且杀掉所有App进程。
4. 再次进行测试推送消息，如果能够收到推送，则表明厂商通道集成成功。

### 8 兼容性 <a id="8-jian-rong-xing"></a>

如果您的App已经集成了个推VIP或极光VIP版本的推送SDK，我们的Android SDK也能兼容。

为了和个推兼容，我们将厂商通道独立打包。OPPO推送通道为例，我们打包两个SDK：gpush-oppo-adapter和gpush-oppo-sdk。如果是从未接过个推、极光等VIP版本的用户可以直接添加OPPO推送通道依赖。

```text
mplementation 'com.growingio.android.gpush:gpush-oppo-adapter:$ersion'
```

如果是个推、极光等VIP版本的用户可以将OPPO官方SDK包gpush-oppo-sdk 排除出去。

```text
implementation ('com.growingio.android.gpush:gpush-oppo-adapter:$gtouch_version'){      exclude(group: 'com.growingio.android.gpush' , module: 'gpush-oppo-sdk')}
```

​

