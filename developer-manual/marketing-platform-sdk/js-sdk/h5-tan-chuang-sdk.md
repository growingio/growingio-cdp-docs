---
id: mp-js-sdk-popup-h5
sidebar_position: 1
---

# H5 弹窗 SDK

## 集成 SDK[](#ji-cheng-sdk)

### 集成数据采集 SDK[](#1-ji-cheng-shu-ju-cai-ji-sdk)

JS 弹窗 SDK 依赖于数据数据采集 SDK，如已集成请跳过

参考 [Web JS SDK](https://growingio.github.io/growingio-sdk-docs/docs/webjs/base/getting_started)​

H5 弹窗 SDK 只能识别移动端 H5 弹窗，不识别 PC 端 Web 弹窗。如果您需要使用PC 端 Web 弹窗，请参考 [Web 弹窗 SDK](/docs/developer-manual/marketing-platform-sdk/js-sdk/mp-js-sdk-popup-web)。如果您的站点自适应 PC 和移动端，请您参考 [Web/H5 自适应弹窗 SDK](/docs/developer-manual/marketing-platform-sdk/js-sdk/mp-js-sdk-popup-web-h5-autofix)。


### 集成 H5 弹窗 JS SDK[](#2-ji-cheng-h5-dan-chuang-js-sdk)

**JS 文件下载地址:**

H5 弹窗 JS SDK：[https://assets.giocdn.com/sdk/cdp/marketing/h5.latest.js](https://assets.giocdn.com/sdk/cdp/marketing/h5.latest.js)​

**SDK 集成方式**

按照以下要求，在数据采集 SDK 集成代码下方添加弹窗 SDK 集成代码

```js
<script type='text/javascript'>

 // 弹窗 SDK 必须与数据采集 SDK 配合才能正常工作

 // 请参考帮助文档「开发者文档 > SDK 集成 > JS SDK」完成数据数据采集 SDK 集成

 // 弹窗 SDK

 gdp('plugin',  {

 id:  'gio_plugin_gtouch-inject',

 src: document.location.protocol +  "//assets.giocdn.com/sdk/cdp/marketing/h5.latest.js",

 dataHost:  '您的弹窗请求地址'

 })

 //custom page code begin here

 //custom page code end here

 gdp('send');

</script>
```

示例代码

以下代码中的配置信息都是示例用的，请不要直接复制使用。

```js
 <script type='text/javascript'>

 // 数据采集 SDK 

 !function  (e, t, n, g, i)  { e[i]  = e[i]  ||  function  ()  {  (e[i].q = e[i].q ||  []).push(arguments)  }, n = t.createElement("script"), tag = t.getElementsByTagName("script")[0], n.async  =  1, n.src = g, tag.parentNode.insertBefore(n, tag)  }(window, document,  "script",  "https://assets.giocdn.com/cdp/gio.js",  "gdp");

 gdp('init',  'a500f222e29e3b0c',  '9eda0bb1d74f86e4',  {

 host:  'gdp-test-api.growingio.com',

 scheme:  'http'

 });

 // 弹窗 SDK

 gdp('plugin',  {

 id:  'gio_plugin_gtouch',

 src: document.location.protocol +  "//assets.giocdn.com/sdk/cdp/marketing/h5.latest.js",

 dataHost:  'gdp-test.growingio.com'

 });

​

 gdp('send');

 </script>
```


### 测试弹窗[](#3-ce-shi-dan-chuang)

集成 SDK 后请务必创建一个「 H5 应用」弹窗进行测试，以保证 SDK 正确集成，弹窗创建方法请参考 [创建弹窗](/docs/product-manual/marketing-platform/user-operation/popup/create-popup)。
