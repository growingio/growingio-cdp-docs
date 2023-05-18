---
id: acquisition-configuration
sidebar_position: 3
---

# 产品配置

获客分析产品配置可对推广渠道、推广活动进行管理配置，同时支持应用层级的归因配置。

## 推广渠道

可统一管理系统预置的公有渠道和客户自主创建的私有渠道，同时可对支持回传的渠道进行回传事件配置，对需要进行授权的渠道进行账号授权。

![图 1](/img/pic_tracking_channel_acquisition-configuration.png)

点击右侧操作按钮可对私有渠道进行修改、删除等操作。公有渠道不支持修改与删除。
对支持回传事件及授权的渠道，点击右侧操作按钮可新建回传事件及账号授权操作：

![图 2](/img/pic_callback_acquisition-configuration.png)

![图 3](/img/pic_callback_create_acquisition-configuration.png)

### 渠道信息

单击列表中的单条渠道，右侧将展开当前渠道的信息视图。

![picture 14](/img/43c0d873e48cdfcb2d0fff47235c151f189d9cc183e0a732ccbe70eb396f598b_pic_1668086793636_2022-11-10.png)

### 新建渠道

点击页面右侧的【新建渠道】可创建渠道列表页中没有的待投放渠道，方便识别渠道来源。

![picture 15](/img/ebb732b6236146478b2ec02333af91dbe9e81ba220f733b9b32a2433c3889cad_pic_1668086825963_2022-11-10.png)

## 广告活动

在广告监测下创建的监测链接时创建的活动都会在此统一管理，也可以在此处直接创建好活动，在创建链接的时候直接选取；利用搜索功能快速查找相应的活动。

![图 6](/img/pic_campaign_acquisition-configuration.png)

### 新建活动

点击页面右侧的【新建活动】可创建新的广告活动，还可以点击操作列的更多删除活动。

![picture 17](/img/7991f4df31d8d72f5f1ff76e20e63a9d96e8f24cea495986a4785b99c0df0b94_pic_1668086940341_2022-11-10.png)

## 深度链接配置

深度链接（DeepLink）是通过链接启动应用的方法。更详细地说是通过映射预定义行为到唯一的链接上，让用户通过点击链接无缝跳转到特定的内容页面。
对于支持深度链接功能的移动应用，用户可以在其他处点击应用提供的深度打开应用，也可跳转到应用内指定页面，如首页、产品详情页面等。

### 1 进入深度链接配置模块

在顶部导航栏选择“获客分析 > 产品配置 > 深度链接配置 ”，进入深度链接配置页面。

![图 9](/img/pic_1677213305248_acquisition-configuration.png)

### 2 iOS 应用配置

找到需要配置的 iOS 应用，查看当前应用的配置。其中将包含所有当前应用的全部 DeepLink 配置信息。

2.1 查看应用基本信息

包含当前应用的基本信息配置，如需修改基本信息数据，如应用 logo、应用描述等，请前往[数据中心-数据源管理]进行修改。

![图 10](/img/pic_1677213393453_acquisition-configuration.png)

2.2 Universal Links 配置

Universal Links 是 Apple 在 iOS 系统中提供的原生方案，如果您希望在 DeepLink 流程中达成更好的跳转体验，需对此进行配置。

而 UniversalLink 跳转方式可以实现无缝跳转，当浏览器识别到预先指定好的 URL，就可以直接唤醒 App，不需要在浏览器中打开再去点击其他按钮。

⭐️ Universal Links 适用于 iOS 9 及以上的版本，当用户设备系统版本在 iOS 9 以下时，DeepLink 将会自动回落至 URL Scheme 方案进行跳转。

2.2.1 获取 Team ID

Step 1：在 Xcode 中勾选 Associated Domains 功能

![图 11](/img/pic_1677213465856_acquisition-configuration.png)

Step 2：添加 GrowingIO 域名到 Xcode.

![图 12](/img/pic_1677213500911_acquisition-configuration.png)

具体域名请与运维服务人员沟通

Step 3：在苹果开发者网站中找到 Team ID 与 Bundle ID，如下图。

![图 13](/img/pic_1677213539979_acquisition-configuration.png)

2.2.2 将 Team ID 配置到 GrowingIO 后台

