---
id: retention-analysis
sidebar_position: 8
---

# 留存分析

## 简介[](#jian-jie)

留存，顾名思义，就是用户在您的产品中留下来、持续使用的意思。

留存为什么重要？留存是 AARRR 模型中重要的环节之一，只有做好了留存，才能保障新用户在注册后不会白白流失。有时候我们光看日活（DAU），会觉得数据不错，但有可能是因为近期有密集的推广拉新活动，注入了大量的新用户，但是留下来的用户不一定在增长，可能在减少，只不过被新用户数掩盖了所以看不出来。这就好像一个不断漏水的篮子，如果不去修补底下的裂缝，而只顾着往里倒水，是很难获得持续的增长的。

一般我们讲的留存率，是指「目标用户」在一段时间内「回到网站/App 中完成某个行为」的比例。常见的指标有次日留存率、七日留存率、次周留存率等。比如：某个时间获取的「新用户」 的 「次日留存率」常用来度量拉新效果。

在 GrowingIO 的留存分析工具中，您可以灵活地自定义「目标用户」，设置特定的 「起始行为」和 「留存行为」，来观测目标用户的留存情况。


## 名词解释[](#ming-ci-jie-shi)

留存分析：用来分析用户参与业务情况的模型，计算进行初始行为后的用户，经过指定时间周期后，仍然使用该业务的用户。


## 功能说明[](#gong-neng-shuo-ming)

### 创建留存分析[](#chuang-jian-liu-cun-fen-xi)

一、在顶部导航栏选择“**分析 > 产品分析 > 留存分析**"，进入留存分析看板。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3eHOvwJqiGSbT-4TFf%2F-M3eHfOJ3kYLOsLyLzgS%2Fimage.png?alt=media&token=2b004d7a-8778-4898-820e-09857980c137)

留存分析看板

二、单击左侧列表上方"**新建分析 > 留存分析"**或单击事件分析看板中“**+”**，进入**创建留存分析**页面。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3eHodoqUhqtLkonYT_%2F-M3eKOzaPi3YntpSs9kQ%2Fimage.png?alt=media&token=e86946f1-9c64-4e1a-946d-d6b9b0b34b49)

创建留存分析页面

| 项   | 说明  |
| --- | --- |
| 1-起始行为 | 起始行为是对目标用户起始行为的限定。比如，如果要观测新用户查看过商品详情之后的留存率是否会有明显提升，那么起始行为可以设定为 "查看商品详情"。 |
| 2-留存行为 | 对目标用户留存行为的限定。某个目标用户完成了起始行为之后，在后续日期完成了特定留存行为，则留存人数 +1；如果某目标用户只完成了起始行为，没有完成相应的留存行为，则留存人数 +0 。 |
| 3-事件过滤 | 起始行为和终止行为支持事件过滤 |
| 4-目标用户 | 目标用户是设定要观测的目标用户人群。比如，要观测新访问用户的留存，那目标用户就设定为新访问用户。 |
| 5-维度对比 | 对起始行为进行维度细分。例：用 "城市"维度对比，会给出不同城市下完成起始行为的用户数量。 |
| 6-用户对比 | 对比不同的目标用户群体的留存表现。例：可以对比新用户和全部用户在特定行为上的留存，辅助判断新用户的留存情况。 |
| 7-行为对比 | 起始行为与留存行为相同，可对比不同行为对用户留存的影响。 |
| 8-留存展示 | 支持用户留存和留存率变化2种展示方法。 |
| 9-时间 | 起始行为的日期范围，最长支持365日的留存，最远日期为该项目生效日期开始。默认值：过去 14 天，代表的起始行为发生的时间范围是过去 14 天，对应留存表中的 "用户量"就是目标用户在过去 14 天做过起始行为的用户量。 |
| 10-留存周期 | 日留存：是指按自然日统计完成起始行为目标用户量并按天来观测后续每天的留存情况，适用时间范围：[1，120]天；周留存：是指按自然周统计完成起始行为目标用户量并按周来观测后续每周的留存情况，适用时间范围：[14，180]天；月留存：是指按自然月统计完成起始行为目标用户量并按月来观测后续每月的留存情况，适用时间范围：[30，365]天。特别说明：日/周/月颗粒度的切换与起始行为日期范围有关；比如，如果选择了过去 7 天，那么我们不提供按照周和月颗粒度来查看留存曲线，因为还没有完整一周或一个月的数据用来观测留存，远不如按日留存直观有效。 |

