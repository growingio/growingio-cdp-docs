---
id: user-tags
sidebar_position: 1
---

# 用户标签

对标签进行定义和管理

## 简介[](#jian-jie)

标签是用户行为和特征的抽象与描述。

在特定业务场景下，标签可以让我们快速的了解一个用户或一群用户的特征。如在电销场景下，我们的客服人员需要了解目标用户的性别、年龄、常住城市、家庭成员数量、历史购买记录、最近浏览偏好等标签信息。这些信息可以帮助客服人员在脑海中快速形成一个鲜活的人物形象，帮助客服人员在与客户的交谈中更好的组织语言、挖掘并满足客户需求。

按照业务特征划分，标签可以分为人口属性标签、交易属性标签、兴趣偏好标签等。

按照创建方式划分，标签可以分为属性标签、计算标签、分层标签和算法标签。

| 标签分类 | 描述                                                        | 特点                                          | 举例                                                                                |
| -------- | ----------------------------------------------------------- | --------------------------------------------- | ----------------------------------------------------------------------------------- |
| 属性标签 | 根据企业沉淀的用户信息加工转换生成                          | 数量少、业务信息大                            | 根据身份证号生成标签。如<br></br>年龄、性别、是否是生日、<br></br>出生省市等        |
| 计算标签 | 根据用户的行为和特征计算生成                                | 数量多、业务信息小                            | 根据购买事件计算生成<br></br>最近购买距今天数(R)、<br></br>购买次数(F)、购买金额(M) |
| 规则标签 | 根据业务经验，人工或半人工通过规则<br></br>计算生成         | 人力成本高、数量少、<br></br>业务信息大       | 根据 RFM 计算标签按业务<br></br>需求根据规则讲用户进行<br></br>分层                 |
| 算法标签 | 大部分依赖算法计算，需要人工参与<br></br>调参和业务效果验证 | 计算成本高、数量多、<br></br>业务效果需要验证 | 根据用户特征和行为<br></br>预测用户购买意向                                         |

标签可以帮助我们更加全面的描述一个用户，但这并不意味着标签需要越多越好。出于计算成本和管理成本考量，我们应结合业务场景和业务需求，考虑什么样的标签能在业务操作中帮助我们更好的完成业务目标，并依据此目标进行标签的创建。

目前 GrowingIO 提供了五种标签计算模型，分别为累计值/平均值/占比标签、最大值/最小值的事件属性标签、最初/最终的事件属性标签、列表类的事件属性标签、分层标签。这五种标签主要用于解决计算标签和规则标签的使用场景。

在客户数据平台中 创建的标签，需要通过 项目管理 > 数据授权 ，将标签分配到项目中使用。 [点此查看](../../../../product-manual/enterprise-management/project-manage/data-authorization)​

目前 GrowingIO 提供了 **五种** **规则标签** 和 **SQL 标签** ，五种规则标签分别为：

- 基础指标值
- 最大值/最小值的事件属性
- 首次/末次的事件属性
- 列表类的事件属性
- 分层标签

## 名词解释[](#ming-ci-jie-shi)

### 基础指标值[](#ji-chu-zhi-biao-zhi)

基础指标值标签为常用的计算标签模型，可以对事件的统计结果作为标签值，对用户打标。

常见使用场景为：

指定周期内，某个事件的

- 发生次数
- 使用天数
- 整数、小数事件属性的求和
- 整数、小数事件属性的平均值
- 某个类型事件发生次数占事件总发生次数的占比
- 某个类型事件的整数、小数事件属性求和占该事件整数、小数事件属性总和的占比
- 字符串事件属性的去重数

指定周期内，某个用户的

- 平均订单支付金额（ 订单支付金额总和 / 下单次数 ）
- 实际订单支付金额（ 订单支付金额总额 - 退款金额总和 ）

### 最大值/最小值的事件属性[](#zui-da-zhi-zui-xiao-zhi-de-shi-jian-shu-xing)

最大值/最小值的事件属性可以按事件属性分组后，对发生次数或整数、小数类型事件属性求和最多或最少的分组属性值作为标签值，对用户打标。

常见使用场景为：

指定周期内，某个事件的

