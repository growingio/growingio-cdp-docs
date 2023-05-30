---
id: segment-profiles
sidebar_position: 1 
---

# 群体画像

## 简介[](#jian-jie)

您可以通过群体画像功能找到目标用户群体并分析群体特征。

您可以通过以下三种方式创建用户群体：

- 通过特定规则提取用户群体，常用规则包含：

  - 找到做过某些事情的人群：比如过去 7 天完成过 3 次购物车结算
  - 找到具有某些特定属性的人群：比如年龄在 25 岁以下的男性

- 根据用户列表上传创建用户群体。

- 根据分析工具创建用户群体，如漏斗分析、留存分析和分布分析下钻群体画像。

## 名词解释[](#ming-ci-jie-shi)

### 基本信息

| 名词     | 解释                                                                                                                                                         |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 群体人数 | 当前最新一次群体画像计算结果中用户总人数                                                                                                                     |
| 更新频次 | 群体画像计算频次<br/>手动更新：创建成功后一次性计算，或者编辑保存后一次性计算<br/>自动更新：每x天更新一次，更新至某个截止日期        |
| 计算状态 | 群体画像当前计算状态<br/>计算未开始：等待计算中<br/>计算中：群体画像计算中<br/>计算成功：群体画像计算完毕且计算成功<br/>计算失败：群体画像计算完毕且计算失败 |
| 创建方式 | 群体画像创建方式，分为以下几种：<br/>1. 规则创建：对应标签/行为/行为序列/组合圈人<br/>2. 文件上传<br/>3. 策略创建：对应人群策略组生成的人群包<br/>4. 分析圈群：来源于增长分析UBA创建的人群包，不可编辑，不可自动更新<br/>5. 营销圈群：来源于智能运营MAP创建的人群包，不可编辑，不可自动更新

### 定义规则

| 名词     | 解释                                                                                                                                                                        |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 用户行为 | 用户发生的行为信息，包含 **做过** 和 **未做过**<br/>做过：在指定时间范围内，发生过某个事件且满足统计规则的用户群体<br/>未做过：在指定时间范围内，未发生过某个事件的用户群体 |
| 用户特征 | 用户的属性特征信息，包含 **用户属性** 和 **用户标签**                                                                                                                       |

## 功能说明[](#gong-neng-shuo-ming)

### 群体画像列表页

在项目中，您可以在导航栏中看到 **用户洞察 > 群体画像**，点击进入群体画像列表页。

在群体画像列表页可以查看项目内创建的所有群体画像，并支持查看群体画像的名称、人数、更新频次、计算状态等基础信息。

您也可以对群体画像进行以下操作：

| 操作         | 步骤                                                           | 限制条件                     |
| ------------ | -------------------------------------------------------------- | ---------------------------- |
| 搜索         | 您可以在搜索框中根据 **群体画像的名称** 搜索群体画像           | 无                           |
| 新建         | 您可以点击 **新建群体画像** 创建群体画像                       | 无                           |
| 查看用户列表 | 您可以点击 **查看用户列表** 跳转到群体画像用户列表页           | 无                           |
| 另存为       | 您可以点击 **另存为** 复制群体画像定义规则，修改并保存群体画像 | 仅规则创建的群体画像支持另存 |
| 下载用户 ID  | 您可以点击 **下载用户 ID** 下载群体画像用户列表                | 仅包含用户 ID 列             |
| 删除         | 您可以点击 **操作 > 删除**，删除不需要的群体画像               | 无                           |

![](/img/用户洞察-群体画像.png)

### 群体画像详情页

在群体画像列表页，您可以点击 **群体画像名称** 进入群体画像详情页。

在群体画像详情页可以查看群体画像的基础信息和画像信息。

您可以可以对群体画像进行以下操作：

