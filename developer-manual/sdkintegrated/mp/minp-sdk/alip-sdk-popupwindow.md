# 弹窗SDK（支付宝小程序）

## 一. 集成小程序弹窗SDK

1. 首先支付宝小程序 无埋点SDK的集成。 数据源中设置url\_scheme与APPID 一致
2. 登陆支付宝小程序后台，进入配置

   打开小程序详情/设置/开发设置

   配置httpRequest接口请求域名白名单：https://XXX.com \(你设置gtouchHost的地址\)

3. 开发者工具要开启**component2**编译

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
  "gio-marketing": "utils/es/components/gio-marketing/gio-marketing"
},
```

2. 在**每一个page**页面的axml文件里，引入gio-marketing组件（原则上只需要在需要弹窗的页面引入组件）

```java
// 例：pages/index/index.wxml

<gio-marketing />
<View>Welcome to GrowingIO</View>
```