- 发生次数最多的事件属性
- 发生次数最少的事件属性
- 整数、小数事件属性的求和最多的事件属性
- 整数、小数事件属性的求和最少的事件属性

### 首次/末次的事件属性[](#shou-ci-mo-ci-de-shi-jian-shu-xing)

首次/末次的事件属性可以对事件第一次或最后一次发生的字符串类型事件属性作为标签值，对用户打标。

常见使用场景为：

指定周期内，某个事件的

- 首次/末次 发生时的事件属性
- 首次/末次 发生时距今天数
- 首次/末次 发生时的具体日期

### 列表类的事件属性[](#lie-biao-lei-de-shi-jian-shu-xing)

列表类的事件属性可以对用户产生事件的全部事件属性列表作为标签值，对用户打标。

常见使用场景为：

指定周期内，某个事件的

- 全部事件属性列表

### 分层标签[](#fen-ceng-biao-qian)

分层标签支持根据自定义规则对用户进行分层打标。exit: ⌘↩

注意：分层标签中，每个用户具有唯一标签值。如一个用户同时满足多个分层规则，则该用户优先被计算在序号最小的分层中。‌

支持计算规则如下：‌

- 用户做过
- 用户属性是
- 用户标签是

### SQL 标签[](#sql-biao-qian)

支持 SQL 语句根据 GrowingIO 开放[数据模型](../../../../getting-started/basic-concept/data-model)自定义用户标签。

目前支持 5 种数值类型的 SQL 标签，分别为字符串、整数、小数、日期和集合。

## 功能说明[](#gong-neng-shuo-ming)

### 分类管理[](#fen-lei-guan-li)

![图 2](/img/30fade413818e0ab541aeea16eead714535497584041324b708f101fa65c575e_tag_type_manager_2021-12-13.png)

| 操作           | 说明                                               |
| -------------- | -------------------------------------------------- |
| 1 - 新建分类   | 添加新的分类。                                     |
| 2 - 添加子分类 | 在目标分类下添加子分类，以满足多层级分类管理场景。 |
| 3 - 重命名     | 修改分类名称。                                     |
| 4 - 删除       | 删除不需要的分类。                                 |

#### 新建分类[](#xin-jian-fen-lei)

操作流程：点击左上角“**+**”新建用户标签分类。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkllnZYUXlma68fUP_%2F-MLkmfZ4YMUK_cJXiZ5r%2Fimage.png?alt=media&token=3128a08f-c6fc-4406-98b2-0d0aab3a2430)

如未选择上级分类，则在第一级最下方添加新的分类。

如选择上级分类，则在该分类下级最下方添加新的分类。

最多支持创建四级分类，即“上级分类”不支持选择第四级分类

#### 添加子分类[](#tian-jia-zi-fen-lei)

操作流程：在自定义分类后点击 操作 \> 添加子分类

如不更改上级分类，则默认在该分类下级最下方添加新的分类。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkllnZYUXlma68fUP_%2F-MLknwaiHGnJSYKnaV-t%2Fimage.png?alt=media&token=ab54e19e-2eab-4e46-999c-f85066028968)

最多支持创建四级分类，即第四级分类不支持添加子分类

#### 重命名[](#zhong-ming-ming)

操作流程：在自定义分类后点击 操作 \> 重命名

修改分类名称后，点击确定保存修改。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkllnZYUXlma68fUP_%2F-MLkoLcUzkV1si9GatS3%2Fimage.png?alt=media&token=7b03bb64-279d-450d-babd-6afac04f0e1f)

分类名称不能与已创建的分类名称重复；

分类名称不能与默认分类名称重复，如全部标签、未分类。

#### 删除[](#shan-chu)

操作流程：在自定义分类后点击 操作 \> 删除

点击确认后，删除该分类。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkllnZYUXlma68fUP_%2F-MLkqIZC9d7YWItlOJqu%2Fimage.png?alt=media&token=37972544-a8e5-49b4-9a62-0414981fdaf7)

您需要将分类中关联的子分类删除，并且移除分类下的所有用户标签才能删除此分类。

### 创建用户标签[](#chuang-jian-yong-hu-biao-qian)

一、在**客戶数据平台 > 数据 > 标签管理**“，进入标签管理页面。

