# H5 弹窗SDK

## 集成SDK

### 1. CDP 埋点SDK

H5弹窗SDK依赖于JS埋点数据采集SDK，请先集成JS埋点数据采集SDK。

> 注意：H5端只能识别H5弹窗，不识别web弹窗。请调试时不要发错弹窗。

### 2. 集成H5弹窗SDK

将以下深色区内的弹窗SDK相关的JS代码复制到您所需分析页面中的`<head>`和`<head>`标签之间, 放置在数据采集SDK集成代码的下方即可。

> **未压缩的代码（供参考）**

```javascript
<script type='text/javascript'>
    // 数据采集SDK
    !function (e, t, n, g, i) { e[i] = e[i] || function () { (e[i].q = e[i].q || []).push(arguments) }, n = t.createElement("script"), tag = t.getElementsByTagName("script")[0], n.async = 1, n.src = g, tag.parentNode.insertBefore(n, tag) }(window, document, "script", "JS数据采集SDK加载地址", "gdp");
    gdp('init', 'your projectId', 'your dataSourceId', {
      debug: true, //默认关闭
      hashtag: true, //默认关闭
      host: '您的埋点数据上报地址',
      scheme: 'http' // 默认https
    });
    
    // 弹窗SDK
    gdp('plugin', {
      id: 'gio_plugin_gtouch',
      src: ('https:' == document.location.protocol ? 'https://' : 'http://') + "JS弹窗SDK加载地址,后缀为xxx/gtouch.js",
      dataHost: '您的弹窗请求地址'
    })
    //custom page code begin here
    //custom page code end here
    gdp('send');
  </script>
```

示例代码

```javascript
 <script type='text/javascript'>
    !function (e, t, n, g, i) { e[i] = e[i] || function () { (e[i].q = e[i].q || []).push(arguments) }, n = t.createElement("script"), tag = t.getElementsByTagName("script")[0], n.async = 1, n.src = g, tag.parentNode.insertBefore(n, tag) }(window, document, "script", "https://assets.giocdn.com/cdp-release/1.0/gio-test.js", "gdp");
    gdp('init', 'a500f222e29e3b0c', '9eda0bb1d74f86e4', {
      // host: 'api.growingio.com',
      host: '117.50.92.65:8080',
      scheme: 'http'
    });
    gdp('plugin', {
      id: 'gio_plugin_gtouch',
      //本demo页面我将文件都发到统一服务器路径了，故使用本地路径，可以改成您服务器对应的IP。
      src: ('https:' == document.location.protocol ? 'https://' : 'http://') + window.location.host + "/push/cdp/gtouch.latest.js",
      dataHost: 'gdp-test.growingio.com'
    })
    //custom page code begin here
    //custom page code end here
    gdp('send');
  </script>
```

### 3. 如何一次集成同时支持web端与h5端

上一步示例代码里的src地址集成的是gtouch.latest.js，但是实际上web弹窗由access.latest.js控制，H5弹窗由h5.latest.js控制。我们的设计思路是把这三个js文件上传到服务器的同一路径下，再由gtouch.latest.js智能根据当前环境加载不同后缀的js文件。这样同一个页面既可以在web端弹窗，也可以在H5端弹窗。

```javascript
//m是sdk加载地址，g表示"是否H5环境",m最终会替换成对应环境的弹窗SDK JS
m = g ? m.replace("gtouch", "h5") : m.replace("gtouch", "access");
```



{% hint style="info" %}
移动端浏览器弹窗需集成H5弹窗SDK
{% endhint %}





