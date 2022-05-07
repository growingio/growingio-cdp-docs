---
id: kpi
sidebar_position: 3
---

# KPI 分析

## 简介[](#jian-jie)

KPI 分析可以帮助业务负责人在 GrowingIO 平台上监控 KPI 数据，判断 KPI 是否符合预期。若数据与预期不符，用户可以借助维度拆解和下钻，迅速找到影响 KPI 表现的原因。

功能包括：

* 趋势对比：指标趋势，以及时间范围内的同环比计算
    
* 维度拆解：基于不同维度的拆解，如根据维度拆解变化量和变化率指标
    
* 维度下钻：支持基于不同维度的下钻分析
    
* 变化洞察：支持 KPI 波动主要影响因子的洞察分析
    

## 名词解释[](#ming-ci-jie-shi)

KPI（Key Performance Indicator）即关键绩效指标，是企业内关键业务表现的衡量方式。在 GrowingIO 增长平台内，常把 “用户量“，“销售额“ ，“购买转化率“ 等用户、业绩相关的核心指标应用在 KPI 分析中进行监控和分析。

## 功能边界和约束[](#gong-neng-bian-jie-he-yue-shu)

支持埋点事件和预定义指标的分析，不支持无埋点事件。

## 功能说明[](#gong-neng-shuo-ming)

### 创建 KPI 分析[](#chuang-jian-kpi-fen-xi)

1. 在导航栏选择“**分析模型 > KPI分析**"，进入 KPI 分析。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj3mziM6kQhkAXytmTW-Mj48wXYKybSP-88wmHFimage.png)

KPI 分析入口

2. 点击 KPI 分析列表页右侧的“**++ 新建KPI分析”**按钮，进入创建页面。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj3mziM6kQhkAXytmTW-Mj4AbKoxKWOQY930c3E%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-09-08%20%E4%B8%8B%E5%8D%887.32.25.png)

创建 KPI 指标页面

| 参数  | 说明  |
| --- | --- |
| 时间范围 | 可选择今天、本周、本月监控KPI指标。* 若您选择今天，可以看到今天的小时级别数据，如果您对某一个指标的关注度是每小时都会看一看，或者每半天都会看一下，建议选择今天。* 若您选择本周（包括今天），可以看到本周的天级别数据，如果您对某一个指标的关注度是每天都会看一看，周末会做一个总结报告，建议选择本周。* 若您选择本月（包括今天），可以看到本月天级别的KPI数据，如果您对某一个指标的关注度是每天或者每周都会看一看，月度会做一个总结报告，建议选择本月。 |
| 目标用户 | 设置目标人群，以便了解特殊人群的KPI表现，如重新购买、新注册等。 |
| KPI指标 | 选择KPI指标。KPI 由事件、事件的度量方式（人、次、人均）和过滤条件构成，以下指标都可以是 KPI：购买人数、购买次数、平均购买次数、购买金额、手机购买量等。他可以借助事件 “购买“，“购买”事件的度量方式 人、次、人均，事件的变量：金额、品类等组合构成。 |

3. 填写完成后单击**保存**，完成一个 KPI 分析的创建。

### 设置 KPI 目标[](#she-zhi-kpi-mu-biao)

您可以对 KPI 设置目标，以便观察目标进度是否符合预期。

在 KPI 分析列表中，点击单个KPI指标右侧“操作“列的 “![](/img/-Lo08UtW7H58ehFKeZ4g-LugKRBPNPab7MdZtndt-LugeasN0wzG5aPiGtgoKPIE79C8BE69DBFE782B9E782B9E782B9.png)“ 选择编辑，在编辑页面设置目标值。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj3mziM6kQhkAXytmTW-Mj4CQhjZUnYgHzj2uXcimage.png)

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj3mziM6kQhkAXytmTW-Mj4Di9Ea5wlpb9GzGu8%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-09-08%20%E4%B8%8B%E5%8D%887.45.46.png)

设置目标值页面

设置完成后即可在看板中的单个 KPI 图右下角查看目标值和完成率。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj3mziM6kQhkAXytmTW-Mj4IbWKLHkyi_rhwfGg%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-09-08%20%E4%B8%8B%E5%8D%888.07.30.png)