二、单击右上角**添加标签**，进入**新建标签**弹窗。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaXKLTn1rbjJDdF9USQ%2F-MaXjQj81hnrY5iiT4UX%2Fimage.png?alt=media&token=a55135e4-b227-43e0-97e8-6ebdbd930038)

选择标签类型后，第一步需要定义标签的名称、标识符、描述 等信息。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaXKLTn1rbjJDdF9USQ%2F-MaXkkU6-BQpn4xllWFZ%2Fimage.png?alt=media&token=52fb390f-5717-4f1a-a3e3-535133c41225)

第二步需要定义标签计算规则，详情请参考五种规则标签说明。

三、根据业务需求选择需要创建的标签类型，配置完成后，单击保存，完成一个标签的创建。

#### 基础指标值[](#ji-chu-zhi-biao-zhi-1)

控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaWT8g4phN_UqWQQthL%2F-MaX7r5FZlB_gIjpWI8V%2Fimage.png?alt=media&token=e75280d8-3ff0-4ff6-aa7a-86cac573c9d9)

| 项             | 说明                                                   |
| -------------- | ------------------------------------------------------ |
| 1.选择时间     | 如过去 7 天、过去 30 天、过去 90 天等                  |
| 2.选择事件     | 如全局指标(访问、活跃)、埋点事件和计算指标             |
| 3.选择属性     | 如次数、天数、埋点事件的整数、小数、字符串类型事件属性 |
| 4.选择计算模型 | 如累计值、平均值、占比、去重数                         |
| 5.选择事件过滤 | 选择事件过滤条件                                       |

由于属性的数值类型不同，支持的计算模型对应关系如下：

| 属性                   | 累计值 | 平均值 | 占比 | 去重数 |
| ---------------------- | ------ | ------ | ---- | ------ |
| 次数                   | ✔️     | ​      | ✔️   | ​      |
| 天数                   | ✔️     | ​      | ​    | ​      |
| 整数、小数类型事件属性 | ✔️     | ✔️     | ✔️   | ​      |
| 字符串类型事件属性     | ​      | ​      | ​    | ✔️     |

#### 最大值/最小值的事件属性[](#zui-da-zhi-zui-xiao-zhi-de-shi-jian-shu-xing-1)

控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaX8gmlITGn2zTUPjta%2F-MaX955wpjSxFGygI76a%2Fimage.png?alt=media&token=8fbc6d27-1014-4ca2-8649-3cd9daeaa64e)

| 项             | 说明                                     |
| -------------- | ---------------------------------------- |
| 1.选择时间     | 如过去 7 天、过去 30 天、过去 90 天等    |
| 2.选择事件     | 如全局指标(访问、活跃)和埋点事件         |
| 3.选择分组属性 | 如次数和埋点事件的整数、小数类型事件属性 |
| 4.选择计算模型 | 如最多、最少                             |
| 5.选择打标属性 | 如埋点事件的字符串类型事件属性           |
| 6.选择事件过滤 | 选择事件过滤条件                         |

#### 首次/末次的事件属性[](#shou-ci-mo-ci-de-shi-jian-shu-xing-1)

控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaX9FEkMV4TtU-ccU95%2F-MaX9iiMNQsxpX2ETO5e%2Fimage.png?alt=media&token=291e868d-4faa-4109-b910-f6711c2a890c)

| 项             | 说明                                           |
| -------------- | ---------------------------------------------- |
| 1.选择时间     | 如过去 7 天、过去 30 天、过去 90 天等          |
| 2.选择计算模型 | 如最初、最终                                   |
| 3.选择事件     | 如全局指标(访问、活跃)和埋点事件               |
| 4.选择属性     | 如距今天数、日期和埋点事件的字符串类型事件属性 |
| 5.选择事件过滤 | 选择事件过滤条件                               |

#### 列表类的事件属性[](#lie-biao-lei-de-shi-jian-shu-xing-1)

控件说明：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaXAPPPHyRVJTXO1Z3e%2F-MaXAllgogkiDLxjhel7%2Fimage.png?alt=media&token=55832063-b163-4e10-9543-6a4bce4ac464)

