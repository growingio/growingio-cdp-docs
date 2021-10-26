---
id: mobile-debugger
sidebar_position: 1
---

# Mobile Debugger

此功能可以方便查看移动端 SDK 上传的数据信息。


## 简介[](#jian-jie)

完成埋点开发后，测试或者业务同学进行验收的过程中，通过该功能进行数据校验，可以查看移动端上传的信息是否正确、完整。


### 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

有数据集成权限的用户，如无权限请联系**管理员**

该工具要求iOS和Android SDK版本在3.1.0及以上

小米手机由于安全限制，该功能要求GrowingIO平台是https协议访问


## 功能说明[](#gong-neng-shuo-ming)

### 启动Mobile Debugger[](#qi-dong-mobile-debugger)

登录GrowingIO平台，在**客户数据平台-数据校验** ![](https://github.com/growingio/growingio-docs-v3/tree/d520f4a494f6c0635c83422f55c665597e79ee96/.gitbook/assets/2019-10-10_18-59-32.png) 选择**Mobile Debugger**进入Mobile Debugger启动页。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MYdATaneuDrmM0B81Ka%2F-MYdBRkK1aVEtey9QJrW%2F%E5%9B%BE%E7%89%87.png?alt=media&token=8e43cdb0-02f8-4b97-9b11-4e274e9118ef)


### 选择已集成SDK的debug应用[](#xuan-ze-yi-ji-cheng-sdk-de-debug-ying-yong)

### 扫码唤起App[](#sao-ma-huan-qi-app)

选择项目中需要进行测试的应用，并保证手机中已经安装该APP，且该APP已经集成GrowingIO 3.1.0及以上的SDK。

使用手机浏览器扫描入口的二维码唤起Debug的APP。


### 成功连接后，开始验证数据[](#cheng-gong-lian-jie-hou-kai-shi-yan-zheng-shu-ju)

在唤起Debug的APP后，该APP采集的行为数据以及当前页面截图就会出现在网页上，测试同学可以根据数据看数据的采集以及发送情况，对数据进行测试。

**通过“事件流”页签查看请求数据**

如下图，可以查看上报事件属性的请求数据

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MeZBV6ixYnoiiYfOOUd%2F-MeZPOkRVBIr9mSewTl5%2F%E4%BA%8B%E4%BB%B6%E6%B5%81%E9%A1%B5%E9%9D%A2.png?alt=media&token=8dce6e01-5f54-48d0-8e62-b500c6c5004d)

连接成功后事件流页面

| 图中序号 | 描述  |
| --- | --- |
| 1   | ​<br></br>可查看当前连接的用户及设备等基本信息 |
| 2   | ​<br></br>筛选器中展示的是系统中已定义的事件标识符列表，如果筛选后无数据，说明本次连接未上报数据 |

**通过“SDK运行日志”查看SDK运行中的信息/警告/错误三种日志**

如下图，可以点击日志发生的时间查看相应的日志

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MeZBV6ixYnoiiYfOOUd%2F-MeZRF90xKX8ecHudHtf%2FSDK%E6%97%A5%E5%BF%97.png?alt=media&token=e0069156-124e-464b-bf0d-6c88ab8cdd5c)

连接成功后进入SDK运行日志

| 图中序号 | 描述  |
| --- | --- |
| 1   | 可点击暂停按钮，停止同步SDK产生的日志，便于查看当前遇到的问题；再次点击继续按钮，则同步所有产生的SDK日志，并展示最新的一条日志数据 |
| 2   | 点击清屏按钮，清除当前所有产生的日志 |
