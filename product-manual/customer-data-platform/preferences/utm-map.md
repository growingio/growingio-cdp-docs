---
id: utm-map
sidebar_position: 1
---

# UTM映射

## 简介[](#jian-jie)

在复杂的广告投放场景中，可能会遇到以下场景：

不同渠道投放时，需要设置不同标识值的投放参数，例如A渠道必须使用ChannelID=A， B渠道必须使用ResourceID =B ;

不同部门在分别渠道投放时，设置的投放参数不一样，例如 A部门的运营活动投放时，渠道参数设置成了 utm_source = A; 而B部门的运营活动投放时，渠道参数设置成了 utm_channel = B;

广告参数一般是固定参数值的，例如常见的utm_source, utm_campaign, utm_medium, utm_content, utm_term。 在面对如上场景时， 就存在一些情况，由于跨部门、跨渠道、跨场景等情况，渠道参数非常难统一，造成经常混用UTM几个不同的参数来统计同一来源角度的情况。使来源分析的可用性和可解读性大大降低。

为了解决这个问题，GrowingIO上线了UTM映射功能，使项目中，同一角度上，多个不同的参数值，可以统一到一个统计维度上，保证来源分析的可用性和可解读性。

例如，针对上面的描述的场景，ChannelID, ResourceID, utm_source, utm_channel 几个参数值，都代表一个分析角度，即获客来源，则都可以映射为utm_source, 在分析中统一使用 **广告来源** 维度进行数据维度对比。

:::danger 注意事项

- 映射创建后，才开始统计做映射的渠道参数
- 删除映射后，没有使用UTM 5个参数的投放数据将不再进行统计
- 严格匹配映射参数，大小写敏感，需要确保填写的映射参数和投放一致
- 不能使用相同的标识表示不同的UTM参数，即A部门使用ChannelID = A，B部门使用ResourceID = A
- 当投放链接中多个标识映射同一个UTM参数时，按顺序取最后一个参数进行映射
:::

## 功能说明[](#gong-neng-shuo-ming)

支持UTM映射参数配置和管理

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2Fsync%2Fd6473de59725fa1cab6446a435381bbe23b18c0b.png?alt=media)

### UTM 参数使用

对于运营人员来说，UTM 是个非常熟悉的东西。例如，通过 UTM 码就可以知道每一篇文章带来的流量和用户。

但是通过 GrowingIO，UTM 码还有更强大的功能：可以根据不同渠道、不同内容做精细化分析，帮你对比区分优质和劣质渠道，提高流量在产品内的转化。

使用添加 GrowingIO 添加 UTM 参数的链接投放后，每一个渠道带来的流量都十分清晰，用户在产品内的行为也一目了然，是否注册了，是否最终购买了，都可以看到。我们可以看到讲述 heatmap 热图的这篇内容在渠道「微博1」投放的链接，带来了 9992 个页面浏览量，2066 个注册用户量，以及 1614 个购买用户量。

![picture 1](/img/0e56715dbf2d0901c1502b9fef565ecfba6feaeb2428cd5e8fb0c3a23c953758_pic_1645610733024_2022-02-23.png)  

而且不仅可以看到同一篇文章在不同渠道的流量情况，如 heatmap 热图这篇内容在微信、微博和其他渠道的推广情况；还可以看到同一个渠道不同文章带来的流量情况，如在微博渠道，heatmap 热图的文章的导流情况比 features 功能文章的导流情况更好。

用户在产品内的行为，有多少进行了注册，有多少完成了购买，清清楚楚，而且，我们还可以将不同渠道进行分组，查看不同渠道的留存和转化。

当您自行在投放链接上添加GrowingIO格式的UTM参数时，请注意保证查询条件格式合法。

查询条件格式为：`www.xxxx.com/path?utm_source=a&utm_medium=b`

常见的错误的格式有：

- 使用多个问号：`https://www.xxx.com/path?utm_source=a?utm_medium=b`
- 缺少问号：`https://www.xxx.com/path&utm_source=a&utm_medium=b`
- 使用其他符号：`https://www.xxx.com/path?otherconfig="utm_source=a&utm_medium=b"`

### UTM 参数设置

通过 UTM 参数追踪外部流量的访问情况的原理是：把你投放在不同渠道的链接打上特定的标记，以监控各个链接的流量情况。

#### 1. 确定目标链接

首先，确定这个链接最终指向的目标网页是哪个？一般来说是你自己的网站的某个页面，然后这个页面需要加载过统计分析工具的 SDK 。也就是说前提是，链接最终指向加载了相应的分析代码的你自己的网站。

