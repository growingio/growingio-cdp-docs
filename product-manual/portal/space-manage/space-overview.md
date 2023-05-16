---
id: space-overview
sidebar_position: 1
---

# 空间概览

## 简介

空间概览包含空间的基本信息与成员的活跃信息。

空间负责人可移交负责人、导出/导入空间资源。

![图 1](/img/kongjiangailan_space-overview.png)  

## 功能说明

### 编辑空间信息

![图 2](/img/bianjikongjianxinxi_space-overview.png)  

### 查看数据授权

数据授权展示了空间可使用项目数据的范围。

![图 6](/img/shujushouquan_space-overview.png)  

### 移交负责人

* 权限：仅空间负责人可操作
* 移交时需要对当前操作人进行二次身份验证

![图 5](/img/yijiaofuzeren_space-overview.png)  

### 导出/导入资源

权限：仅空间负责人可操作

:::caution 注意

导出资源和导入资源配套使用，以满足空间快速复制的场景。

导出空间资源范围，仅包括数据看板、全部报表、指标、分群

由于空间间人员组织结构等不同，导出和导入有如下约束和处理：

* 导入空间为新建空间，即未添加角色、人员，未设置数据授权，未创建任何指标、分群、报表和看板
* 新空间导入资源后，与源空间的差异：
  * 新空间所有资源的创建人为空间负责人
  * 新空间所有数据看板的共享设置为隐私模式
  * 源空间所有数据看板的邮件推送管理不导入新项目
  * 源空间所有数据看板的订阅关系不导入新项目
  * 源空间所有群体画像的图表看板不导入新项目
  * 导出资源和导入资源的操作，仅适用同一环境，项目内的空间复制，不适用跨环境，跨项目的空间复制

:::

![图 7](/img/daorudaochuziyuan_space-overview.png)  

### 查看成员活跃信息

查看过去7/14/30天活跃人数及活跃趋势。

![图 3](/img/kongjianhuoyuexinxi_space-overview.png)  

### 下载成员活跃明细

选择时间范围、空间，点击下载。活跃成员明细，包含成员姓名、账号、天数。

![图 9](/img/portal-project-activeusersdownload_project-overview.png)  