Step1：在应用列表页，点击应用更多信息按钮后，在展开页面点击模块右上角的“编辑”，进入配置 UniversalLink 界面。

![图 14](/img/pic_1677213604124_acquisition-configuration.png)  
![图 15](/img/pic_1677213642618_acquisition-configuration.png)

配置获取到的 Team ID 并勾选“我已完成 Xcode 配置，允许 Universal Link 跳转”并进行保存。

### 3 Android 应用配置

找到需要配置的 Android 应用，查看当前应用的配置。其中将包含所有当前应用的全部 DeepLink 配置信息。

3.1 查看应用基本信息
包含当前应用的基本信息配置，如需修改基本信息数据，如应用 logo、应用描述等，请前往[数据中心-数据源管理]进行修改。

![图 16](/img/pic_1677213680450_acquisition-configuration.png)

3.2 AppLinks 配置
App Links 是 Google 在 Android 系统中提供的原生方案，如果您希望在 DeepLink 流程中达成更好的跳转体验，需对此进行配置。App Links 适用于 Android 6.0 及以上的版本，当用户设备系统版本在 Android 6.0 以下时，DeepLink 将会自动回落至 URL Scheme 方案进行跳转。

Step1 ：在应用列表页，点击应用更多信息按钮后，在展开页面点击模块右上角的“编辑”，进入配置 APP Links 界面。

![图 17](/img/pic_1677213742406_acquisition-configuration.png)
![图 18](/img/pic_1677213780270_acquisition-configuration.png)

Step 2：获取应用签名 SHA256 指纹证书

● 使用命令行进入你的证书目录，一般签名分为 debug keystore 和 release keystore ，开发期间建议先配置为 debug keystore ，上线前一定要更新为 release keystore 。如果担心忘记，建议新建数据源集成应用。

● 执行以下命令 ：

keytool -list -v -keystore my-release-key.keystore

● 执行后你将看到类似下面这样的结果，请复制下来并填写进 GrowingIO 对应的应用配置中。

![图 19](/img/pic_1677213839539_acquisition-configuration.png)

Step 3：在 Manifest.xml 中配置 Intent Filter

● 点击「复制代码片段」

● 进入您的安卓应用源码中的 manifest.xml 文件中，找到您的主页面，建议复制在主页，即为 Launcher Activity 中。

● 复制完成后，您的 manifest.xml 文件将类似这样：

```xml
  <activity
            android:name=".LauncherActivity"
            android:launchMode="singleTop"
            android:theme="@style/AppTheme">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
​
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
​
            <!-- GIO 集成配置，使用圈选和 Debugger 等功能用作唤醒 APP-->
            <intent-filter>
                <data android:scheme="growing.xxxxxxxxxxxxxx" />
​
                <action android:name="android.intent.action.VIEW" />
​
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
            </intent-filter>
​
            <!-- GIO APPLinks 配置，广告监测用途，APP 用户点击广告监测短链直接跳转 APP-->
            <intent-filter android:autoVerify="true">
                <action android:name="android.intent.action.VIEW" />
​
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />

                <data
                    android:host="n.datayi.cn"
                    android:pathPattern="/xxxxx.*"
                    android:scheme="https" />
                <data
                    android:host="n.datayi.cn"
                    android:pathPattern="/xxx.*xx.*"
                    android:scheme="https" />
                <data
                    android:host="n.datayi.cn"
                    android:pathPattern="/xxx.*xx.*"
                    android:scheme="https" />
            </intent-filter>
​
        </activity>
```

Step 4：验证您的 App Links

● 完成上述配置后，安装在手机上

● 执行以下命令：

adb shell dumpsys package d

● 上述命令执行后的结果中，查找您应用的包名，当 Domains 已经出现 n.datayi.cn 说明您的 Intent Filter 配置正确，示例如下：

> Package: com.growingio.android.test
> Domains: n.datayi.cn
> Status: always

Step 5：测试 App Links 唤起方式

当您 App Links 所有的环节已经配置完成后，可以利用测试设备测试唤起效果，测试步骤如下：

● 创建一条用于测试的 DeepLink ；

● 在测试设备中原生场景下进行测试，如：短信、备忘录等等；
（不要直接在第三方软件中进行测试，例如微信。第三方软件通常对 DeepLink 跳转存在限制）

