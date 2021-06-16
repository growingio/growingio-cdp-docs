# iOS 推送证书设置指南

### 创建应用程序 ID <a id="id"></a>

* 登陆 [苹果开发者网站](https://developer.apple.com/) 进入开发者账户。
* 从开发者账户页面左侧入口进入 “Certificates, IDs & Profiles” 页面。
* 创建 App ID，填写 App ID 的 NAME 和 Bundle ID（如果 ID 已经存在可以直接跳过此步骤）。
* 为 App 开启 Push Notification 功能。如果是已经创建的 App ID 也可以通过设置开启 Push Notification 功能。
* 填写好以上属性后，点击 “Continue”，确认 AppId 属性的正确性，点击 “Register”，注册 AppId 成功。

### 1. 项目配置

在项目工程中打开后台推送权限设置，如下图所示

![](../../../../.gitbook/assets/image%20%28247%29.png)

打开推送开关Push Notifications，如下图所示  
****

![](../../../../.gitbook/assets/image%20%28231%29.png)

### 2. 创建App ID

> 如果之前已经创建了App ID可跳过这一步。

登录苹果开发者账号，点击如下图红色箭头区域，进入证书配置页面。

![](../../../../.gitbook/assets/image%20%28256%29.png)

选中“Identifiers”，并且对应的是“App IDs”  


![](../../../../.gitbook/assets/image%20%28235%29.png)

选中对应的平台（Platform），输入对应的描述（Description）、Bundle ID

![](../../../../.gitbook/assets/image%20%28238%29.png)

打开推送功能，选中如下图所示，点击右上角“continue”按钮，执行下一步

![](../../../../.gitbook/assets/image%20%28246%29.png)

确定信息无误后，点击右上角“Register”进行注册

![](../../../../.gitbook/assets/image%20%28255%29.png)

### 3. 创建本地CRS证书

打开MAC电脑上的钥匙串访问，点击窗口左上角的“钥匙串访问”中的“证书助理”，选择“从证书颁发机构请求证书…”

![](../../../../.gitbook/assets/image%20%28236%29.png)

将证书选择为“存储到磁盘”，输入任意合法的邮箱地址后即可将证书保存到本地目录路径下

![](../../../../.gitbook/assets/image%20%28252%29.png)

### 4. 创建推送证书

登录苹果开发者账号，点击下图红色箭头指示区域

![](../../../../.gitbook/assets/image%20%28245%29.png)

点击加号“+”，创建证书

![](../../../../.gitbook/assets/image%20%28226%29.png)

选择“Services”下创建推送证书，其中红色箭头指示的为创建开发调试环境下的推送证书，蓝色箭头指示的为创建生产环境以及开发调试下的推送证书，这里

![](../../../../.gitbook/assets/image%20%28239%29.png)

这里假如创建的是开发环境的推送证书，选中红色箭头对应的圆圈，点击右上角的“continue”按钮，进入下一步，选择项目对应的“App ID”，点击右上角的“continue”按钮，进入下一步

![](../../../../.gitbook/assets/image%20%28233%29.png)

选择本地的“CRS”文件，点击右上角的“continue”按钮，进入下一步，即可生成对应项目开发环境下的推送证书，点击右上角的“Download”按钮，将证书下载到本地，选中刚才下载的证书，双击安装。

### 5. 导出推送证书p12

打开MAC电脑上的钥匙串访问，找到刚才安装的推送证书，选中右击导出该证书

![](../../../../.gitbook/assets/image%20%28248%29.png)

设置证书的本地存储路径，选择导出证书的格式为个人信息交换\( .p12 \)，设置证书密码

![](../../../../.gitbook/assets/image%20%28240%29.png)

### 6. 上传证书

登录网站， 确保已经成功集成了触达推送SDK，在产品配置中的“应用配置”中

选择需要配置的推送证书的环境，输入对应的“BundleID”，选中本地导出的p12的推送证书，输入密码并保存。