| 操作         | 步骤                                                       | 限制条件                                                                                                                                                   |
| ------------ | ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 查看规则     | 您可以点击 **查看规则** 查看群体画像定义规则               | 无                                                                                                                                                         |
| 编辑         | 您可以点击 **编辑** 编辑群体画像定义规则                   | 规则创建：仅支持修改名称、描述和定义规则<br/>文件上传：仅支持修改名称、描述<br/>漏斗创建：不支持修改<br/>留存创建：不支持修改<br/>分布分析创建：不支持修改 |
| 删除         | 您可以点击 **操作 > 删除**，删除不需要的用户群体           | 无                                                                                                                                                         |
| 查看用户列表 | 您可以点击 **查看用户列表** 查看群体用户列表               | 无                                                                                                                                                         |
| 添加画像图表 | 您可以点击 **添加画像图标** 在下方画像看板添加群体分析图表 | 无                                                                                                                                                         |
| 群组对比 | 您可以点击 **对照组选择群组** 在下方画像看板查看对照组的群组特征，与目标群组进行对比 | 无                                                                                                                                                         |

![图 16](/img/08e114a2044f1916436ece787be8f203b95355294e1e2492084a0a8018b0e6f6.png)  


### 群体画像用户列表页

在群体画像详情页，您可以点击 **查看用户列表** 进入群体画像用户列表页。

在群体画像用户列表页可以查看群体用户列表以及自定义查看用户身份、用户属性和用户标签。

您也可以对用户列表进行以下操作：

| 操作               | 步骤                                                                              | 限制条件                                                                              |
| ------------------ | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| 查看用户详情       | 您可以通过点击 **gio_id(即系统ID)** 查看单用户详情                                         | 无                                                                                    |
| 自定义用户身份展示 | 您可以通过勾选 “仅展示最终获取用户身份”<br/>选择用户身份展示形式                  | 勾选：每个用户仅展示最终获取的用户身份<br/>未勾选：每个用户展示当前具有的全部用户身份 |
| 自定义列           | 您可以点击 **自定义列** 自定义用户列表<br/>可选择展示用户身份、用户属性和用户标签 | 最多支持选择 20 列                                                                    |
| 下载当前列表       | 您可以点击 **下载当前列表** 下载当前自定义的用户列表                              | 无                                                                                    |

![](/img/用户洞察-群体画像-用户列表.png)

#### 仅展示最终获取用户身份

在实际业务中，一个用户可能具有多个终端的使用设备，如 App、小程序、浏览器；也可能使用多个不同手机号。

在用户列表页中，如勾选 ”仅展示最终获取用户身份“，此时每个用户仅展示最终获取的用户身份。如下表：

| gio_id  | 用户 ID | 手机号 | 设备 ID |
| ------- | ------- | ------ | ------- |
| 1       | C001    | m1     | X       |
| 2       | C002    | m2     | Y       |
| 3       | ...     | ...    | ...     |

如取消勾选 ”仅展示最终获取用户身份“，此时每个用户展示当前具有的全部用户身份。如下表：

| gio_id  | 用户 ID | 手机号          | 设备 ID       |
| ------- | ------- | --------------- | ------------- |
| 1       | C001    | [ 'm1' , 'm3' ] | [ 'X' , 'Z' ] |
| 2       | C002    | [ 'm2' , 'm4' ] | [ 'Y' , 'W' ] |
| 3       | ...     | ...             | ...           |

> 如需了解用户身份可阅读 [用户模型](../../../getting-started/basic-concept/user-model) 和 [数据模型-用户身份](../../../getting-started/basic-concept/data-model#用户身份)

当使用群体画像下载进行用户运营或系统对接时，建议 **勾选** “仅展示最终获取用户身份”避免重复触达骚扰用户；

当使用群体画像下载用户列表进行用户名单查看等使用场景时，可 **取消勾选** “仅展示最终获取用户身份”以查看用户全部信息。

#### 自定义列

点击 **自定义列** 后可以看到自定义列弹窗，您可以进行以下操作：

> 自定义列对浏览器生效，同一浏览器浏览不同用户列表自定义列配置相同

- 搜索用户身份、用户属性和用户标签，并添加到自定义列中

![](/img/用户洞察-群体画像-用户列表-自定义列.png)

- 拖动、删除、清空用户身份、用户属性和用户标签

![](/img/用户洞察-群体画像-用户列表-自定义列-拖拽.png)

