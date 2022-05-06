---
id: webhook-tunnel
sidebar_position: 1
---

# Webhook通道

Webhook 方便企业将通知提醒发送至其它系统，如 IM工具、短信服务，邮件服务。


## 简介[](#jian-jie)

Webhook 方便企业将通知提醒发送至其它系统，如 IM工具、短信服务，邮件服务。

对于已经有建设或采购自己的 邮件、短信、IM等系统的客户， 只需要使用 GIO 的配置webhook通道，用 Webhook 是较灵活、简易“跨系统对接”解决方案，用户只需要选择配置好的 Webhook 配置，信息发送的动作由其他系统来完成。

当前企业配置中的webhook 通道 ，可用于 帐号审批通知、忘记密码等 ， GIO 系统对其他系统进行消息场景。

权限控制：只有企业拥有者、企业超级管理员，可以进行設置。


## 功能说明[](#gong-neng-shuo-ming)

### 查看Webhook[](#cha-kan-webhook)

点击，进入 企业设置 - Webhook通道 。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHC9wqJ-tGbBb7Luvn%2F-MkHCFND6d_ZDRDSfxpN%2Fimage.png?alt=media&token=58bcfc31-f934-4575-9d48-8174066642d6)


### 新建Webhook[](#xin-jian-webhook)

step1 : 点击，新建 webhook

step2 : 填写，通道名称 、 请求地址 、密钥

1.确定webhook通道名称（客户内部统一即可）

2.确定请求地址（即客户开放给gio的调用接口）

3.确定鉴权 密钥 (若没有可不填）

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHC9wqJ-tGbBb7Luvn%2F-MkHCJe25XUf919XnT3_%2Fimage.png?alt=media&token=38cfbcb3-86e9-4caf-b117-8a3b9c22f24c)


### 禁用/启用Webhook[](#jin-yong-qi-yong-webhook)

点击，操作 点击，启用/禁用

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHC9wqJ-tGbBb7Luvn%2F-MkHCO7wrgp-pB-iuMOa%2Fimage.png?alt=media&token=e79f91ea-e50a-47d1-be60-3ba70ab299f7)

禁用时，当此webhook 被使用在 相关连的通知任务时，会给予提示 。 若确定禁用webhook ，关联的通知任务将失效 。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHC9wqJ-tGbBb7Luvn%2F-MkHCSzmXp3HtdCDVmFj%2Fimage.png?alt=media&token=36ed4172-d6ab-4ec0-84df-9e67b56319e1)

​
### WebHook推送数据格式说明[](#webhook-tui-song-shu-ju-ge-shi-shuo-ming)

#### Request Headers[](#request-headers)

WebHook request headers 包含以下一些关键数据

X-GIO-Token: "***" # 用户新建 WebHook 通道提供的密钥

#### Request Payload[](#request-payload)

以下是推送的示范数据（仅供参考，请以实际收到的数据为准）。

```json
{
 "title": "Test",
 "content": "Test content",
 "receivers": [] 
}
```
