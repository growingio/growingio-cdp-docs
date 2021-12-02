---
id: user-properties
sidebar_position: 2
---

# 用户属性

在GrowingIO平台对用户属性进行声明和管理


## 简介[](#jian-jie)

在开始用户属性配置与定义之前，推荐您阅读[用户模型](https://growingio.gitbook.io/op/v/14.7/getting-started/basic-concept/user-identifications)文档，了解 GrowingIO 如何标记用户。

用户属性用来保存跟用户本身相关的信息，不建议在用户属性中保存跟交互行为相关的信息。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiOaLdgbw_FKXD4e4sr%2F-MiObBIsVVGicCdPnu_F%2Fimage.png?alt=media&token=15593e09-4d01-4904-ad3e-b4ff3498f998)

| 项   | 说明  |
| --- | --- |
| 1   | 分类管理列表 |
| 2   | 用户属性详情页 |
| 3   | 用户属性管理列表页 |


## 名词解释[](#ming-ci-jie-shi)

### 用户属性归因模型[](#yong-hu-shu-xing-gui-yin-mo-xing)

GrowingIO 的用户属性采用最终归因的计算模型，即如果一个用户同一个用户属性上传过多个不同数值，按时间排序后距今最近一次上传的用户属性值会保留下来。

例子：

| 日期  | 行为  |
| --- | --- |
| Day 1 | 小明使用 设备X 访问GrowingIO官网 |
| Day 2 | 小明使用 设备X 登录GrowingIO官网，填写职位为 数据分析师<br></br>( 即上传用户属性 职位 = 数据分析师 ) |
| Day 3 | 小明使用 设备X 登录GrwoingIO官网，修改职位为 产品经理 |

说明：

Day 1：此时在 GrowingIO 系统中，小明的用户属性职位为空

Day 2：此时在 GrowingIO 系统中，小明的用户属性职位为“数据分析师”

Day 3：此时在 GrowingIO 系统中，小明的用户属性职位为“产品经理”

时效性：

用户属性上传后 T+1 生效，即今天上传的用户属性次日凌晨更新入 GrowingIO 系统中。


### 预置用户属性[](#yu-zhi-yong-hu-shu-xing)

为方便客户使用，系统预置了32个用户属性，分别为：

除 **首次识别日期** 为系统默认采集字段，其他字段均需主动上报数据。

部分预置用户属性支持在 [360画像](../../../product-manual/user-insights/user-profiles#用户搜索页) 中搜索用户

| 名称  | 标识符 | 类型  |
| --- | --- | --- |
| 首次识别日期 | $first_day | 日期  |
| IDFV | $device_idfv | 字符串 |
| IDFA | $device_idfa | 字符串 |
| 安卓 ID | $device_androidId | 字符串 |
| IMEI | $device_imei | 字符串 |
| 姓名  | $basic_name | 字符串 |
| 注册时间 | $basic_createdAt | 日期  |
| 出生年月日 | $basic_birthday | 日期  |
| 手机号 | $basic_mobile | 字符串 |
| 电子邮箱 | $basic_email | 字符串 |
| 性别  | $basic_gender | 字符串 |
| 地址  | $basic_address | 字符串 |
| 微信 openid | $wechat_openId | 字符串 |
| 微信 unionid | $wechat_unionId | 字符串 |
| 微信昵称 | $wechat_nickName | 字符串 |
| 微信头像 | $wechat_avatarUrl | 字符串 |
| 微信用户性别 | $wechat_gender | 字符串 |
| 微信用户所在国家 | $wechat_country | 字符串 |
| 微信用户所在省份 | $wechat_province | 字符串 |
| 微信用户所在城市 | $wechat_city | 字符串 |
| 微信语言 | $wechat_language | 字符串 |
| 关注公众号 | $wechat_subscribeList | 字符串 |
| 支付宝用户 ID | $alipay_userId | 字符串 |
| 支付宝头像 | $alipay_avatar | 字符串 |
| 支付宝用户所在省份 | $alipay_province | 字符串 |
| 支付宝用户所在城市 | $alipay_city | 字符串 |
| 支付宝用户昵称 | $alipay_nickName | 字符串 |
| 支付宝学生认证 | $alipay_isStudentCertified | 字符串 |
| 支付宝用户类型 | $alipay_userType | 字符串 |
| 支付宝用户状态 | $alipay_userStatus | 字符串 |
| 支付宝实名认证 | $alipay_isCertified | 字符串 |
| 支付宝用户性别 | $alipay_gender | 字符串 |


### 首次识别日期[](#shou-ci-shi-bie-ri-qi)

首次识别日期( $first_day )为系统首次识别用户，生成gio_id的具体日期，用户生成规则详见 [用户模型](../../../getting-started/basic-concept/user-model/user-model)。


## 功能说明[](#gong-neng-shuo-ming)

### 分类管理[](#fen-lei-guan-li)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MVZ9jA0SnTmhf79G6pr%2F-MVZIYB63KY2989o_fdI%2Fimage.png?alt=media&token=ae1ad4a4-64e6-45f9-a3c5-757bbb52a142)

| 操作  | 说明  |
| --- | --- |
| 1 - 新建分类 | 添加新的分类。 |
| 2 - 添加子分类 | 在目标分类下添加子分类，以满足多层级分类管理场景。 |
| 3 - 重命名 | 修改分类名称。 |
| 4 - 删除 | 删除不需要的分类。 |


#### 新建分类[](#xin-jian-fen-lei)

操作流程：点击左上角“**+**”新建用户属性分类。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkllnZYUXlma68fUP_%2F-MLkmfZ4YMUK_cJXiZ5r%2Fimage.png?alt=media&token=3128a08f-c6fc-4406-98b2-0d0aab3a2430)

