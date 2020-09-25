# Web端数据定义

## 圈选准备

GrowingIO 全量采集用户行为数据，你可以通过「圈选」来定义页面，作为数据分析的基础指标。

定义后的页面事件默认回溯过去7天的浏览量。

### Hashtag使用说明：

如果您的Web页面URL使用了Hashtag，请在加载SDK进行预先配置，请参考[JS SDK](../../../../developer-manual/sdkintegrated/cdp/js-sdk.md#chu-shi-hua-can-shu-api)。

### 插件下载和安装：

下载地址：GIO Web Collection

安装步骤：

Step 1: 打开Chrome浏览器后，在导航栏点击 **窗口 &gt; 扩展程序** 进入扩展程序管理页面。

Step 2: 点击 **加载已解压的扩展程序**，打开插件解压目录，选择解压文件夹并完成插件安装。

![](../../../../.gitbook/assets/image%20%28367%29.png)

Step 3: 在Chrome地址栏右侧点击 **扩展程序** 图标，选择插件将插件固定在导航栏，方便后续使用。

![](../../../../.gitbook/assets/image%20%28368%29.png)

### 插件打开：

Step 1: 在Chrome中单击右键点击检查，或使用F12唤起检查模式。

Step 2: 在检查模式中选择GIO Web Collection插件。

![](../../../../.gitbook/assets/image%20%28366%29.png)

Step 3: 输入服务器地址、账号、密码完成注册登陆

![](../../../../.gitbook/assets/image%20%28371%29.png)

{% hint style="success" %}
请向工程师询问服务器地址；账号和密码为GrowingIO平台登陆账号和密码。

登陆成功后默认保存服务器地址和账号。
{% endhint %}

Step 4: 建议设置检查模式在右侧边栏展示。

设置方法：Chrome检查模式右上角点击![](https://docs.growingio.com/.gitbook/assets/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择展示形式。

![](../../../../.gitbook/assets/image%20%28370%29.png)

### URL解读：

URL示意：www.xxx.com**/**12345/678/123**?**id=1&ig=2

拆分：域名/路径?查询条件

即：

![](../../../../.gitbook/assets/image%20%28369%29.png)

## 圈选操作

在顶部导航栏选择“**数据中心 &gt; 无埋点事件定义（圈选） &gt; 您的Web应用”**，进入Web圈选模式。

















