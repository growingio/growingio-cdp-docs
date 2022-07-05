---
id: ab-experiment
sidebar_position: 4
---

# A/B 测试

通过快速实验和数据，验证假设，然后推广，增长的重要手段之一就是实验。

下面按使用场景介绍弹窗的高级功能：A/B测试

使用限制

* 支持 App 弹窗实验，小程序弹窗实验，H5弹窗实验
    
* 仅支持单一变量实验对比：比如对比素材、对比分群等，不能同时对比变量
    

# 场景1：配置分群/控制组对比[](#chang-jing-1-pei-zhi-fen-qun-kong-zhi-zu-dui-bi)

> 分群对比：不同分群对相同弹窗内容的投放对比。
> 
> 控制组对比：同一个分群中收到与未收到弹窗内容的效果对比。


### 添加不同分群对比[](#tian-jia-bu-tong-fen-qun-dui-bi)

单击**添加分群/控制组对比**，选择**添加分群对比**。

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly3BZ5aYrTd2zCV4C-l-Ly3Exk-RXdlbpmuJPKK%E5%88%86%E7%BE%A4%E5%AF%B9%E6%AF%94%E6%8C%89%E9%92%AE.png)

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly3BZ5aYrTd2zCV4C-l-Ly3F24s7QHZxgI4Z-f1%E5%88%86%E7%BE%A4%E5%AF%B9%E6%AF%94list.png)

添加效果如下图：

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly3BZ5aYrTd2zCV4C-l-Ly3FYjRGhBnm6sDQi3C%E5%88%86%E7%BE%A4ab.png)


### 添加控制组对比[](#tian-jia-kong-zhi-zu-dui-bi)

单击**添加分群/控制组对比**，选择**添加控制组对比**。

添加效果如下图：

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly2hXtTGw6zsdRYPJiv-Ly2wzzSOLhODXQSMRRf%E6%8E%A7%E5%88%B6%E7%BB%84ab.png)

您可以自定义实验组占当前分群的百分比数，只有分配到实验组的用户会收到弹窗，控制组的用户不会收到（只作为对比人群）。要对比的数据取决于您设置的转化目标，比如可以对比两组人的 留存，活跃，成交情况等等。


## 场景2：配置素材对比[](#chang-jing-2-pei-zhi-su-cai-dui-bi)

> 对比同一分群用户，投放不同素材的投放效果对比。

在配置触发和素材时，单击**添加素材对比**。

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly2hXtTGw6zsdRYPJiv-Ly2x82vtsdgDUN8HhyO%E6%B7%BB%E5%8A%A0%E7%B4%A0%E6%9D%90%E5%AF%B9%E6%AF%94.png)

支持上传两种素材，自动成为实验A组和实验B组，所选择的目标分群用户触发了相应的条件后，会随机展示（各50%概率）其中一个素材。

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly2hXtTGw6zsdRYPJiv-Ly2xENfP8OoLj6rRY2o%E7%B4%A0%E6%9D%90ab.png)


## 场景3：配置活动对比[](#chang-jing-3-pei-zhi-huo-dong-dui-bi)

> 对比在同一分群，相同投放素材，不同活动（转跳页面）的投放对比。

单击**添加活动对比**

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly2hXtTGw6zsdRYPJiv-Ly3--p8vzQBS0e_BDzl%E6%B7%BB%E5%8A%A0%E6%B4%BB%E5%8A%A8%E5%AF%B9%E6%AF%94.png)


## 实验数据查看[](#shi-yan-shu-ju-cha-kan)

A/B弹窗编辑上线后，该组弹窗将会出现在弹窗列表的 「**实验弹窗**」Tab下，可以点击列表中的弹窗名称，进入到数据报告页，查看到详细数据。对于已上线的A/B弹窗可以在列表页看到两组的数据对比情况（展示、点击和点击率）。

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly2hXtTGw6zsdRYPJiv-Ly30CXTrqNLY5ec-j-G%E5%AE%9E%E9%AA%8C%E5%88%97%E8%A1%A8.png)

以下是不同对比场景详细的数据报表页：


### 控制组对比[](#kong-zhi-zu-dui-bi)

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly2hXtTGw6zsdRYPJiv-Ly3Ar9QmLu0WgkxkqBJ%E6%8E%A7%E5%88%B6%E7%BB%84%E6%95%B0%E6%8D%AE.png)

在测试过程中，可以密切关注弹窗的点击以及活动的效果数据，及时调整活动页。如果达到的预期的效果，可以点击推广该实验，会对该分群全量的发送弹窗（之前收到过的用户不会再收到）。


### 素材对比[](#su-cai-dui-bi)

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly2hXtTGw6zsdRYPJiv-Ly3Ax42J_8NN7iZAIqh%E7%B4%A0%E6%9D%90%E5%AF%B9%E6%AF%94%E6%95%B0%E6%8D%AE.png)

如果不设置转化目标，默认给出两组实验的点击数据，展示数据，方便的进行对比。

如果设置了转化目标，可以对比两个弹窗的转化率。比如 想引导用户去活动详情页，点击某元素参加活动，可以设置该元素的点击事件作为 转化目标。


### 实验迭代数据[](#shi-yan-die-dai-shu-ju)

支持对实验进行迭代，比如经过初步对比，发现实验A组的数据较好，但还没有达到理想的转化效果，此时可以修改实验，通过更改实验 B 的素材，继续进行对比，修改后上线，将会自动成为 实验版本2（实验版本1的数据也将保留），实验B的标示变为B2。

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly2hXtTGw6zsdRYPJiv-Ly3BS-DarKmrOfGXSAz%E8%BF%AD%E4%BB%A3%E6%95%B0%E6%8D%AE.png)


### 在其他分析工具中的使用[](#zai-qi-ta-fen-xi-gong-ju-zhong-de-shi-yong)

我们会在实验弹窗的名称后加上实验版本，如「新人大礼包**-实验组A1**」、「新人大礼包**-实验组B1**」，如果您需要在其他分析工具中使用，请在输入弹窗名称时，加上实验的版本号。如下图所示：

![](/img/assets-Lpwgem-x8KzhBglybzw-Ly3GjgSisrHvDPoQcX2-Ly3LOKuOB3ZVZkcdRxQab%E6%BC%8F%E6%96%97%E5%BA%94%E7%94%A8.png)