#### 2. 添加自定义的参数

接下来，我们需要设置 UTM 的参数，也就是在链接上添加规则，进行标记，投放链接后我们就可以知道是哪个来源带来的流量了。对于不同的活动或文章，我们要设置不同的 UTM 参数用来区分。

这里就是指你用各种各样的内容来描述这条链接是放在哪个活动、哪个来源上的，例如：

![picture 2](/img/c62391541d4649250b98f0515430a6a3693dff21786408c4615cc92150288384_pic_1645610817729_2022-02-23.png)

以现在很常用的新媒体营销方式为例，我们在微信的阅读原文里放了一条引导流量的链接：

[https://www.growingio.com/?utm_source=weixin&utm_medium=article1&utm_campaign=product&utm_content=0811-tool&utm_term=tool](https://www.growingio.com/?utm_source=weixin&utm_medium=article1&utm_campaign=product&utm_content=0811-tool&utm_term=tool)

这条链接的意思是什么呢？

![picture 3](/img/f4c9119eb39dcfa68fccc8d51eae84dff67c7c450abc2459e1257e232434ea90_pic_1645611534968_2022-02-23.png)  

“?” 之后的 UTM 参数可以理解为链接的名字，即为投放在不同渠 道的每个链接起的分析工具能够识别的名字。 这条 UTM 代表的含义就是：这个指向 [www.growingio.com](https://www.growingio.com) 的投放链接，是在 8 月 11 日 utm_content=0811-tool 微信公众号 utm_source=weixin 的首条推送文章里 utm_medium=article1 投放的，这篇文章是介绍工具 utm_term=tool 的产品文章 utm_campaign=product 。

网页链接也有很多种表现形式，比如说做成二维码，用在各个活动里使用。​

以现在很常用文章内二维码获客方式为例，我们在公众号关于增长的内容里放了一个小程序链接二维码，可以让用户直接扫一扫打开。生成二维码的实际链接如下：

pages/index/index?utm_source=wechat_articel&utm_content=618Growth

这条链接的意思是什么呢？“?” 之后的 UTM 参数可以理解为链接的信息，即为投放在不同渠 道的每个链接起的分析工具能够识别的名字。这条 UTM 代表的含义就是：这个指向你的小程序页面 pages/index/index 的投放链接，是一个在微信公众号中的618推送的增长相关的文章，因为 utm_source=wechat_article 标记是微信公众号文章渠道，utm_content=618Growth 标记是 618 增长文章。

另外公众号链接到小程序的图文链接，也可以在微信公众号设置文字、图片或者卡片链接时，在落地指向页面的连接中添加UTM参数。

当我们有很多内容同时在各个渠道投放时，这样的链接就十分有用了。例如通过大V公众号推广小程序时，utm_source上标记不同大V的ID，我们就可以非常清晰的知道每个大V的内容带来的流量；也可以按照不同的渠道将流量进行分组，分析不同渠道带来的效果和质量。

GrowingIO 提供的 UTM 参数和自定义参数的方式采用的是目前市面上最常用的定义方式：

![picture 4](/img/58d0cac5fa8c542de2c263bbb9dc7871baf76f8f7f8ae8e6f0818b029d7c5163_pic_1645611580358_2022-02-23.png)  

我们可以根据需要，进行各种各样自定义的填充，因为UTM最初是用在广告监控上的，所以它的很多名称还是关于广告的，但是我们现在已经可以把它放在各个内容、活动、推广中，监控渠道的流量情况。具体的填写参数的意义和方法，可以根据具体的场景进行灵活的变通。

小程序可监测的UTM参数维度，和网站监测产品是一致的，采用的是目前市面上最常用的定义方式。

### UTM参数映射

如果你有自定义的参数没办法进行调整，你可以使用UTM映射功能进行参数映射和配置。请参考[UTM映射管理](../../../product-manual/customer-data-platform/preferences/utm-map)

## 常见问题

### 1. UTM 参数中存在多个问号会遇到什么问题？

问号在 HTTP 协议中作为特殊字符，GrowingIO 会根据 "?" 符号来获取查询条件参数，用 “&” 符号分隔查询条件中的参数，用 “=” 分隔参数与具体值。

当网页地址中有多个问号时，默认处理逻辑会从第一个问号开始做参数识别，后续再次出现的问号会作为参数中的信息被识别，影响后续参数信息的识别，从而影响 UTM 各维度的信息统计。在广告投放时需要对网页地址做规范化处理。