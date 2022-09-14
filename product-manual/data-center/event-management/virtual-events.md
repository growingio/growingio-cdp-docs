---
id: virtual-events
sidebar_position: 2
---

# 虚拟事件

## 简介[](#jian-jie)

虚拟事件支持合并、拆分预置事件和埋点事件，满足多项目数据划分的使用场景。


## 功能说明[](#gong-neng-shuo-ming)

### 创建虚拟事件[](#chuang-jian-xu-ni-shi-jian)

一、在 客户数据平台 选择 “**事件管理 > 虚拟事件**" ，进入虚拟事件管理页面。

![](/img/assets-M2qbZInaXgdm8kkNosp-MdGhZcKgFVqs99_pO5G-MdGy1_31o_FicAJo4EYimage.png)

二、单击右上角 **新建虚拟事件**、进入 **新建虚拟事件** 弹窗。

![](/img/assets-M2qbZInaXgdm8kkNosp-MdGhZcKgFVqs99_pO5G-MdGyKdlPwLXuKkP1wIPimage.png)

![](/img/assets-M2qbZInaXgdm8kkNosp-MdGhZcKgFVqs99_pO5G-MdGyXoYmhaI00texTxlimage.png)

| 参数  | 说明  |
| --- | --- |
| 名称  | GrowingIO平台上虚拟事件的名称。 |
| 标识符 | 用于API接口使用虚拟事件。 |
| 描述  | 虚拟事件的描述，可填写虚拟事件的触发时机和应用场景。 |
| 虚拟事规则 | 虚拟事件触发规则。 |

> * 虚拟事件 名称 和 标识符 与埋点事件去重
> 
> * 虚拟事件支持使用 预置事件、埋点事件 以及 预置事件属性、事件属性。
> 
> * 虚拟事件触发规则中最多支持配置100个事件以及每个事件做多配置5个触发条件。
> 
> * 虚拟事件定义规则全局唯一，即每一个定义规则仅支持定义一次。

三、填写完成后单击 **完成**，完成一个虚拟事件的创建。

> 虚拟事件创建成功后，需要在 企业管理后台 进行数据授权，授权后的事件支持在项目内使用。


### 虚拟事件管理页面[](#xu-ni-shi-jian-guan-li-ye-mian)

在虚拟事件管理页面可以查看虚拟事件的名称、标识符、创建日期、创建人、最后编辑日期、最后编辑人。

![](/img/assets-M2qbZInaXgdm8kkNosp-MkW5rUsvP-VWF51ulfh-MkW7JE9U_7jkrWFl-8aimage.png)

您也可以对虚拟事件进行以下操作：

**搜索：**您可以在页面中列表上方的搜索框按虚拟事件名称和标识符来搜索虚拟事件。

**QuickView：**单击任一虚拟事件，您可以在右侧弹出的虚拟事件详情中，查看虚拟事件的基本信息。

**编辑：**在QuickView界面单击 **编辑** 修改虚拟事件参数，修改后单击 **完成** 保存修改。

**删除：**单击单条事件右侧的 ![](/img/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的虚拟事件。

**批量操作**：在列表中使用复选框选择多个虚拟事件，可以进行批量删除。
