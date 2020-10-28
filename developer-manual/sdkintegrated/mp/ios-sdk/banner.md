# 资源位 SDK（iOS）

资源位SDK最低兼容iOS 8.0 系统。

库简介

> **GrowingTouchCoreKit.framework 运营基础库  
> GrowingTouchCoreUI.bundle UI页面图  
> GrowingTouchKit.framework 运营弹窗库  
> GrowingTouchBannerKit.framework 运营banner库**

资源位SDK主要提供两种接入方式：

* 原生模板
* 自渲染（GIO 提供数据，由客户端自行渲染）

## 集成SDK

### 1. 集成GrowingIO iOS CDP数据采集SDK \(如已集成跳过\)

[https://growingio.gitbook.io/cdp/developer-manual/sdkintegrated/cdp/ios-sdk](https://growingio.gitbook.io/cdp/developer-manual/sdkintegrated/cdp/ios-sdk)

### 2. 集成运营SDK

手动集成SDK

* 下载最新的iOS GrowingTouch SDK包，并将其中的GrowingTouchCoreKit.framework、

  GrowingTouchCoreUI.bundle以及GrowingTouchBannerKit.framework 添加到iOS工程中。下载链接：[http://assets.giocdn.com/cdp/ios/CDP1.2.4\_Touch1.4.1.zip](http://assets.giocdn.com/cdp/ios/CDP1.2.4_Touch1.4.1.zip)

![](../../../../.gitbook/assets/image%20%28110%29.png)

### 3. 初始化SDK

在 AppDelegate 中导入 `#import <GrowingTouchCoreKit/GrowingTouchCoreKit.h>` 并添加初始化方法，且保证在埋点 SDK 初始化代码`[Growing startWithAccountId:@"ACCOUNT_ID" dataSourceId:@"DATASOURCE_ID"]`后

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    ...
    // 启动GrowingIO
    [Growing startWithAccountId:@"YOUR_ACCOUNT_ID"  dataSourceId:@"YOUR_DATASOURCE_ID"]; //替换为您的项目ID
    
    // 设置弹窗和banner请求地址，一般与访问页面域名一致
    [GrowingTouch setServerHost:@"http://test.xxx.com"];
    // 启动GrowingTouch
    [GrowingTouch start];
}

```

{% hint style="info" %}
请注意调用顺序，需要在 \[Growing startWithAccountId\] 函数调用后，再调用 \[GrowingTouch start\] 函数。
{% endhint %}

## 原生模板

生成**Banner**视图示例，并根据对应**bannerKey**填充**Banner**数据，视图的位置尺寸由用户定义。 bannerKey 来自GIO页面生成

![](../../../../.gitbook/assets/image%20%28133%29.png)

### 1. 初始化

导入对应的包\#import "GrowingTouchCoreKit/GrowingTouchBannerView.h"

在需要的位置调用Banner视图的初始化方法，对应的API为

```objectivec
/**
 初始化方法
 
 @param frame 尺寸位置
 @param placeholderImage 占位图
 @return 返回初始化的实例
 */
+ (GrowingTouchBannerView *)bannerKey:(NSString*) bannerKey bannerFrame:(CGRect)frame placeholderImage:(UIImage *)placeholderImage;
```

其中：

**bannerKey：**为该**Banner**对应的唯一标识，在资源位**Banner**的**web**页面上配置获取，属于必填项

**frame**：**Banner**视图的位置尺寸

**placeholderImage**：**Banner**视图中单个**Item**视图的占位图

### 2. 属性设置

Banner视图支持以下属性设置

| 属性含义 | 属性变量名称 |
| :--- | :--- |
| 轮播时间间隔，单位为秒（s），默认为3s | scrollTimeInterval |
| 自动轮播，默认YES | autoScroll |
| pageControl的样式，默认系统样式 | pageControlStyle |
| pageControl的位置 | pageControlAlignemnt |
| 轮播视图为空的默认错误占位图 | bannerViewErrorImage |
| 图片的填充模式，包括轮播图以及没有轮播图时的背景图 | imageViewContentMode |
| pageControl 选中时的图片\(运营bannerSDK 1.4.4 及以上支持\) | currentPageIndicatorImage |
| pageControl 未选中时的图片\(运营SDK 1.4.4 及以上支持\) | pageIndicatorImage |
| 非图片模式pageControl 选中的颜色\(运营SDK 1.4.4 及以上支持\) | currentPageIndicatorTintColor |
| 非图片模式pageControl 未选中的颜色\(运营SDK 1.4.4 及以上支持\) | pageIndicatorTintColor |
| pageControl 选中的尺寸大小 CGSize | currentPageIndicatorSize |
| pageControl 未选中的尺寸大小 CGSize | pageIndicatorSize |
| pageControl 间距大小 CGFloat | pageIndicatorSpaing |

```objectivec
// 示例代码
// 设置pageControl图片
self.bannerView.currentPageIndicatorImage = [UIImage imageNamed:@"page_select"];
self.bannerView.pageIndicatorImage = [UIImage imageNamed:@"page_unselect"];
self.bannerView.currentPageIndicatorSize = CGSizeMake(10,10);
self.bannerView.pageIndicatorSize = CGSizeMake(10,10);
​
//    self.bannerView.currentPageIndicatorTintColor = [UIColor redColor];
//    self.bannerView.pageIndicatorTintColor = [UIColor yellowColor];
```

### 3. 数据请求

生成**Banner**视图实例后，请求对应**Banner**视图数据**API**

```objectivec
/**
 加载数据

 @param delegate banner数据请求回调代理
 */
- (void)loadBannerWithDelegate:(id <GrowingTouchBannerViewDelegate>)delegate;
```

### 4. 方法回调

在数据请求中设置**Banner**数据请求代理后，可在代理中实现以下代理方法监听**Banner**数据请求状态与**Banner**的交互行为

```objectivec
/**
 banner 加载成功
 
 @param bannerView 对应的banner视图
 */
- (void)growingTouchBannerLoadSuccess:(GrowingTouchBannerView*) bannerView;

/**
 banner 加载失败
 
 @param bannerView 对应的banner视图
 @param error 失败error
 */
- (void)growingTouchBannerLoadFailed:(GrowingTouchBannerView*) bannerView error:(NSError *)error;

/**
 点击选中某一个banner视图,是否消费此次点击事件
 
 @param bannerView 对应的banner视图
 @param index banner 位置
 @param openUrl 跳转的链接
 @return 是否消费此次点击
 */
- (BOOL)growingTouchBanner:(*) bannerView didSelectAtIndex:(NSInteger)index openUrl:(NSString *)openUrl;

/**
 视图展示方法
 
 @param bannerView 对应的banner视图
 @param index banner 位置
 */
- (void)growingTouchBanner:(GrowingTouchBannerView*) bannerView didShowAtIndex:(NSInteger)index;

/**
 banner视图加载失败未展示的默认点击事件

 @param bannerView 对应的banner视图
 */
- (void)growingTouchBannerErrorImageClick:(GrowingTouchBannerView*) bannerView;
```

### 5. 点击跳转

**Banner**视图的代理方法中可决定指定位置的点击事件是否在SDK内部处理，对应的代理回调方法为

```swift
- (BOOL)growingTouchBanner:(GrowingTouchBannerView*) bannerView didSelectAtIndex:(NSInteger)index openUrl:(NSString *)openUrl;
```

默认**Banner**视图上的点击跳转逻辑全部在**SDK**内部处理，如果用户想要自行处理该点击事件，可在上述代理回调方法获取对应的**openUrl**自行实现点击跳转逻辑，同时返回YES禁止SDK内部自动处理该事件。



### 原生模板容错处理：

假如服务器出错， 会先取缓存里banner的数据，如果没有缓存，会加载用户配置的错误占位图bannerViewErrorImage，如果没有设置错误占位图，会显示空白，所以建议设置好错误占位图。  
如果请求图片加载慢的话，可以设置默认占位图placeholderImage，作为中间过程显示的图片。  
支持灵活资源位，没有banner数据模版渲染自动隐藏，布局修改需要开发者自行处理。

## 自渲染

仅提供Banner数据（调用API注意block的循环引用问题）

### 1. 数据请求

根据**bannerKey**获取对应的**Banner**数据

```objectivec
/**
 自渲染的初始化方法
 
 @param bannerKey banner的唯一标识
 @param bannerData 请求成功回调数据
 @param failure 请求失败消息
 */
+ (void)growingTouchBannerDataTaskBannerKey:(NSString*) bannerKey success:(void(^)(GrowingTouchBannerData *)) bannerData failure:(void(^)(NSError*))failure;
```

### 2. Banner数据模型

返回的Banner数据模型为

* GrowingTouchBannerData：整个Banner数据模型

| 属性名称 | 含义 |
| :--- | :--- |
| name | Banner名称 |
| bannerKey | Banner唯一标识 |
| Items | Banner包含的条目Item数组 |

* GrowingTouchBannerItem：Banner中单个Item的模型

| 属性名称 | 含义 |
| :--- | :--- |
| index | item的索引，从0开始 |
| title | 当前item的名称 |
| imageUrl | 图片地址 |

### 3. 视图绑定

请在下面方法中进行自定义**Banner**单个视图与**Item**的绑定，单个视图的点击在**completedBlock**进行处理，**openUrl**为对应Item的跳转参数

{% hint style="info" %}
itemView为Banner中的单个视图
{% endhint %}

```csharp
/**
item 绑定视图
@param itemView item绑定的视图
@param completedBlock 绑定视图点击的回调
*/
- (void)bindItemDataToClickView:(UIView *)itemView selectCompleted:(void(^)(NSString *openUrl, NSError *error)) completedBlock;
```

#### 



{% hint style="info" %}
旧的API（建议用上述新的API进行替换）  
bannerView为Banner中的单个视图
{% endhint %}

```objectivec
/**
 自渲染视图与Item的绑定，以及点击回调

 @param bannerKey banner的唯一标识
 @param bannerView item对应的视图
 @param item banner的单个数据item
 @param completedBlock 点击的回调，返回跳转参数
 */
+ (void)growingTouchBannerDataTaskBannerKey:(NSString*) bannerKey bannerView:(UIView *)bannerView bannerItem:(GrowingTouchBannerItem *)item selectCompleted:(void(^)(NSString *openUrl, NSError *error)) completedBlock;
```



## 异常错误码

| 错误码 | 错误信息 | 错误原因 |
| :--- | :--- | :--- |
| -994 | Can not get banner data for key! | banner数据为空 |
| -993 | There are no banner item! | banner数据中不存在对应的Item |
| -992 | The bannerView is not the kind of UIView! | 自渲染视图模型绑定时传入的视图不是UIView类 |
| -991 | The item is not the kind of GrowingTouchBannerItem! | 自渲染视图模型绑定时传入的模型不是GrowingTouchBannerItem类 |
| -990 | The bannerItem is NULL! | 自渲染视图模型绑定时传入的模型Item传入为空 |
| -989 | The bannerKey is NULL! | 传入的bannerKey为空 |