| 项             | 说明                                  |
| -------------- | ------------------------------------- |
| 1.选择时间     | 如过去 7 天、过去 30 天、过去 90 天等 |
| 2.选择事件     | 如全局指标(访问、活跃)和埋点事件      |
| 3.选择属性     | 如埋点事件的字符串类型事件属性        |
| 4.选择事件过滤 | 选择事件过滤条件                      |

#### 分层标签[](#fen-ceng-biao-qian-1)

控件说明:

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-Mj2BWCC4TS6k2BV0XPv%2F-Mj2CS4254gARATZucRG%2Fimage.png?alt=media&token=769e0758-7cea-4669-9b8d-90740bd28d48)

**SQL 标签**

控件说明：‌

- 支持选择数值类型
- 支持写入 SQL 规则

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiQNGh3wdzlC8uur13S%2F-MiQObm0w2zbwDsZsT_e%2Fimage.png?alt=media&token=37910440-3c54-4a19-b1a8-192d882e4eb5)

### 用户标签管理[](#yong-hu-biao-qian-guan-li)

#### 用户标签详情页[](#yong-hu-biao-qian-xiang-qing-ye)

在用户标签详情页可以查看单一用户标签的名称、标签类型、数值类型、创建人、创建日期和统计分布。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiOcnswk2NsfjzfU50l%2F-MiOdKz5sPHo7c68wR3E%2Fimage.png?alt=media&token=ba1db44d-a9eb-4aa5-a8b0-9d12e2dd9c3e)

您也可以对用户标签进行以下操作：

**搜索：**您可以在页面中分类上方的搜索框按用户标签名称搜索用户标签。

**编辑：**单击页面右上方的编辑按钮后进入编辑弹窗，修改后单击保存。

**下载：**单击页面右上方的下载按钮后，下载标签统计分布数据。

