---
id: data-import
sidebar_position: 2
---

# 数据导入管理

## 简介

通过 SDK 或者其他方式产生的用户相关历史数据，进行处理加工成固定的格式后，通过创建数据导入任务的方式将历史用户产生的数据导入 CDP 系统中，数据上传成功即可在其他分析模块进行用户行为的分析

## 功能边界或约束

- 创建相应类型的数据源，使用说明请参考[数据源管理](../../../product-manual/customer-data-platform/data-integration/datasource-manage)​

- 需要有该模块的权限，如无权限请找**管理员**开通

- 数据导入用户行为数据：预置事件（如$visit、$page 等）、预置事件属性（$domain、$city、$ip 等等）范围格式

- 匿名用户行为数据导入，需要严格按照时序导入，这样能确保新户计算逻辑准确

- 用户属性：[详见预置用户属性](../../../product-manual/customer-data-platform/user-management/user-properties/user-properties#预置用户属性)​

## 功能说明

### 创建数据导入任务

在导航栏选择“ **数据集成 > 数据导入管理**“，进入数据导入管理页面

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiP-vXPkE-uA5KtzgH1%2F-MiP2i-sTHYQhEcNzPKX%2Fimage.png?alt=media&token=5cca6ea6-4e4d-4171-bf33-53cf6e5d1daa)

数据导入管理页面

点击**创建数据导入任务**按钮

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M3nM56TsoOujwX51vzR%2F-M3nMU8i8kZb0eJFEpK_%2Fimage.png?alt=media&token=a8bc5d35-8de8-4d40-8c50-bd663258dddf)

数据导入类型选择

### 选择数据导入类型，[用户行为数据](../../../product-manual/customer-data-platform/data-integration/data-import#用户行为数据)或[用户属性数据](../../../product-manual/customer-data-platform/data-integration/data-import#用户属性数据)​

#### 用户行为数据

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiP4bnSGGXSvckGtuwF%2F-MiP5HN7DVMFDRDMiD3E%2Fimage.png?alt=media&token=d5d7d98e-c363-46e0-a312-13868377c9ee)

选择数据源：选择在数据源管理中创建的数据源，如果是事件数据创建用户行为类的数据源，如是用户属性则选择用户属性类数据源。

选择时间范围：数据所覆盖的所有时间，例如需要导入的数据涵盖 2020 年 1 月 1 日~2020 年 4 月 1 日，则选择时间 2020 年 1 月 1 日至 2020 年 4 月 1 日即可。

选择上传方式：[CSV](../../../product-manual/customer-data-platform/data-integration/data-import#用户行为数据csv格式)、[JSON](../../../product-manual/customer-data-platform/data-integration/data-import#用户行为数据json格式)、FTP

#### 用户属性数据

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiPHrfX2odbRP0lbysX%2F-MiPIF4LVgd6KLqgaT79%2Fimage.png?alt=media&token=eb4c1245-3b77-44a0-b114-acd6113bdea4)

选择数据源：选择用户属性类型的数据源

选择上传方式：[CSV](../../../product-manual/customer-data-platform/data-integration/data-import#用户属性csv格式)、[JSON](../../../product-manual/customer-data-platform/data-integration/data-import#用户属性json格式)、FTP

### 确定创建任务

### 上传数据，将按照固定[数据格式](../../../product-manual/customer-data-platform/data-integration/data-import#数据导入格式)导入 CDP[](#shang-chuan-shu-ju-jiang-an-zhao-gu-ding-shu-ju-ge-shi-dao-ru-cdp)

选择 CSV 进入页面

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiPM0hVPL61RNWF_0Vt%2F-MiPg1z4Sc9ksA1FQ_VA%2Fimage.png?alt=media&token=b00ba491-ef94-405f-b737-63f184475d1e)

上传 CSV 页面

选择 JSON

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiPM0hVPL61RNWF_0Vt%2F-MiPh1YbQzRYp-t6wMDM%2Fimage.png?alt=media&token=81dd89f6-e750-487d-8fa9-38a75d09e86d)

上传 JSON 页面

