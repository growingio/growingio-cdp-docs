---
id: chuang-jian-tui-song
sidebar_position: 3
---

# 创建推送

## 第一步：选择分群和应用[](#di-yi-bu-xuan-ze-fen-qun-he-ying-yong)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC69QsEpCF9Wo2tDOFe%2F-MC69komugfnkQwL32vs%2Fimage.png?alt=media&token=be4caa64-d05e-4428-bb93-0eed746d4757)

* 选择接受 Push 的用户分群（需要先**创建用户分群**）
    
* 选择应用，可以选择的应用必须同时满足：
    
1.  加载了推送SDK
    
2.  安卓配置了至少一个厂商通道，建议配置所有厂商通道，可以有效提升到达率
    
3.  iOS需要已经上传过生产和测试环境证书
    
华为渠道和魅族渠道需要配置通道的回传地址，否则拿不到送达数。


## 第二步：设置Push基本内容和测试[](#di-er-bu-she-zhi-push-ji-ben-nei-rong-he-ce-shi)

**推送标题+文本**

标题+正文，支持emoji ，（iOS 支持图片推送）

在标题和正文处填写需要的内容，左侧手机上会实时展示模拟效果（如下图所示）。

**点击跳转至**

就是用户点击这条推送后的动作，默认「**打开App**」，也可以选择打开至**App内某个特定页面**，打开**H5页面**或者**自定义参数**。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC69QsEpCF9Wo2tDOFe%2F-MC6A2MIL6G_FSCPKriL%2Fimage.png?alt=media&token=c701d85d-8e7c-41e1-941d-9fe7c4f5598b)

**真机测试**

使用GIO推送，可以非常方便的用测试机测试效果，如果是第一次在某个应用下使用真机测试，需要先点击「添加」设备：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC69QsEpCF9Wo2tDOFe%2F-MC6AAUixHlJJ-BCv3tg%2Fimage.png?alt=media&token=45a6db84-5090-4a5d-a84b-90a30b56b76e)

点击「添加」后会出现弹窗，选择需要添加测试设备的应用，一个应用下面可以关联多个测试设备：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC69QsEpCF9Wo2tDOFe%2F-MC6AFyQXt6d6Vjs5i8T%2Fimage.png?alt=media&token=0f3647be-f7f8-4baa-9b60-3bbc134986ab)

用**符合条件的**测试设备扫描该二维码（**该测试设备需要已经安装了对应的App，且该App安装有推送SDK**），扫描成功后，需要您为该测试设备命名，便于之后选择，建议使用设备型号命名（如下图）。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC69QsEpCF9Wo2tDOFe%2F-MC6AMM2taSuBVteXta4%2Fimage.png?alt=media&token=24c1648e-43e4-4eac-add0-0ffcd0750362)

保存成功后，可以点击测试按钮，选择自己刚才添加的设备进行推送预览：

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC69QsEpCF9Wo2tDOFe%2F-MC6ASULlMO31v8OChFk%2Fimage.png?alt=media&token=3b17eb89-1bd1-48f7-8e35-08b69b939301)

点击「向该设备发送」，正常情况下就可以收到测试推送了。


## 第三步：设置推送类型和上线时间[](#di-san-bu-she-zhi-tui-song-lei-xing-he-shang-xian-shi-jian)

**推送类型选择：**

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MC69QsEpCF9Wo2tDOFe%2F-MC6AaszWgBHM5JNS5lC%2Fimage.png?alt=media&token=886ccaf2-9db5-461b-b76b-f844db9e2343)

* **一次性推送：**适用于运营活动和每日推荐，在推送到达上线时间时，推送的总人群会定下来，发送后即使分群变化，选定的用户群不会有变化，发完即停。
    
* **循环推送：**满足分群的规则就会每天推送一次，基于每天分群计算的最新结果，适用于对 N 天未登录用户的召回，用户一旦满足某个条件就发推送等场景。（默认不去重，按照当天的分群来发送，如果需要分群去重功能，可以在选择分群的时候利用这个规则，但推送名称需要提前定好）
