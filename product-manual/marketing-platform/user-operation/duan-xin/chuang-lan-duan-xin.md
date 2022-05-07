---
id: chuang-lan-duan-xin
sidebar_position: 3
---

# 创蓝短信

在用户运营界面，您可以通过后台向选择分群向用户发送短信，在使用第三方短信平台【创蓝】之前，您需要完成以下工作：

## 配置创蓝账号[](#1-pei-zhi-chuang-lan-zhang-hao)

前往官网，登录/注册

![](/img/assets-Lpwgem-x8KzhBglybzw-LyX4gha-vc4hUiZahrp-LyX50YHmRQsw2Y4OKUz%E5%88%9B%E8%93%9D1.png)

进行企业认证后，点击**通知短信，**查看API接口信息。记录**账号、密码**和**接口，**稍后需要在GrowingIO平台填写。需要注意的是，**如需发送带有变量的短信，接口地址中的\`send\`需要被替换成\`variable\`。但是GrowingIO平台会自动根据您的短信内容判断是否带有变量，所以您在GrowingIO平台上只需填写**\`smssh1.253.com\`(每个账号该地址不同)

![](/img/assets-Lpwgem-x8KzhBglybzw-LyX4gha-vc4hUiZahrp-LyX589-zepy5E4NwgzS%E5%88%9B%E8%93%9D2.png)

点击 **通知短信**->**签名管理** 进行短信签名的申请

![](/img/assets-Lpwgem-x8KzhBglybzw-LyX4gha-vc4hUiZahrp-LyX5FBiZFu8zeslgxsp%E5%88%9B%E8%93%9D3.png)

点击 **通知短信**->**模板管理** 进行短信签名的申请。**需要注意的是，**如需发送带有变量的短信，请将所有变量用**{$var}**替代(例如:{$var}你好,你的年龄是{$var}。填写完变量后：abc你好，你的年龄是10.)。**截图所示为错误示范，**按照创蓝平台创建变量短信的提示内容，创建的短信无法通过接口发送。**必须将变量用{$var}替换.**![](/img/assets-Lpwgem-x8KzhBglybzw-LvKdvGkhaZzf6Cgrprf-LvKgeq0YPkxgG0PCPJ4image.png)​

另外，如果您认为自己的短信内容没有敏感信息，也可以直接在GrowingIO平台上输入您的短信内容，创蓝平台会在发送前进行审核(有一定延迟)。

![](/img/assets-Lpwgem-x8KzhBglybzw-LyX4gha-vc4hUiZahrp-LyX5NqGOGfcBlp7L2rk%E5%88%9B%E8%93%9D4.png)


## 平台配置[](#2-zai-gio-ping-tai-pei-zhi)

在「触达->短信配置」中，先选择保存有手机号的用户属性名称。

![](/img/assets-Lpwgem-x8KzhBglybzw-LyX4gha-vc4hUiZahrp-LyX5Z0LM1xUD8GFru7J%E5%88%9B%E8%93%9D5.png)

然后找到「创蓝」，填入上一步中得到的 **短信签名, 账号, 密码 , 接口**参数并完成开通。

配置完成后，在新建活动时，可以选择短信消息通道给用户发信息，填写**模板id、短信内容变量**后， 满足条件的用户就会收到一条短信。


## 运营人员使用GrowingIO发送短信[](#3-yun-ying-ren-yuan-shi-yong-growingio-fa-song-duan-xin)

1. 选择分群和厂商（目前支持阿里云，根据客户的实际需求可以对接客户正在使用的短信SSP，方便直接用户GrowingIO给相应分群发送精细化运营短信）

2. 选择短信签名，填写模版code获取状态码，判断是否可用

**其他**

1.想查看对应分群里面手机号的显示。可以去 用户分析-用户细查 里面查看

![](/img/assets-Lpwgem-x8KzhBglybzw-LyX4gha-vc4hUiZahrp-LyX5djfP5haCFo9nG3e12.png)

## 发送短信后，未收到查看原因[](#4-fa-song-duan-xin-hou-wei-shou-dao-cha-kan-yuan-yin)

​[1.查看创蓝短信发送状态](https://zz.253.com/index.html)​
