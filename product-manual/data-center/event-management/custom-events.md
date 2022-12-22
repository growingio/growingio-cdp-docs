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
| 标签         | 事件的标签，支持设置多个标签，以便于通过标签对事件进行分组和过滤等操作                                                                                        |
| 描述         | 事件的描述，可填写事件的触发时机和应用场景。                                                                        |
| 关联事件属性 | 该事件需要采集的具体信息。<br></br>注：所需属性需要先在事件属性中定义，才能选择。                                   |

## 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

### 重复性约束[](#zhong-fu-xing-yue-shu)

事件的名称和标识符均不可重复

### 预置事件的编辑范围[](#yu-zhi-shi-jian-bu-ke-bian-ji)

预置事件是由系统时安装部署时预置好，而无需您去定义的事件。这些事件有的是由客户端 SDK 自动采集上报的事件，有的是系统离线计算的事件，它们的名称、标识符、类型和描述不可编辑，仅可以添加或调整关联的自定义事件属性。另外，预置事件不能被删除。

![](/img/assets-M2qbZInaXgdm8kkNosp-MkLvFBmmrT0SdiKh72R-MkLyHHt7rUd3S7y1vhiimage.png)

## 功能说明[](#gong-neng-shuo-ming)

### 新增/创建[](#xin-zeng-chuang-jian)

通过定义名称、标识符、描述、关联事件属性来完成一条新的埋点事件的定义。

![picture 2](/img/5b7302218a7a3da6db58f5ace9a25cac8a2904a9731925c2ba79d729c2b30056_pic_1663661303299_2022-09-20.png)

### 查询[](#cha-xun)

已创建的事件默认按照创建时间逆序排列，支持翻页查看，也支持通过名称或标识符检索来查找已定义的事件。

![picture 3](/img/467a85cf510803281c97b70b1237ddb88308b815206f9d1a26a6ad8c34a66b3f_pic_1663661577850_2022-09-20.png)

点击某事件行，除了可查看事件定义详情外，还可以了解该事件过去 7 天的数量趋势。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mj4GOzneVzxyp0-Oy-B-Mj4MIYHaxuClgsljcGG.png)

### 修改[](#xiu-gai)

点击某事件行，在事件详情中，修改事件信息后保存。注：由于标识符是事件的唯一标识，不支持对它的修改。

![picture 4](/img/d62bacec9043a42df8eb96a2e99852e3c0cf508265866157e7cbc0edf8c5c16a_pic_1663661613110_2022-09-20.png)

### 删除[](#shan-chu)

点击某事件行的操作列的图标，可删除单个事件。也可以在列表中使用复选框选择多个事件，进行批量删除。

![picture 5](/img/7c4daca9c05f3766186c0744f5b2599fbaf064ed533f109678be3ffb6dc46a63_pic_1663661696415_2022-09-20.png)

![picture 6](/img/9d71787ce33bd0e4ce871832de4f741c89cea5ea9bc3876614133da73a1bc2cd_pic_1663661744740_2022-09-20.png)

事件被删除后不可恢复，引用它的看板图表将受到影响，请谨慎操作。

### 批量打标[](#shan-chu)

选择一行或多行事件，点击“批量打标”按钮，弹出窗口可以给所选事件增加多个标签。

![picture 2](/img/92f1c3173a9c66ae0ab15cc4490acc895da520a1c3bb032fa631ee0c71eae7e6_pic_1667299248380_2022-11-01.png)  

![picture 3](/img/e04a4064523c0e89a24e3d0f4337cc5c2ec9a6cbc41bd662c107466817004836_pic_1667299266874_2022-11-01.png)  

![picture 4](/img/10646d7fdfea1886bdd0c6dca8450875ba438d93df5e66ffb198facc75572739_pic_1667299279945_2022-11-01.png)  


## 应用案例[](#ying-yong-an-li)

以 APP 中常见的用户点击首页顶部轮播图事件为例，来看看埋点事件的定义方法。

首先，明确对于要分析该点击事件的维度，比如：

- 轮播图的位置索引，这样可以统计轮播图各帧的点击率
- 轮播图的图片类型，这样可以统计不同类型的点击率，常用于流量实验场景

其次，在[事件属性](../../../product-manual/data-center/event-management/event-property)中，先定义出如上两个属性

| 名称     | 标识符          | 类型   |
| -------- | --------------- | ------ |
| 位置索引 | swiper_imgindex | 字符串 |
| 图片类型 | swiper_imgtype  | 字符串 |

最后，定义该事件，并将如上两个属性关联到该事件上。

![](/img/assets-M2qbZInaXgdm8kkNosp-MjChPIe0rCI5X4MaWq8-MjCl2EMk1ZymQ0wEaW0image.png)

## 常见问题[](#chang-jian-wen-ti)

Q1：要定义的事件太多，支持批量定义吗？

在[批量工具](../../../developer-manual/toolbox/metadata-creator)中，支持上传模板文件，将事件及其属性的 CSV 文件上传进行批量创建。
