# 360°单用户画像 new

## 功能介绍

在360°单用户画像中您可以通过用户ID、姓名、手机号、邮箱、OpenID或UnionID查找用户并查看用户画像详情；也可以通过预置分群来查找用户，如过去30天来访用户活跃度Top10，今日活跃用户、三周连续活跃用户、上两周流失用户。

找到用户后，您可以在用户细查页面查看用户行为明细和用户特征。

## 用户搜索页

![](../../../.gitbook/assets/ying-mu-jie-tu-20210119-shang-wu-10.34.54%20%281%29.png)

用戶搜索 ： 目前支持 用戶ID、姓名、手機號、郵箱、unionID、OPenID ，使用用戶唯一標示查詢用戶。

高活躍用戶： 一段時間內，訪問次數最多的用戶 top 10 。

預置分群：

* 今日活跃用户 ： 今天發生過“任意事件"的用戶。
* 三周连续活跃用户 :  以周为单位计算 ，连续3周 都发生过任意行为。
* 上两周的流失用户 ： 周为单位计算 ，两周前有多任意行为，但已经连续两周未发生任意行为。

##  单用户画像的解读 

![](../../../.gitbook/assets/ying-mu-jie-tu-20210119-shang-wu-11.02.54.png)

### 用户基础信息 ：  

帮助你了解此用户的基础用戶信息 

* 展示该项目中被授权查看的用户属性、用户信息 。
* [用戶屬性](https://app.gitbook.com/@growingio/s/op/~/drafts/-MRNTpOkBG--LB98j4NK/v/v2020.13.0/product-manual/customer-data-platform/data-center/property/user-property)  为在系统中定义上报。点击查看
* [用戶信息](https://app.gitbook.com/@growingio/s/op/~/drafts/-MRNTpOkBG--LB98j4NK/v/v2020.13.0/product-manual/customer-data-platform/data-center/property/user-info) 为系统中上报。点击查看
* 可勾選只展示有值的信息 。



### 轨迹概览： 

展示此用户 在最近14 天的行为统计 ，帮助你了解此用户的行为情况概括。

* 可切换展示行为 近14天行为合计占比 /  近14天 行为趋势。
* 可筛选特定事件作为统计 。
* 占比中默认展示前5 ，其余用合并为其他展示 。
* 支持事件筛选，选择想关注的事件 。

![](../../../.gitbook/assets/ying-mu-jie-tu-20210119-shang-wu-11.20.59.png)

### 轨迹细查：

在这里展示了此用户所有被采集的行为，支持事件筛选，选择想关注的事件 。

默认会按照日期从近到远的顺序来显示行为轨迹，即最先显示今天的行为轨迹，然后显示昨天的，前天的，更早的行为……

刷新方式：支持手动刷新、5分钟刷新、实时刷新。

![](../../../.gitbook/assets/ying-mu-jie-tu-20210119-xia-wu-12.26.20.png)





### 常見問題 ：

Q:为什么轨迹细查中事件、事件属性会出现  “未知”的事件 ？ 

A:  未知 是由于 系统收到事件、事件属性的数据，但系统中并未对次进行申明定义 。 

可在 客户数据平台-  埋点事件、事件属性中定义。[点击查看](https://app.gitbook.com/@growingio/s/op/~/drafts/-MRNsMPXZ_pWeFh-4QGQ/v/v2020.13.0/product-manual/customer-data-platform/data-center/event-management/manual)

![](../../../.gitbook/assets/ying-mu-jie-tu-20210119-xia-wu-12.23.55.png)













