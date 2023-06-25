---
id: webhook-channel
sidebar_position: 1
---

# Webhook通道

## 简介

Webhook方便企业将通知提醒发送至其它系统，如 IM工具、短信服务，邮件服务。

## 功能说明

### 新建Webhook

请求地址：接收推送数据的接口地址。
秘钥：Webhook推送数据时，放在请求头的关键数据。

![图 16](/img/d3529f8193cae5d0f0ceb42abc984847d003fbd4501224118b59466e6f6b5db1.png)

### 编辑Webhook

![图 2](/img/portal-edit_webhook-channel.png)  

### 禁用Webhook

仅未在使用中的通道才可禁用。

![图 4](/img/jinyongwebhook_webhook-channel.png)  

### 启用Webhook

可重新启用被禁用的通道。

![图 5](/img/qiyongwebhook_webhook-channel.png)  

### 删除Webhook

仅未在使用中的通道才可删除。删除后，将不在列表中展示。

![图 6](/img/shanchuwebhook_webhook-channel.png)  

## WebHook推送数据格式说明

1. WebHook request headers 包含以下关键数据

X-GIO-Token: "***" # 在 Webhook 通道内设置的密钥

2. Request Payload以下是推送的示范数据（仅供参考，请以实际收到的数据为准）。

```json

{    
    "title": "",//仅邮件使用。
    "content": "**",//在个人安全设置里面，勾选短信时，设置短信发送模版的内容
    "receivers": [] //手机号
}

```
