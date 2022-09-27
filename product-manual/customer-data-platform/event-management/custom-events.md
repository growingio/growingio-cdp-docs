---
id: custom-events
sidebar_position: 1
---

# 埋点事件

## 简介[](#jian-jie)

埋点事件作为用户行为分析的数据基础，在您对应用程序或网站进行埋码采集上报数据之前，请先定义好需要采集上报的事件，包括它们的基本信息、属性信息等。

![](/img/assets-M2qbZInaXgdm8kkNosp-MkLvFBmmrT0SdiKh72R-MkLzSSvFYrANEIPwMprimage.png)

## 名词解释[](#ming-ci-jie-shi)

| 信息         | 说明                                                                                                                |
| ------------ | ------------------------------------------------------------------------------------------------------------------- |
| 名称         | 事件在使用过程中的显示名。                                                                                          |
| 标识符       | 事件在系统内的唯一标识符。<br></br>注：仅允许大小写英文、数字、下划线，并且不能以数字开头， 最大长度支持 100 字符。 |
| 类型         | 默认类型为计数器，不可更改。                                                                                        |
| 描述         | 事件的描述，可填写事件的触发时机和应用场景。                                                                        |
| 关联事件属性 | 该事件需要采集的具体信息。<br></br>注：所需属性需要先在事件属性中定义，才能选择。                                   |

## 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

### 重复性约束[](#zhong-fu-xing-yue-shu)

事件的名称和标识符均不可重复

### 预置事件不可编辑[](#yu-zhi-shi-jian-bu-ke-bian-ji)

预置事件是由系统时安装部署时预置好，而无需您去定义的事件。这些事件有的是由客户端 SDK 自动采集上报的事件，有的是系统离线计算的事件，它们均不可编辑、删除。

![](/img/assets-M2qbZInaXgdm8kkNosp-MkLvFBmmrT0SdiKh72R-MkLyHHt7rUd3S7y1vhiimage.png)

## 功能说明[](#gong-neng-shuo-ming)

### 新增/创建[](#xin-zeng-chuang-jian)

通过定义名称、标识符、描述、关联事件属性来完成一条新的埋点事件的定义。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj4GOzneVzxyp0-Oy-B-Mj4ILbHD9AVxcb8SLum.png)

### 查询[](#cha-xun)

已创建的事件默认按照创建时间逆序排列，支持翻页查看，也支持通过名称或标识符检索来查找已定义的事件。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj4GOzneVzxyp0-Oy-B-Mj4KW9tXONtw3a7bW00.png)

点击某事件行，除了可查看事件定义详情外，还可以了解该事件过去 7 天的数量趋势。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj4GOzneVzxyp0-Oy-B-Mj4MIYHaxuClgsljcGG.png)

### 修改[](#xiu-gai)

点击某事件行，在事件详情中，修改事件信息后保存。注：由于标识符是事件的唯一标识，不支持对它的修改。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj4GOzneVzxyp0-Oy-B-Mj4LJ2LNM9DVenIkqm9.png)

### 删除[](#shan-chu)

点击某事件行的操作列的图标，可删除单个事件。也可以在列表中使用复选框选择多个事件，进行批量删除。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj4GOzneVzxyp0-Oy-B-Mj4NJq8LitXy9huxC2U.png)

事件被删除后不可恢复，引用它的看板图表将受到影响，请谨慎操作。

## 应用案例[](#ying-yong-an-li)

以 APP 中常见的用户点击首页顶部轮播图事件为例，来看看埋点事件的定义方法。

首先，明确对于要分析该点击事件的维度，比如：

- 轮播图的位置索引，这样可以统计轮播图各帧的点击率
- 轮播图的图片类型，这样可以统计不同类型的点击率，常用于流量实验场景

其次，在[事件属性](../../../product-manual/customer-data-platform/event-management/event-property)中，先定义出如上两个属性

| 名称     | 标识符          | 类型   |
| -------- | --------------- | ------ |
| 位置索引 | swiper_imgindex | 字符串 |
| 图片类型 | swiper_imgtype  | 字符串 |

最后，定义该事件，并将如上两个属性关联到该事件上。

![](/img/assets-M2qbZInaXgdm8kkNosp-MjChPIe0rCI5X4MaWq8-MjCl2EMk1ZymQ0wEaW0image.png)

## 常见问题[](#chang-jian-wen-ti)

Q1：要定义的事件太多，支持批量定义吗？

在[批量工具](../../../developer-manual/toolbox/metadata-creator)中，支持上传模板文件，将事件及其属性的 CSV 文件上传进行批量创建。
