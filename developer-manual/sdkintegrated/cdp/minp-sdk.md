# 小程序 SDK

## **下载小程序SDK**

下载微信小程序SDK，并解压，下载地址：[https://assets.giocdn.com/sdk/cdp/gio-minp.js](https://assets.giocdn.com/sdk/cdp/gio-minp.js)

将解压后的gio-minp目录放在小程序目录下（比如：/src/utils目录）

```text
var gio = require("./utils/gio-minp.js").default;
```

## **添加数据追踪代码**

请将以下的页面代码放置到小程序App.js首部，即可完成小程序SDK 代码的安装。请注意使用具体的项目 ID 替换代码中的 your projectId ，your dataSourceId，使用具体的小程序Id代替代码中的your appId。

```text
var gio = require("./utils/gio-minp.js").default;
gio('init', 'your projrctId','your datasourceID','your appId', {})；
App({
onLaunch: function () {
},
globalData: {
gio: gio
}
})
```

## **添加请求服务器域名**

要正常采集微信小程序的数据并发送，需要在微信小程序里事先设置一个通讯域名，允许跟 GrowingIO API 服务器进行网络通信。具体步骤如下：

1. 登陆微信小程序后台，进入配置。
2. 打开开发设置，到服务器域名配置部分。
3. 在request合法域名中添加：同init中的host地址。

![](../../../.gitbook/assets/image%20%2891%29.png)

## **数据校验**

在初始化时打开 debug 为true，打开控制台，即可看到实时采集的数据。

```text
gio('init', 'your projectId', 'your dataSourceId', 'your appId',{debug: true});
```

## **配置系统变量**

### **host**

GrowingIO 默认不配置发数的api，需要在初始化时设置 host，否则会初始化失败。

```text
gio('init', 'your projectId','your dataSourceId', 'your appId', {host: 'api.growingio.com'});
```

### **Scheme**

GrowingIO 默认发数时是https，如果您的请求协议为http，可以参考如下设置：

```text
gio('init', 'your projectId','your dataSourceId','your appId',{scheme: 'http'});
```

### **getLocation**

GrowingIO 默认不获取用户的地理位置信息，如果您的小程序在打开时就需要获取用户地理信息，需要在初始化时设置获取用户地理位置信息和位置格式**。**

autoGet：true \| false

type：wgs84 \| gcj02 //gcj02 为火星坐标系

```text
gio('init', 'your projectId','your dataSourceId', 'your appId' , {getLocation: {
autoGet: true,
type: 'wgs84'
}
}
);
```

## **常用API**

### **初始化参数API**

初始化参数，用来设置项目ID和一些常用的配置项。

| 参数名称 | 类型 | 是否必填 | 说明 |
| :--- | :--- | :--- | :--- |
| projectId | string | 是 | 项目ID。 |
| options | JSON Object | 否 | 系统变量配置。 |
| dataSourceId | string | 是 | 数据源ID。 |
| appId | string | 是 | 微信应用ID。 |

```text
//init API原型
gio('init', projectId,dataSourceId,appId,options);
//init API调用示例
//配置发数api为 http://api.test.com
gio('init', '1234567890', 'test','wx112222',{
scheme: 'http',
host: 'api.test.com'
});
```

### **登录用户ID**

当用户登录之后调用setUserId设置登录用户ID；当用户退出登录后调用clearUserId清除已经设置的登录用户ID。

| 参数名称 | 类型 | 是否必填 | 说明 |
| :--- | :--- | :--- | :--- |
| userId | string | 是 | 应用的登录用户ID。 |

```text
//setUserId API原型和调用示例
gio('setUserId', userId);
gio('setUserId', '1234567890');
//clearUserId API原型和调用示例
gio('clearUserId');
```

### **用户变量API**

setPlatformProfile在取得用户授权后，可以获得微信用户的信息，需要在获取用户授权的回调函数中调用。

| 参数名称 | 类型 | 是否必填 | 说明 |
| :--- | :--- | :--- | :--- |
| userAttributes | JSON Object | 是 | 包含用户变量的JSON对象。 |

```text
// setUserAttributes API调用原型和调用示例
gio('setUserAttributes', userAttributes);
gio('setUserAttributes', {name: 'hjh'})
// setPlatformProfile API调用原型和调用示例
gio('setPlatformProfile');
```

### **自定义事件API**

| 参数名称 | 类型 | 是否必填 | 说明 |
| :--- | :--- | :--- | :--- |
| eventId | string | 是 | 事件标识符。 |
| eventLevelVariables | JSON Object | 否 | 事件变量。 |

```text
// track API调用原型
gio(track, eventId);
gio('track', eventId, eventLevelVariables);
// track API调用示例
gio('track','order', {type: 'hjh'})
```

### **GDPR数据采集开关**

GrowingIO 全面支持欧盟《一般数据保护条例》。

```text
// 停止采集数据
gio('setConfig',{"dataCollect": false}); 全局配置, 可以放到send之后
// 采集数据 (默认)
gio('setConfig',{"dataCollect": true});
```