三、选择参数后，右侧即可实时展示分析图表。

四、单击右上角保存，完成一个留存分析的创建。


### 解读留存分析[](#jie-du-liu-cun-fen-xi)

留存图中的数据是根据留存表来绘制的，我们针对留存表来说明一下数据统计口径。首先，需要明确的是，留存表中的每个绝对值，指的都是人数。

下面，我们把留存表分成 "汇总行"和"日期行"：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3egu9H4doH8J97LS5t%2F-M3ejqmlYkA0dvyUi4pP%2Fimage.png?alt=media&token=43556ab5-f730-4bbc-9742-7505d6134aed)

"汇总行"的数据是依据 "日期行"的数据来计算的。下面具体解读一下：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3egu9H4doH8J97LS5t%2F-M3ejopcuXbhd_g3os_i%2Fimage.png?alt=media&token=9e0dd276-bbc9-43e6-b23d-dbb5c695ad63)

**5722：**这个是日期行的 "用户量"一列，代表的是 9 月 18 日，"目标用户"中完成"起始行为"的用户量，这是后续用户留存的基数。图中给出的 "日颗粒度"，如果是周颗粒度，那么这个单元格中的用户量是当前自然周的获取的用户去重得到的独立用户量。

**26.9%：**这个是日期行的留存率图中的留存率数据。

Tips 给出了统计口径；5722 个满足起始行为的用户，有 1537 个用户在第二天(09月/19日)完成了留存行为。次日留存率的计算：

26.9% = 1537（人）/5722（人）

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3egu9H4doH8J97LS5t%2F-M3ejjkK65pWeXznenvl%2Fimage.png?alt=media&token=2ff6ae99-0b65-4c79-82a5-373d8408d900)

**117012：**这个是汇总行 "用户量"列。是日期行每一行的 "用户量"数据直接算数相加得到的，没有做去重。**需要特别注意，这个数据不是在选定的时间范围内的实际用户量，因为这个数据没有去重。**

**12.2%：**这个是汇总行的留存率数据。这个留存率数据是日期行每一行数据加权平均得到的。

具体算法是：

12.2% = 每个日期行 "3日后" 列的用户量算数相加/ 对应每个日期行 "用户量" 列的用户量算数相加

为了更好地理解计算口径，下面是一个示例：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3egu9H4doH8J97LS5t%2F-M3ejduDmlZ68GyaPc67%2Fimage.png?alt=media&token=7c616eaf-b59c-4dbc-8a44-d1d8e990412b)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MDIN0ScxdJLg7ZtVis_%2F-MDIxqY-zVvQXhL8GhvR%2Fimage.png?alt=media&token=bfead6ca-d0d7-4d0e-acf0-d359acc048a8)

点击留存详情可以下载除了汇总行之外的用户ID，例如您可以下载未留存的用户进行召回。

点击留存详情可以创建除了汇总行之外的用户分群，分群生成成功后您可以查看分群的画像。


### 视图介绍[](#shi-tu-jie-shao)

用户留存视图

留存率趋势视图

用户留存视图

用户留存视图给出的是一段时间内获取的用户后续留存情况；

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3egu9H4doH8J97LS5t%2F-M3ekc0sUDHOSJSYndQ0%2Fimage.png?alt=media&token=0e8261f1-d594-4964-ba0b-785a8ec7cf38)

日留存

* 横坐标：相对日期；日留存颗粒度下，给出的是当日、次日、2日后...n 日后；留存率曲线会随着相对日期的推移而衰减，理想情况下会稳定在一定的留存率不再衰减。如果留存率一直衰减下去接近0，说明这个产品/功能本身没有被用户认可，没有给用户带来价值。
    
