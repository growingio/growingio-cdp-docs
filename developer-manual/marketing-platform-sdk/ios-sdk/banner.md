---
id: mp-ios-banner-sdk
sidebar_position: 3
---

# 资源位 SDK（iOS）

资源位 SDK 最低兼容 iOS 8.0 系统。

库简介

> GrowingTouchCoreKit.framework 运营基础库
> GrowingTouchCoreUI.bundle UI 页面图
> GrowingTouchKit.framework 运营弹窗库
> GrowingTouchBannerKit.framework 运营 banner 库

资源位 SDK 主要提供两种接入方式：

- 原生模板
- 自渲染（GIO 提供数据，由客户端自行渲染）

## 集成 SDK[](#ji-cheng-sdk)

### 集成 GrowingIO iOS CDP 数据采集 SDK[](#1-ji-cheng-growingio-ios-cdp-shu-ju-cai-ji-sdk)

资源位 SDK 依赖于数据数据采集 SDK

版本要求最低 1.2.3，如已集成请跳过

参考 [iOS SDK](https://growingio.github.io/growingio-sdk-docs/docs/ios)

### 集成运营 SDK[](#2-ji-cheng-yun-ying-sdk)

手动集成 SDK

- 下载最新的 iOS GrowingTouch SDK 包，并将其中的 GrowingTouchCoreKit.framework、
  GrowingTouchCoreUI.bundle 以及 GrowingTouchBannerKit.framework 添加到 iOS 工程中。下载链接：[http://assets.giocdn.com/cdp/ios/CDPTouch1.4.7.zip](http://assets.giocdn.com/cdp/ios/CDPTouch1.4.7.zip)​

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4mOetDAxVVM8YCSlJs%2F-M4mOmcb0LHDIZj_s540%2Fimage.png?alt=media&token=ba7ac106-deb9-444b-b087-3e5b7033fc4b)

### 初始化 SDK[](#3-chu-shi-hua-sdk)

在 AppDelegate 中导入 `#import <GrowingTouchCoreKit/GrowingTouchCoreKit.h>` 并添加初始化方法，且保证在 GrowingIO 采集 SDK 启动代码后

```swift
-  (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

 ...

 // 启动GrowingIO采集SDK代码

 // 设置弹窗和banner请求地址，一般与访问页面域名一致

 \[GrowingTouch setServerHost:@"http://test.xxx.com"\];

 // 启动GrowingTouch

 \[GrowingTouch start\];

}
```

​

请注意调用顺序，需要在 GrowingIO 采集 SDK 启动代码调用后，再调用 \[GrowingTouch start\] 函数。

## 原生模板[](#yuan-sheng-mo-ban)

生成**Banner**视图示例，并根据对应**bannerKey**填充**Banner**数据，视图的位置尺寸由用户定义。 bannerKey 来自 GIO 页面生成

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M4m_flROTOExvFFkcvz%2F-M4m_lgu_2PWAKMNPdfp%2Fimage.png?alt=media&token=e153302d-e6a1-4d3f-b2dc-fe5aaadc22be)

### 初始化[](#1-chu-shi-hua)

导入对应的包#import "GrowingTouchCoreKit/GrowingTouchBannerView.h"

在需要的位置调用 Banner 视图的初始化方法，对应的 API 为

```swift
/**

 初始化方法

 @param frame 尺寸位置

 @param placeholderImage 占位图

 @return 返回初始化的实例

 */

+  (GrowingTouchBannerView *)bannerKey:(NSString*) bannerKey bannerFrame:(CGRect)frame placeholderImage:(UIImage *)placeholderImage;
```

其中：

**bannerKey：**为该**Banner**对应的唯一标识，在资源位**Banner**的**web**页面上配置获取，属于必填项

**frame**：**Banner**视图的位置尺寸

**placeholderImage**：**Banner**视图中单个**Item**视图的占位图

### 属性设置[](#2-shu-xing-she-zhi)

Banner 视图支持以下属性设置

