# Web 弹窗SDK

## 集成SDK

### 1. CDP 埋点SDK

Web弹窗SDK依赖于Web数据采集SDK，请先根据 Web数据采集SDk

> 注意：web sdk只能识别web弹窗，不识别H5弹窗，想要使用H5弹窗请集成H5 SDK.

### 2. 集成Web弹窗SDK

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

## 浏览器兼容性

### Web浏览器

| IE | Firefox | Chorme | Safari | QQ Browser | 360 | 百度浏览器 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 8、9、10、11 | 全部 | 全部 | 12 | 10.5 | 10 | 8.7 |

{% hint style="info" %}
移动端浏览器弹窗需集成H5弹窗SDK
{% endhint %}





