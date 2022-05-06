---
id: mp-minp-sdk-banner
sidebar_position: 3
---

# 资源位SDK（微信小程序）

## 集成小程序资源位SDK[](#yi-ji-cheng-xiao-cheng-xu-banner-sdk-zui-di-ban-ben-0-5)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MDnWiE5j6cXk-SjElDb%2F-MDnX85qKCFtyaGxsu0E%2Fimage.png?alt=media&token=f3c65e6c-fde2-44a3-afd0-21bf38bcc2b5)


### 首先微信小程序 数据采集SDK的集成[](#1-shou-xian-wei-xin-xiao-cheng-xu-shu-ju-cai-ji-sdk-de-ji-cheng)

参考[微信小程序 SDK 集成](https://growingio.github.io/growingio-sdk-docs/docs/miniprogram/3.3/integration/wx) 资源位依赖于数据采集SDK，index.js 是数据采集SDK，如果你之前集成过数据采集SDK老版本，替换则是升级数据采集js，然后引入资源位组件。

弹窗[SDK下载地址](https://assets.giocdn.com/sdk/cdp/3.0/gio-minp.zip)(gio-banner为弹窗SDK)

### 配置gtouchHost, 请求资源位地址，一般与您环境的host一致[](#2-pei-zhi-gtouchhost-qing-qiu-banner-di-zhi-yi-ban-yu-nin-huan-jing-de-host-yi-zhi)

```js
gdp('init', 'your GrowingIO accountId', 'your dataSourceID', 'your AppId', {
    version: '小程序版本',
    host: 'api.growingio.com',
    gtouchHost:'popupwindow.test.com',
    ...其他配置项
});
```


### 登陆微信小程序后台，进入配置[](#3-deng-lu-wei-xin-xiao-cheng-xu-hou-tai-jin-ru-pei-zhi)

打开开发设置，到服务器域名配置部分

在`request合法域名`中添加：https://XX.com (你设置的gtouchhost地址) `downloadFile请求合法域名列表`中添加您的图片地址域名


## 平台创建微信小程序SDK消息[](#er-ping-tai-chuang-jian-wei-xin-xiao-cheng-xu-sdk-xiao-xi)

进入  **用户运营**，点击左上角的**新建**按钮，选择**资源位**，然后选择**小程序**，即可进入微信小程序的资源位配置页面

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5ESYD_de7WR234LbA%2F-MC5EvZw5tc81JPFySX7%2Fimage.png?alt=media&token=7f39d6ae-ba6f-4fbf-a258-11df502efe5d)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5ESYD_de7WR234LbA%2F-MC5EzuBl94AXegl_1g8%2Fimage.png?alt=media&token=92ce2f2d-0bae-4040-9ba6-a226f7f0905e)

根据您的需要，选择对应的**产品**、**触发时机**、**触发次数**、**图片素材**、**点击事件后**、**上线时间**、**停止时间**后，**保存上线**即可。


## 使用微信小程序SDK组件[](#san-shi-yong-wei-xin-xiao-cheng-xu-sdk-zu-jian)

> 这里以**原生小程序应用**与**Taro应用**为例，其余微信小程序框架可参考对应框架对于小程序原生组件的使用方式。如果是第一次集成小程序SDK，建议下载最新GIOSDK全量替换。


### 原生小程序应用[](#31-yuan-sheng-xiao-cheng-xu-ying-yong)

1. 在**app.json**文件中的**usingComponents**属性中，添加**gio-banner**组件

```js
"usingComponents":  {

 "gio-banner":  "utils/gio-minp/components/gio-banner/gio-banner"

},
```

2. 在**每一个page**页面的wxml文件里，引入gio-banner组件（原则上只需要在需要资源位的页面引入组件）

```js
// 例：pages/index/index.wxml

<gio-banner />

<View>Welcome to GrowingIO</View>
```


### Taro应用[](#32-taro-ying-yong)

在每一个page页面的**config配置项里**通过**usingComponents属性引入组件**，接着在**render方法**中使用组件（原则上只需要在需要埋点的页面引入组件）。

```js
// 例：pages/index/index.js

export default  class  Index  extends  Component  {

 config =  {

 navigationBarTitleText:  'GrowingIO',

 usingComponents:  {

 'gio-banner':  'utils/gio-minp/components/gio-banner/gio-banner'

 }

 }

 ...

 render()  {

 return  (

 <View>

 <gio-banner />

 <View>Welcome to GrowingIO</View>

 </View>

 )

 }

}
```


### mpvue应用[](#33-mpvue-ying-yong)

1.  将SDK文件包解压后放到**/src/utils**下
    
2.  将其中的**components**目录移动到**/static**下
    
3.  在**/src/pages/**下具体页面的**main.json**中或**/src/app.json**中使用**usingComponents**引入组件
    
```js
{

 "usingComponents":  {

 "gio-banner":  "../static/components/gio-banner/gio-banner"

 }

}
```

4. 在具体渲染组件的template中使用

```xml
<template>

 <div>

 <gio-banner />

 </div>

</template>
```


## 资源位大小说明[](#banner-da-xiao-shuo-ming)

宽度是窗口的80%，高度随内容的高度自动伸缩
