---
id: metric-management
sidebar_position: 1
---

# 指标管理

## 简介

在制作单图，搭建分析看板过程中，经常会遇到一些需要在各处复用的、口径一致的指标，比如GMV、CTR、ARPU等，为了提高协作效率，我们可以在指标管理中，把这些复用性强的指标管理起来，以便于在制作图表过程中可以快速引用它们。

## 功能边界或约束
考虑到指标在统计查询中的性能，GrowingIO对创建指标的复杂度做了限制，具体是：

- 指标依赖的事件数量不超过10个
- 指标中的每个事件的过滤条件数量不超过5个

## 功能说明

指标管理的访问入口：【项目XXX】 - 【数据管理】 - 【指标管理】

### 创建指标

![image.png](https://cdn.nlark.com/yuque/0/2021/png/25447572/1639051713050-8587bd83-23f0-425d-bdb9-ea2239971d30.png#clientId=u5fec0028-7b00-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=429&id=ucb8e31b8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=858&originWidth=1443&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36770&status=done&style=none&taskId=u9102ff89-ba2f-4f85-a1de-6abda87e819&title=&width=721.5)

| 项目     | 含义                                                                                                 |
|----------|------------------------------------------------------------------------------------------------------|
| 名称     | 要创建指标的名称                                                                                     |
| 描述     | 要创建指标的描述                                                                                     |
| 运算指标 | 指标的运算项，支持选择事件+度量+过滤条件。每个运算项都有对应的英文大写字母，作为计算公式中引用的代号 |
| 计算公式 | 指标的四则运算公式，引用运算指标中各运算项的英文字母代号做计算                                       |
| 展示     | 指标结果的展示格式，可选项百分比、两位小数和取整                                                     |

### 编辑指标

对于已创建的指标，支持您再次编辑。

具体操作是点击某行指标，在详情页中点击“编辑”按钮，即可进入编辑弹窗。

![image.png](https://cdn.nlark.com/yuque/0/2021/png/25447572/1639131156512-2d01fc66-643a-4d8e-a371-198b3b1d8b7c.png#clientId=u0af89b97-ded7-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=394&id=u31257607&margin=%5Bobject%20Object%5D&name=image.png&originHeight=788&originWidth=1916&originalType=binary&ratio=1&rotation=0&showTitle=false&size=61901&status=done&style=none&taskId=ufaa10bac-c3bd-4a84-8aa0-f8f80b06344&title=&width=958)

### 删除指标

对于已创建的指标，如果不再使用需要删除，可点击某指标行的操作列，在弹窗中点击“删除”按钮，即可删除该指标。

![image.png](https://cdn.nlark.com/yuque/0/2021/png/25447572/1639107786329-dc15ee77-122a-4300-91d8-37f246cd93bf.png#clientId=ub6504370-0573-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=192&id=ud1745e32&margin=%5Bobject%20Object%5D&name=image.png&originHeight=383&originWidth=1920&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33674&status=done&style=none&taskId=u6af8c69e-5de8-4669-8ede-783297f4e78&title=&width=960)

### 切换预置指标

GrowingIO预置了常用指标，以便于您快速上手，具体操作是点击页面上的“预置”按钮，表格中的内容即展示预置的指标。预置指标的含义、口径等详情请见附录。

![image.png](https://cdn.nlark.com/yuque/0/2021/png/25447572/1639107907262-dad01723-acbc-4492-944b-0439b22ee973.png#clientId=ub6504370-0573-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=517&id=u196ea112&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1034&originWidth=1967&originalType=binary&ratio=1&rotation=0&showTitle=false&size=61606&status=done&style=none&taskId=ub517ebf3-5e3a-4fbb-95c4-c4c6e01ecf4&title=&width=983.5)

## 应用案例

### 案例：电商平台计算付费客户的人均日消费

假设埋点了订单支付事件payOrder，该事件关联了事件属性支付金额（pay_amount，小数类型），可以创建一个指标ARPU来表征付费客户的人均日消费，创建指标的表单内容如下：

![image.png](https://cdn.nlark.com/yuque/0/2021/png/25447572/1639112089578-b6ec5a62-d8ab-4261-87b3-01ad6d000036.png#clientId=ub6504370-0573-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=431&id=u2483158b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=861&originWidth=1449&originalType=binary&ratio=1&rotation=0&showTitle=false&size=34760&status=done&style=none&taskId=u373097c1-f685-4303-9096-216941fe353&title=&width=724.5)

## 常见问题

### Q：是否支持创建项目间可复用的全局指标？

A：暂不支持。

## 附录：预置指标

| 指标名称           | 含义描述                                              | 计算口径                        | 查询语句                                                                                          |
|--------------------|-------------------------------------------------------|---------------------------------|---------------------------------------------------------------------------------------------------|
| 用户量             | 网站、App、小程序上有过任意行为的独立用户数量         | 任意事件的总人数                | select count(distinct gio_id) <br/>from event <br/>where event_key='$anyevent'                  |
| 页面浏览量         | 用户实际浏览过的网页数量                              | 页面浏览的总次数                | select count(1)<br/>from event <br/>where event_key='$page'                                     |
| 访问量             | 访问事件的数量                                        | 访问的总次数                    | select count(1)<br/>from event <br/>where event_key='$visit'                                    |
| 每次访问页面浏览量 | 用户平均每次进入网站/APP/小程序所带来的页面浏览的数量 | 页面浏览的总次数 / 访问的总次数 | select sum($page_count)/count(1) from event <br/>where event_key='$visit'                        |
| 人均访问次数       | 用户平均进入网站/APP/小程序的次数                     | 访问量 / 访问的总人数           | select count(1)/count(distinct gio_id)<br/>from event<br/>where event_key='$visit'              |
| 总访问时长         | 所有访问的总时长                                      | 访问的时长的总和                | select sum($duration)<br/>from event<br/>where event_key='$visit'                               |
| 平均访问时长       | 所有访问的平均时长                                    | 访问的时长的平均值              | select sum($duration)/count(1)<br/>from event<br/>where event_key='$visit'                      |
| 跳出次数           | 访问中仅浏览1个页面就离开的访问次数                   | 访问跳出的总次数                | select count(1)<br/>from event<br/>where event_key='$bounce'                                    |
| 跳出率             | 只有1个页面浏览的访问占所有访问的比率                 | 跳出次数 / 访问量               | select count(if(event_key='$visit',1,null))/count(if(event_key='$bounce',1,null))<br/>from event |
| 总页面停留时长     | 所有页面浏览的总时长                                  | 页面浏览的时长的总和            | select sum($duration)<br/>from event<br/>where event_key='$page'                                |
| 平均页面停留时长   | 所有页面浏览的平均时长                                | 页面浏览的时长的平均值          | select sum($duration)/count(1)<br/>from event<br/>where event_key='$page'                       |
| 退出次数           | 用户退出网站/App/小程序的数量                         | 访问退出的总次数                | select count(1)<br/>from event<br/>where event_key='$exit'                                      |

