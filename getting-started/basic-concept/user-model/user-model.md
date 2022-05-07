---
id: user-model
sidebar_position: 1
---

# 用户模型

## 简介[](#jian-jie)

在业务场景中，一个真实的用户会通过多种渠道接触我们的公司和产品。在互联网业务中，一个用户可能会有多端设备，如手机、Pad、电脑等，用户会通过多终端设备体验我们的产品和服务。在金融业务中，用户会通过线上、线下和代理渠道购买我们的产品。在零售业务中，用户也会通过微信、淘宝、京东、抖音等平台购买我们的产品。

因此，如何正确去理解和使用用户模型是使用GrowingIO平台的第一步，我们支持2种身份模型，分别为 唯一身份ID 和 弱身份ID。

GrowingIO系统默身份配置仅支持使用 用户ID 和 UUID(设备ID)，如需使用多用户身份请联系相关工作人员，并在工作人员指导下进行多身份ID配置。

![](/img/assets-M2qbZInaXgdm8kkNosp-MiZzW5GAZav2VvW_jxc-Mi_3rcuT9G4nBtbayamimage.png)

### 唯一身份ID[](#wei-yi-shen-fen-id)

通常情况下，唯一身份ID可以设置为统一的会员账号或身份证。每一个系统识别用户有且仅有一个唯一身份ID，且唯一身份ID有值时仅存在唯一身份ID值。

### 弱身份ID[](#ruo-shen-fen-id)

通常情况下，弱身份ID可以设置为UUID(设备ID)、邮箱号、手机号等。每一个系统识别用户可以具有多个弱身份ID，且每一个弱身份ID可以同时具有多个值。

> 举例：通常场景下，一个真实用户可能具有多端设备ID或一个用户具有多个邮箱号和手机号

## 用户识别[](#yong-hu-shi-bie)

对每一个发生行为的用户，GrowingIO系统会根据行为上记录的用户身份自动生成一个用户标识符。比如一个匿名设备首次访问时，系统会根据匿名设备ID生成系统用户gio_id1，并将该访问行为记录给gio_id1。该设备首次登陆会员ID后，系统会记录gio_id1同时具有该匿名设备和会员ID，并将该登陆行为记录给gio_id1。

### 识别规则[](#shi-bie-gui-ze)

* 具体某一时刻，一个唯一身份ID值或弱身份ID值仅对应唯一系统用户(gio_id)
    
* 唯一身份ID值和系统用户(gio_id)关系一旦绑定不可取消
    
* 唯一身份ID值和系统用户(gio_id)绑定关系为一一对应关系，即GrowingIO系统会置信唯一身份ID
    
* 弱身份ID值和系统用户(gio_id)绑定关系可以变更
    
* 弱身份ID值和系统用户(gio_id)绑关系为多对一关系，即一个系统用户可以同时具有多个不同弱身份ID值
    
* 唯一身份ID置信度高于弱身份ID，多个弱身份ID之间存在严格置信度高低顺序
    
* 当一个事件具有多个用户身份，且每个身份对应不同系统用户，低置信度身份对应系统用户具有其他更高置信度的身份时，低置信度身份值会从其对应的系统用户移动到高置信度身份对应的系统用户，该事件归属于高置信度身份对应的系统用户。此时历史事件对应的系统用户不发生变化。
    
* 当一个事件具有多个用户身份，且每个身份对用不同系统用户，低置信度身份对应系统用户不具备其他更高置信度身份时，低置信度身份对应的系统用户会合并到高置信度身份对应的系统用户，用户属性会按最终归因形式进行合并，该事件属性高置信度身份对应的系统用户。此时历史事件对应的系统用户不发生变化，但会在用户融合结果表中记录系统用户融合关系。
    
* 系统用户融合和，系统字段首次识别日期($first_day)会按最初归因保留用户首次识别日期
    

## 案例[](#an-li)

### 案例一：首次访问设备匿名转登陆[](#an-li-yi-shou-ci-fang-wen-she-bei-ni-ming-zhuan-deng-lu)

![](/img/assets-M2qbZInaXgdm8kkNosp-Mi_Q1oe-e4TjH-PqhSf-Mi_a2Ap-6sjV5IcjOCyimage.png)

