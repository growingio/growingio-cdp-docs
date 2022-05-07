---
id: mp-minp-sdk-popup
sidebar_position: 1
---

# 弹窗SDK（微信小程序）

## 集成小程序弹窗SDK(最低版本0.5)[](#yi-ji-cheng-xiao-cheng-xu-dan-chuang-sdk-zui-di-ban-ben-0-5)

![](/img/assets-M2qbZInaXgdm8kkNosp-MDnWiE5j6cXk-SjElDb-MDnX85qKCFtyaGxsu0Eimage.png)


### 首先微信小程序 数据采集SDK的集成[](#1-shou-xian-wei-xin-xiao-cheng-xu-shu-ju-cai-ji-sdk-de-ji-cheng)

参考[小程序 SDK](https://growingio.github.io/growingio-sdk-docs/docs/miniprogranm/base/gettingStarted) 弹窗依赖于数据采集SDK,数据采集SDK版本需要0.5及以上，index.js 是数据采集SDK，如果你之前集成过数据采集SDK老版本，替换则是升级数据采集js，然后引入弹窗组件。

### 配置gtouchHost, 请求弹窗地址，一般与您环境的host一致[](#2-pei-zhi-gtouchhost-qing-qiu-dan-chuang-di-zhi-yi-ban-yu-nin-huan-jing-de-host-yi-zhi)

```js
gdp('init', 'your projectId','your dataSourceId', 'your appId', {host: 'api.growingio.com',gtouchHost:'popupwindow.test.com'}); 
```


### 登陆微信小程序后台，进入配置[](#3-deng-lu-wei-xin-xiao-cheng-xu-hou-tai-jin-ru-pei-zhi)

打开开发设置，到服务器域名配置部分

在`request合法域名`中添加：https://XX.com (你设置的gtouchhost地址) `downloadFile请求合法域名列表`中添加您的图片地址域名


## 平台创建微信小程序SDK消息[](#er-ping-tai-chuang-jian-wei-xin-xiao-cheng-xu-sdk-xiao-xi)

进入  **用户运营**，点击左上角的**新建**按钮，选择**弹窗**，然后选择**小程序**，即可进入微信小程序的弹窗配置页面

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5ESYD_de7WR234LbA-MC5EvZw5tc81JPFySX7image.png)

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5ESYD_de7WR234LbA-MC5EzuBl94AXegl_1g8image.png)

根据您的需要，选择对应的**产品**、**触发时机**、**触发次数**、**图片素材**、**点击事件后**、**上线时间**、**停止时间**后，**保存上线**即可。


## 使用微信小程序SDK组件[](#san-shi-yong-wei-xin-xiao-cheng-xu-sdk-zu-jian)

> 这里以**原生小程序应用**与**Taro应用**为例，其余微信小程序框架可参考对应框架对于小程序原生组件的使用方式。如果是第一次集成小程序SDK，建议下载最新GIOSDK全量替换。


### 原生小程序应用[](#31-yuan-sheng-xiao-cheng-xu-ying-yong)

1. 在**app.json**文件中的**usingComponents**属性中，添加**gio-marketing**组件

```js
"usingComponents":  {

 "gio-marketing":  "utils/gio-minp/components/gio-marketing/gio-marketing"

},
```

2. 在**每一个page**页面的wxml文件里，引入gio-marketing组件（原则上只需要在需要弹窗的页面引入组件）

```js
// 例：pages/index/index.wxml

<gio-marketing />

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

 'gio-marketing':  'utils/gio-minp/components/gio-marketing/gio-marketing'

 }

 }

 ...

 render()  {

 return  (

 <View>

 <gio-marketing />

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

 "gio-marketing":  "../static/components/gio-marketing/gio-marketing"

 }

}
```

4. 在具体渲染组件的template中使用

```xml
<template>

 <div>

 <gio-marketing />

 </div>

</template>
```


## 弹窗大小说明[](#dan-chuang-da-xiao-shuo-ming)

宽度是窗口的80%，高度随内容的高度自动伸缩
