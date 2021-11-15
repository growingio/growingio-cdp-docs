---
id: user-identifications-13.x
sidebar_position: 2
---

# 旧用户模型 - 13.x版本

GrowingIO系统使用 **gid** 来对每个GrowingIO识别的用户进行唯一标识。目前系统支持采集匿名和登录用户(user_id)，GrowingIO系统会根据匿名和登录用户的匹配关系生成 gid 唯一识别一个真实的使用用户。

## 基本概念[](#ji-ben-gai-nian)

### 匿名用户[](#ni-ming-yong-hu)

匿名用户是GrowingIO对访问您的应用（包括网页、App、微信小程序等 ）用户的一种识别机制。每一个访问您应用的用户都会在对应的设备中生成并记录一个唯一的 ID，我们称之为访问用户 ID。

对于不同平台类型的应用，GrowingIO 提供了多种识别方案，从而尽可能地实现对用户的唯一标识。

### 登录用户[](#deng-lu-yong-hu)

登录用户也就是注册用户，当用户访问您的产品并发生注册/登录行为时，您可以通过GrowingIO SDK 中的 API 将该用户的注册ID（或与之对应的唯一标识，可以加密处理）上传给 GrowingIO。

这个 ID 会被作为今后用户在各个地方使用您的产品的身份识别 ID。

## GrowingIO识别用户(gid)[](#growingio-shi-bie-yong-hu-gid)

GrowingIO提供ID-Mapping逻辑，帮助您打通匿名用户和登录用户，唯一识别一个真实的使用用户。

> ID-Mapping功能支持设置开启和关闭状态

### 计算逻辑[](#ji-suan-luo-ji)

如果一个设备( 网站应用、APP、小程序 )从未登录过，我们会将该设备识别为一个“用户”，此时gid为设备匿名ID；如果一个设备曾经登录过，我们会将该设备的所有行为归属于它所登录的用户ID，通过登录用户ID来唯一识别一个用户，此时gid为登录ID。

### 常见场景[](#chang-jian-chang-jing)

* 匿名用户首次登录后，关联用户首次登录前后产生的行为
    
* 用户在设备登录后，关联用户登录行为和匿名行为
    
* 用户多应用使用时，关联用户跨应用行为
    
* 多用户使用同一应用时，区分不同用户使用行为
    

## 案例[](#an-li)

### 案例一：关联用户登录行为和匿名行为[](#an-li-yi-guan-lian-yong-hu-deng-lu-hang-wei-he-ni-ming-hang-wei)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPqe3oSw0qIX24L9FgQ%2F-MPqjiM0ADmElBR3z-KP%2Fimage.png?alt=media&token=aeecc2e9-abd8-4ea3-9342-178f0f2d6de8)

| 时间  | 用户行为 |
| --- | --- |
| 1   | **小明** 使用浏览器 **X** 未登录访问GrowingIO官网。<br></br>SDK首次识别浏览器根据cookie生成匿名ID c1，未识别到登录ID。<br></br>此时根据匿名ID c1生成gid 1，并在Event表中记录该事件属于用户gid 1。 |
| 2   | **小明** 使用浏览器 **X** 在GrowingIO官网登录账户u1。<br></br>SDK识别匿名ID(cookie) c1和登录ID u1。<br></br>此时根据登录ID u1生成gid 2，并在Event表中记录该事件属于用户gid 2。<br></br>同时在虚拟表(ID-Mapping)记录 时刻2 匿名ID c1和登录ID u1的绑定关系。 |
| 3   | **小明** 在浏览器 **X** 上退出登录，继续浏览GrowingIO官网。<br></br>SDK识别匿名ID(cookie) c1，未识别到登录ID。<br></br>由于该设备最后登录ID为u1，此时我们认为该匿名行为仍是u1发生的，因此在Event表中记录该事件属于用户gid 2。 |
| 4   | **小明** 在浏览器 **X** 上未登录状态下继续浏览GrowingIO官网。<br></br>SDK识别匿名ID(cookie) c1，未识别到登录ID。<br></br>由于该设备最后登录ID为u1，此时我们认为该匿名行为仍是u1发生的，因此在Event表中记录该事件属于用户gid 2。 |
| 5   | **小红** 使用浏览器 **Y** 未登录访问GrowingIO官网。<br></br>SDK首次识别浏览器根据cookie生成匿名ID c2，未识别到登录ID。<br></br>此时根据匿名ID c2生成gid 3，并在Event表中记录该事件属于用户gid 3。 |

查询时间：1 - 5

计算指标：活跃用户量

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPqe3oSw0qIX24L9FgQ%2F-MPqkc7i9RavXABSWjZO%2Fimage.png?alt=media&token=35d99750-1fb8-486b-a0e5-eb64f86a7732)

第一步：虚拟表中，时间1 - 时间5根据ID-Mapping最终归因原则匹配匿名ID和登录ID的匹配关系。

* 匿名ID: c1 - 登录ID: u1 - gid: 2
    

第二步：Event表中，时间1 - 时间5根据Mapping关系将匿名ID生成的gid进行映射，打通首次登录前行为和首次登录后行为。

