# Web/H5 自适应弹窗 SDK

## 集成 SDK

### 1. 集成数据采集 SDK

JS 弹窗 SDK 依赖于数据数据采集 SDK，如果还没有集成，请先集成 [数据采集 SDK](../../cdp/js-sdk.md)。

### 2. 集成弹窗 JS SDK

{% hint style="danger" %}
如果你的站点只在移动端使用，可以使用 [H5 弹窗 SDK ](h5-tan-chuang-sdk.md)，如果您的站点只在 PC 端使用，可以使用 [Web 弹窗 SDK](web-tan-chuang-sdk.md)。
{% endhint %}

**JS 文件下载地址:**

弹窗 JS SDK：[https://assets.giocdn.com/sdk/cdp/marketing/gtouch.latest.js](https://assets.giocdn.com/sdk/cdp/marketing/gtouch.latest.js)

**SDK 集成方式**

按照以下要求，在数据采集 SDK 集成代码下方添加弹窗 SDK 集成代码

```javascript
<script type='text/javascript'>
    // 弹窗 SDK 必须与数据采集 SDK 配合才能正常工作
    // 请参考帮助文档「开发者文档 > SDK 集成 > JS SDK」完成数据数据采集 SDK 集成
    
    // 弹窗 SDK
    gdp('plugin', {
      id: 'gio_plugin_gtouch',
      src: document.location.protocol + '/assets.giocdn.com/sdk/cdp/marketing/gtouch.latest.js',
      dataHost: '您的弹窗请求地址'
    })
    //custom page code begin here
    //custom page code end here
    gdp('send');
</script>
```

**示例代码**

{% hint style="danger" %}
以下代码中的配置信息都是示例用的，请不要直接复制使用。
{% endhint %}

```javascript
 <script type='text/javascript'>
    // 数据采集 SDK 
    !function (e, t, n, g, i) { e[i] = e[i] || function () { (e[i].q = e[i].q || []).push(arguments) }, n = t.createElement("script"), tag = t.getElementsByTagName("script")[0], n.async = 1, n.src = g, tag.parentNode.insertBefore(n, tag) }(window, document, "script", "https://assets.giocdn.com/cdp/gio.js", "gdp");
    gdp('init', 'a500f222e29e3b0c', '9eda0bb1d74f86e4', {
      host: 'gdp-test-api.growingio.com',
      scheme: 'http'
    });
    // 弹窗 SDK
    gdp('plugin', {
      id: 'gio_plugin_gtouch',
      src: document.location.protocol + "//assets.giocdn.com/sdk/cdp/marketing/gtouch.latest.js",
      dataHost: 'gdp-test.growingio.com'
    });

    gdp('send');
  </script>
```

### 3. 测试弹窗

集成 SDK 后请务必创建分别创建一个 「 网页」弹窗和「 H5 应用」 弹窗进行测试，以保证 SDK 正确集成，弹窗创建方法请参考[ 创建弹窗](../../../../product-manual/mp/popup/create.md)。

### 4.  自适配 SDK 工作原理

自动适应弹窗主要的工作原理如下，其会自动探测浏览器环境，判断是 PC 端还是移动端，根据当前环境加载移动端 H5 或 PC 端  Web  SDK。代码示例如下：

```javascript
//gtouch.latest.js源码分析
//m是sdk加载地址，g表示"是否H5环境",m最终会替换成对应环境的弹窗SDK JS
m = g ? m.replace("gtouch", "h5") : m.replace("gtouch", "access");
```

所以，如果您选择了在自己的服务器或 CDN 托管弹窗 SDK 代码，请务必保证以下三个文件在同一个目录下。

* Web 弹窗 JS SDK： [https://assets.giocdn.com/sdk/cdp/marketing/access.latest.js](https://assets.giocdn.com/sdk/cdp/marketing/access.latest.js)
* H5 弹窗 JS SDK：[https://assets.giocdn.com/sdk/cdp/marketing/h5.latest.js](https://assets.giocdn.com/sdk/cdp/marketing/h5.latest.js)
* 弹窗 JS SDK：[https://assets.giocdn.com/sdk/cdp/marketing/gtouch.latest.js](https://assets.giocdn.com/sdk/cdp/marketing/gtouch.latest.js)



