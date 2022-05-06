---
id: metadata-management
sidebar_position: 9
---

# 元数据管理

## 简介[](#jian-jie)

你可以在该模块批量创建埋点事件、事件属性、用户属性，且能批量将埋点事件与事件属性进行绑定，提高创建的效率。


## 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

拥有**事件管理权限**的用户，可以批量定义事件标识符、事件属性标识符、事件与事件属性的绑定关系

拥有**用户管理权限**的用户，可以批量定义用户属性标识符

无权限请找**管理员**开通权限

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MiyEGWYQmJ2OQOT-QK0%2F-Miyn0OWL58fJLU2Qaz8%2Fimage.png?alt=media&token=00c6cbb5-dd5c-4b0f-a29a-a34fe60dfbe2)

元数据管理页面


## 功能说明[](#gong-neng-shuo-ming)

### 进入“元数据批量创建”页面[](#jin-ru-yuan-shu-ju-pi-liang-chuang-jian-ye-mian)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-Mkf0tkMeWql1MQunqYQ%2F-Mkf2YDZYX5270nXTGKB%2Fimage.png?alt=media&token=ecca4fcf-3ad9-4c5c-9cb7-5c84a2e61aef)

选择模板


### 选择模板：埋点事件及事件属性[](#xuan-ze-mo-ban-mai-dian-shi-jian-ji-shi-jian-shu-xing)

#### 埋点事件及事件属性模板，下载模板[](#mai-dian-shi-jian-ji-shi-jian-shu-xing-mo-ban-xia-zai-mo-ban)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-Mkf0tkMeWql1MQunqYQ%2F-Mkf2eeSAlOXtZrXVRZi%2Fimage.png?alt=media&token=0ed2ac9e-214c-4112-8edd-d54932e5c182)

选择类型，下载模板


#### 填写模板[](#tian-xie-mo-ban)

点击下载模板，模板内仅包含表头，**不要修改表头信息**，并按照“查看提示和规范”填写模板，导入成功后在事件管理模块内查看数据

模板及数据样例：

| 标识符（事件）* | 名称（事件）* | 描述（事件） | 标识符（事件属性）* | 名称（事件属性）* | 类型（事件属性）* | 描述（事件属性） |
| --- | --- | --- | --- | --- | --- | --- |
| event1 | 事件1 | ​   | test1 | test1 | 字符串 | test1绑定事件1 |
| event1 | 事件1 | ​   | test2 | test2 | 字符串 | test2绑定事件1 |
| event2 | 事件2 | ​   | test2 | test2 | 字符串 | test2绑定事件2 |

不能修改表头，模板中带“*”必须填写

事件标识符不能为空，如不绑定事件属性，对应“*”字段填入“-”

所有的数据均会以增量的方式进入系统

每个模板限制最多2000条数据

填写规范：

| 名称  | 描述  |
| --- | --- |
| 事件标识符 | 仅允许大小写英文、数字、以及下划线，并且不能以数字开头，最长为100个字符。 |
| 事件名称 | 最长为30个字符。 |
| 事件描述 | 最长为150个字符。 |
| 事件属性标识符 | 仅允许大小写英文、数字、以及下划线，并且不能以数字开头，最长为100个字符。 |
| 事件属性名称 | 最长为30个字符。 |
| 事件属性类型 | 字符串（string）、整数（int）、小数（double）。 |
| 事件属性描述 | 最长为150个字符。 |

#### 将填写好的模板上传到页面中[](#jiang-tian-xie-hao-de-mo-ban-shang-chuan-dao-ye-mian-zhong)


### 选择模板：用户属性[](#xuan-ze-mo-ban-yong-hu-shu-xing)

#### 用户属性，下载模板[](#yong-hu-shu-xing-xia-zai-mo-ban)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-Mkf0tkMeWql1MQunqYQ%2F-Mkf3AmZTCvBafLx9j0Z%2Fimage.png?alt=media&token=46a1b3a1-c4ca-44c6-940e-458fe7d57444)

选择类型，下载模板

#### 填写模板[](#tian-xie-mo-ban-1)

点击下载模板，模板内仅包含表头，**不要修改表头信息**，并按照“查看提示和规范”填写模板，导入成功后，到用户管理模块内查看创建的数据

模板及数据样例：

| 标识符（用户属性）* | 名称（用户属性）* | 类型（用户属性）* | 描述（用户属性） |
| --- | --- | --- | --- |
| prop1 | 属性1 | 字符串 | ​   |

所有的数据均会以增量的方式进入系统

每个模板限制最多2000条数据

填写规范：

| 名称  | 描述  |
| --- | --- |
| 用户属性标识符 | 仅允许大小写英文、数字、以及下划线，并且不能以数字开头，最长为100个字符。 |
| 用户属性名称 | 最长为30个字符。 |
| 用户属性类型 | 字符串（string）、整数（int）、日期（date）。 |
| 用户属性描述 | 最长为150个字符。 |

#### 将填写好的模板上传到页面中[](#jiang-tian-xie-hao-de-mo-ban-shang-chuan-dao-ye-mian-zhong-1)


### 确认上传内容[](#que-ren-shang-chuan-nei-rong)

如模板内容有格式问题，错误提示会在页面中显示，请按照页面中提示进行修改，并重新上传模板

如模板内无报错提示，请再次确认上传内容


### 保存并上传[](#bao-cun-bing-shang-chuan)

点击“保存并创建”按钮，上传成功后在“客户数据平台-用户管理-事件管理”或者“客户数据平台-用户管理-用户属性”中查看


## 常见问题[](#chang-jian-wen-ti)

* **需要上传事件标识符A，名称为A，系统已存在名称为A的事件，此时如何处理？**

事件标识符、事件名称、事件属性标识符、事件属性名称不能与系统已存在的重复，如上传有误会提供报错信息。

* **需上传的文件中存在事件标识符test1，数据类型为字符串，系统中存在事件标识符test1，事件类型为整数，此时如何处理？**

不支持修改操作，上传时，会通过事件标识符、事件属性标识符去判断是否在系统中已存在，如存在test1，无论对应的数据类型是否一致，都忽略，不进行修改。

* **上传文件中包含事件标识符test1绑定事件属性prop1、prop2，此时系统中存在事件标识符test1，已绑定事件属性prop1，prop3，此时导入结果是？**

支持增量更新，不支持批量修改删除操作。此时导入结果为，事件标识符test1，绑定事件属性prop1、prop2、prop3。
