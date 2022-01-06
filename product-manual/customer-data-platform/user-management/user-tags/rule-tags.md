---
id: rule-tags
sidebar_position: 3
---

# 创建规则标签











### 创建用户标签[](#chuang-jian-yong-hu-biao-qian)

一、在**客戶数据平台 > 数据 > 标签管理**“，进入标签管理页面。

二、单击右上角**添加标签**，进入**新建标签**弹窗。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaXKLTn1rbjJDdF9USQ%2F-MaXjQj81hnrY5iiT4UX%2Fimage.png?alt=media&token=a55135e4-b227-43e0-97e8-6ebdbd930038)

选择标签类型后，第一步需要定义标签的名称、标识符、描述 等信息。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaXKLTn1rbjJDdF9USQ%2F-MaXkkU6-BQpn4xllWFZ%2Fimage.png?alt=media&token=52fb390f-5717-4f1a-a3e3-535133c41225)

第二步需要定义标签计算规则，详情请参考五种规则标签说明。

三、根据业务需求选择需要创建的标签类型，配置完成后，单击保存，完成一个标签的创建。


#### 基础指标值[](#ji-chu-zhi-biao-zhi-1)

控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaWT8g4phN_UqWQQthL%2F-MaX7r5FZlB_gIjpWI8V%2Fimage.png?alt=media&token=e75280d8-3ff0-4ff6-aa7a-86cac573c9d9)

| 项   | 说明  |
| --- | --- |
| 1.选择时间 | 如过去7天、过去30天、过去90天等 |
| 2.选择事件 | 如全局指标(访问、活跃)、埋点事件和计算指标 |
| 3.选择属性 | 如次数、天数、埋点事件的整数、小数、字符串类型事件属性 |
| 4.选择计算模型 | 如累计值、平均值、占比、去重数 |
| 5.选择事件过滤 | 选择事件过滤条件 |

由于属性的数值类型不同，支持的计算模型对应关系如下：

| 属性  | 累计值 | 平均值 | 占比  | 去重数 |
| --- | --- | --- | --- | --- |
| 次数  | ✔️  | ​   | ✔️  | ​   |
| 天数  | ✔️  | ​   | ​   | ​   |
| 整数、小数类型事件属性 | ✔️  | ✔️  | ✔️  | ​   |
| 字符串类型事件属性 | ​   | ​   | ​   | ✔️  |


#### 最大值/最小值的事件属性[](#zui-da-zhi-zui-xiao-zhi-de-shi-jian-shu-xing-1)

控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaX8gmlITGn2zTUPjta%2F-MaX955wpjSxFGygI76a%2Fimage.png?alt=media&token=8fbc6d27-1014-4ca2-8649-3cd9daeaa64e)

| 项   | 说明  |
| --- | --- |
| 1.选择时间 | 如过去7天、过去30天、过去90天等 |
| 2.选择事件 | 如全局指标(访问、活跃)和埋点事件 |
| 3.选择分组属性 | 如次数和埋点事件的整数、小数类型事件属性 |
| 4.选择计算模型 | 如最多、最少 |
| 5.选择打标属性 | 如埋点事件的字符串类型事件属性 |
| 6.选择事件过滤 | 选择事件过滤条件 |


#### 首次/末次的事件属性[](#shou-ci-mo-ci-de-shi-jian-shu-xing-1)

控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaX9FEkMV4TtU-ccU95%2F-MaX9iiMNQsxpX2ETO5e%2Fimage.png?alt=media&token=291e868d-4faa-4109-b910-f6711c2a890c)

| 项   | 说明  |
| --- | --- |
| 1.选择时间 | 如过去7天、过去30天、过去90天等 |
| 2.选择计算模型 | 如最初、最终 |
| 3.选择事件 | 如全局指标(访问、活跃)和埋点事件 |
| 4.选择属性 | 如距今天数、日期和埋点事件的字符串类型事件属性 |
| 5.选择事件过滤 | 选择事件过滤条件 |


#### 列表类的事件属性[](#lie-biao-lei-de-shi-jian-shu-xing-1)

控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaXAPPPHyRVJTXO1Z3e%2F-MaXAllgogkiDLxjhel7%2Fimage.png?alt=media&token=55832063-b163-4e10-9543-6a4bce4ac464)

| 项   | 说明  |
| --- | --- |
| 1.选择时间 | 如过去7天、过去30天、过去90天等 |
| 2.选择事件 | 如全局指标(访问、活跃)和埋点事件 |
| 3.选择属性 | 如埋点事件的字符串类型事件属性 |
| 4.选择事件过滤 | 选择事件过滤条件 |


#### 分层标签[](#fen-ceng-biao-qian-1)

控件说明:
* 用户行为
    * 做过
    * 未做过
* 用户属性
    * 用户是


![图 1](/img/9a3fa2b94ae53b6f3c33f6ae3090d485e8e318b2ec6fc83369305adf19bdb903_pic_1639999256652_2021-12-20.png)  


**SQL标签**

控件说明：‌

* 支持选择数值类型
    
* 支持写入SQL规则
    
![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiQNGh3wdzlC8uur13S%2F-MiQObm0w2zbwDsZsT_e%2Fimage.png?alt=media&token=37910440-3c54-4a19-b1a8-192d882e4eb5)