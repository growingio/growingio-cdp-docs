---
id: item-management
sidebar_position: 1
---

# 物品管理

## 简介[](#jian-jie)

如果您的业务中存在物品(如商品、保险产品、课程 etc.)，需要分析人对物品的偏好或分析物品特征时，可以使用GrowingIO提供的物品模型来创建和管理物品。物品模型支持通过异步上传的方式导入物品信息，相对于事件属性SDK埋点方式，文件上传可以规避大量的前端技术埋点工作。

> GrowingIO中对于物品的定义：
> 
> 以商品为例，满足以下点特征可以使用物品模型。
> 
> 1.  每一个商品具有唯一识别标识，即商品ID(product_id)。
> 
> 2.  不同商品具有共有的属性特征，如供应商、商品型号、商品颜色 etc.；且商品特征的个数相对稳定，不会频繁增加或减少。
> 
> 3.  单一商品的属性值不会频繁变更，一天内商品属性值不会发生变化。
> 


## 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

一个事件仅能关联一个物品。


## 功能说明[](#gong-neng-shuo-ming)

### 创建物品[](#chuang-jian-wu-pin)

一、在客户数据平台模块中，选择“**物品管理**“，进入物品管理页面。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M397mvLNcyag8pMLao3%2F-M39NyrYXiaTWby2Bt6e%2Fimage.png?alt=media&token=480263c9-5b48-4194-8f0b-96b3b507850b)

物品管理页面

二、单击右上角**添加物品**，进入**新建物品**页面。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M397mvLNcyag8pMLao3%2F-M39ObiKHKSQ0NP9YJH4%2Fimage.png?alt=media&token=e12f0b00-b027-45f6-964f-9ca53d2729cf)

Step 1: 新建物品

| 参数  | 说明  |
| --- | --- |
| 名称  | 输入物品名称，如商品、保险产品、课程 etc.。 |
| 描述  | 物品的描述。 |

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M397mvLNcyag8pMLao3%2F-M39PPC6Y4PuR7nqBVB0%2Fimage.png?alt=media&token=e65db743-e10b-4325-bcc7-f769850b1f68)

Step 2: 设置唯一识别属性

| 参数  | 说明  |
| --- | --- |
| 名称  | 输入物品唯一识别属性的名称，如商品ID、保险产品ID、课程ID etc.。 |
| 标识符 | 输入物品唯一识别属性的标识符，如product_id、insurance_id、lecture_id etc.。<br></br>此变量在代码中的标识，仅允许大小写英文、数字、下划线，并且不能以数字开头。 |
| 类型  | 物品唯一属性的字符类型，默认为字符串，不可更改。 |
| 描述  | 物品唯一识别属性的描述。 |

三、填写完成后，单击完成，完成一个物品的创建。

物品创建成功后自动跳转到物品详情页，在物品详情页可以创建和管理物品属性。


### 创建物品属性[](#chuang-jian-wu-pin-shu-xing)

一、在物品管理页面点击物品名称，进入物品详情页。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M39Qvh2TzPbcSVWhz1G%2F-M39U2cfpFL7EhJCrAnb%2Fimage.png?alt=media&token=5297509e-8f79-420d-91ff-a41139e58614)

物品管理页面

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M39Qvh2TzPbcSVWhz1G%2F-M39U_CP0Zu-kxJ_lNUG%2Fimage.png?alt=media&token=12ff1599-56b7-4299-821a-1741096fce08)

物品详情页

二、单击右上角**添加物品属性**，进入**新建物品属性**页面。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M39Qvh2TzPbcSVWhz1G%2F-M39V6EYbAC_xeWec-zA%2Fimage.png?alt=media&token=444d80d5-46f2-4078-86eb-312cd9cc0a39)

新建物品属性

| 参数  | 说明  |
| --- | --- |
| 名称  | 输入物品属性名称，如供应商、商品颜色、商品型号 etc.。 |
| 标识符 | 输入属品属性标识符。<br></br>此变量在代码中的标识，仅允许大小写英文、数字、下划线，并且不能以数字开头。 |
| 类型  | 物品属性的字符类型，默认为字符串，不可更改。 |
| 描述  | 物品属性的描述。 |

三、填写完成后，单击确定，完成一个物品属性的创建。

物品和物品属性创建成功后，需关联事件与对应的物品属性。


### 关联事件与物品[](#guan-lian-shi-jian-yu-wu-pin)

> 一个事件仅能关联唯一一个物品。

一、新建事件时关联物品

在事件管理页面新建事件时，可单击**关联物品属性**选择物品。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M39Xpfweu5RXrS7ARhH%2F-M39Zzng0A7kbUTmD9DP%2Fimage.png?alt=media&token=08b6426b-51aa-4aaf-9e61-0dff292e0515)

新建事件页面

二、已创建事件关联物品

在事件管理页面单击事件进入QuickView页面，下拉到底部单击**关联物品属性**选择物品。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M39Xpfweu5RXrS7ARhH%2F-M39cSPcrEGNLojSiJwM%2Fimage.png?alt=media&token=9920d77d-5d1d-4ce8-b1b3-b1dd7ab0455b)

事件 \- QuickView界面

在完成了以上配置，以及物品数据上传和正确的代码实施后。我们即可以在对应的事件中使用物品及相关的物品属性。


### 使用物品和物品属性[](#shi-yong-wu-pin-he-wu-pin-shu-xing)

在完成以上配置后，可在配置了物品的事件属性选择器中使用物品属性。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-M39dicnzGBCtcdh-jxS%2F-M39e5ORbBTfDaZYg3yV%2Fimage.png?alt=media&token=da4361dc-b8b9-4059-9a1f-eb1f3ed6871a)

维度选择器


### 物品管理页面[](#wu-pin-guan-li-ye-mian)

在物品管理页面可以查看物品的名称、描述、创建人、更新日期、创建日期。

您也可以对物品进行以下操作：

**搜索：**您可以在页面中列表上方的搜索框按物品名称来搜索物品。

**QuickView：**单击任一物品，您可以在右侧弹出的物品详情中，查看物品的基本信息。

**编辑：**在QuickView界面单击物品的参数进行修改，修改后单击保存。

**删除：**单击单条物品右侧的 ![](/img/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的物品。

**批量操作**：在列表中使用复选框选择多个物品，可以进行批量删除。


### 物品属性管理页面[](#wu-pin-shu-xing-guan-li-ye-mian)

在物品属性管理页面可以查看物品属性的名称、标识符、类型、创建人、创建日期。

> 物品属性列表第一行默认为唯一标识，不可更改。

您也可以对物品属性进行以下操作：

**搜索：**您可以在页面中列表上方的搜索框按物品属性名称和标识符来搜索物品属性。

**QuickView：**单击任一物品属性，您可以在右侧弹出的物品属性详情中，查看物品属性的基本信息。

**编辑：**在QuickView界面单击物品属性的参数进行修改，修改后单击保存。

**删除：**单击单条物品属性右侧的 ![](/img/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的物品属性。

**批量操作**：在列表中使用复选框选择多个物品属性，可以进行批量删除。


## 常见问题[](#chang-jian-wen-ti)

Q1.商品金额能不能设置成物品属性？

商品金额一天内有可能发生多次变化，如抢购活动、新手活动 etc.。对于一天内发生多次变化的属性应使用SDK埋方式上传，不能设置成物品属性。