KPI 分析展示

#### 监控 KPI 表现[](#jian-kong-kpi-biao-xian)

将 KPI 分析添加到看板后，可持续监控 KPI 指标的表现。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj3mziM6kQhkAXytmTW-Mj4It6xcTNyKn5X__MFimage.png)

KPI 分析在看板中的展示

一个 KPI 分析卡片包含以下6个元素：

| 元素  | 说明  |
| --- | --- |
| 标题  | 我们默认用了事件名称来指代标题，您可以通过 KPI 分析列表页右侧的操作按钮进行编辑。建议标题设置一定要简单明了，所有人看到标题后就能明白它的业务含义。 |
| 时间范围 | 考察 KPI 的时间范围，一般情况下公司用今天、本周、本月来看 KPI 的表现。在编辑时您可以更灵活地选择时间。 |
| 同比  | 同比是一个业务概念，是基于业务周期的定义。对比规则：本周比上周、本月比上月、今年比去年。如果今天是周三，那么本周比上周就是本周一至周三的数据比上周一至周三的数据。 |
| 环比  | 定义为这个N天比上个N天。比如：今天比昨天，过去7天的数据比过去8 -14天数据，环比更关注业务的连续性。 |
| 目标  | 给予所选时间范围和粒度的目标。比如本周目标、本月目标等。对于所选时间范围和粒度的 KPI 您可以设定对应的目标。注：当所选时间范围发生变化时，目标需要重新填写。 |
| 目标完成率 | 实际 KPI 表现/目标值，您可以借助目标完成率来追踪进程是否符合预期。 |

#### 分析 KPI 波动[](#fen-xi-kpi-bo-dong)

当您发现 KPI 表现不符合预期时，点击 KPI 卡片进入 KPI 详情页，详情页将帮助您快速定位数据波动的原因。

KPI详情页构成：

![](/img/assets-M2qbZInaXgdm8kkNosp-M3drdF8rGIEP7RdyLCx-M3dubXK0XS9yCictplUimage.png)

KPI详情页

| 项   | 说明  |
| --- | --- |
| 1-时间范围与粒度 | 灵活选择事件与粒度。 |
| 2-用户范围 | 更改目标人群。 |
| 3-趋势图 | 趋势线图，帮助您监测 KPI 趋势与波动状况。 |
| 4-变化洞察 | 基于您关注的业务维度，直接呈现 KPI 变化的主要影响因子。快速理解导致数据波动的核心原因。 |
| 5-维度拆解 | 您可以按照业务维度对您的 KPI 进行拆解，找到 KPI 变化的影响因子。同时提供不同业务维度下的数据变化量与变化率。 |
| 6-选择下钻维度 | 单击维度列单元格可以对维度进行下钻。可以根据您的业务思路，不断拆解下钻找到最小粒度的原因。 |
| 7-展示条数 | 设置图表中展示的维度条数。 |

## 应用案例[](#ying-yong-an-li)

**以某电商公司直播带货的 KPI 监控为例：**

我们将直播GMV、预约开播提醒人数、直播观看人数、直播商品点击、直播商品加车次数等核心业务数据放在看板中。您打开看板后，借助 KPI 卡片图，所有核心指标表现一览无余，帮您迅速了解整体表现和有异常的 KPI。

比如，我们可以看到下图中 **直播GMV** 这个 KPI 出现了波动，同比下降24.6%、环比下降28.2%。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj3mziM6kQhkAXytmTW-Mj4MLeRv8DTqcpcMvlB%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-09-08%20%E4%B8%8B%E5%8D%888.23.37.png)

此时，我们可以点击该 KPI 分析卡片，在 KPI 分析详情页了解不同维度下直播 GMV 的变化状况，迅速判断业务指标下降原因。KPI分析包含以下功能：

* 自定义维度拆分
    
* 自动业务分析
    

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj3mziM6kQhkAXytmTW-Mj4Ma730IapAfyX4O6Y%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-09-08%20%E4%B8%8B%E5%8D%888.24.34.png)
