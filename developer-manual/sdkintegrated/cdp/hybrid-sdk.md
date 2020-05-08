---
description: H5 内嵌页提供数据采集 SDK。
---

# H5内嵌页SDK

## 1. 添加跟踪代码 <a id="1-tian-jia-gen-zong-dai-ma"></a>

###  1. H5页面添加代码 <a id="1-h-5-ye-mian-tian-jia-dai-ma"></a>

将以下JS代码复制到H5页面的 **&lt;head&gt;** 和 **&lt;/head&gt;** 标签之间即可。安装成功后，除 localhost 和 IP 地址外，网址下所有的行为数据都将会被收集。

```javascript
<script type="text/javascript">
      !function(e,t,n,g,i){e[i]=e[i]||function(){(e[i].q=e[i].q||[]).push(arguments)},n=t.createElement("script"),tag=t.getElementsByTagName("script")[0],n.async=1,n.src=('https:'==document.location.protocol?'https://':'http://')+g,tag.parentNode.insertBefore(n,tag)}(window,document,"script","assets.giocdn.com/gio_hybrid_cdp.js","gio");
      gio('init', '你的项目ID', {debug: false, platform:'hybrid'});
      gio('send');
</script>
```

{% hint style="info" %}
不要和其他的GIO的  JS SDK 共同使用
{% endhint %}

### 设置自定义事件及事件级变量（track） <a id="she-zhi-zi-ding-yi-shi-jian-ji-shi-jian-ji-bian-liang-track"></a>

手动发送一个自定义事件。在添加所需要发送的事件代码之前，需要在平台里配置添加事件。

**接口定义**

```javascript
gio('track', eventName: string, properties: object);
```

**参数说明**

| 名称 | 类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| eventName | string | 是 | 事件标识符。 |
| properties | Object | 否 | 事件级变量，即事件发生时所伴随的维度信息参数。 |

```javascript
//代码示例
gio('track','homepage');
gio('track','homepage',{ key1: 'value1', key2: 'value2'});

```

