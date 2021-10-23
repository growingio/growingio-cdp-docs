---
id: yu-jing
sidebar_position: 2
---

# 指标预警 (beta)

## 简介[](#jian-jie)

预警可以帮助您及时发现指标异常。您可以在事件分析的图表创建预警，当数据高于或者低于阈值时，您可以收到邮件通知。

## 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

指标预警仅可在事件分析中使用。

## 功能说明[](#gong-neng-shuo-ming)

### 创建预警[](#chuang-jian-yu-jing)

您可以在**已经保存**的单图创建新预警。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MYdzXGwMzDe2Bb-oIBb%2F-MYe-FQglUrBnzLVT6Gp%2F%E9%A2%84%E8%AD%A61.png?alt=media&token=5f76ddc0-cee0-4b9e-a9a7-653620eea290)

点击创建新预警后，您会看到新建预警的弹窗：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MYdzXGwMzDe2Bb-oIBb%2F-MYe-PRGn906FkajVyPh%2F%E9%A2%84%E8%AD%A62.png?alt=media&token=a9894592-4cc3-4399-8489-909fe5e755f2)

您需要填写**预警名称、触发预警的条件** 和 **预警邮件的接收人**。

**预警名称：** 填写您认为具有意义的预警名称，因为预警名称会成为预警邮件标题的组成部分。 邮件接收者可以根据邮件标题判断是否与他相关。

**预警条件：** 预警条件由 预警对象 \+ 预警规则 \+ 阈值构成。如下图

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MYdzXGwMzDe2Bb-oIBb%2F-MYe-Y0LeSWkxegGvMWY%2F%E9%A2%84%E8%AD%A63.png?alt=media&token=f66c5cae-cea1-45ab-a9da-ad4e78996689)

**预警对象：**包括指标和指标对应的过滤条件，如过去7天北京购买人数，即时间范围是过去7天，城市为北京，购买事件的总人数；昨天VIP用户消费金额，即时间是昨天，用户等级为VIP， 缴费金额求和。

注：我们会自动将事件分析的规则填充到预警对象中，事件分析的第一个指标会成为预警的指标，您也可以选择其他指标作为需要预警的指标。

维度会默认选取第一个属性的维度值，您也可以选择其他维度作为需要预警的维度值，全局过滤会直接继承，无法修改。

分群的第一个分群会成为参与指标过滤的分群，您也可以选择其他分群作为参与过滤的分群。

**时间维度：**

如果单图有时间维度（比如线图），那么我们提供对应时间粒度下的最近一个值，以确保当数据出现问题时，直接发送给您。 如果时间粒度是天，那么我们提供最近1天的指标对应数据值。如果时间粒度是周，我们提供最近一周的指标作为监测值。（本期暂不支持小时）

如果单图没有时间维度，那么我们提供对应指标的时间范围的数据作为监测值。

**预警规则：**本期支持大于小于两种预警规则**。**

**阈值：**您可以输入任意数值，包括负数。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MYdzXGwMzDe2Bb-oIBb%2F-MYe-rdgJsXQytvFBU9V%2F%E9%A2%84%E8%AD%A64.png?alt=media&token=a72dfbed-d355-4532-8da0-c8402983eb74)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MYdzXGwMzDe2Bb-oIBb%2F-MYe06mB3qm-GA5ArB24%2F%E9%A2%84%E8%AD%A66.png?alt=media&token=7cb97f38-5c64-4760-92d7-e5d62bbd6b89)

**预警的邮件接收人**：你可以选择或者填写邮箱。

### 预警管理[](#yu-jing-guan-li)

您可以发送邮件给任意邮件地址。检查数据的逻辑：每晚会比较预警对象的数据和阈值数据，不符合预期则发送邮件到指定邮箱**预警管理**入口：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MYdzXGwMzDe2Bb-oIBb%2F-MYe0HCiAI5eWbunsVGh%2F%E9%A2%84%E8%AD%A67.png?alt=media&token=9c05785c-fc20-41a1-b93f-b2d19942484c)

​![](https://growingio.feishu.cn/space/api/box/stream/download/asynccode/?code=MWUzNzhkZTg0M2RiODQ5MTJmYjU0YTMzOTlkNmM4MmNfcWJCbElHQ0FINzI3V1JKNTVMaXBsVjY3VE1GMWVjQ2dfVG9rZW46Ym94Y24ybXNFWnZYNllxMUxyQWFDTmI5aFBkXzE2MTgxOTM1NjU6MTYxODE5NzE2NV9WNA)​

**预警管理页面操作：**

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MYdzXGwMzDe2Bb-oIBb%2F-MYe0UDJMO3oZpylIOit%2F%E9%A2%84%E8%AD%A68.png?alt=media&token=00d6b3c4-f19e-4348-b467-b68aebc429af)

点击预警名称，您可以对预警进行修改，包括预警名称、预警规则、阈值和邮件接收人信息。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MYdzXGwMzDe2Bb-oIBb%2F-MYe1-DyRDToJiH1xyTi%2F%E9%A2%84%E8%AD%A610.png?alt=media&token=17f3adb4-cf1e-4fd8-bf36-11d3a47d0240)

您可以点击分析单图名称进入对应的分析页面。

您可以删除预警，删除后将不会对预警接收人发信息。
