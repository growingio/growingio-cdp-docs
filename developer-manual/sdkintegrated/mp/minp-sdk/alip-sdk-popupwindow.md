# 弹窗SDK（支付宝小程序）

## 一. 集成小程序弹窗SDK\(最低版本0.5\)

![](../../../../.gitbook/assets/image%20%28282%29.png)

1. 首先微信小程序 无埋点SDK的集成。下载链接[https://assets.giocdn.com/sdk/cdp/gio-alip.zip](https://assets.giocdn.com/sdk/cdp/gio-alip.zip
   )   弹窗依赖于无埋点，无埋点版本需要0.5及以上，index.js 是无埋点，如果你之前集成过无埋点老版本，替换则是升级无埋点js，然后引入弹窗组件。
2. **配置**gtouchHost, 请求弹窗地址，一般与您环境的host一致

   ```text
   gio('init', 'your projectId','your dataSourceId', 'your appId', {host: 'api.growingio.com',gtouchHost:'popupwindow.test.com'});
   ```

3. 数据中设置url\_scheme与APPID 一致，不一致会导致获取不到弹窗

![](../../../../.gitbook/assets/image%20%28295%29.png)

4.登陆支付宝小程序后台，进入配置

打开小程序详情/设置/开发设置

配置httpRequest接口请求域名白名单：https://XXX.com \(你设置gtouchHost的地址\)

5.开发者工具要开启**component2**编译

## 二. 平台创建支付宝小程序SDK消息

进入 **** **用户运营**，点击左上角的**新建**按钮，选择**弹窗**，然后选择**小程序**，即可进入小程序的弹窗配置页面

![](../../../../.gitbook/assets/image%20%28260%29.png)

![](../../../../.gitbook/assets/image%20%28258%29.png)

根据您的需要，选择对应的**产品**、**触发时机**、**触发次数**、**图片素材**、**点击事件后**、**上线时间**、**停止时间**后，**保存上线**即可。

## 三. 使用微信小程序SDK组件

> 这里以**原生小程序应用**与**Taro应用**为例，其余支付宝小程序框架可参考对应框架对于小程序原生组件的使用方式。如果是第一次集成小程序SDK，建议下载最新GIOSDK全量替换。

### 3.1 原生小程序应用

1. 在**app.json**文件中的**usingComponents**属性中，添加**gio-marketing**组件

```java
"usingComponents": {
  "gio-marketing": "utils/components/gio-marketing/gio-marketing"
},
```

2. 在**每一个page**页面的axml文件里，引入gio-marketing组件（原则上只需要在需要弹窗的页面引入组件）

```java
// 例：pages/index/index.wxml

<gio-marketing />
<View>Welcome to GrowingIO</View>
```

