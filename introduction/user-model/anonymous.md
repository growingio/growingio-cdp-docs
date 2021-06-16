# 匿名用户

## WEB JS SDK

> 包括 Web 页面与 H5 页面

GrowingIO会使用随机 UUID 的方法生成访问用户ID，并将之记录在浏览器的 cookie 中

## iOS SDK

GrowingIO会按照如下顺序获取访问用户ID：

1. IDFA
2. IDFV
3. 随机 GUID

并将之存储至 keychain 中。

## Android SDK

GrowingIO 会按照如下顺序获取访问用户ID：

1. Android ID
2. IMEI
3. 随机UUID

进行 MD5 加密后将之存储至本地文件系统。

## 小程序 SDK

GrowingIO默认使用 UUID（随机 UUID 的方法生成访问用户 ID，并将之记录在浏览器的 cookie 中）来作为访问用户 ID，您也可以通过 API 设置使用 openID 作为访问用户ID。

访问用户ID 将保存到微信浏览器的 cookie 中。

## 常见问题 <a id="chang-jian-wen-ti"></a>

访问用户 ID 在哪些情况下会发生变化？

JS：用户使用浏览器的隐身模式、用户手动清空Cookie、同一个用户使用多个浏览器

iOS：当访问用户ID为 IDFV 或 IDFA 时，会随着 IDFA 和 IDFV 的变化而变化；当访问用户 ID 为 GUID 时，用户删除了应用重新安装或者是清除了数据。

Android：当访问用户ID为Android或IMEI时，会随着Android和IMEI的变化而变化；当访问用户ID为UUID时，用户删除了应用重新安装或者是清除了数据。

微信小程序：当用户ID 是 UUID时，用户长按小程序入口的小程序图标，删除了小程序；更换了手机设备；手动更新了微信的缓存等。当用户 openID 上述行为不会导致 访问用户ID 变化。

