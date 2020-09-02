# Webhook 技术对接文档

* [简介](https://growingio.atlassian.net/wiki/spaces/MP/pages/1517159187/webhook#%E7%AE%80%E4%BB%8B)
* [Webhook 请求](https://growingio.atlassian.net/wiki/spaces/MP/pages/1517159187/webhook#Webhook-%E8%AF%B7%E6%B1%82)
  * [Response Code](https://growingio.atlassian.net/wiki/spaces/MP/pages/1517159187/webhook#Response-Code)
  * [Request Header](https://growingio.atlassian.net/wiki/spaces/MP/pages/1517159187/webhook#Request-Header)
  * [Request Body](https://growingio.atlassian.net/wiki/spaces/MP/pages/1517159187/webhook#Request-Body)
    * [正式发送的webhook请求](https://growingio.atlassian.net/wiki/spaces/MP/pages/1517159187/webhook#%E6%AD%A3%E5%BC%8F%E5%8F%91%E9%80%81%E7%9A%84webhook%E8%AF%B7%E6%B1%82)
    * [测试webhook配置和测试webhook](https://growingio.atlassian.net/wiki/spaces/MP/pages/1517159187/webhook#%E6%B5%8B%E8%AF%95webhook%E9%85%8D%E7%BD%AE%E5%92%8C%E6%B5%8B%E8%AF%95webhook)
  * [Request 验证](https://growingio.atlassian.net/wiki/spaces/MP/pages/1517159187/webhook#Request-%E9%AA%8C%E8%AF%81)
* [Webhook 配置](https://growingio.atlassian.net/wiki/spaces/MP/pages/1517159187/webhook#Webhook-%E9%85%8D%E7%BD%AE)
  * [模版参数支持类型](https://growingio.atlassian.net/wiki/spaces/MP/pages/1517159187/webhook#%E6%A8%A1%E7%89%88%E5%8F%82%E6%95%B0%E6%94%AF%E6%8C%81%E7%B1%BB%E5%9E%8B)

### 简介 <a id="&#x7B80;&#x4ECB;"></a>

客户可以使用webhook将分群信息\(用户属性\)发送到自己的内部系统，比如电商自有的发券系统，Push系统等，也可以将信息发送到自己的后台， 比如当用户发生了某些行为后若干次数后，客户可以在后台增加某个用户的会员积分等。应用场景是非常灵活的。

### Webhook 请求 <a id="Webhook-&#x8BF7;&#x6C42;"></a>

Webhook请求是一个POST请求，会发送到某个客户提供的URL上，可以添加额外的参数，例

![](../.gitbook/assets/image%20%28332%29.png)

#### Response Code <a id="Response-Code"></a>

GIO 会遵循HTTP状态码，200代表post成功，其余的都是错误信息。

####  <a id="Request-Header"></a>

#### Request Header <a id="Request-Header"></a>

Content-Type:application/json

X-gio-signature:xxx

####  <a id="Request-Body"></a>

#### Request Body <a id="Request-Body"></a>

![](../.gitbook/assets/image%20%28327%29.png)

\*\*\*\*

**正式发送的webhook请求**

暂定发送速率为每秒1000个用户的信息

在growingio的页面上能配置若干模板参数

![](../.gitbook/assets/image%20%28335%29.png)

例如:

![](../.gitbook/assets/image%20%28340%29.png)

如果不查询用户属性，userAttr字段为空数组:

![](../.gitbook/assets/image%20%28330%29.png)

**webhook配置和测试webhook**

Request Body

![](../.gitbook/assets/image%20%28343%29.png)

如果不查询用户属性:

![](../.gitbook/assets/image%20%28329%29.png)

####  <a id="Request-&#x9A8C;&#x8BC1;"></a>

#### Request 验证 <a id="Request-&#x9A8C;&#x8BC1;"></a>

一些场景下，客户需要验证 Webhook 请求是来自GIO而不是第三方伪造，可为 Webhook 配置一个 Secret Key，该 Secret Key 在GIO运营服务端和 客户的服务器上共享。

对于配置了Secret Key的可以生成消息签名来验证消息的合法性和完整性，未配置的默认用空字符串作为Secret Key。

![](../.gitbook/assets/image%20%28324%29.png)

生成的签名放置在http响应头X-gio-signature中，例如:

X-gio-signature:1e089260ba1bfde37f88eca8e665d8b1fb690ae763979d25dd10a831dedd52a8



### Webhook 配置 <a id="Webhook-&#x914D;&#x7F6E;"></a>

#### 模版参数支持类型 <a id="&#x6A21;&#x7248;&#x53C2;&#x6570;&#x652F;&#x6301;&#x7C7B;&#x578B;"></a>

![](../.gitbook/assets/image%20%28331%29.png)

 赞成为首赞无标签写下评论…

