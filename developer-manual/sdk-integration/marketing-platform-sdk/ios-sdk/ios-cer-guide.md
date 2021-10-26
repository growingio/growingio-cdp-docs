---
id: mp-ios-cer-guide
sidebar_position: 5
---

iOS 推送证书设置指南
============

创建应用程序 ID[](#id)


--------------------

* 登陆 [苹果开发者网站](https://developer.apple.com/) 进入开发者账户。
    
* 从开发者账户页面左侧入口进入 “Certificates, IDs & Profiles” 页面。
    
* 创建 App ID，填写 App ID 的 NAME 和 Bundle ID（如果 ID 已经存在可以直接跳过此步骤）。
    
* 为 App 开启 Push Notification 功能。如果是已经创建的 App ID 也可以通过设置开启 Push Notification 功能。
    
* 填写好以上属性后，点击 “Continue”，确认 AppId 属性的正确性，点击 “Register”，注册 AppId 成功。
    

1\. 项目配置[](#1-xiang-mu-pei-zhi)


-----------------------------------

在项目工程中打开后台推送权限设置，如下图所示

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC55PLQhk-GqF5quhkP%2Fimage.png?alt=media&token=bf7ce79e-1ae0-4dd5-a6fb-348e88fbf454)

打开推送开关Push Notifications，如下图所示

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC55XrDhYWHyLGqU-oX%2Fimage.png?alt=media&token=83d7293e-fadd-4dde-b13e-401b281ac9c9)

2\. 创建App ID[](#2-chuang-jian-app-id)


-----------------------------------------

> 如果之前已经创建了App ID可跳过这一步。

登录苹果开发者账号，点击如下图红色箭头区域，进入证书配置页面。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC55fgSDLV3-TRIDtp-%2Fimage.png?alt=media&token=1e7cd9ba-b1f8-4536-a1f0-07852a3bb92d)

选中“Identifiers”，并且对应的是“App IDs”

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC55mqPekPrJahgwu3v%2Fimage.png?alt=media&token=8ae2d978-b59c-462d-9cbc-f17981b427fb)

选中对应的平台（Platform），输入对应的描述（Description）、Bundle ID

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC55vRLSt0OI161skpv%2Fimage.png?alt=media&token=a8e1e7bd-e6e8-4a8e-86a1-5ce1d1ef5a58)

打开推送功能，选中如下图所示，点击右上角“continue”按钮，执行下一步

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC561GZyXS8lHybbZ-D%2Fimage.png?alt=media&token=bde24005-2cfe-4ecc-8a19-49e6ccb76eff)

确定信息无误后，点击右上角“Register”进行注册

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC5692xccb4hHgWCsRd%2Fimage.png?alt=media&token=320432ea-7320-4776-a550-a8a62df65677)

3\. 创建本地CRS证书[](#3-chuang-jian-ben-di-crs-zheng-shu)


--------------------------------------------------------

打开MAC电脑上的钥匙串访问，点击窗口左上角的“钥匙串访问”中的“证书助理”，选择“从证书颁发机构请求证书…”

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC56GoUtm5iAW4CfWU1%2Fimage.png?alt=media&token=0281e08a-0f12-447f-8793-cea87893456d)

将证书选择为“存储到磁盘”，输入任意合法的邮箱地址后即可将证书保存到本地目录路径下

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC56NsvUY64zCbxEQPs%2Fimage.png?alt=media&token=18b1d69c-278c-4d86-9aff-702a7c3d87ed)

4\. 创建推送证书[](#4-chuang-jian-tui-song-zheng-shu)


---------------------------------------------------

登录苹果开发者账号，点击下图红色箭头指示区域

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC5280m7UGgVPsbeiOx%2F-MC56VRS4BaLnGmkjqK7%2Fimage.png?alt=media&token=a4c499e0-f6f4-4508-980e-a2e5e90953f8)

点击加号“+”，创建证书

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC56XkcdA4-cv6tX-44%2F-MC56oZqScnJewCcb6i6%2Fimage.png?alt=media&token=9fed35f5-5ec4-4f5c-b13d-ff487013afa0)

选择“Services”下创建推送证书，其中红色箭头指示的为创建开发调试环境下的推送证书，蓝色箭头指示的为创建生产环境以及开发调试下的推送证书，这里

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC56vjCNQAU-iph3Ek1%2F-MC5991p9mEjaHPvwg0W%2Fimage.png?alt=media&token=04b49852-7195-4f14-9357-5ffc6536091f)

这里假如创建的是开发环境的推送证书，选中红色箭头对应的圆圈，点击右上角的“continue”按钮，进入下一步，选择项目对应的“App ID”，点击右上角的“continue”按钮，进入下一步

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC56vjCNQAU-iph3Ek1%2F-MC59F4UkeYRoV4RknKx%2Fimage.png?alt=media&token=d0864ce5-4467-4ca2-b088-6184f0087614)

选择本地的“CRS”文件，点击右上角的“continue”按钮，进入下一步，即可生成对应项目开发环境下的推送证书，点击右上角的“Download”按钮，将证书下载到本地，选中刚才下载的证书，双击安装。

5\. 导出推送证书p12[](#5-dao-chu-tui-song-zheng-shu-p12)


------------------------------------------------------

打开MAC电脑上的钥匙串访问，找到刚才安装的推送证书，选中右击导出该证书

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC56vjCNQAU-iph3Ek1%2F-MC59NVDYr3KRxeC71cx%2Fimage.png?alt=media&token=c3eec922-b967-48c1-a1c4-372cabecc33e)

设置证书的本地存储路径，选择导出证书的格式为个人信息交换( .p12 )，设置证书密码

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC56vjCNQAU-iph3Ek1%2F-MC59Uce7xIqvklqfid_%2Fimage.png?alt=media&token=810f8b3c-e28e-428a-b70b-424e678b8d86)

6\. 上传证书[](#6-shang-chuan-zheng-shu)


----------------------------------------

登录网站， 确保已经成功集成了触达推送SDK，在产品配置中的“应用配置”中

选择需要配置的推送证书的环境，输入对应的“BundleID”，选中本地导出的p12的推送证书，输入密码并保存。
