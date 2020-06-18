---
description: H5 内嵌页提供数据采集 SDK。
---

# H5内嵌页SDK\(仅支持app内的H5\)

## 1. 添加跟踪代码 <a id="1-tian-jia-gen-zong-dai-ma"></a>

###  1. H5页面添加代码 <a id="1-h-5-ye-mian-tian-jia-dai-ma"></a>

将以下JS代码复制到H5页面的 **&lt;head&gt;** 和 **&lt;/head&gt;** 标签之间即可。安装成功后，除 localhost 和 IP 地址外，网址下所有的行为数据都将会被收集通过移动端上报，移动端需要去设置[链接](https://docs.growingio.com/op/developer-manual/sdkintegrated/cdp/ios-sdk#bridgeforwebview)。

```javascript
<script type="text/javascript">
      !function(e,t,n,g,i){e[i]=e[i]||function(){(e[i].q=e[i].q||[]).push(arguments)},n=t.createElement("script"),tag=t.getElementsByTagName("script")[0],n.async=1,n.src=('https:'==document.location.protocol?'https://':'http://')+g,tag.parentNode.insertBefore(n,tag)}(window,document,"script","assets.giocdn.com/cdp/hybrid/gio_hybrid_cdp.js","gio");
      gio('init', '你的项目ID', {debug: false, platform:'hybrid'});
      gio('send');
</script>
```

{% hint style="info" %}
不要和其他的GIO的  JS SDK 共同使用
{% endhint %}

## 2. 高级配置 <a id="2-gao-ji-pei-zhi"></a>

内嵌页 SDK 还有以下额外参数可以使用：

| 参数 | 值 | 解释 |
| :--- | :--- | :--- |
| hashtag | true \| false | GrowingIO默认不会把 hashtag 识别成页面 URL 的一部分。对于使用 hashtag 进行页面跳转的单页面网站应用来说，可以启用 hashtag 作为标识页面的一部分，将hashtag设置为true，默认为false。 |
| debug | true \| false | 开启debug可以进行数据的实时调试，默认为false，调试方式为打开开发者工具，在console中查看。 |

### 启用hashtag识别 <a id="qi-yong-hashtag-shi-bie"></a>

GrowingIO默认不会把 hashtag 识别成页面 URL 的一部分。对于使用 hashtag 进行页面跳转的单页面网站应用来说，可以启用 hashtag 作为标识页面的一部分，将hashtag设置为true

```javascript
gio('init', '你的项目ID', {debug: false, platform:'hybrid',hashtag:true});

```

### 设置自定义事件及事件级变量（track）、物品模型 <a id="she-zhi-zi-ding-yi-shi-jian-ji-shi-jian-ji-bian-liang-track"></a>

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
| item | Object | 否 | key 和 id   不能修改为其他 |

```javascript
//代码示例
gio('track','homepage');
gio('track','homepage',{ key1: 'value1', key2: 'value2'});

// track API调用示例 - 物品模型
gio('track','testEvent',{},{key:'order_id',id:'123456'})
// key为物品模型唯一标识属性

```



### **设置用户属性**

```javascript
//代码示例
gio('setUserAttributes', {name: 'helloworld'})

```