| 属性含义                                                       | 属性变量名称                  |
| -------------------------------------------------------------- | ----------------------------- |
| 轮播时间间隔，单位为秒（s），默认为 3s                         | scrollTimeInterval            |
| 自动轮播，默认 YES                                             | autoScroll                    |
| pageControl 的样式，默认系统样式                               | pageControlStyle              |
| pageControl 的位置                                             | pageControlAlignemnt          |
| 轮播视图为空的默认错误占位图                                   | bannerViewErrorImage          |
| 图片的填充模式，包括轮播图以及没有轮播图时的背景图             | imageViewContentMode          |
| pageControl 选中时的图片(运营 bannerSDK 1.4.4 及以上支持)      | currentPageIndicatorImage     |
| pageControl 未选中时的图片(运营 SDK 1.4.4 及以上支持)          | pageIndicatorImage            |
| 非图片模式 pageControl 选中的颜色(运营 SDK 1.4.4 及以上支持)   | currentPageIndicatorTintColor |
| 非图片模式 pageControl 未选中的颜色(运营 SDK 1.4.4 及以上支持) | pageIndicatorTintColor        |
| pageControl 选中的尺寸大小 CGSize                              | currentPageIndicatorSize      |
| pageControl 未选中的尺寸大小 CGSize                            | pageIndicatorSize             |
| pageControl 间距大小 CGFloat                                   | pageIndicatorSpaing           |

```swift
// 示例代码

// 设置pageControl图片

self.bannerView.currentPageIndicatorImage =  \[UIImage imageNamed:@"page_select"\];

self.bannerView.pageIndicatorImage =  \[UIImage imageNamed:@"page_unselect"\];

self.bannerView.currentPageIndicatorSize =  CGSizeMake(10,10);

self.bannerView.pageIndicatorSize =  CGSizeMake(10,10);

​

//    self.bannerView.currentPageIndicatorTintColor = \[UIColor redColor\];

//    self.bannerView.pageIndicatorTintColor = \[UIColor yellowColor\];
```

### 数据请求[](#3-shu-ju-qing-qiu)

生成**Banner**视图实例后，请求对应**Banner**视图数据**API**

```swift
/**

 加载数据

​

 @param delegate banner数据请求回调代理

 */

-  (void)loadBannerWithDelegate:(id <GrowingTouchBannerViewDelegate>)delegate;
```

### 方法回调[](#4-fang-fa-hui-tiao)

在数据请求中设置**Banner**数据请求代理后，可在代理中实现以下代理方法监听**Banner**数据请求状态与**Banner**的交互行为

```swift
/**

 banner 加载成功

 @param bannerView 对应的banner视图

 */

-  (void)growingTouchBannerLoadSuccess:(GrowingTouchBannerView*) bannerView;

​

/**

 banner 加载失败

 @param bannerView 对应的banner视图

 @param error 失败error

 */

-  (void)growingTouchBannerLoadFailed:(GrowingTouchBannerView*) bannerView error:(NSError *)error;

​

/**

 点击选中某一个banner视图,是否消费此次点击事件

 @param bannerView 对应的banner视图

 @param index banner 位置

 @param openUrl 跳转的链接

 @return 是否消费此次点击

 */

-  (BOOL)growingTouchBanner:(*) bannerView didSelectAtIndex:(NSInteger)index openUrl:(NSString *)openUrl;

​

/**

 视图展示方法

 @param bannerView 对应的banner视图

 @param index banner 位置

 */

-  (void)growingTouchBanner:(GrowingTouchBannerView*) bannerView didShowAtIndex:(NSInteger)index;

​

/**

 banner视图加载失败未展示的默认点击事件

​

 @param bannerView 对应的banner视图

 */

-  (void)growingTouchBannerErrorImageClick:(GrowingTouchBannerView*) bannerView;
```

### 点击跳转[](#5-dian-ji-tiao-zhuan)

**Banner**视图的代理方法中可决定指定位置的点击事件是否在 SDK 内部处理，对应的代理回调方法为

```swift
-  (BOOL)growingTouchBanner:(GrowingTouchBannerView*) bannerView didSelectAtIndex:(NSInteger)index openUrl:(NSString  *)openUrl;
```

