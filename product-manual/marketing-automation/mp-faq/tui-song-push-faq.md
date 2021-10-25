---
id: tui-song-push-faq
sidebar_position: 3
---

# 推送（Push） FAQ

## 1. **第一期支持哪些厂商通道？对应的注册地址是？**[](#1-di-yi-qi-zhi-chi-na-xie-chang-shang-tong-dao-dui-ying-de-zhu-ce-di-zhi-shi)

第一期支持小米、华为、魅族、vivo、oppo。如果是其他机型默认选择小米（需要app在前台保活）‌

华为需要在华为的网页上配置指纹‌，华为、魅族需要配置回调地址‌。

## **2. 推送可以统计到哪些数据？**[](#2-tui-song-ke-yi-tong-ji-dao-na-xie-shu-ju)

1.  推送权限打开设备数：该推送选择的目标推送人群中，打开了推送权限的设备数量。
    
2.  消息发送设备数：指的是发送推送请求到第三方服务器。
    
3.  消息送达设备数：指的是厂商通过回调接口返回给 GIO 的设备送达数据。关机、无网络、卸载App以及关闭推送权限的设备是无法送达的。厂商每秒会发送一次回调数据。
    
4.  消息点击：指用户点击该Push的数量。是 GIO 的 SDK 采集到用户点击消息事件。
    
## **3. GIO 推送跟个推极光等传统推送平台相比有什么优势劣势？**[](#3-gio-tui-song-gen-ge-tui-ji-guang-deng-chuan-tong-tui-song-ping-tai-xiang-bi-you-shen-me-you-shi-lie-shi)

**Android：**优势是我们推送是直接对接到厂家的通道，并通过手机的机型启动相应的通道。比如小米手机启动小米推送通道、华为手机启动华为推送通道。即使APP不是保活状态也可以及时收到消息。劣势是我们没有自己的通道，暂时不支持消息透传。还有不支持APP相互唤醒的流氓功能。‌

**iOS：**直接对接的苹果APNs服务器，这个跟其他没有区别。‌

**GIO 最大的优势**是既保证到达率，又能做到每一步数据的精准迅速的获得，再也不会出现到达率很高，点击率很低，对于中间环节哪里出了问题摸不着头脑的情况。还能结合分群，做基于用户行为+业务数据的精准推送，真正做到精细化运营。‌

## **4. 能覆盖设备有哪些？到达率怎么样？**[](#4-neng-fu-gai-she-bei-you-na-xie-dao-da-lv-zen-me-yang)

**Android：**基本能覆盖所有的设备。我们现在对接的厂家通道有华为、小米和魅族，oppo和vivo等。通过手机的机型启动相应的通道，比如小米手机启动小米推送通道、华为手机启动华为推送通道。在其他手机上，比如联想、一加等机型上我们是直接利用小米的推送通道，这些手机上可能保证不了push消息能够及时送达。‌

**iOS：**直接对接的苹果APNs服务器。覆盖所有的苹果设备，包括iPad。‌


## **5. 应用在后台被杀死，还能收到推送吗？怎么做到的？**[](#5-ying-yong-zai-hou-tai-bei-sha-si-hai-neng-shou-dao-tui-song-ma-zen-me-zuo-dao-de)

**Android：**可以收到推送。我们直接使用的厂家通道，除非厂家通道的自己服务器的问题，不然可以直接推送。如上文所述通过手机的机型启动相应的通道，比如小米手机启动小米推送通道、华为手机启动华为推送通道。这时候是不需要长连接的，因为厂商手机系统本身就有自己的push长连接通道。未接入厂商通道的其他手机暂时是直接利用小米的推送通道，这个需要有一个长连接在后台，如果APP被杀死，可能保证不了push消息能够及时送达。‌

**iOS：**直接对接的苹果APNs服务器，肯定能收到。‌

## 6. 提示推送成功，但是没有收到推送[](#6-ti-shi-tui-song-cheng-gong-dan-shi-mei-you-shou-dao-tui-song)

