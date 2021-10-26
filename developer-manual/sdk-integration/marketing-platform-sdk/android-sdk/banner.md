---
id: mp-android-banner-sdk
sidebar_position: 2
---

# 资源位 SDK（Android）

::: info
最低兼Android版本4.2 API 17

资源位SDK主要提供两种接入方式：
:::

* 原生模板

在视图对应位置进行轮播图GTouchBanner的初始化,banner配置后调用轮播图API，数据请求、banner视图的样式、图片缓存、点击跳转行为等全部通过接口下发的配置在SDK内部处理

集成与使用代码参考 [GIO电商demo](https://github.com/growingio/AndroidDemo) shopping分支的HomeFragment文件

* 自渲染

调用API接口GrowingTouch#loadBannerData获取banner数据模型以及响应信息,后续展示及点击逻辑由用户进行自实现


## 集成SDK[](#ji-cheng-sdk)

### 集成GrowingIO Android CDP SDK[](#1-ji-cheng-growingio-android-cdp-sdk)

资源位 SDK 依赖于数据数据采集 SDK

版本要求最低1.2.3，如已集成请跳过

参考 [Android SDK](/op/v/2.0/developer-manual/sdkintegrated/client-sdk-3.0/android-sdk) ​


### 添加依赖[](#2-tian-jia-yi-lai)

#### 2.1 在app build.gradle添加SDK依赖[](#21-zai-app-buildgradle-tian-jia-sdk-yi-lai)

```java
dependencies {

 ...

 //由于资源位底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖

 implementation "com.squareup.okhttp3:okhttp:3.12.1"

 //资源位SDK依赖

 implementation "com.growingio.android:gtouch:$gtouch_version"

 //触达原生banner模板依赖

 implementation "com.growingio.android.widget:gtouch-banner:$gtouch_version"

}
```

> $gtouch_version 为最新SDK版本号，现最新的版本号为请参考[SDK更新日志](https://growingio.gitbook.io/op/v/v20200701/developer-manual/sdkintegrated/mp/gtouchsdk-releasenotes)。


### 需要的权限列表[](#3-xu-yao-de-quan-xian-lie-biao)

所需权限同无埋点SDK

```xml
<uses-permission android:name="android.permission.INTERNET"  />

<!--非危险权限，不需要运行时请求，Manifest文件中添加即可-->

<uses-permission android:name="android.permission.ACCESS\_NETWORK\_STATE"  />

<uses-permission android:name="android.permission.SYSTEM\_ALERT\_WINDOW"/>

<uses-permission android:name="android.permission.ACCESS\_WIFI\_STATE"  />
```


### 初始化SDK[](#4-chu-shi-hua-sdk)

请将以下`GrowingTouch.startWithConfig`加在您的Application 的 `onCreate` 方法中，且保证在GrowingIO 采集SDK 启动代码之后

```java
public  class  MyApplication  extends  Application  {

​

 @Override

 public  void  onCreate()  {

 super.onCreate();

 // GrowingIO 采集SDK 启动代码

​

 // GrowingIO 资源位SDK 启动代码

​

 GrowingTouch.startWithConfig(this,  new  GTouchConfig()

 .setDebugEnable(BuildConfig.DEBUG)

 .setMessageHost("获取您的服务器上发出的弹窗和banner数据")

 );

 }

}
```

请注意调用顺序，需要在 GrowingIO 采集SDK 启动代码调用后，再调用 `GrowingTouch.startWithConfig` 函数。


### 代码混淆[](#6-dai-ma-hun-xiao)

如果您启用了代码混淆，请务必在您的proguard-rules.pro文件里加入下面的代码：

```java
#GrowingIO

-keep class  com.growingio.**  {

 *;

}

-dontwarn com.growingio.**

-keepnames class  *  extends  android.view.View

-keepnames class  *  extends  android.app.Fragment

-keepnames class  *  extends  android.support.v4.app.Fragment

-keepnames class  *  extends  androidx.fragment.app.Fragment

-keep class  android.support.v4.view.ViewPager{

 *;

}

-keep class  android.support.v4.view.ViewPager$**{

 *;

}

-keep class  androidx.viewpager.widget.ViewPager{

 *;

}

-keep class  androidx.viewpager.widget.ViewPager$**{

 *;

}

​

#okhttp

-dontwarn okhttp3.**

-keep class  okhttp3.**{*;}

​

#okio

-dontwarn okio.**

-keep class  okio.**{*;}
```


## 原生模板接入[](#yuan-sheng-mo-ban-jie-ru)

### 参数说明[](#1-can-shu-shuo-ming)

| 配置字段 | 属性字段 | 是否必填 | 类型  | 说明  |
| --- | --- | --- | --- | --- |
| Bannerkey | gtouchBannerKey | 是   | string | 在服务端进行查看后配置到本地,一个bannerKey对应一个banner(唯一标识),不设置抛出IllegalArgumentException |
| 轮播间隔 | gtouchAutoPlayInterval | 否   | long | 不设置默认为3000ms,注意单位为ms |
| 自动循环 | gtouchAutoPlayAble | 否   | boolean | 不设置默认为true |
| 轮播指示器样式 | gtouchPointDrawable | 否   | ResourceId | 不设置为SDK默认小圆点 |
| 轮播指示器位置 | gtouchIndicatorGravity | 否   | int（Gravity） | 默认为Gravity.CENTER_HORIZONTAL \| Gravity.BOTTOM |
| 默认占位图 | gtouchPlaceholderDrawable | 否   | ResourceId | 用户设置,不设置默认为-1 |
| 图片的填模式 | scaleType | 否   | ImageView.ScaleType | 不设置默认为CENTER_CROP |
| 错位占位图 | gtouchErorReplaceDrawable | 是   | ResourceId | 用户设置，不设置抛出IllegalArgumentException |


### 在对应视图xml中添加Banner控件（建议使用xml布局）[](#2-zai-dui-ying-shi-tu-xml-zhong-tian-jia-banner-kong-jian-jian-yi-shi-yong-xml-bu-ju)

```xml
<com.growingio.android.sdk.gtouch.widget.banner.GTouchBanner

 android:id="@+id/gtouch_banner"

 android:layout_width="match_parent"

 android:layout_height="107dp"

 app:gtouchBannerKey="99299c5d32d6e14a"

 app:gtouchErrorReplaceDrawable="@mipmap/load_error"

 app:gtouchIndicatorGravity="bottom|right"

 app:gtouchPlaceholderDrawable="@mipmap/loading"  />
```


### GTouchBanner初始化代码如下[](#3-gtouchbanner-chu-shi-hua-dai-ma-ru-xia)

```java
private  GTouchBanner mGTouchBanner;

mGTouchBanner =  findViewById(R.id.gtouch_banner);

mGTouchBanner.loadData(new  BannerStateChangedListener()  {

 /**

 \* Banner数据加载成功

 *

 \* @param banner Banner控件对象

 */

 @Override

 public void onLoadDataSuccess(GTouchBanner banner)  {

 Log.e(TAG,  "onLoadDataSuccess: ");

 }

​

​

 /**

 \* Banner数据加载失败

 *

 \* @param banner Banner控件对象

 \* @param errorCode 错误码

 \* @param description 错误描述，有可能为null

 */

 @Override

 public void onLoadDataFailed(GTouchBanner banner, int errorCode,  String description)  {

 Log.e(TAG,  "onLoadDataFailed: errorCode = "  + errorCode +  ", description = "  + description);

 }

​

​

 /**

 \* Banner item被点击

 *

 \* @param banner Banner控件对象

 \* @param position item所处位置

 \* @param targetUrl 需要跳转的路由url

 \* @return 返回为true，资源位SDK不在处理跳转的路由url；返回为false，资源位SDK会处理跳转内部界面和H5两种资源位系统提供的路由

 */

 @Override

 public boolean onItemClick(GTouchBanner banner, int position,  String targetUrl)  {

 Log.e(TAG,  "onItemClick: position = "  + position +  ", targetUrl = "  + targetUrl);

 return  false;

 }

​

 /**

 \* 加载失败图片被点击

 *

 \* @param banner Banner控件对象

 */

 @Override

 public void onErrorImageClick(GTouchBanner banner)  {

 Log.e(TAG,  "onErrorImageClick");

 }

});
```


## 自渲染接入[](#zi-xuan-ran-jie-ru)

### 数据模型说明[](#1-shu-ju-mo-xing-shuo-ming)

* BannerData

| 属性字段 | 类型  | 说明  |
| --- | --- | --- |
| getName() | string | bannerd名称 |
| getBannerkey() | string | banner的唯一标识 |
| getItem() | List&lt;BannerItemData&gt; | banner的所有item，类型为bannerItemData |

* BanneritemData

| 属性字段 | 类型  | 说明  |
| --- | --- | --- |
| getIndex() | int | index标识，从0开始 |
| getTitle() | string | item的名称 |
| getImageUrl() | string | bannerItem显示图片url |


### 获取banner数据模型[](#2-huo-qu-banner-shu-ju-mo-xing)

使用GrowingTouch#loadBannerData(@NonNull String bannerKey,@NonNull final BannerDataCallback callback)

v1.3.0-cdp 版本新增了对灵活资源位的支持，注意灵活资源位可能发生没有banner的情况，需要特殊处理。

```java
// bannerKey在服务端进行查看后配置到本地

GrowingTouch.loadBannerData("9e38f09a9cc50a79",  new  BannerDataCallback()  {

 /**

 \* Banner数据请求成功

 *

 \* @param bannerData Banner所有数据

 */

 @Override

 public void onSuccess(BannerData bannerData)  {

 if(bannerData.getItems().size <  1){

 throw  new  GTouchSDKException("灵活资源位会发生item为0的情况，需特殊处理")

 }

 }

​

​

 /**

 \* Banner数据请求失败

 *

 \* @param errorCode 错误码

 \* @param description 错误描述，有可能为null，如网络错误时

 */

 @Override

 public void onLoadFailed(int errorCode,  String description)  {

 }

});
```


### bannerItem绑定对应的itemview的点击事件[](#3-banneritem-bang-ding-dui-ying-de-itemview-de-dian-ji-shi-jian)

使用BannerItemData#bindItemDataToClickView(final View clickView, final BannerItemOnClickListener listener)

```java
// itemView即每个bannerItemData对应的视图

bannerItemData.bindItemDataToClickView(itemView,  new  BannerItemOnClickListener()  {

 /**

 \* 点击回调

 *

 \* @param clickView 点击的View

 \* @param itemData 点击的Item的数据

 \* @param targetUrl 需要跳转的目标Url

 \* targetUrl两种格式分别为:

 \* 1.直接的网址(如:https://www.growingio.com)

 \* 2.跳转应用内部界面(如:GInApp://com.growingio.gtouch.InAppPageActivity?key1=value1&key2=value2),在自渲染中跳转需要用户进行处理 

 */

 @Override

 public void onClick(View clickView,  BannerItemData itemData,  String targetUrl)  {

 }

});
```
​
使用bannerItem进行绑定点击事件的原因及注意事项：

* 添加额外依赖:com.android.support:viewpager:x.x.x(含有该依赖即可,如依赖包:com.android.support:appcompat-v7:x.x.x)
    
* 使用androidx时请同时设置android.enableJetifier为true
    
* 保证banner的展示以及点击事件能够正确传给GroiwngIO的数据端,需要使用BannerItemData#bindItemDataToClickView进行点击事件的绑定
    
* 将对应视图的点击事件实现在BannerItemOnClickListener回调时,不要进行额外的点击事件设置
    
* 保证banner的展示事件准确,需要在视图真正显示时进行BannerItemData#bindItemDataToClickView调用,注意如使用ViewPager存在预加载(无法disable),建议在类似PagerAdapter#setPrimaryItem函数中进行绑定调用
    
* 如使用ViewPager2(目前版本:androidx.viewpager2:viewpager2:1.0.0-beta03),为保证展示事件的准确性建议关闭离屏加载(类似ViewPager的预加载,默认关闭),使用预加载时在视图绑定时(在创建时将导致展示事件错乱)进行BannerItemData#bindItemDataToClickView调用
    

## 原生模板接入异常情况说明[](#yuan-sheng-mo-ban-jie-ru-yi-chang-qing-kuang-shuo-ming)

### 获取Banner数据失败（包括获取到的BannerItem的size为0）[](#1-huo-qu-banner-shu-ju-shi-bai-bao-kuo-huo-qu-dao-de-banneritem-de-size-wei-0)

* 当存在上一次获取到Banner数据时，将会加载上一次数据
    
* 没有上一次数据时，将会回调用户错误（onLoadDataFailed）并加载设置的错误图片
    
* 获取到的BannerItem的size为0时，原生模板所在的view会自动隐藏，界面上会有对应的隐藏动画，请开发者酌情考虑使用我们的模板。
    

### 后端返回的配置数据banneritem的index不连续（包括：自渲染接入）[](#2-hou-duan-fan-hui-de-pei-zhi-shu-ju-banneritem-de-index-bu-lian-xu-bao-kuo-zi-xuan-ran-jie-ru)

SDK中会将index进行去重并重新编号

### BannerItem单张图加载失败[](#3-banneritem-dan-zhang-tu-jia-zai-shi-bai)

删除该item，删除后不存在item将会加载用户与设置的错误图片（errorReplaceDrawable）