**删除：**单击页面右上方的![](/img/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的用户标签。

**另存：**单击页面右上方的![](/img/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择另存，可对该标签规则进行另存操作。

**批量管理**：单击左下角的管理全部用户标签，进入用户标签管理列表页。

#### 用户标签管理页面[](#yong-hu-biao-qian-guan-li-ye-mian)

在用户标签管理页面可以查看用户标签的名称、标识符、标签类型、所属分类、创建日期、创建人、最后修改人等信息。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiOZz2nstnrikOkEx0b%2F-MiO_cLiEoIuuRcTkMsC%2Fimage.png?alt=media&token=9d714698-6adf-4268-b2ef-0020cfd19f90)

您也可以对用户标签进行以下操作：

**搜索：**您可以在页面中列表上方的搜索框按用户标签名称和标识符来搜索用户标签。

**编辑：**单击单条用户标签右侧的 ![](/img/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择编辑，进入标签编辑弹窗修改后单击保存。

**删除：**单击单条用户标签右侧的 ![](/img/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的用户标签。

**批量删除**：在列表中使用复选框选择多个用户标签，可以进行批量删除。

**批量移动**：在列表中使用复选框选择多个用户标签，可以进行批量移动，将用户标签移动到目标分类中。

## 应用场景[](#ying-yong-chang-jing)

### 基础指标值：过去 30 天活跃天数[](#ji-chu-zhi-biao-zhi-guo-qu-30-tian-huo-yue-tian-shu)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MAToWSSk0On29958fqk%2F-MATpu7WBphvmM_ZYft1%2Fimage.png?alt=media&token=83cf0379-36c6-4015-ad83-4da32be97f2c)

| 项             | 说明       |
| -------------- | ---------- |
| 1.选择时间     | 过去 30 天 |
| 2.选择事件     | 活跃       |
| 3.选择属性     | 天数       |
| 4.选择计算模型 | 累计值     |
| 5.选择事件过滤 | ​          |

### 基础指标值：过去 90 天平均订单支付金额[](#ji-chu-zhi-biao-zhi-guo-qu-90-tian-ping-jun-ding-dan-zhi-fu-jin-e)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MAToWSSk0On29958fqk%2F-MATqV6IcxhwCuzgmVmr%2Fimage.png?alt=media&token=0ff1bb9b-c55a-4d4b-bb71-96648c8e7295)

| 项             | 说明         |
| -------------- | ------------ |
| 1.选择时间     | 过去 90 天   |
| 2.选择事件     | 订单支付成功 |
| 3.选择属性     | 实际购买金额 |
| 4.选择计算模型 | 平均值       |
| 5.选择事件过滤 | ​            |

### 基础指标值：过去 7 天男装商品浏览次数占总商品浏览次数占比[](#ji-chu-zhi-biao-zhi-guo-qu-7-tian-nan-zhuang-shang-pin-liu-lan-ci-shu-zhan-zong-shang-pin-liu-lan-ci-shu-zhan-bi)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MAToWSSk0On29958fqk%2F-MATr0kCWB-cFIxbKtPC%2Fimage.png?alt=media&token=9d60f046-b74c-455c-8e3f-b4e86a9a5c4f)

| 项             | 说明               |
| -------------- | ------------------ |
| 1.选择时间     | 过去 7 天          |
| 2.选择事件     | 浏览商品详情页     |
| 3.选择属性     | 次数               |
| 4.选择计算模型 | 占比               |
| 5.占比属性     | 一级分类 等于 男装 |

### 最大值/最小值的事件属性：过去 30 天浏览次数最多的商品一级分类[](#zui-da-zhi-zui-xiao-zhi-de-shi-jian-shu-xing-guo-qu-30-tian-liu-lan-ci-shu-zui-duo-de-shang-pin-yi-ji-fen-lei)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MAU29Bnt1JKBodOmP_S%2F-MAU2zp4DQ2FHbsBWx2e%2Fimage.png?alt=media&token=ea0bae1f-7ca3-483b-8055-b0ec0aaa40ac)

| 项             | 说明           |
| -------------- | -------------- |
| 1.选择时间     | 过去 30 天     |
| 2.选择事件     | 浏览商品详情页 |
| 3.选择分组属性 | 次数           |
| 4.选择计算模型 | 最多           |
| 5.选择打标属性 | 一级分类       |
| 6.选择事件过滤 | ​              |

### 首次/末次的事件属性：过去 90 天末次(最后一次)订单购买距今日期[](#shou-ci-mo-ci-de-shi-jian-shu-xing-guo-qu-90-tian-mo-ci-zui-hou-yi-ci-ding-dan-gou-mai-ju-jin-ri-qi)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaXA41F188ZJnOOM7Tc%2F-MaXAGNawGLXbipq7t1M%2Fimage.png?alt=media&token=33e21c07-6fce-4a5e-9cbe-8663ff933b10)

| 项             | 说明         |
| -------------- | ------------ |
| 1.选择时间     | 过去 90 天   |
| 2.选择计算模型 | 末次发生     |
| 3.选择事件     | 订单支付成功 |
| 4.选择属性     | 距今天数     |
| 5.选择事件过滤 | ​            |

### 列表类的事件属性：过去 30 天全部浏览的商品名称[](#lie-biao-lei-de-shi-jian-shu-xing-guo-qu-30-tian-quan-bu-liu-lan-de-shang-pin-ming-cheng)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MAUBp9Ib2qBIHwfvihV%2F-MAUEmdyl_o3vcBNcIbc%2Fimage.png?alt=media&token=7f500bc8-5592-45ac-8bda-1d9ae25ad69f)

| 项             | 说明           |
| -------------- | -------------- |
| 1.选择时间     | 过去 30 天     |
| 2.选择事件     | 浏览商品详情页 |
| 3.选择属性     | 商品名称       |
| 4.选择事件过滤 | ​              |

### 分层标签：用户活跃度[](#1-fen-ceng-biao-qian)

高活跃用户：过去 30 天累计交易金额大于 1 千元且活跃天数大于 4 天 ‌

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaXAPPPHyRVJTXO1Z3e%2F-MaXCTAgdtqU7Mlq--YD%2Fimage.png?alt=media&token=3277031e-18ee-4312-b9a7-d5432440c1e5)

中活跃用户：过去 30 天累计交易金额大于 300 元或活跃天数大于 2 天 ‌

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaXDLQjyWiMW4vv5TSA%2F-MaXJ_-YnLxRxmvZ0spv%2Fimage.png?alt=media&token=4215dce4-360c-4e33-ab04-f157bec142ea)

低活跃用户：过去 30 天有活跃的用户

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MaXDLQjyWiMW4vv5TSA%2F-MaXJf4PNfheimCYJSn4%2Fimage.png?alt=media&token=44dc2509-27d0-4c5d-b279-cb114de6a802)

