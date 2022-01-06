---
id: user-properties
sidebar_position: 1
---

# 用户属性

在GrowingIO平台对用户属性进行声明和管理


## 简介[](#jian-jie)

在开始配置用户属性之前，推荐您阅读[用户模型](/getting-started/basic-concept/user-model)文档，了解 GrowingIO 如何标记用户。

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

用户属性上传后 **秒级** 生效。


### 预置用户属性[](#yu-zhi-yong-hu-shu-xing)

为方便客户使用，系统预置了32个用户属性，分别为：

除 **首次识别日期** 为系统默认采集字段，其他字段均需主动上报数据。

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

首次识别日期( $first_day )为系统首次识别用户，生成gio_id的具体日期，用户生成规则详见 [用户模型](../../../getting-started/basic-concept/user-model)。


## 功能说明[](#gong-neng-shuo-ming)

### 创建用户属性[](#chuang-jian-yong-hu-shu-xing)

一、您可以在 **客户数据平台 > 用户管理 > 用户属性** 中点击 **新建用户属性** 进入用户属性创建弹窗。

| 项 | 是否必填 | 说明 | 限制条件 |
| -- | -- | -- | -- |
| 名称 | 是 | 用户属性名称 | 名称唯一，不可重复</br></br>最大输入30个字符 |
| 标识符 | 是 | 用户属性标识符</br></br>可用于数据库和API查询 | 名称唯一，不可重复</br></br>最大输入100个字符</br></br>仅允许大小写英文、数字、以及下划线，并且不能以数字开头 |
| 数值类型 | 是 | 用户属性数值类型 | 仅支持字符串、整数、日期 |
| 所属分类 | 否 | 选择自定义的用户属性分类</br></br>如人口属性、交易特征 etc. | 如不选择则为未分类 |
| 描述 | 否 | 用户属性的业务意义描述 | 最大输入150个字符 |

![](/img/用户属性-新建用户属性.png)

三、填写完成后单击 **确定**，完成一个用户属性的创建。

在完成了配置，以及正确的代码实施后。我们即可开始在GrowingIO 使用用户属性。


### 用户属性详情页[](#yong-hu-shu-xing-xiang-qing-ye)

在用户属性详情页可以查看单一用户属性的名称、数值类型、创建人、创建日期和统计分布。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiOcCbtjXNmr4hLXvhp%2F-MiOcInDOM0H4GrJTzPi%2Fimage.png?alt=media&token=8bcda439-dcf4-4d7d-88fb-2bd42deeb45d)

您也可以对用户属性进行以下操作：

* **搜索：**您可以在页面中分类上方的搜索框按用户属性名称搜索用户属性。
    
* **编辑：**单击页面右上方的编辑按钮后进入编辑弹窗，修改后单击保存。
    
* **删除：**单击页面右上方的![](/img/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的用户属性。
    
* **批量管理**：单击左下角的管理全部用户属性，进入用户属性管理列表页。
    

### 用户属性管理页面[](#yong-hu-shu-xing-guan-li-ye-mian)

在用户属性管理页面可以查看用户属性的名称、标识符、类型、预置、所属分类、创建日期、创建人、最后编辑时间。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MVZ9jA0SnTmhf79G6pr%2F-MVZHoBPaSiTV8Xgczqz%2Fimage.png?alt=media&token=3831737d-92d9-4530-90d8-5743ddefac0b)

您也可以对用户属性进行以下操作：

* **搜索：**您可以在页面中列表上方的搜索框按用户属性名称和标识符来搜索用户属性。
    
* **QuickView：**单击任一用户属性，您可以在右侧弹出的用户属性详情中，查看用户属性的基本信息。
    
* **编辑：**在QuickView界面单击用户属性的参数进行修改，修改后单击保存。
    
* **删除：**单击单条用户属性右侧的 ![](/img/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的用户属性。
    
* **批量删除**：在列表中使用复选框选择多个用户属性，可以进行批量删除。
    
* **批量移动**：在列表中使用复选框选择多个用户属性，可以进行批量移动，将用户属性移动到目标分类中。
