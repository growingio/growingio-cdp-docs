---
id: sagment-profiles
sidebar_position: 1
---

# 群体画像

## 简介[](#jian-jie)

群体画像，就是通过一定的规则找到对应的用户群体。 常用的方法包括：

* 找到做过某些事情的人群：比如过去 7 天完成过 3 次购物车结算
    
* 有某些特定属性的人群：比如年龄在 25 岁以下的男性
    
* 在转化过程中流失的人群：比如提交了订单但没有付款
    
您可以根据自己要解决的业务问题，来定义关注的用户群体，还可以在 GrowingIO 平台中通过将分群套用在漏斗分析与留存分析等分析工具中进一步分析；或者通过运营手段对这部分人群进行运营。


## 功能说明[](#gong-neng-shuo-ming)

### 用户分群列表[](#yong-hu-fen-qun-lie-biao)

从导航栏选择“**群体画像**”，进入群体画像列表页面。

![](/img/assets-M2qbZInaXgdm8kkNosp-MjTJ7Zw-AgRjr4TXqvg-MjTJyN6Q0wgboKvFwJt%E7%BE%A4%E4%BD%93%E7%94%BB%E5%83%8F-%E7%BE%A4%E7%94%BB%E5%83%8F%E5%88%97%E8%A1%A8.png)

在群体画像列表页面中，可以查看项目内所有人创建的群体画像，支持按照分群名称进行搜索、下载分群的用户ID列表，以及新建分群。

| 列表项 | 说明  |
| --- | --- |
| 分群名称 | 单击分群名称可进入 群体画像 详情页面 |
| 分群人数 | 当前最新一次计算的分群人数 |
| 分群类型 | 每天计算/一次性计算，分群类型在 [创建群体画像](../../product-manual/user-insights/sagment-profiles#创建群体画像) 时可选择 |
| 计算状态 | 计算未开始/计算中/计算成功/计算失败 |
| 分群创建方式 | 1、规则创建 [点击查看](../../product-manual/user-insights/sagment-profiles#规则创建)<br></br>2、文件上传 [点击查看](../../product-manual/user-insights/sagment-profiles#上传用户列表)<br></br>3、漏斗创建 [点击查看](../../product-manual/product-analysis/funnel)​<br></br>4、留存创建 [点击查看](../../product-manual/product-analysis/retention-analysis)​<br></br>5、分布创建 [点击查看](../../product-manual/product-analysis/frequency)​ |
| 创建人 | 创建分群的用户名 |
| 更新时间 | 分群创建或分群规则最近一次修改的时间 |
| 最近计算 | 最近一次计算分群人数的时间 |
| 操作  | 支持对分群用户进行下载导出、删除分群 |


### 创建群体画像[](#chuang-jian-qun-ti-hua-xiang)

在 用户分群列表页面，选择“**新建分群**”按钮开始创建用户分群。用户分群支持2种创建方法，分别为规则创建分群和上传用户列表。

![](/img/assets-M2qbZInaXgdm8kkNosp-MjTQWBZ3lLGDZEFlRoY-MjTSlIRn-e9LomDkYSNimage.png)

新建分群弹窗


#### 规则创建[](#1-gui-ze-chuang-jian)

在新建分群弹窗中选择“**规则创建**"，进入新建用户分群页面。

![](/img/assets-M2qbZInaXgdm8kkNosp-M3f05PE2aifwnPNiTlY-M3f1mQPrZbPferiIhCrimage.png)

新建用户分群页面

| 参数  | 说明  |
| --- | --- |
| 请输入分群名称 | 命名当前用户分群。 |
| 分群规则 | 您可以通过用户的行为、属性和标签来定位目标用户。您可以通过“**做过**”来筛选用户行为，通过“**属性为**”来筛选用户属性，通过“**标签为**”来筛选用户标签。<br></br>​<br></br>​📙 注意事项：<br></br>* 当您想设置用户未做过某个行为时，选择“做过”行为的次数N=0即可 |
| 计算周期 | 计算周期可选每天计算一次和只计算一次。<br></br>* 每天计算一次：每天的固定时间计算一次分群用户<br></br>* 只计算一次：在保存分群后，立即计算分群用户，之后不再进行计算 |

选择以上参数后，单击右上角保存，完成一个用户分群的创建。

#### 上传用户列表[](#2-shang-chuan-yong-hu-lie-biao)

> 您可能遇到过这样的场景：
>
> 通过第三方系统举办了一场线上公开课，希望追踪报名并且参加了课程的用户后续在产品中的转化和使用情况。
>
> 这样的情况下如何可以在 GrowingIO 构建出目标用户分群以便分析这些用户在产品中的行为呢？就可以通过 "上传用户列表" 的方式。

在新建分群弹窗中选择“**文件上传创建**"，进入上传文件界面。

![](/img/assets-M2qbZInaXgdm8kkNosp-M3f05PE2aifwnPNiTlY-M3f2ZLFPshxvEuUjivGimage.png)

新建用户分群页面

GrowingIO支持根据手机号、邮箱、UserID、OpenID、UnionID共5种类型的用户ID进行分群创建。

选择待上传ID的类别，拖动用户ID文件到上传框，在提示完成后单击继续，完成分群命名后单击保存，完成一个用户分群的创建。


### 群体画像详情页[](#qun-ti-hua-xiang-xiang-qing-ye)

![](/img/assets-M2qbZInaXgdm8kkNosp-MiOgW6qdEzWgbbS5bNy-MiOhR7gBiuMc_QNL2dXimage.png)

| 项   | 说明  |
| --- | --- |
| 分群规则 | 创建分群时的规则，以且、或关系进行关联 |
| 用户量 | 用户分群选定的目标用户群体数量，点击用户量可跳转到 [分群用户列表](../../product-manual/user-insights/sagment-profiles#分群用户列表)。 |
| 时间  | 群体画像的创建时间及最近一次计算时间 |
| 自定义维度 | 页面底部点击“**+**”按钮，可添加更多分群展示维度，支持添加常用维度及用户属性维度。<br></br>支持筛选图表的日期范围，默认为最近30天。 |
| 编辑  | 修改当前分群的名称及分群规则，更新方式不可修改 |


### 分群用户列表[](#fen-qun-yong-hu-lie-biao)

在 群体画像详情页 点击用户量按钮，跳转至分群用户列表。列表默认展示用户ID、UUID等信息，可自定义列选择其他的用户属性字段。列表默认最多展示1000条数据，可通过下载用户用户列表获取全部用户ID。

![](/img/assets-M2qbZInaXgdm8kkNosp-MjT_L-eew9kNgYR6OTS-MjTapgvnxMLBpSQnQ2Dimage.png)

| 项   | 说明  |
| --- | --- |
| 自定义列 | 可选择在列表中展示的其他用户属性，最多支持20列 |
| 下载  | 下载全部的用户的属性列。 |
| 用户ID | 固定展示不可删除，点击用户ID可查看该用户的 [360 画像](../../product-manual/user-insights/user-profiles) 。 |