需要选一下iOS证书 **开发环境**：需要确定 App 已使用开发环境的签名证书打包，使用`Xcode`直接编译安装到设备。 **生产环境**：需要确定 App 已使用生产环境的签名证书打包，生产环境的 App 有以下3种打包方式：`Ad-Hoc`  `TestFlight`  `AppStore`。

​![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-LqygDO5T25ZXFW1XV74%2F-LqylKD4pErthxilPSzc%2Fimage.png?alt=media&token=830e1b9b-021b-4605-bff7-9e47aa1286ca)​![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-LqygDO5T25ZXFW1XV74%2F-LqylPkEacVZRi8C76b4%2Fimage.png?alt=media&token=5e7060da-535f-4b62-8ed8-35ef033de5f7)‌

## 7. 安卓推送测试机注册失败[](#7-an-zhuo-tui-song-ce-shi-ji-zhu-ce-shi-bai)

可以从三个原因分析：‌

1 厂商通道要求配的appKey，appId，appSecret没有在build.gralde文件里配对‌

2 不同的品牌厂商通道支持机型不一样，比如一加手机注册小米通道的推送测试机容易失败‌

3 网络因素，oppo手机连接wifi时注册可能失败‌

建议开发人员在Logcat里搜索「PushRegister」这个tag，找到对应的code报错码，再去对应的产商推送平台上找报错码对应的异常情况。


​[魅族错误码文档](http://open.res.flyme.cn/fileserver/upload/file/201806/64d803e0fcd94154bc29233404f2a29f.pdf)​‌

​[小米错误码文档](https://dev.mi.com/console/doc/detail?pId=1557)​‌

​[VIVO错误码文档](https://dev.vivo.com.cn/documentCenter/doc/368)​‌

​[华为错误码文档](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/push-faq-v4)​‌

​[OPPO错误码文档](https://open.oppomobile.com/wiki/doc#id=10196)​‌

## **8. 安装app当天测试推送能推送到,但是分群推送推不到**[](#8-an-zhuang-app-dang-tian-ce-shi-tui-song-neng-tui-song-dao-dan-shi-fen-qun-tui-song-tui-bu-dao)

莫慌，因为分群T+1 ，推送令牌等信息还没有写入分群，请在第二天测试推送分群‌

## **9.一**个登陆用户ID对应两个手机设备，是否两个设备会同时收到推送？一个设备对应两个用户，是否在同一设备上收到两个用户的推送？[](#9-yi-ge-deng-lu-yong-hu-id-dui-ying-liang-ge-shou-ji-she-bei-shi-fou-liang-ge-she-bei-hui-tong-shi-shou-dao-tui-song-yi-ge-she-bei-dui-ying-liang-ge-yong-hu-shi-fou-zai-tong-yi-she-bei-shang-shou-dao-liang-ge-yong-hu-de-tui-song)

* 只会推送该用户最近一次登陆的设备
    
* 推送时按照设备去重，一个设备只会收到一条该Push
    
（1）web页面创建任务，推送发送人数少于分群实际人数​‌

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MDPaHfh1aJFqaZJIGyX%2F-MDPbHHt5oVajB_EPypZ%2Fimage.png?alt=media&token=7b24bde7-8232-4b9f-b673-b7394c2d5b67)

（2）api推送提示：1017查询目标用户为空，请检查audience参数‌

**以上两种情况都可通过事件分析进行排查。**‌

* 新版界面：产品分析 -> 分析工具 -\> 事件分析
    
* 旧版界面：产品分析 -\> 事件分析
    
推送任务理论正常送达（排除厂商未送达、用户断网关机等异常原因）需要：**GIO_触达推送通道**不为空、**GIO_触达推送包名**正常、**GIO_触达推送令牌**不为空、**GIO_触达推送权限开关**为true。​

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MDPaHfh1aJFqaZJIGyX%2F-MDPbWllySDVIwmooVsQ%2Fimage.png?alt=media&token=a9b3ee02-1a96-4693-8f7f-c0875795b4f7)