● 点击测试 DeepLink，如果可以直接跳转到 App 中，说明可以直接唤起 App，为最理想流程。

● 如果未直接跳转到 App 中，而是跳入下载引导中间页，并且系统弹窗询问是否要在应用中打开，此时可以在上一步的 Status 中查看状态，如果状态显示为“ask”，并且确认 App Links 集成流程正确无误，则可能是当前测试设备机型在 AppLinks 遇到校验问题。

● 对于该情况请参考下方常见问题说明如下：

对于 Status 状态的说明

![图 20](/img/pic_1677215561627_acquisition-configuration.png)

为什么在验证环节得到的 Status 为 ask？

AppLinks 的合法性是由系统校验，不同的手机系统使用不同的校验组件，即使是一个厂商的不同型号手机都可能使用不同的校验组件。
如果系统使用 com.android.statementservice 进行 AppLinks 的校验，在网络正常的情况下基本都能顺利通过， 如果系统使用 com.google.android.gms 组件校验，在手机能够科学上网的情况，也就是能够正常访问 Google 时，校验才能通过。常见华为 mate 系列、P 系列使用的都是 gms，也就是 Status 会为 ask。

查看自己手机是使用哪种组件，在命令行中输入以下命令：

adb shell dumpsys package i

综上，Applink 不能顺利通过系统检验，原因有以下可能：

● 可能是国内网络问题，使用 gms 组件校验的手机需要联通 Google 服务

● 可能是您产品配置问题，GIO 填写的签名和手机上运行的 APP 签名不同

Status 状态为 ask 不代表唤起流程有问题，当用户操作允许后，后续唤起流程中将直接唤起，不会再出现询问弹窗。

Step 6： 在 Callback 中接收自定义参数并跳转页面

在上文中，建议各位开发者将 GIO Intent Filter 代码块配置在 Launcher Activity 下，在用户点击短链后打开 App ，系统将自动跳转到 Launcher Activity ，此时 GIO DeepLink Callback 则会返回您在 GIO 官网广告监测中配置的自定义参数，此时您需要接收您的自定义参数，跳转到指定页面。

详见 SDK 集成文档中 Android DeepLink CallBack 接收参数文档。

3.3 配置应用宝微下载

GrowingIO 提供跳转到应用宝微下载的功能，应用宝微下载为腾讯应用宝体系下的微下载链接。使用应用宝微下载，在微信等腾讯旗下软件中将转至微下载逻辑。

腾讯微下载介绍：[腾讯开放平台微下载介绍文档](https://wikinew.open.qq.com/?title=mobile/%E5%BA%94%E7%94%A8%E5%AE%9D%E5%BE%AE%E4%B8%8B%E8%BD%BD#/iwiki/870029633)

Step 1：在应用列表页，点击应用更多信息按钮后，在展开页面点击应用宝微下载右上角的“编辑”，进入配置界面。

![图 21](/img/pic_1677215678363_acquisition-configuration.png)

Step 2：进行应用宝微下载配置并勾选开启应用宝微下载后进行保存操作。

![图 22](/img/pic_1677215713364_acquisition-configuration.png)

在确认开启应用宝微下载前，请确认您已经达到腾讯微下载服务的量级标准，并且审核通过，否则直接开启将导致用户使用体验下降。

4 引导中间页配置

当您认为 GrowingIO 提供的默认下载引导页风格无法满足您的需求时，可以对 DeepLink 中的下载引导页面进行定制，使其更符合您产品与品牌的风格。

Step 1：在应用列表页，点击应用更多信息按钮后，在展开页面点击下载引导中间页右上角的“编辑”，进入配置界面。

![图 23](/img/pic_1677215749468_acquisition-configuration.png)

![图 24](/img/pic_1677215779132_acquisition-configuration.png)

Step 2：根据提供的两种样式对下载引导中间页进行定制，样式分别是简易布局和自由布局。

简易布局

在默认页面风格中对页面元素进行简单调整，如替换背景图片，对按钮颜色进行更换等。

自由布局

在此布局中，页面将只保留必要的操作按钮在页面底部，其余空间全部开放，您可以通过对背景图的自由设计，来实现任何您想要的关键元素或页面风格设计。