如未选择上级分类，则在第一级最下方添加新的分类。

如选择上级分类，则在该分类下级最下方添加新的分类。

最多支持创建四级分类，即“上级分类”不支持选择第四级分类


#### 添加子分类[](#tian-jia-zi-fen-lei)

操作流程：在自定义分类后点击 操作 \> 添加子分类

如不更改上级分类，则默认在该分类下级最下方添加新的分类。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkllnZYUXlma68fUP_%2F-MLknwaiHGnJSYKnaV-t%2Fimage.png?alt=media&token=ab54e19e-2eab-4e46-999c-f85066028968)

最多支持创建四级分类，即第四级分类不支持添加子分类


#### 分类重命名[](#fen-lei-zhong-ming-ming)

操作流程：在自定义分类后点击 操作 \> 重命名

修改分类名称后，点击确定保存修改。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkllnZYUXlma68fUP_%2F-MLkoLcUzkV1si9GatS3%2Fimage.png?alt=media&token=7b03bb64-279d-450d-babd-6afac04f0e1f)

分类名称不能与已创建的分类名称重复；

分类名称不能与默认分类名称重复，如全部属性、未分类。


#### 删除分类[](#shan-chu-fen-lei)

操作流程：在自定义分类后点击 操作 \> 删除

点击确认后，删除该分类。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkllnZYUXlma68fUP_%2F-MLkqIZC9d7YWItlOJqu%2Fimage.png?alt=media&token=37972544-a8e5-49b4-9a62-0414981fdaf7)

您需要将分类中关联的子分类删除，并且移除分类下的所有用户属性才能删除此分类。


### 用户属性管理[](#yong-hu-shu-xing-guan-li)

#### 创建用户属性[](#chuang-jian-yong-hu-shu-xing)

一、在顶部导航栏选择 “数据 > 属性 \> 用户属性“ ，进入用户属性管理页面。

二、单击右上角**添加用户属性**，进入**新建用户属性**页面。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MVZ9jA0SnTmhf79G6pr%2F-MVZGe0W18gzO6GGj9PC%2Fimage.png?alt=media&token=4509a22f-8416-4016-a0c4-74bc6c86ca9c)

| 参数  | 说明  |
| --- | --- |
| 名称  | GrowingIO平台上属性的名称。 |
| 标识符 | 此属性在代码中的标识，仅允许大小写英文、数字、下划线，并且不能以数字开头。 |
| 类型  | 支持选择字符串、整数、日期类型用户属性。 |
| 所属分类 | 选择自定义的用户属性分类，如人口属性、交易特征 etc. |
| 描述  | 属性的描述。 |

三、填写完成后单击**确定**，完成一个用户属性的创建。

在完成了配置，以及正确的代码实施后。我们即可开始在GrowingIO 使用用户属性。


#### 用户属性详情页[](#yong-hu-shu-xing-xiang-qing-ye)

在用户属性详情页可以查看单一用户属性的名称、数值类型、创建人、创建日期和统计分布。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiOcCbtjXNmr4hLXvhp%2F-MiOcInDOM0H4GrJTzPi%2Fimage.png?alt=media&token=8bcda439-dcf4-4d7d-88fb-2bd42deeb45d)

您也可以对用户属性进行以下操作：

* **搜索：**您可以在页面中分类上方的搜索框按用户属性名称搜索用户属性。
    
* **编辑：**单击页面右上方的编辑按钮后进入编辑弹窗，修改后单击保存。
    
* **删除：**单击页面右上方的![](/img/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的用户属性。
    
* **批量管理**：单击左下角的管理全部用户属性，进入用户属性管理列表页。
    

#### 用户属性管理页面[](#yong-hu-shu-xing-guan-li-ye-mian)

在用户属性管理页面可以查看用户属性的名称、标识符、类型、预置、所属分类、创建日期、创建人、最后编辑时间。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MVZ9jA0SnTmhf79G6pr%2F-MVZHoBPaSiTV8Xgczqz%2Fimage.png?alt=media&token=3831737d-92d9-4530-90d8-5743ddefac0b)

您也可以对用户属性进行以下操作：

* **搜索：**您可以在页面中列表上方的搜索框按用户属性名称和标识符来搜索用户属性。
    
* **QuickView：**单击任一用户属性，您可以在右侧弹出的用户属性详情中，查看用户属性的基本信息。
    
* **编辑：**在QuickView界面单击用户属性的参数进行修改，修改后单击保存。
    
* **删除：**单击单条用户属性右侧的 ![](/img/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的用户属性。
    
* **批量删除**：在列表中使用复选框选择多个用户属性，可以进行批量删除。
    
* **批量移动**：在列表中使用复选框选择多个用户属性，可以进行批量移动，将用户属性移动到目标分类中。
