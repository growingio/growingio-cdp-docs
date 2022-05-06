---
id: event-flow
sidebar_position: 6
---

# 事件流分析

## 简介[](#jian-jie)

‌ 借助事件流分析可以了解用户进入产品的流向，查看用户路径是否符合预设路径，同时定位不符合预期的节点，进而进行针对性产品或者策略调整优化。

## 名词解释[](#ming-ci-jie-shi)

事件流：通过可视化的方式，展示用户触发事件的先后顺序。

起始事件：事件流分析的起点，查看该事件之后的流向分布。

事件流窗口期：相对起始事件的时间范围，下一步事件在窗口期之内发生视为转化，未转化视为流失。如当转化窗口设置为 1 分钟，用户在起始事件 A 发生 1 秒后，点击事件 B，则视为用户流向事件 B；用户在起始事件 A 发生 1 分 01 秒后发生事件 B，则视为用户流失。

## 功能说明[](#gong-neng-shuo-ming)

### 事件流的创建[](#shi-jian-liu-de-chuang-jian)

‌ 目前，事件流分析支持您选择起始行为， 查看起始行为流向。如注册后，用户做了什么，商品购买后用户做了什么。

‌ 选择目标用户，您可以查看全部用户或者自定义用户分群的具体流向。比如过去 30 天的 VIP 会员的产品路径。

‌ 您可以设置窗口期，窗口期是指相对于起始事件的时间区间。当发生了起始事件后，分析者可以查看在规定的时间窗口内的用户流向。注：某个事件在相对于起始事件的时间窗口之外发生，则视为流失。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2Fop%2F-MguACBZstjXsH0HZJf_%2F-MguCL1u4-udgKP67r8-%2F0.png?alt=media)

Enter a caption for this image (optional)

‌ 当选择要查看的起始事件之后，GrowingIO 会对项目里里的全部埋点数据进行计算，帮助用户了解进行起始行为的用户接下来的流向。如果您对某一步路径感兴趣，您可以选择对该路径进行展开，进一步聚焦分析。如果展开过多节点影响了你对数据的消费，也可以选择收起节点。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2Fop%2F-MguACBZstjXsH0HZJf_%2F-MguCL1vyzBPLmnB5gk0%2F1.png?alt=media)

Enter a caption for this image (optional)

‌ 为了让您更专注于下一步的主要流向，我们默认呈现了下一步 top5 流向，其他流向用更多表示。如果您想查看更多，点击更多进行展开即可：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2Fop%2F-MguACBZstjXsH0HZJf_%2F-MguCL1wuLSiKyo1E_u9%2F2.png?alt=media)

Enter a caption for this image (optional)
‌

### 隐藏事件节点[](#yin-cang-shi-jian-jie-dian)

如果事件流中某些事件对您造成了干扰，您可以选择隐藏事件：

‌ 例如隐藏掉没有业务意义的埋点事件，隐藏掉全部的页面浏览事件或者元素点击事件

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2Fop%2F-MguACBZstjXsH0HZJf_%2F-MguCL1xp6VnnqRSWzDa%2F3.png?alt=media)

Enter a caption for this image (optional)

### ‌ 节点和纽带数据说明[](#jie-dian-he-niu-dai-shu-ju-shuo-ming)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2Fop%2F-MguACBZstjXsH0HZJf_%2F-MguCL1yloRukMvS__9U%2F4.png?alt=media)

Enter a caption for this image (optional)

‌ 节点默认展示节点的次数，节点和起始事件的转化率。如上图 转化率 15.1%=28/185

‌Hover 后展示 节点对应的人数和相比起始事件人数的转化率。如上图 转化率 19.2%=24/125 (125 为订单支付的人数)

‌ 退出统计：规定的转化窗口期内，未有下一步动作视为流失。我们提供了对应节点的统计人数和统计次数，以及统计流失人数占当前节点的占比和统计流失次数占当前节点的占比。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2Fop%2F-MguACBZstjXsH0HZJf_%2F-MguCL1zIuW5dVKV1kJi%2F5.png?alt=media)

Enter a caption for this image (optional)

‌ 我们提供了纽带右侧节点的人数次数，和两个节点的人数转化率和次数转化率评估两个节点之间的转化效率（纽带链接效率）。
