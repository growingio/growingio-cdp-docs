---
id: android-sdk-compliance
sidebar_position: 1
---

# Android SDK 合规说明

请使用对应版本中的最新 GrowingIO Android SDK

* 根据[工业和信息化部关于开展纵深推进APP侵害用户权益专项整治行动](http://www.gov.cn/zhengce/zhengceku/2020-08/02/content_5531975.htm)，App 需要通过隐私政策说明应用采集数据
    
* 需要告知用户您集成了 GrowingIO SDK，并且 GrowingIO SDK 会尝试获取 ANDROID_ID，IMEI 信息用于渠道信息，并且采集用户信息进行行为分析
    

## 集成步骤[](#ji-cheng-bu-zhou)

​请参考[客户端采集 SDK 3.0](https://growingio.github.io/growingio-sdk-docs/docs) 中 Android SDK


## 隐私政策[](#yin-si-zheng-ce)

如您的 App 需要通过第三方安全检测，建议在隐私政策授权成功之后，再初始化 GrowingIO SDK


## Google Play[](#google-play)

如您的 App 需要在 Google Play 分发，依据 Google Play [相关政策](https://support.google.com/googleplay/android-developer/answer/9888379?hl=zh-Hans&ref_topic=9877467#zippy=%2C%E5%B8%B8%E8%A7%81%E8%BF%9D%E8%A7%84%E8%A1%8C%E4%B8%BA%E7%A4%BA%E4%BE%8B)，请使用对应版本中的最新 GrowingIO Android SDK


## 合规步骤[](#he-gui-bu-zhou)


### GDPR[](#gdpr)

​[General Data Protection Regulation 欧盟通用数据保护条例](https://zh.wikipedia.org/wiki/%E6%AD%90%E7%9B%9F%E4%B8%80%E8%88%AC%E8%B3%87%E6%96%99%E4%BF%9D%E8%AD%B7%E8%A6%8F%E7%AF%84)​

GrowingIO SDK 提供`dataCollect`设置接口，可在用户不同意数据采集时，调用对应接口设置不发送数据；在用户同意数据采集后，调用对应接口设置发送数据

> 当使用`dataCollect`在禁止数据采集阶段， SDK 不发送数据，数据量将会较之前有所下降