* gid: 1 -> gid: 2
    

第三步：Event表中，时间1 - 时间5根据“合并后gid"计算用户量，结果为2。

### 案例二：同一用户多应用使用时，关联用户跨应用行为[](#an-li-er-tong-yi-yong-hu-duo-ying-yong-shi-yong-shi-guan-lian-yong-hu-kua-ying-yong-hang-wei)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPqe3oSw0qIX24L9FgQ%2F-MPqjrjOe0XujMNBIwWq%2Fimage.png?alt=media&token=bf1637b0-d0c1-4601-8bf0-72b2210035e4)

| 时间  | 用户行为 |
| --- | --- |
| 1   | **小明** 使用浏览器 **X** 未登录访问GrowingIO官网。<br></br>SDK首次识别浏览器根据cookie生成匿名ID c1，未识别到登录ID。<br></br>此时根据匿名ID c1生成gid 1，并在Event表中记录该事件属于用户gid 1。 |
| 2   | **小明** 使用浏览器 **X** 在GrowingIO官网登录账户u1。<br></br>SDK识别匿名ID(cookie) c1和登录ID u1。<br></br>此时根据登录ID u1生成gid 2，并在Event表中记录该事件属于用户gid 2。<br></br>同时在虚拟表(ID-Mapping)记录 时刻2 匿名ID c1和登录ID u1的绑定关系。 |
| 3   | **小明** 在浏览器 **X** 上退出登录，继续浏览GrowingIO官网。<br></br>SDK识别匿名ID(cookie) c1，未识别到登录ID。<br></br>由于该设备最后登录ID为u1，此时我们认为该匿名行为仍是u1发生的，因此在Event表中记录该事件属于用户gid 2。 |
| 4   | **小明** 在浏览器 **X** 上未登录状态下继续浏览GrowingIO官网。<br></br>SDK识别匿名ID(cookie) c1，未识别到登录ID。<br></br>由于该设备最后登录ID为u1，此时我们认为该匿名行为仍是u1发生的，因此在Event表中记录该事件属于用户gid 2。 |
| 5   | **小红** 使用浏览器 **Y** 未登录访问GrowingIO官网。<br></br>SDK首次识别浏览器根据cookie生成匿名ID c2，未识别到登录ID。<br></br>此时根据匿名ID c2生成gid 3，并在Event表中记录该事件属于用户gid 3。 |
| 6   | **小明** 使用苹果手机 **A** 未登录访问GrowingIO APP。<br></br>SDK首次识别手机设备生成匿名ID IDFA，未识别到登录ID。<br></br>此时根据匿名ID IDFA生成gid 4，并在Event表中记录该事件属于用户gid 4。 |
| 7   | **小明** 使用苹果手机 **A** 在GrowingIO APP登录账户u1。<br></br>SDK识别匿名ID IDFA和登录ID u1。<br></br>此时根据登录ID u1生成gid 2，并在Event表中记录该事件属于用户gid 2。<br></br>同时在虚拟表(ID-Mapping)记录 时刻7 匿名ID IDFA和登录ID u1的绑定关系。 |
| 8   | **小明** 使用苹果手机 **A** 未登录访问GrowingIO APP。<br></br>SDK识别匿名ID IDFA，未识别到登录ID。<br></br>由于该设备最后登录ID为u1，此时我们认为该匿名行为仍是u1发生的，因此在Event表中记录该事件属于用户gid 2。 |

查询时间：1 - 7

计算指标：活跃用户量

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPqe3oSw0qIX24L9FgQ%2F-MPqksrhjAwxmCg2B-BR%2Fimage.png?alt=media&token=34ba5fc3-7521-4788-90e0-5339e6892dc5)

第一步：虚拟表中，时间1 - 时间7根据ID-Mapping最终归因原则匹配匿名ID和登录ID的匹配关系。

* 匿名ID: c1 - 登录ID: u1 - gid: 2
    
* 匿名ID: IFDA - 登录ID: u1 - gid: 2
    

第二步：Event表中，时间1 - 时间7根据Mapping关系将匿名ID生成的gid进行映射，打通首次登录前行为和首次登录后行为。

* gid: 1 -> gid: 2
    
* gid: 4 -> gid: 2
    

第三步：Event表中，时间1 - 时间7根据“合并后gid"计算用户量，结果为2。

> 活跃用户量为2，包含gid 2( u1, c1, IDFA ) 和 gid 3( c2 )
> 
> 实际访问设备数为3，包含浏览器设备c1、c2和App设备IDFA
> 
> 实际登录用户数为1，包含登录用户ID u1

### 案例三：多用户使用同一应用时，区分不同用户使用行为[](#an-li-san-duo-yong-hu-shi-yong-tong-yi-ying-yong-shi-qu-fen-bu-tong-yong-hu-shi-yong-hang-wei)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPqe3oSw0qIX24L9FgQ%2F-MPqm-da5IXRJAiqxarI%2Fimage.png?alt=media&token=94d30bd8-01ed-4c45-a26e-4a820abe381d)

