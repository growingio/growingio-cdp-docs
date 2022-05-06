---
id: a-li-yun-duan-xin
sidebar_position: 1
---

# 阿里云短信

在运营平台上，您可以直接选择分群向用户发送短信，在使用第三方短信平台【阿里大鱼（阿里云）】之前，您需要完成以下工作：

## 配置阿里短信[](#1-pei-zhiali-duan-xin)

前往阿里云官网，登录/注册。

在阿里云控制台首页搜索RAM访问控制。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTDOrlOJ9ArXkiT8y3%2F1.png?alt=media&token=985bdc25-30e4-440a-9166-dc0cfe3efcea)

进入RAM(resource access management)访问控制,点击**用户 -\> 新建用户**, 在**访问方式**中勾选**编程访问**, 点击**确认**

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTDZC_kMafs0VpS7aY%2F2.png?alt=media&token=c47bccd4-852d-479a-94c7-a13484b1ad17)

点击左侧栏用户, 选择上一步创建的用户, 点击链接进入用户详情页, 点击**创建新的AccessKey**, 并保存生成的AccessKeyId和AccessKeySecret

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTDgNLojamo8e1rXEw%2F3.png?alt=media&token=0600bc5a-55f2-4b85-9ef8-c00d370c8214)

创建完成后点击左侧边栏用户,出现以下页面.

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTDpJLW8vxpeiDPuEt%2F4.png?alt=media&token=900a258b-5621-437f-a1f6-9fd8e4af521f)

点击**操作**栏下方添加权限,为用户添加**AliyunDysmsFullAccess**权限,点击**确认.**

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTE7ccK4tYcQjCqWl6%2F5.png?alt=media&token=e389635c-7ab5-44be-afac-8909c6062024)

阿里平台通过模板短信的方式提供 短信验证码 和 短信通知 类的短信下发，在阿里云控制台首页搜索**短信服务**，进入短信服务控制台即可创建短信签名和短信模板。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTEig6qNUZFjbjQB0n%2F6.png?alt=media&token=79a31414-49f4-4917-b958-4f4198573c17)

点击 **国内消息 -> 签名管理 -\> 添加签名,** 按提示要求填写签名.满足条件即可提交签名。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTEt_cNf8WuSz_YpOH%2F7.png?alt=media&token=f70a4938-d695-4856-822d-829e7e314c90)

点击 **国内消息 -> 模板管理 -\> 添加模板** ，按提示要求填写模板内容、短信签名、模板标题、模板类型；满足条件即可提交模板。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTF3_o6p5qXMcRow9x%2F8.png?alt=media&token=782b1be2-877f-4f39-ab8e-e0fd4b841b5c)

提交后，可在模板列表中看见自己创建的短信签名和短信模板，当前状态为审核中，**注意：审核通过后，才可以使用。**在签名列表中可以查看**签名名称;**在模板列表中可以查看**模板CODE**(TemplateCode)。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTFDczzBJcVwcriFj4%2F9.png?alt=media&token=47fee33d-3f85-4154-8779-a33cb5a80f4e)


## 配置GrowingIO平台[](#2-pei-zhi-growingio-ping-tai)

需要在数据中心-数据管理-用户变量，增加手机号变量相关信息，客户端调用相关API上报手机号。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTFSR6ecUyuTFG6Rue%2F10.png?alt=media&token=c4b8d0ae-a599-41a1-a234-c1233a8adadf)

在运营平台配置界面的左侧边栏中选择短信配置，选择保存有手机号的用户属性名称。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTFZOtKVB21JiSfohf%2F11.png?alt=media&token=91e3ca2d-c170-4863-a615-6536e8180b00)

然后找到「阿里云」，填入上一步中得到的 **短信签名 , AccessKeyId , AccessKeySecret**参数并完成开通。

配置完成后，在新建活动时，可以选择短信消息通道给用户发信息，填写**模板CODE(TemplateCode)、短信内容变量**后， 满足条件的用户就会收到一条短信。

注意：

短信内容变量 并非真正的消息内容，指的是 在相对固定的模板内容中，有一些变量是可以根据实际情况作出调整的。

_实例模板：【GrowingIO】你好{name}，恭喜你获得100元VIP优惠券，请于3天内在App使用。_

其中{name}就是一个内容变量，在GIO系统中 可以点击内容变量框选择一个用户属性默认填入该变量中，变量会根据用户的变化而自动展示对应信息。

达成真实短信效果：_【GrowingIO】_你好王小明，恭喜你获得_100元VIP优惠券_，请于3天内在App使用。


## 运营人员使用GrowingIO发送短信[](#3-yun-ying-ren-yuan-shi-yong-growingio-fa-song-duan-xin)

1. 选择分群和厂商（目前支持阿里云，根据客户的实际需求可以对接客户正在使用的短信SSP，方便直接用户Gio给相应分群发送精细化运营短信）

2. 选择短信签名，填写模版code获取状态码，判断是否可用

**其他**

1.想查看对应分群里面手机号的显示。可以去用户分析-用户细查 里面查看

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lpwgem-x8KzhBglybzw%2F-LyTDME0NcW9pXhR94Xf%2F-LyTFco16ATvMqvEvI_o%2F12.png?alt=media&token=26b3827d-36ee-4d3f-babc-6a4515500396)


## 发送短信后，未收到查看原因[](#4-fa-song-duan-xin-hou-wei-shou-dao-cha-kan-yuan-yin)

​[1.阿里云点击查看短信发送状态](https://dysms.console.aliyun.com/dysms.htm?spm=5176.12818093.recent.ddysms.cce816d0C9LbBj#/statistic/record) ​[2.阿里云短信发送状态回执错误码](https://help.aliyun.com/document_detail/101347.html)​
