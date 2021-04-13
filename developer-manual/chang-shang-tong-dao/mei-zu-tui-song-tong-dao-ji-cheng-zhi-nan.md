---
description: 魅族推送通道是由魅族官方提供的系统级推送通道。在魅族手机上，推送消息能够通过魅族的系统通道抵达终端，并且无需打开应用就能够收到推送。
---

# 魅族推送通道集成指南



### 1. 获取魅族推送秘钥 <a id="1-huo-qu-mei-zu-tui-song-mi-yue"></a>

1. 打开[魅族推送官网](https://open.flyme.cn/open-web/views/push.html)​
2. 注册/登录开发者账号。（如果您是新注册账号，进行实名认证大约需要2天左右时间，具体请咨询魅族侧）
3. 在魅族推送平台（[http://push.meizu.com）](http://push.meizu.com/%29/) 中新建应用。注意「应用包名」需跟您在GrowingIO 推送填写的包名保持一致

注：更多详情请参照[魅族开发文档](http://open.res.flyme.cn/fileserver/upload/file/201709/a271468fe23b47408fc2ec1e282f851f.pdf)​

### 2. 在app build.gradle添加魅族通道SDK依赖 <a id="2-zai-app-buildgradle-tian-jia-mei-zu-tong-dao-sdk-yi-lai"></a>

```text
dependencies {    ...    //由于推送底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖    implementation 'com.squareup.okhttp3:okhttp:3.12.1'    //推送SDK依赖    implementation 'com.growingio.android:gtouch:$gtouch_version'    //魅族推送SDK依赖    implementation 'com.growingio.android.gpush:gpush-meizu-adapter:$gtouch_version'}
```

> $gtouch\_version 为最新SDK版本号，现最新的版本号为请参考[SDK更新日志](https://docs.growingio.com/mp/developers/integrations/changelog)。

### 3. 配置AppID和AppKey <a id="3-pei-zhi-appid-he-appkey"></a>

```text
android {        ......        defaultConfig {            manifestPlaceholders = [                PACKAGE_NAME        : "您的APP包名",​                GPUSH_MEIZU_APP_ID  : "魅族推送的AppId",                GPUSH_MEIZU_APP_KEY : "魅族推送的AppKey",            ]            ......        }        ......}
```

### 4. 代码混淆 <a id="4-dai-ma-hun-xiao"></a>

```text
-dontwarn com.meizu.cloud.pushsdk.**​-keep class com.meizu.cloud.pushsdk.**{*;}
```

### 5. 配置服务端AppID和AppSecret <a id="5-pei-zhi-fu-wu-duan-appid-he-appsecret"></a>

![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-LwW7qFJdkpsyPiAUXoG%2F-LwWLG80EBxNYCGOz7JB%2Fimage.png?alt=media&token=e8f2cc58-ba94-4189-8559-9b3602d9db11)

### 6. 设置推送消息回执 <a id="6-she-zhi-tui-song-xiao-xi-hui-zhi"></a>

在魅族推送APP配置界面配置回执，以便于我们GrowingIO更好的统计推送数据![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-LqiImfa22AAr2Os4K3V%2F-Lqi_QykIOBNa0ensh3-%2F7.png?alt=media&token=776acb94-4e8e-4c5b-986d-5eafe762e30b)

其中回执地址：

```text
https://messages.growingio.com/v1/callback/meizu
```

### 7. 厂商通道测试方法\(通用\) <a id="7-chang-shang-tong-dao-ce-shi-fang-fa-tong-yong"></a>

1. 将集成好的App（测试版本）安装在一台魅族测试机上，并且运行App
2. 保持App在前台运行，尝试扫码测试推送消息
3. 如果应用收到消息，将App退到后台，并且杀掉所有App进程
4. 再次进行测试推送消息，如果能够收到推送，则表明厂商通道集成成功