* 次日/周/月留存：是指一段时间内获取的用户，在接下来的一个周期的留存情况；留存率越高，说明留下来的用户越多；留存率越低，说明留下来的用户越少。
    
* 留存曲线长期趋势：
    
    * **曲线稳定**：推着时间的推移，我们期望留存率会稳定在某个值。留存率曲线平滑稳定下来，说明有一部分用户稳定地留下来使用对应的产品/功能，对应地反映了产品/功能的价值；
        
    * **曲线一直衰减**：如果留存曲线随着时间的推移一直衰减而不能平滑稳定下来，说明我们度量的这个产品/功能没有得到用户的认可，基本上没有人在使用这个产品/功能。
        
留存率趋势视图

用户留存率趋势给出特定留存率（比如：次周留存率）随时间（绝对日期坐标）的变化。

比如，新用户次周留存率趋势可以辅助判断获客策略，好的获客策略会带来新用户次周留存率的稳定或提升。

另外我们在留存趋势视线图下，提供转置table的形式展示留存率。根据您选择的时间周期和显示留存率的时间粒度，显示留存率。表格的每列为具体每天或者某个时间区间下的留存率，每行为具体周期内的留存率。

**例：**下图为在选择了周期为过去 14 天，显示粒度为日留存下的留存率具形式展现。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3egu9H4doH8J97LS5t%2F-M3el29lXgXgZp-qcpc-%2Fimage.png?alt=media&token=b48f85bc-949b-4d0e-9abd-7c40633a9385)

日/周/月颗粒度下，我们提供如下的留存率趋势：

| 颗粒度 | 留存率 |
| --- | --- |
| 日   | 次日留存率、7日留存率、14日留存率、30日留存率 |
| 周   | 次周留存率、2周留存率、3周留存率、4周留存率 |
| 月   | 次月留存率、2月留存率、3月留存率 |

* 以 "日留存"颗粒度为例，留存图中的横坐标和留存率趋势曲线和留存表的对应关系如下图。
    
![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3egu9H4doH8J97LS5t%2F-M3elJeKTbdeTwPu1kqP%2Fimage.png?alt=media&token=9d3286ba-f729-4f41-9b9c-8c8b50a544c6)

* 以“周留存”颗粒度为例，过去90天的留存率变化趋势图，不同颜色代表不同的不同的阶段留存率。
    
![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3egu9H4doH8J97LS5t%2F-M3elNKMzoDnlH_ykmHD%2Fimage.png?alt=media&token=17875991-1fd5-4c23-b108-6358ed5f3b18)

新增的「留存率」视图下留存表与在「用户留存」下的留存表(除去表中的第一行“全部访问用户”的数据)对应关系如下：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3egu9H4doH8J97LS5t%2F-M3elSTA3EWzlVaA3YjC%2Fimage.png?alt=media&token=0daaf461-4a1d-4368-b6d0-6c8bad85da8f)

同样地，您可以根据具体业务需求灵活的切换时间与显示粒度。

### 留存分析看板[](#liu-cun-fen-xi-kan-ban)

留存分析看板与分析看板的管理方式相同，请参考看板管理。

## 常见问题[](#chang-jian-wen-ti)

一、留存分析中在留存趋势细节表中切换天、周留存，为什么显示用户数不同？[](#1-liu-cun-fen-xi-zhong-zai-liu-cun-qu-shi-xi-jie-biao-zhong-qie-huan-tian-zhou-liu-cun-wei-shi-mo-xian-shi-yong-hu-shu-bu-tong)

造成用户数差异的原因有：

1.  周留存分析时会根据设置的时间范围调整到自然周，比如设置的时间为周三，在分析周留存的时候会自动从当周的周一开始分析。所以周留存和天留存的统计时间范围可能是不同的。
    
2.  周留存中的用户数表示当周做过起始行为的用户，如果用户在当周的三天做过起始行为，在天留存表中会表示为三个用户，而在周留存表中会表示为一个。
    

二、查看留存的时候，如何区分 iOS 和Android呢？[](#2-cha-kan-liu-cun-de-shi-hou-ru-he-qu-fen-ios-he-android-ni)

可以在「维度对比」里，选择不同的平台。