操作步骤如下：ddd

| 时间  | 用户行为 |
| --- | --- |
| 1   | **小明** 使用浏览器 **X** 未登录访问GrowingIO官网。<br></br>SDK首次识别浏览器生成匿名ID cookie，未识别到登录ID。<br></br>此时根据匿名ID cookie生成gid 1，并在Event表中记录该事件属于用户gid 1。 |
| 2   | **小明** 使用浏览器 **X** 在GrowingIO官网登录账户u1。<br></br>SDK识别匿名ID cookie和登录ID u1。<br></br>此时根据登录ID u1生成gid 2，并在Event表中记录该事件属于用户gid 2。<br></br>同时在虚拟表(ID-Mapping)记录 时刻2 匿名ID cookie和登录ID u1的绑定关系。 |
| 3   | **小明** 在浏览器 **X** 上退出登录，继续浏览GrowingIO官网。<br></br>SDK识别匿名ID cookie，未识别到登录ID。<br></br>由于该设备最后登录ID为u1，此时我们认为该匿名行为仍是u1发生的，因此在Event表中记录该事件属于用户gid 2。 |
| 4   | **小红** 使用同一个浏览器 **X** ，并登录自己的账户u2浏览GrowingIO官网。<br></br>SDK识别匿名ID cookie和登录ID u2。<br></br>此时首次识别登录ID u2，并根据u2生成gid 3，Event表中记录该事件属于用户gid 3。<br></br>同时在虚拟表(ID-Mapping)记录 时刻4 匿名ID cookie和登录ID u2的绑定关系。 |
| 5   | **小红** 在浏览器 **X** 上退出登录，继续浏览GrowingIO官网。<br></br>SDK识别匿名ID cookie，未识别到登录ID。<br></br>由于该设备最后登录ID为u2，此时我们认为该匿名行为仍是u2发生的，因此在Event表中记录该事件属于用户gid 3。 |
| 6   | **小明** 使用苹果手机 **A** 未登录访问GrowingIO APP。<br></br>SDK首次识别手机设备生成匿名ID IDFA，未识别到登录ID。<br></br>此时根据匿名ID IDFA生成gid 4，并在Event表中记录该事件属于用户gid 4。 |
| 7   | **小明** 使用苹果手机 **A** 在GrowingIO APP登录账户u1。<br></br>SDK识别匿名ID IDFA和登录ID u1。<br></br>此时根据登录ID u1生成gid 2，并在Event表中记录该事件属于用户gid 2。<br></br>同时在虚拟表(ID-Mapping)记录 时刻7 匿名ID IDFA和登录ID u1的绑定关系。 |
| 8   | **小明** 使用浏览器 **X** 未登录访问GrowingIO官网。<br></br>SDK识别匿名ID cookie，未识别到登录ID。<br></br>由于该设备最后登录ID为u2，此时我们认为该匿名行为仍是u2发生的，因此在Event表中记录该事件属于用户gid 3。<br></br>( 此时记录使用用户为gid 3 即用户 **小红** ，但实际使用用户是gid 2 即用户 **小明** ) |
| 9   | **小明** 使用浏览器 **X** 在GrowingIO官网登录账户u1。<br></br>SDK识别匿名ID cookie和登录ID u1。<br></br>此时根据登录ID u1生成gid 2，并在Event表中记录该事件属于用户gid 2。<br></br>同时在虚拟表(ID-Mapping)记录 时刻9 匿名ID cookie和登录ID u1的绑定关系。 |
| 10  | **小明** 在浏览器 **X** 上退出登录，继续浏览GrowingIO官网。<br></br>SDK识别匿名ID cookie，未识别到登录ID。<br></br>由于该设备最后登录ID为u1，此时我们认为该匿名行为仍是u1发生的，因此在Event表中记录该事件属于用户gid 2。<br></br>( 此时虽然也是匿名访问，但由于最后操作的登录账户是u1，我们认为该行为属于gid 2 即用户 **小明** ) |

查询时间：1 - 8

计算指标：活跃用户量

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPqe3oSw0qIX24L9FgQ%2F-MPqmWzV-0r_cIijEcWM%2Fimage.png?alt=media&token=ce3993be-e9eb-4a25-85f1-8f196930a33c)

第一步：时间1 - 时间8虚拟表中根据ID-Mapping最终归因原则匹配匿名ID和登录ID的匹配关系。

* 匿名ID: cookie - 登录ID: u2 - gid: 3
    
* 匿名ID: IDFA - 登录ID: u1 - gid: 2
    

第二步：在Event表中，根据Mapping关系将匿名ID生成的gid进行映射，打通首次登录前行为和首次登录后行为。

* gid: 1 -> gid: 3
    
* gid: 4 -> gid: 2
    

第三步：时间1 - 时间8根据“合并后gid"计算用户量，结果为2。

> 活跃用户量为2，包含gid 2和gid 3
> 
> 实际访问设备数为2，包含浏览器设备cookie和App设备IDFA
> 
> 实际登录用户数为2，包含登录用户ID u1、u2