选择 FTP：提供任务目录地址，将 JSON 文件放入 FTP 目录中，格式参考[数据格式 JSON](../../../product-manual/customer-data-platform/data-integration/data-import#yong-hu-hang-wei-shu-ju-json-ge-shi)。将数据放入指定 FTP 目录，点击“操作”，查看文件上传，勾选注意事项，进行下一步

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MjTvs4LLbAI_eTi1HGa%2F-MjTx3uJcFB36TNkmuek%2Fimage.png?alt=media&token=60d9c432-9e76-43c8-bae5-a0f1757dc86e)

FTP 方式，未上传数据时状态

### 上传数据成功后，开始导入

### 查看任务详情

主页点击某一任务，弹出任务详情信息栏，还未导入的任务可通过右上角的“上传文件”按钮，进入导入页面

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiPM0hVPL61RNWF_0Vt%2F-MiPhorFmwrBltDCvdQ5%2Fimage.png?alt=media&token=2ee14986-a450-46ef-a8cd-47bd1d72259b)

任务详情

### 查看导入状态

还未导入：任务还未开始

排队中：系统压力过大时，任务会按照提交顺序进行排队，正在等待执行

正在导入：任务正在队列中等待进行或任务已经启动

导入成功：数据已进入系统中

导入失败：点击“操作”列查看错误详情

![](/img/数据导入管理状态页.jpg)

数据导入管理页面

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MjTvs4LLbAI_eTi1HGa%2F-MjTyTDtn6xlzg-yQ-AE%2Fimage.png?alt=media&token=d87f2984-4543-42a5-8cff-a32a66f2beff)

FTP 方式，导入失败状态

## 数据导入格式

### 用户行为数据（CSV 格式）

| ​      | 固定列名  | 数据类型 | 描述                                                                                                                                                                                       |
| ------ | --------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 第一列 | userId    | 字符串   | 必填，用户的登录 ID                                                                                                                                                                        |
| 第二列 | event     | 字符串   | 必填，系统内已定义的事件标识符                                                                                                                                                             |
| 第三列 | timestamp | 字符串   | 必填，支持格式 2021-07-01 00:00:00.000、2021-07-01、2021-07-01 00:00:00、秒级时间戳（1630379476）、毫秒级时间戳（1630379476000）、2021/07/01 00:00:00.000、2021/07/01、2021/07/01 00:00:00 |

**已定义事件与事件属性绑定关系：**

| 事件标识符 | 事件属性标识符         |
| ---------- | ---------------------- |
| batchi0809 | batch10809，batch20809 |
| batchi0810 | batch20809，batch30809 |
| batchi0811 | batch30809             |

**数据样例：**

| userId | event      | timestamp  | batch10809 | batch20809 | batch30809 |
| ------ | ---------- | ---------- | ---------- | ---------- | ---------- |
| 123321 | batchi0809 | 2021-07-01 | 绑定 0809  | 绑定 0809  | ​          |
| 123321 | batchi0809 | 2021-07-02 | 绑定 0809  | 绑定 0809  | ​          |
| 123321 | batchi0810 | 2021-07-03 | ​          | 绑定 0810  | 绑定 0810  |
| 123321 | batchi0811 | 2021-07-04 | ​          | ​          | 绑定 0811  |

### 用户行为数据（JSON 格式）

| 字段名    | 类型                      | 描述                                                                                                  |
| --------- | ------------------------- | ----------------------------------------------------------------------------------------------------- |
| userId    | String                    | 必填，登录用户 id                                                                                     |
| event     | String                    | 必填，事件标识，​ 需提前在数据管理中创建，预定义属性请在事件管理-预定义属性中查看相应属性的 key 标识  |
| timestamp | Long                      | 必填，事件发生 unix 毫秒时间戳                                                                        |
| eventId   | String                    | 选填，可自定义生成事件 ID，默认将由系统生成，用于事件去重条件之一                                     |
| userKey   | String                    | 选填，默认登录用户 id，如需导入多身份，请填写用户身份配置的 key，例如配置手机为用户身份 key 为“phone” |
| attrs     | Map&lt;String, String&gt; | 可不填，事件属性，其中属性的 key ​ 需要提前在数据管理中创建 ​ 并关联                                  |

