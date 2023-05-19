---
id: custom-dimension
sidebar_position: 2
---

# 自定义维度

## 使用场景

1.当您需要根据业务情况，希望投放链接可以统计到更多维度数据时，可以使用链接自定义维度配置。

2.举例，如果您想跟踪不同区域的效果数据，可以在此新建自定义维度参数“area”，显示名称“区域”。配置后，可以在任一 GrowingIO 的监测链接中使用。

3.形如：https://s.domain.com/r3jEmQe 这样的链接，配置“area”自定义维度后，可直接在链接后缀此参数，得到https://s.domain.com/r3jEmQe?area=huabei 的新链接。

4.进行投放后，增加的“区域”维度可以在事件分析/用户分群/漏斗等模块引用查看“区域”维度中不同值的表现。

5.其中自定义的维度链接参数需以数字+英文字母表达。显示名称则为在 GrowingIO 后台中维度的显示名称，可使用中文表达。

## 新增链接参数

一. 在顶部导航栏选择“数据中心 > 数据集成 > UTM 管理 > 自定义维度”，进入维度配置功能页面。
![图 4](/img/UTM dimension list_utm-dimension.png)  
点击新建自定义维度进入创建页面。
![图 5](/img/create utm dimension_utm-dimension.png)

按页面提示填写对应的名称、标识符及描述后，点击确定即可完成创建。可在自定义维度列表页查看已创建的自定义维度，并进行编辑和删除操作。
![图 6](/img/edit delete utm%20dimension_utm-dimension.png)

## 自定义维度应用场景



在获客分析>获客追踪>监测链接中创建一条形如：https:// s.domain.com/r3jEmQe 这样的链接


可以直接使用Query String的方式将创建好的自定义维度拼接到短链后形成：https:// s.domain.com/r3jEmQe?area=beijing 的链接、

这样北京分公司可在投放北京区域广告时直接使用此链接进行数据监测，并在查看数据（事件、分群、漏斗等）时，引用维度“分公司所在地”查看不同推广城市带来的效果。

自定义维度值建议使用英文或数字；如果使用中文，请使用 URL Encode 编码。

实例：https://s.domain.com/r3jEmQe?keyword=%e5%a2%9e%e9%95%bf

实例：https:// s.domain.com/r3jEmQe?keyword=%e5%a2%9e%e9%95%bf


## 新增自定义维度


一. 在顶部导航栏选择“数据中心 > 数据集成 > UTM管理 > 自定义维度”，进入维度配置功能页面。

![图 7](/img/pic_utmdimension_utm-dimension.png)  


如需创建自定义维度，点击右侧的新建自定义维度按钮进入创建页面。

![图 8](/img/pic_createutmdimension_utm-dimension.png)  


按页面提示填写对应的名称、标识符及描述后，点击确定即可完成创建。

创建成功后可在自定义维度列表页查看已创建的自定义维度，并进行编辑和删除操作。

 ![图 9](/img/pic_utmdimensionaction_utm-dimension.png)  




