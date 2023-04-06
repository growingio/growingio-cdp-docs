---
id: user-tags
sidebar_position: 5
---

# 用户标签

## 用户标签详情页[](#yong-hu-biao-qian-xiang-qing-ye)

面向业务运营人员，在用户标签详情页可以查看单一 **用户标签** 的名称、数值类型、创建人、创建日期和统计分布。

![](/img/用户洞察-用户标签.png)

您也可以对用户标签进行以下操作：

| 操作 | 步骤 | 限制条件 |
| -- | -- | -- |
| 搜索 | 您可以在搜索框中根据 **用户标签名称** 搜索用户标签 | 无 |
| 下载 | 您可以点击 **下载** 下载用户标签统计分布数据 | 无 |
| 分析设置     | 对于数值及日期类型的用户标签，可以通过自定义分组，进行灵活分析。     | 小数型、整数型、日期型 标签      |
| 极端值设置     | 对于数值类型的用户标签，可以剔除1%-10%的极端值后，再查看分析结果。     | 日期型 标签      |

> 空间内仅支持查看和使用数据授权的用户属性，详情请参见[数据授权](../../product-manual/enterprise-management/project-manage/data-authorization)。

### 分析设置

默认按离散数据进行分布，可切换为默认区间或自定义区间
![图 5](/img/032415183cf397f0a4d8d008ce1b8d26c51967dc69504d2274a9341e48d205f0.png)  

| 选择区间     | 详细说明                                                   |  |
| -------- | ------------------------------------------------------ | -------- |
| 离散数值     | 即没有区间，将按照标签自身的离散数值进行分布 |      |
| 默认区间     | 系统会依据智能算法计算出该标签的最佳的区间分组 |    |
| 自定义区间     | 可根据业务需求对数值分段随时进行自定义，第一个区间左开右开，其他区间均是左闭右开  |    |

### 极端值设置

默认保留极端值进行计算，可剔除一定比例的极端值
![图 6](/img/7c6320072f32ff6dc164fd3810ed62957c32128218e15e35a7adc4d77750b8f6.png)  

| 选择剔除方式     | 详细说明                                                   |  |
| -------- | ------------------------------------------------------ | -------- |
| 保留极端值     | 将全局数据展示在图表汇中 |      |
| 按百分比剔除极端值     | 默认数据对称分布，将百分比折半后选择部分极大和极小数据作为极端值剔除 |    |
> 剔除极端值常用于配合箱线图进行分析