**数据样例：**

```json
{​"event"​:​ ​"paySuccess"​,​ ​"userId"​:​ "​156xxx"​,​ ​"timestamp"​:​ ​1577246696001​,​ ​"attrs"​:​ ​{​"type"​: "Wechat"​}}
{​"event"​:​ ​"paySuccess"​,​ ​"userId"​:​ "​156xxx"​,​ ​"timestamp"​:​ ​1577246696002​,​ ​"attrs"​:​ ​{​"type"​: "Wechat"​}}
{​"event"​:​ ​"paySuccess"​,​ ​"userId"​:​ "​157xxx"​,​ ​"timestamp"​:​ ​1577246696001​,​ ​"attrs"​:​ ​{​"type"​: "Wechat"​}}
{​"event"​:​ ​"paySuccess2"​,​ ​"userId"​:​ ​"158xxx"​,​ ​"timestamp"​:​ ​1577246696003​,​ ​"attrs"​:​ ​{​"type"​: "Wechat"​}}
{"userId":"aaaa","eventId":"bbbb``","event":"paySuccess_event","timestamp":1637337600000, "attrs":{"payAmount_var":"66.66"}}
{"userId":"123","timestamp":"11111","event":"test","userKey":"$basic_userId",{"var_test":"123"}}
{"userId":"1880001111","timestamp":"11111","event":"test","userKey":"phone",{"var_test":"123"}}
```

### 用户行为数据（JSON 格式，匿名用户）

| 字段名      | 类型                      | 描述                                                                                               |
| ----------- | ------------------------- | -------------------------------------------------------------------------------------------------- |
| anonymousId | String                    | 必填，匿名用户 id                                                                                  |
| event       | String                    | 必填，事件标识，需提前在数据管理中创建，预定义属性请在事件管理-预定义属性中查看相应属性的 key 标识 |
| timestamp   | Long                      | 必填，事件发生 unix 毫秒时间戳                                                                     |
| eventId     | String                    | 选填，可自定义生成事件 ID，默认将由系统生成，用于事件去重条件之一                                  |
| attrs       | Map&lt;String, String&gt; | 可不填，事件属性，其中属性的 key 需要提前在数据管理中创建并关联                                    |

**数据样例：**

```json
{"event": "paySuccess", "anonymousId": "ahjdgdgfdgd", "timestamp": 1577246696001, "attrs": {"type": "Wechat"}}
{"event": "paySuccess", "anonymousId": "ahjdgdgfdgd", "timestamp": 1577246696002, "attrs": {"type": "Wechat"}}
{"event": "paySuccess", "anonymousId": "ahjdgdgfdgd", "timestamp": 1577246696001, "attrs": {"type": "Wechat"}}
{"event": "paySuccess2", "anonymousId": "ahjdgdgfdgd", "timestamp": 1577246696003, "attrs": {"type": "Wechat"}}
```

### 用户属性（CSV 格式）

| ​      | 固定列名    | 描述                 |
| ------ | ----------- | -------------------- |
| 第一列 | userId      | 必填，登录用户 ID    |
| 第二列 | 用户属性... | 系统已定义的用户属性 |
| ​      | ...         | ...                  |

**数据样例：**

| userId | sex | age | test1 |
| ------ | --- | --- | ----- |
| 123    | 男  | 19  | 初级  |
| 234    | 女  | 38  | 中级  |
| 345    | 男  | 22  | 高级  |

### 用户属性（JSON 格式）

| 字段名 | 类型                      | 描述                                                                               |
| ------ | ------------------------- | ---------------------------------------------------------------------------------- |
| userId | String                    | 必填，登录用户 id                                                                  |
| attrs  | Map&lt;String, String&gt; | 必填，用户属性，其中属性的 key ​ 需要提前在 “数据管理 -> 用户属性“ 中创建 ​ 并关联 |

**数据样例：**

