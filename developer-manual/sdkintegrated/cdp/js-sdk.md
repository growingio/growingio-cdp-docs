# JS SDK

> **加载JS SDK的Web应用所需要满足的浏览器环境：**
>
> IE5以上的IE浏览器、360浏览器、谷歌浏览器、搜狗浏览器、火狐浏览器、QQ浏览器、Safari浏览器、Maxthon、Mobile端浏览器，并且全面支持H5，覆盖市面上的主流浏览器。

## **添加初始化代码**

请将以下的页面代码放置需要分析页面中的&lt;head&gt;和&lt;head&gt;标签之间，即可完成JS SDK页面代码的添加。

> 请注意使用具体的项目ID替换代码中的 your projectId、your DataSourceId 确保JS资源地址正确。

```javascript
<!-- GrowingIO Analytics code version 1.0 -->
<!-- Copyright 2015-2020 GrowingIO, Inc. More info available at http://www.growingio.com -->
<script type='text/javascript'>
!function(e,t,n,g,i){e[i]=e[i]||function(){(e[i].q=e[i].q||[]).push(arguments)},n=t.createElement("script"),tag=t.getElementsByTagName("script")[0],n.async=1,n.src=g,tag.parentNode.insertBefore(n,tag)}(window,document,"script","JS 资源地址","gdp");
  gdp('init', 'your projectId', 'your dataSourceId', {});
​
  //custom page code begin here
  //custom page code end here
  gdp('send');
</script>
<!-- End GrowingIO Analytics code version: 1.0 -->
```

> 常见的初始化失败情况：
>
> 1. 初始化需要设置host，不设置会失败。
> 2. 初始化必须填写projectId、datasourceId，否则会失败。
> 3. 不支持file协议、localhost、127.0.0.1

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

GrowingIO默认发数请求协议是HTTPS，如果您的请求协议为HTTP，可以参考如下设置进行修改。

```javascript
gdp('init', 'your projectId','your dataSourceId', {scheme: 'http'});
```

## **JS SDK API**

### **初始化参数API**

初始化参数，用来设置项目ID和一些商用的配置项。

```javascript
//init API原型
gdp('init', projectId,dataSourceId,options);
```

| 参数名称 | 类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| projectId | string | 是 | 项目ID。 |
| options | JSON Object | 否 | 重要配置项。 |
| dataSourceId | string | 是 | 数据源ID。 |

代码示例：

```javascript
//init API调用示例
//配置发数api为 http://api.test.com
gdp('init', '1234567890', 'test',{
  scheme: 'http',
  host: 'api.test.com'
});
```

### **设置登录用户ID**

当用户登录之后调用setUserId，上传登录用户ID。

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

```text
// 停止采集数据
gdp('config',{"dataCollect": false}); 全局配置, 可以放到send之后
// 采集数据 (默认)
gdp('config',{"dataCollect": tr
```

\*\*\*\*

