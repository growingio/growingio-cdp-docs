# Web端数据定义

## 圈选准备

GrowingIO 全量采集用户行为数据，你可以通过「圈选」来定义页面，作为数据分析的基础指标。

定义后的页面事件默认回溯过去7天的浏览量。

### Hashtag使用说明

如果您的Web页面URL使用了Hashtag，请在加载SDK进行预先配置，请参考[JS SDK](../../../../developer-manual/sdkintegrated/cdp/js-sdk.md#chu-shi-hua-can-shu-api)。

### 插件下载和安装

下载地址：GIO Web Collection

安装步骤：

第一步: 打开Chrome浏览器后，在导航栏点击 **窗口 &gt; 扩展程序** 进入扩展程序管理页面。

第二步: 点击 **加载已解压的扩展程序**，打开插件解压目录，选择解压文件夹并完成插件安装。

![](../../../../.gitbook/assets/image%20%28367%29.png)

第三步: 在Chrome地址栏右侧点击 **扩展程序** 图标，选择插件将插件固定在导航栏，方便后续使用。

![](../../../../.gitbook/assets/image%20%28368%29.png)

### 插件打开

第一步: 在Chrome中单击右键点击检查，或使用F12唤起检查模式。

第二步: 在检查模式中选择GIO Web Collection插件。

![](../../../../.gitbook/assets/image%20%28366%29.png)

第三步: 输入服务器地址、账号、密码完成注册登陆

![](../../../../.gitbook/assets/image%20%28372%29.png)

{% hint style="success" %}
请向工程师询问服务器地址；账号和密码为GrowingIO平台登陆账号和密码。

登陆成功后默认保存服务器地址和账号。
{% endhint %}

Step 4: 建议设置检查模式在右侧边栏展示。

设置方法：Chrome检查模式右上角点击![](https://docs.growingio.com/.gitbook/assets/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择展示形式。

![](../../../../.gitbook/assets/image%20%28371%29.png)

### URL解读

URL示意：www.xxx.com**/**12345/678/123**?**id=1&ig=2

拆分：域名/路径?查询条件

即：

![](../../../../.gitbook/assets/image%20%28369%29.png)

## 圈选操作

在顶部导航栏选择”数据 &gt; 事件 &gt; 无埋点事件 &gt; 新建无埋点事件**”**，进入Web圈选说明页面。

![](../../../../.gitbook/assets/image%20%28370%29.png)

{% hint style="success" %}
无埋点页面定义：需要在Chrome中打开目标页面，在GIO Web Collection插件中完成页面定义。
{% endhint %}

### 页面定义

在Chrome中打开目标页面，打开插件后开始定义无埋点页面事件。

![](../../../../.gitbook/assets/image%20%28376%29.png)

| 项 | 说明 |
| :--- | :--- |
| 1 | URL地址输入框：输入目标页面URL |
| 2 | 显示登陆账户名 |
| 3 | 退出登陆按钮：点击后退出登陆 |
| 4 | 定义页面按钮：点击后开始页面定义点击 |

点击“**定义页面**“后，进入页面定义流程。

![](../../../../.gitbook/assets/image%20%28375%29.png)

| 项 | 说明 |
| :--- | :--- |
| 1 | \(必填\) 页面名称，请参考“无埋点事件命名规范“ |
| 2 | 页面事件定义业务场景描述 |
| 3 | \(必填\) 域名，点击定义后默认识别当前页面域名，支持使用通配符 \*。 |
| 4 | \(必填\) 路径，点击定义后默认识别当前页面路径，支持使用通配符 \*。 |
| 5 | 路径启用/仅用状态，禁用后定义规则忽略路径变化。默认开启路径识别 |
| 6 | 查询条件，点击定义后默认识别当前页面查询参数，参数值支持使用通配符 \*。 |
| 7 | 添加查询条件，点击后添加新的查询条件定义。 |
| 8 | 查看数据，点击后查看定义规则历史数据趋势。 |

点击保存后，保存定义规则，无埋点页面事件创建成功。

{% hint style="success" %}
无埋点页面事件创建成功后，仅能修改事件名称和描述。
{% endhint %}

## 定义页面案例

### 案例一：定义GrowingIO官网首页页面浏览事件

步骤一：在Chrome中打开 www.growingio.com，进入GrowingIO官网首页。

步骤二：点击“**定义页面**“按钮，进入页面定义流程。

![](../../../../.gitbook/assets/image%20%28378%29.png)

步骤三：输入页面名称“页面\_官网首页"，输入描述"GrowingIO官网首页"，点击保存完成页面定义。

### 案例二：定义GrowingIO官网下所有页面

步骤一：在Chrome中打开 www.growingio.com，进入GrowingIO官网首页。

步骤二：点击“**定义页面**“按钮，进入页面定义流程。

步骤三：禁用路径匹配按钮

![](../../../../.gitbook/assets/image%20%28381%29.png)

{% hint style="success" %}
此时定义的页面是 www.growingio.com 域名下的全部页面
{% endhint %}

步骤四：输入页面名称“页面\_官网\(全部页面\)"，输入描述"GrowingIO官网下全部页面"，点击保存完成页面定义。

### 案例三：定义GrowingIO官网行业解决方案详情页

![](../../../../.gitbook/assets/image%20%28379%29.png)

步骤一：在Chrome中打开 www.growingio.com/solutions/retail-ecommerce，进入GrowingIO官网电商行业解决方案详情页

步骤二：点击“**定义页面**“按钮，进入页面定义流程。

![](../../../../.gitbook/assets/image%20%28374%29.png)

步骤三：修改路径规则为 /solutions/\*。

该规则的含义为路径规则为以 /solutions/ 开头，后续包含任意字符的路径。

> 电商行业解决方案页面：www.growingio.com/solutions/retail-ecommerce
>
> 保险行业解决方案页面：www.growingio.com/solutions/insurance
>
> 运营商行业解决方案页面：www.growingio.com/solutions/telecom-carrier
>
> 在线旅游行业解决方案页面：www.growingio.com/solutions/online-travel
>
> 企业服务行业解决方案页面：www.growingio.com/solutions/saas

步骤四：输入页面名称“页面\_解决方案详情页"，输入描述"GrowingIO官网下全部解决方案详情页“，点击保存完成页面定义。

### 案例四：定义从百度渠道访问的GrowingIO官网的全部页面

步骤一：在Chrome中打开 www.growingio.com，进入GrowingIO官网。

步骤二：点击“**定义页面**“按钮，进入页面定义流程。

步骤三：禁用路径匹配按钮；添加查询条件，输入参数为utm\_source，参数值为baidu。

步骤四：输入页面名称“页面\_官网\(baidu来源\)"，输入描述"通过baidu搜索访问GrowingIO的全部页面“，点击保存完成页面定义。

## 常见问题

### 1.定义查询参数的计算规则是什么？

定义查询参数后，计算规则为包含该查询参数的全部页面。

举例：

![](../../../../.gitbook/assets/image%20%28373%29.png)

该规则定义的页面是，域名为 www.growingio.com，不限制路径，查询参数包含 utm\_source 且参数值为 baidu 的全部页面。

因此该页面规则包含页面 www.growingio.com/cdp?utm\_source=baidu&keyword=growingio

不包含页面 www.growingio.com/product?keyword=growingio

### 2.为什么查询参数值与URL输入框中不一致？

在Chrome中打开页面 www.growingio.com?city=%e5%8c%97%e4%ba%ac 后，我们可以在URL输入框看到页面路径为 www.growingio.com?city=北京。

此时“定义页面“后，我们可以看到插件中识别的路径规则为

![](../../../../.gitbook/assets/image%20%28377%29.png)

此时插件中识别的查询参数与URL输入框中参数不一致。

原因是浏览器展示时，URL输入框会默认将中文进行解码\( 即“%e5%8c%97%e4%ba%ac“解码后为“北京“ \)，但SDK实际采集上报数据仍为编码路径数据\( 即%e5%8c%97%e4%ba%ac \)。

为保证页面定义规则与采集数据一致，插件识别域名、路径、查询条件时默认不做解码处理，仍保持原始路径格式。