| 时间  | 用户行为 |
| --- | --- |
| t1  | **小明** 使用浏览器 X 未登陆访问GrowingIO官网<br></br>根据设备X生成系统用户 gio_id 1，记录到user表中<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |
| t2  | **小明** 使用浏览器 X 在GrowingIO官网登录账户U1<br></br>识别设备X对应系统用户 gio_id 1，且该用户不具有更高置信度身份<br></br>将U1添加给系统用户 gio_id 1，记录到user表中<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |
| t3  | **小明** 在浏览器 X 上退出登录，匿名浏览GrowingIO官网。<br></br>识别设备X对应系统用户 gio_id 1<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |

### 案例二：同一用户跨多设备使用[](#an-li-er-tong-yi-yong-hu-kua-duo-she-bei-shi-yong)

![](/img/assets-M2qbZInaXgdm8kkNosp-Mi_Q1oe-e4TjH-PqhSf-Mi__zFRopAtSCTneEbpimage.png)

| 时间  | 用户行为 |
| --- | --- |
| t1  | **小明** 使用浏览器 X 未登陆访问GrowingIO官网。<br></br>根据设备X生成系统用户 gio_id 1，记录到user表中<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |
| t2  | **小明** 使用浏览器 X 在GrowingIO官网登录账户U1<br></br>识别设备X对应系统用户 gio_id 1，且该用户不具有更高置信度身份<br></br>将U1添加给系统用户 gio_id 1，记录到user表中<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |
| t3  | **小明** 在浏览器 X 上退出登录，匿名浏览GrowingIO官网。<br></br>识别设备X对应系统用户 gio_id 1<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |
| t4  | **小明** 在浏览器 Y 上未登录状态下继续浏览GrowingIO官网。<br></br>根据设备Y生成系统用户 gio_id 2，记录到user表中<br></br>该事件属于系统用户 gio_id 2，记录到event表中 |
| t5  | **小明** 使用浏览器 Y 在GrowingIO官网登录账户U1<br></br>识别登陆用户 U1 对应系统用户 gio_id 1，设备Y对应系统用户 gio_id 2<br></br>系统用户 gio_id 2 不具备其他更高置信度身份<br></br>系统用户 gio_id 2 融合到 gio_id 1，记录到id_mapping_log中<br></br>系统用户 gio_id 2 的身份融合到 gio_id 1，并标记为融合(is_merged=1)，记录到user表中<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |
| t6  | **小明** 使用浏览器 Y 未登陆访问GrowingIO官网。<br></br>识别设备Y对应系统用户 gio_id 1<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |
| t7  | **小明** 使用浏览器 未登陆访问GrowingIO官网。<br></br>识别设备X对应系统用户 gio_id 1<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |

### 案例三：多用户交叉使用同一设备[](#an-li-san-duo-yong-hu-jiao-cha-shi-yong-tong-yi-she-bei)

![](/img/assets-M2qbZInaXgdm8kkNosp-Mi_Q1oe-e4TjH-PqhSf-Mi_cnUWpwuihtQgUnS1image.png)

| 时间  | 用户行为 |
| --- | --- |
| t1  | **小明** 使用浏览器 X 未登陆访问GrowingIO官网。<br></br>根据设备X生成系统用户 gio_id 1，记录到user表中<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |
| t2  | **小明** 使用浏览器 X 在GrowingIO官网登录账户U1<br></br>识别设备X对应系统用户 gio_id 1，且该用户不具有更高置信度身份<br></br>将U1添加给系统用户 gio_id 1，记录到user表中<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |
| t3  | **小明** 在浏览器 X 上退出登录，匿名浏览GrowingIO官网。<br></br>识别设备X对应系统用户 gio_id 1<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |
| t4  | **小红** 在浏览器 X 上未登陆访问GrowingIO官网。<br></br>识别设备X对应系统用户 gio_id 1<br></br>该事件属于系统用户 gio_id 1，记录到event表中 |
| t5  | **小红** 使用浏览器 X 在GrowingIO官网登录账户U2<br></br>登陆用户 U2 未识别，识别设备X对应系统用户 gio_id 1<br></br>根据登陆用户 U2 生成系统用户 gio_id 2，记录到user表中<br></br>将弱身份 X 从系统用户 gio_id 1 移动到 gio_id 2<br></br>该事件属于系统用户 gio_id 2，记录到event表中 |
| t6  | **小红** 在浏览器 X 上退出登录，匿名浏览GrowingIO官网。<br></br>识别设备X对应系统用户 gio_id 2<br></br>该事件属于系统用户 gio_id 2，记录到event表中 |
| t7  | **小明** 使用浏览器 X 未登陆访问GrowingIO官网。<br></br>识别设备X对应系统用户 gio_id 2<br></br>该事件属于系统用户 gio_id 2，记录到event表中 |
