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

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5280m7UGgVPsbeiOx-MC55PLQhk-GqF5quhkPimage.png)

打开推送开关Push Notifications，如下图所示

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5280m7UGgVPsbeiOx-MC55XrDhYWHyLGqU-oXimage.png)

2\. 创建App ID[](#2-chuang-jian-app-id)


-----------------------------------------

> 如果之前已经创建了App ID可跳过这一步。

登录苹果开发者账号，点击如下图红色箭头区域，进入证书配置页面。

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5280m7UGgVPsbeiOx-MC55fgSDLV3-TRIDtp-image.png)

选中“Identifiers”，并且对应的是“App IDs”

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5280m7UGgVPsbeiOx-MC55mqPekPrJahgwu3vimage.png)

选中对应的平台（Platform），输入对应的描述（Description）、Bundle ID

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5280m7UGgVPsbeiOx-MC55vRLSt0OI161skpvimage.png)

打开推送功能，选中如下图所示，点击右上角“continue”按钮，执行下一步

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5280m7UGgVPsbeiOx-MC561GZyXS8lHybbZ-Dimage.png)

确定信息无误后，点击右上角“Register”进行注册

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5280m7UGgVPsbeiOx-MC5692xccb4hHgWCsRdimage.png)

3\. 创建本地CRS证书[](#3-chuang-jian-ben-di-crs-zheng-shu)


--------------------------------------------------------

打开MAC电脑上的钥匙串访问，点击窗口左上角的“钥匙串访问”中的“证书助理”，选择“从证书颁发机构请求证书…”

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5280m7UGgVPsbeiOx-MC56GoUtm5iAW4CfWU1image.png)

将证书选择为“存储到磁盘”，输入任意合法的邮箱地址后即可将证书保存到本地目录路径下

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5280m7UGgVPsbeiOx-MC56NsvUY64zCbxEQPsimage.png)

4\. 创建推送证书[](#4-chuang-jian-tui-song-zheng-shu)


---------------------------------------------------

登录苹果开发者账号，点击下图红色箭头指示区域

![](/img/assets-M2qbZInaXgdm8kkNosp-MC5280m7UGgVPsbeiOx-MC56VRS4BaLnGmkjqK7image.png)

点击加号“+”，创建证书

![](/img/assets-M2qbZInaXgdm8kkNosp-MC56XkcdA4-cv6tX-44-MC56oZqScnJewCcb6i6image.png)

选择“Services”下创建推送证书，其中红色箭头指示的为创建开发调试环境下的推送证书，蓝色箭头指示的为创建生产环境以及开发调试下的推送证书，这里

![](/img/assets-M2qbZInaXgdm8kkNosp-MC56vjCNQAU-iph3Ek1-MC5991p9mEjaHPvwg0Wimage.png)

这里假如创建的是开发环境的推送证书，选中红色箭头对应的圆圈，点击右上角的“continue”按钮，进入下一步，选择项目对应的“App ID”，点击右上角的“continue”按钮，进入下一步

![](/img/assets-M2qbZInaXgdm8kkNosp-MC56vjCNQAU-iph3Ek1-MC59F4UkeYRoV4RknKximage.png)

选择本地的“CRS”文件，点击右上角的“continue”按钮，进入下一步，即可生成对应项目开发环境下的推送证书，点击右上角的“Download”按钮，将证书下载到本地，选中刚才下载的证书，双击安装。

5\. 导出推送证书p12[](#5-dao-chu-tui-song-zheng-shu-p12)


------------------------------------------------------

打开MAC电脑上的钥匙串访问，找到刚才安装的推送证书，选中右击导出该证书

![](/img/assets-M2qbZInaXgdm8kkNosp-MC56vjCNQAU-iph3Ek1-MC59NVDYr3KRxeC71cximage.png)

设置证书的本地存储路径，选择导出证书的格式为个人信息交换( .p12 )，设置证书密码

![](/img/assets-M2qbZInaXgdm8kkNosp-MC56vjCNQAU-iph3Ek1-MC59Uce7xIqvklqfid_image.png)

6\. 上传证书[](#6-shang-chuan-zheng-shu)


----------------------------------------

登录网站， 确保已经成功集成了触达推送SDK，在产品配置中的“应用配置”中

选择需要配置的推送证书的环境，输入对应的“BundleID”，选中本地导出的p12的推送证书，输入密码并保存。