```json
{"userId": "156xxx", "attrs": {"sex": "男", "age": "16"}}
{"userId": "157xxx", "attrs": {"sex": "女", "age": "28"}}
```

## 支持导入预置事件、属性、用户属性明细表

### 预置事件

| 预置事件标识符 | 描述             |
| -------------- | ---------------- |
| $visit         | 用户访问一次页面 |
| $page          | 页面浏览         |

### 预置事件属性

| 预置事件属性        | 类型    | 描述               |
| ------------------- | ------- | ------------------ |
| $session            | String  | 会话 ID            |
| $package            | String  | 包名(App 专用)     |
| $platform           | String  | 应用平台端         |
| $referrer_domain    | String  | 访问来源           |
| $utm_source         | String  | 广告来源           |
| $utm_medium         | String  | 广告媒介           |
| $utm_campaign       | String  | 广告名称           |
| $utm_term           | String  | 广告关键字         |
| $utm_content        | String  | 广告内容           |
| $ads_id             | String  | 广告 id            |
| $key_word           | String  | 搜索词             |
| $country_code       | String  | 国家代码           |
| $country_name       | String  | 国家名称           |
| $region             | String  | 地区               |
| $city               | String  | 城市               |
| $browser            | String  | 浏览器             |
| $browser_version    | String  | 浏览器版本         |
| $os                 | String  | 操作系统           |
| $os_version         | String  | 操作系统版本       |
| $client_version     | String  | App 版本           |
| $channel            | String  | 自定义 App 渠道    |
| $device_brand       | String  | 设备品牌           |
| $device_model       | String  | 设备型号           |
| $device_type        | String  | 设备类型           |
| $device_orientation | String  | 设备方向           |
| $resolution         | String  | 屏幕大小（高\*宽） |
| $language           | String  | 操作系统语言       |
| $referrer_type      | String  | 一级访问来源       |
| $account_id         | String  | ai/项目 id         |
| $domain             | String  | 域名               |
| $ip                 | String  | Ip                 |
| $user_agent         | String  | 用户代理           |
| $sdk_version        | String  | sdk 版本           |
| $location_latitude  | Float64 | 纬度               |
| $location_longitude | Float64 | 经度               |
| $path               | String  | 页面               |
| $referrer_path      | String  | 页面来源           |
| $textValue          | String  | 元素内容           |
| $index              | String  | 元素位置           |
| $xpath              | String  | 元素路径           |
| $hyperlink          | String  | 元素链接           |

### 预置用户属性

​[详见预置用户属性](../../../product-manual/customer-data-platform/user-management/user-properties/user-properties#预置用户属性)​

特殊用户属性说明

| 用户属性       | 标识符                     | 说明                                              |
| -------------- | -------------------------- | ------------------------------------------------- |
| 出生年月日     | $basic_birthday            | 日期，格式：yyyy-MM-dd                            |
| 性别           | $basic_gender              | 字符串，枚举值：UNKNOWN,MALE,FEMALE               |
| 地址           | $basic_addresses           | list 格式，用英文逗号分隔，例如：中国,北京,朝阳区 |
| 注册时间       | $basic_createdAt           | 时间戳格式（毫秒级），默认值 false                |
| 关注公众号     | $wechat_subscribeList      | list 格式，用英文逗号分隔 ，例如：GrowingIO,易数  |
| 支付宝学生认证 | $alipay_isStudentCertified | boolean 类型（true 或 false），默认值 false       |
| 支付宝实名认证 | $alipay_isCertified        | boolean 类型（true 或 false），默认值 false       |

## 数据导入限制

1.  数据格式为 json，每条记录单独一行，用换行符分割
2.  **建议**单个数据文件为 256MB 以内较为合适，同一任务可以支持多个文件的上传
3.  暂时不支持压缩的文件，请上传原始数据
4.  历史数据会按天分组导入。对于用户行为数据**同一个事件、同一用户、同一事件属性等完整一条数据**重复导入会**覆盖**，并且会覆盖历史 SDK 打点的数据。对于用户属性数据会和历史数据做合并，一般为 T+1 生效，如未生效可联系 GrowingIO 技术支持。
