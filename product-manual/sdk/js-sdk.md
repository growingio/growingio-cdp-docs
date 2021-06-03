# JS SDK

{% hint style="success" %}
3.0 SDK适用于 Web JS、H5 和 Hybrid
{% endhint %}

> **加载JS SDK的Web应用所需要满足的浏览器环境：**
>
> IE5以上的IE浏览器、360浏览器、谷歌浏览器、搜狗浏览器、火狐浏览器、QQ浏览器、Safari浏览器、Maxthon、Mobile端浏览器，并且全面支持H5，覆盖市面上的主流浏览器。

## **添加初始化代码**

请将以下的页面代码放置需要分析页面中的&lt;head&gt;和&lt;head&gt;标签之间，即可完成JS SDK页面代码的添加。

> 请注意使用具体的项目ID替换代码中的 your projectId、your DataSourceId 确保JS资源地址正确。
>
> JS文件地址：[https://assets.giocdn.com/sdk/cdp/gio.js](https://assets.giocdn.com/sdk/cdp/gio.js)

```javascript
<!-- GrowingIO Analytics code version 3.0 -->
<!-- Copyright 2015-2021 GrowingIO, Inc. More info available at http://www.growingio.com -->
<script type='text/javascript'>
//配置后file协议才能产生事件，默认值false。该配置在3.2.0版本起生效
window._gr_ignore_local_rule = true

!function(e,t,n,g,i){e[i]=e[i]||function(){(e[i].q=e[i].q||[]).push(arguments)},n=t.createElement("script"),tag=t.getElementsByTagName("script")[0],n.async=1,n.src=g,tag.parentNode.insertBefore(n,tag)}(window,document,"script","JS 资源地址","gdp");
  gdp('init', 'your projectId', 'your dataSourceId', { host: 'your apiServerHost' });
​
  //custom page code begin here
  //custom page code end here
  gdp('send');
</script>
<!-- End GrowingIO Analytics code version: 3.0 -->
```

> 常见的初始化失败情况：
>
> 1. 初始化需要设置host，不设置会失败。
> 2. 初始化必须填写projectId、datasourceId，否则会失败。
> 3. 不支持file协议（3.2.0版本起支持）、localhost、127.0.0.1

## **JS SDK API**

### **初始化参数API**

初始化参数，用来设置项目ID和一些商用的配置项。

```javascript
//init API原型
gdp('init', projectId, dataSourceId, options);
```

| 参数名称 | 类型 | 是否必须 | 说明 |  |
| :--- | :--- | :--- | :--- | :--- |
| projectId | string | 是 | 项目ID |  |
| dataSourceId | string | 是 | 数据源ID |  |
| options | JSON Object | 是 | 重要配置项，至少需要配置 host |  |

**options 说明**

| 配置项 | 类型 | 是否必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| host | string | 是 | 无 | SDK 上报数据的服务器地址，如 api.test.com，该值必须设置。 |
| scheme | string | 否 | https | SDK 上报数据的服务器的协议类型，只能是 https 或 http。 |
| debug | boolean | 否 | false | 是否开启 Debug 模式。开启后 SDK 上报的数据会在开发者工具 console 中打印。**仅测试时设置为 true**。 |
| hashtag | boolean | 否 | false | 是否支持 hashtag。开启后 SDK 采集时 path 中将包含 hashtag，一些使用 hashtag 作为前端页面路由的单页应用，可以使用此开关，区分不同的页面。例如https://www.growingio.com/index.html\#hash-tag-name 页面，hashtag=true 时采集的 path 会是 /index.html\#hash-tag-name，hashtag=false 时，采集的 path 会是 /index.html。 |
| dataCollect | boolean | 否 | true | 是否采集数据。关闭后 SDK 将不再采集数据。 |
| appVer | string | 否 | undefined | 设置网站应用的版本。 |
| compress | boolean | 否 | fasle | 是否开启数据压缩。开启后 SDK 上报数据会经过压缩，无法通过抓包工具直接看到明文。v0.6.0 版本新增，**需要配合新版 collector 服务使用，如果您不确定您的服务是否支持，请联技术支持**。修改后请一定现在测试环境测试数据接收无问题。 |

**代码示例**

```javascript
//init API调用示例
//配置发数api为 http://api.test.com
gdp('init', 'project-id', 'data-source-id',{
  scheme: 'http', // api 服务协议头
  host: 'api.test.com' // api 服务地址
});
```

## 重要配置

### **开启debug模式**

在初始化时设置debug模式为true，打开浏览器控制台，即可看到实时采集的数据。

> IE 9以下不支持。

```javascript
gdp('init', 'your projectId', 'your dataSourceId', {debug: true});
```

### **开启识别hashtag**

GrowingIO 默认不会把hashtag识别成页面URL的一部分。对于使用hashtag 进行页面转跳的单页面网站应用来说，可以启用hashtag 作为标识页面的一部分。

```javascript
gdp('init', 'your projectId', 'your dataSourceId', {hashtag: true});
```

### **设置host**

设置上传当前应用埋点数据的接受服务器的域名。

GrowingIO默认不配置发数的API，需要在初始化时设置host，否则会初始化失败。

```javascript
gdp('init', 'your projectId', 'your dataSourceId',{host: 'api.growingio.com'});
```

### **设置请求协议**

GrowingIO 默认发数请求协议是 HTTPS，如果您的请求协议为 HTTP，可以参考如下设置进行修改。

```javascript
gdp('init', 'your projectId','your dataSourceId', {scheme: 'http'});
```

### 设置 appVer

如果网站在不停升级版本，同时想了解不同版本的数据情况，可以参考如下代码设置应用版本。在实际使用中应用版本对移动端 app 更有价值。

```javascript
gdp('init', 'your projectId','your dataSourceId', {appVer: 'v1.2.3'});
```

### 开启数据压缩

GrowingIO Web SDK 默认发送数据是明文，可以通过这个开关将数据压缩，一方面保证数据不能被直接查看，增强了数据的安全性。另一方面可以节省用户的流量。可以通过下面方式开启数据压缩传输。

```javascript
gdp('init', 'your projectId','your dataSourceId', {compress: true});
```

{% hint style="danger" %}
数据压缩是在 SDK 0.6.0 版本新增，需要同步升级数据收集服务，否则数据将无法正常采集。如果您不确定您的服务是否支持，请联技术支持。并且务必在修改配置后测试数据采集功能正常。
{% endhint %}

### **设置登录用户ID**

当用户登录之后调用 setUserId，上传登录用户ID。

```javascript
//setUserId API原型
gdp('setUserId', userId);
```

| 参数名称 | 类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| userId | string | 是 | 应用的登录用户ID。 |

代码示例：

```javascript
//setuserId API调用示例
gdp('setUserId', '1234567890');
```

### **清除登录用户ID**

当用户退出登录后，调用clearUserId，清除已经设置的登录用户ID。

```javascript
//clearUserId API原型和调用示例
gdp('clearUserId');
```

### **设置访问用户ID**

```javascript
// 获取访问用户ID 
gdp('getVisitorId');
```

### **设置用户属性**

```javascript
// setUserAttributes API调用原型
gdp('setUserAttributes', userAttributes);
```

### **自定义数据上传**

```javascript
// track API调用原型
gdp(track, eventId);
// 事件属性上传
gdp('track', eventId, eventLevelVariables);
// 物品模型上传
gdp('track', eventId, eventLevelVariables, item);
```

| 参数名称 | 类型 | 是否必填 | 说明 |
| :--- | :--- | :--- | :--- |
| eventId | string | 是 | 事件标识符。 |
| eventLevelVariable | JSON Object | 否 | 事件变量。 |
| item | JSON Object | 否 | 物品模型。 |

```javascript
// track API调用示例 - 事件属性
gdp('track','order', {type: 'hjh'})
// track API调用示例 - 物品模型
gdp('track','testEvent',{},{key:'order_id',id:'123456'})
// key为物品模型唯一标识属性
```

## **GDPR**

GrowingIO 全面支持欧盟《一般数据保护条例》。

```javascript
// 停止采集数据
gdp('config',{"dataCollect": false}); 全局配置, 可以放到send之后
// 采集数据 (默认)
gdp('config',{"dataCollect": true});
```