### SQL 标签：过去 7 天订单支付金额总和[](#sql-biao-qian-guo-qu-7-tian-ding-dan-zhi-fu-jinezong-he)

```sql
-- 埋点事件: 订单支付事件  payOrderSuccess

-- 事件属性：实际支付金额  payAmount_var

select

 gio_id

 ,sum( var\_payAmount\_var ) as tag_value

from olap.event

where event_key = 'payOrderSuccess'

 and dateDiff( 'day' , dt , today () ) between 1 and 7

group by gio_id
```

### SQL 标签：过去 30 天浏览次数 Top 3 的商品名称[](#sql-biao-qian-guo-qu-30-tian-liu-lan-ci-shu-top-3-de-shang-pin-ming-cheng)

```sql

-- 埋点事件：商品浏览事件   goodsDetailPageView

-- 事件属性：商品名称      var\_goodsName\_var

​

--- 方法一(推荐) ---

select

 gio_id

 ,groupArray(3)(var\_goodsName\_var) as tag_value

from

(

select

 gio_id

 ,var\_goodsName\_var

 ,count(1) as pv

from olap.event

where event_key = 'goodsDetailPageView'

 and dateDiff( 'day' , dt , today () ) between 1 and 30

group by gio_id

 ,var\_goodsName\_var

order by gio_id

 ,count(1) desc

 ,var\_goodsName\_var

)

group by gio_id

​

--- 方法二 ---

 gio_id

 ,groupUniqArray(var\_goodsName\_var) as tag_value

from

(

select

 gio_id

 ,var\_goodsName\_var

 ,count(1) as pv

 ,row\_number() over ( partition by gio\_id order by count(1) desc, var\_goodsName\_var ) as num

from olap.event

where event_key = 'goodsDetailPageView'

 and dateDiff( 'day' , dt , today () ) between 1 and 30

group by gio_id

 ,var\_goodsName\_var

)

where num <= 3

group by gio_id
```

### SQL 标签：过去 90 天最后一次订单支付具体日期[](#sql-biao-qian-guo-qu-90-tian-zui-hou-yi-ci-ding-dan-zhi-fu-ju-ti-ri-qi)

```sql

-- 埋点事件: 订单支付事件  payOrderSuccess

​

--- 方法一(推荐) ---

select

 gio_id

 ,argMax( dt , dt ) as tav_value

from olap.event

where event_key = 'payOrderSuccess'

 and dateDiff( 'day' , dt , today () ) between 1 and 90

group by gio_id

​

--- 方法二 ---

select

 gio_id

 ,groupArray(1)(dt)\[1\] as tag_value

from

(

 select

 gio_id

 ,dt

 from olap.event

 where event_key = 'payOrderSuccess'

 and dateDiff( 'day' , dt , today () ) between 1 and 90

 order by gio_id

 ,dt desc

)

group by gio_id
```

### SQL 标签：过去 90 天最后一次订单支付距今天数[](#sql-biao-qian-guo-qu-90-tian-zui-hou-yi-ci-ding-dan-zhi-fu-ju-jin-tian-shu)

```sql
-- 埋点事件: 订单支付事件  payOrderSuccess

​

--- 方法一(推荐) ---

select

 gio_id

 ,dateDiff( 'day' , argMax( dt , dt ) , today() )  as tav_value

from olap.event

where event_key = 'payOrderSuccess'

 and dateDiff( 'day' , dt , today () ) between 1 and 90

group by gio_id

​

--- 方法二 ---

select

 gio_id

 ,dateDiff( 'day' , groupArray(1)(dt)\[1\] , today() ) as tag_value

from

(

 select

 gio_id

 ,dt

 from olap.event

 where event_key = 'payOrderSuccess'

 and dateDiff( 'day' , dt , today () ) between 1 and 90

 order by gio_id

 ,dt desc

)

group by gio_id
```