默认**Banner**视图上的点击跳转逻辑全部在**SDK**内部处理，如果用户想要自行处理该点击事件，可在上述代理回调方法获取对应的**openUrl**自行实现点击跳转逻辑，同时返回 YES 禁止 SDK 内部自动处理该事件。

​

### 原生模板容错处理：[](#yuan-sheng-mo-ban-rong-cuo-chu-li)

假如服务器出错， 会先取缓存里 banner 的数据，如果没有缓存，会加载用户配置的错误占位图 bannerViewErrorImage，如果没有设置错误占位图，会显示空白，所以建议设置好错误占位图。 如果请求图片加载慢的话，可以设置默认占位图 placeholderImage，作为中间过程显示的图片。 支持灵活资源位，没有 banner 数据模版渲染自动隐藏，布局修改需要开发者自行处理。

## 自渲染[](#zi-xuan-ran)

仅提供 Banner 数据（调用 API 注意 block 的循环引用问题）

### 数据请求[](#1-shu-ju-qing-qiu)

根据**bannerKey**获取对应的**Banner**数据

```swift
/**

 自渲染的初始化方法

 @param bannerKey banner的唯一标识

 @param bannerData 请求成功回调数据

 @param failure 请求失败消息

 */

+  (void)growingTouchBannerDataTaskBannerKey:(NSString*) bannerKey success:(void(^)(GrowingTouchBannerData *)) bannerData failure:(void(^)(NSError*))failure;
```

### Banner 数据模型[](#2-banner-shu-ju-mo-xing)

返回的 Banner 数据模型为

- GrowingTouchBannerData：整个 Banner 数据模型

| 属性名称  | 含义                        |
| --------- | --------------------------- |
| name      | Banner 名称                 |
| bannerKey | Banner 唯一标识             |
| Items     | Banner 包含的条目 Item 数组 |

- GrowingTouchBannerItem：Banner 中单个 Item 的模型

| 属性名称 | 含义                   |
| -------- | ---------------------- |
| index    | item 的索引，从 0 开始 |
| title    | 当前 item 的名称       |
| imageUrl | 图片地址               |

### 视图绑定[](#3-shi-tu-bang-ding)

请在下面方法中进行自定义**Banner**单个视图与**Item**的绑定，单个视图的点击在**completedBlock**进行处理，**openUrl**为对应 Item 的跳转参数

itemView 为 Banner 中的单个视图

```swift
/**

item 绑定视图

@param itemView item绑定的视图

@param completedBlock 绑定视图点击的回调

*/

-  (void)bindItemDataToClickView:(UIView *)itemView selectCompleted:(void(^)(NSString *openUrl, NSError *error)) completedBlock;
```

旧的 API（建议用上述新的 API 进行替换） bannerView 为 Banner 中的单个视图

```swift
/**

 自渲染视图与Item的绑定，以及点击回调

​

 @param bannerKey banner的唯一标识

 @param bannerView item对应的视图

 @param item banner的单个数据item

 @param completedBlock 点击的回调，返回跳转参数

 */

+  (void)growingTouchBannerDataTaskBannerKey:(NSString*) bannerKey bannerView:(UIView *)bannerView bannerItem:(GrowingTouchBannerItem *)item selectCompleted:(void(^)(NSString *openUrl, NSError *error)) completedBlock;
```

​

## 异常错误码[](#yi-chang-cuo-wu-ma)

| 错误码 | 错误信息                                            | 错误原因                                                     |
| ------ | --------------------------------------------------- | ------------------------------------------------------------ |
| -994   | Can not get banner data for key!                    | banner 数据为空                                              |
| -993   | There are no banner item!                           | banner 数据中不存在对应的 Item                               |
| -992   | The bannerView is not the kind of UIView!           | 自渲染视图模型绑定时传入的视图不是 UIView 类                 |
| -991   | The item is not the kind of GrowingTouchBannerItem! | 自渲染视图模型绑定时传入的模型不是 GrowingTouchBannerItem 类 |
| -990   | The bannerItem is NULL!                             | 自渲染视图模型绑定时传入的模型 Item 传入为空                 |
| -989   | The bannerKey is NULL!                              | 传入的 bannerKey 为空                                        |

​
