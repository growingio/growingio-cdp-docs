---
id: third-part-dashboard
sidebar_position: 6
---

# 第三方看板

## 简介

您可以通过接入第三方 BI 工具的仪表盘，实现在系统集中查看各个 BI 数据的能力，当前我们支持 Metabase 的接入，后续会支持更多第三方 BI 工具的接入。

## 功能边界或约束

如果需要使用第三方看板接入功能，需要购买相应的授权，并通过管理员配置相应的权限，以下通过接入 Metabase 为例。

## 功能说明

### 创建第三方看板

购买 Metabase 的授权，并由运维人员配置环境，开通 GrowingIO 增长平台的 Metabase 创建权限，并在集成应用中选择 Metabase 应用，点击并登录 Metabase。

![picture 1](/img/d081cef7400e9e209ddcc23eaf73c84cc24e647e37085172ac8c6dec70583811_pic_1656417017406_2022-06-28.png)

在 Metabase 中创建仪表盘，选择“分享并且编辑”。

![picture 2](/img/492253174df148dfb70cfbce92a85f384b265e6e1df0d460fa85ccd1c3e6a412__2022-06-28.png)

记住链接 Metabase 仪表盘网址最后的编号，例如，图上的编号=1。

### 在项目中接入第三方看板

在项目的看板中新建看板：类型为“Metabase 看板”，看板 ID 为 1。

![picture 3](/img/1de55e7340d429b9a6d1d07487aed7e6a315d3085408740e180366f30f19a5d1_pic_1656417145235_2022-06-28.png)

点击确定后，就可以将 Metabase 看板添加到项目的看板里，同时在订阅的看板列表里，也可以看到带有“Metabase”标识的看板名称。

![picture 4](/img/d4ee3f8cbf940d192461c4e312b037094cb2fea5b68cbcd406d68bade9e90a50_pic_1656417166669_2022-06-28.png)

### 分享看板

在隐私设置中，可以选择把第三方看板共享给项目成员，目前可以设置项目成员为阅读者。

![picture 5](/img/55d6135d924a9f84e60766695062f10d9b11ae232b308b64298b4909c0bf74b4_pic_1656417192021_2022-06-28.png)
