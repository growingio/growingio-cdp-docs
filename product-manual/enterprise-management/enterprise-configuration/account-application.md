---
id: account-application
sidebar_position: 2
---

# 帐号申请

成员可在登录页面进行帐号申请，管理员可根据通知进行帐号审批

## 简介[](#jian-jie)

成员可在登录页面进行帐号申请，管理员可根据申請通知进行帐号审批。

> 系统开启单点登入时 ，无法使用帐号申请功能。


## 功能说明[](#gong-neng-shuo-ming)

### 帐号申请[](#zhang-hao-shen-qing)

step1 : 在登入页面，可点击 【帐号申请】。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHDH_hoYCtwZ-jUbqK%2F-MkHDMb3Uw8YMpNB31YY%2Fimage.png?alt=media&token=d791a67d-a2ff-4dfe-89a9-636f362c7d84)

step2 : 在表单中填写申请内容。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHDH_hoYCtwZ-jUbqK%2F-MkHDR8h6nZdw-D_7VQH%2Fimage.png?alt=media&token=31825350-0d47-4482-a4f8-eaba20504c6e)

step3 : 提交申请，审批人员接收申请通知 。

系统开启单点登入时 ，无法使用帐号申请功能。


### 帐号审批[](#zhang-hao-shen-pi)

权限控制：只有企业拥有者、企业超级管理员，可以进行帐号审批。

step1 : 点击帐号申请审批，进入审批页面 。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHDH_hoYCtwZ-jUbqK%2F-MkHDbzWRx7j5gm6c2ob%2Fimage.png?alt=media&token=d74238e4-e136-46cc-a66d-50faf3d602e6)

step2 : 点击 申请通知进行审批操作

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHDH_hoYCtwZ-jUbqK%2F-MkHDjAlD7YZ-NAW-0z1%2Fimage.png?alt=media&token=e336f294-d1e9-4cb4-8077-aeb71f51c1ec)

step3 : 填写成员信息 ，进行 通过 / 拒绝 。

信息可设置：修改成员的企业角色、邮箱、手机号等信息 ，但不可调整 申请的密码/帐号 。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHDH_hoYCtwZ-jUbqK%2F-MkHDow9FSEwFRlaF6vP%2Fimage.png?alt=media&token=8c36b966-be8d-41b9-97bf-c76ab8120cce)

step4 : 审批通过后 ，申请者即可使用帐号密码进行登入操作 。


### 帐号申请设置[](#zhang-hao-shen-qing-she-zhi)

权限控制：只有企业拥有者、企业超级管理员，可以进行設置。

可配置，启用/禁用帐号申请功能、申请填写表单与申请时的通知任务。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHDH_hoYCtwZ-jUbqK%2F-MkHDtDxvm-qYocVlDYj%2Fimage.png?alt=media&token=413fc60d-6c03-4d35-a391-e5513e83cc7d)


#### 配置申请表单内容[](#pei-zhi-shen-qing-biao-dan-nei-rong)

勾选，表单中的填写项并选择必填或选填 。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHDH_hoYCtwZ-jUbqK%2F-MkHDx6JkGf-tCkYpWMG%2Fimage.png?alt=media&token=ca3b20de-5984-4538-9b6a-8a2a7d964b0b)


#### 配置通知任务[](#pei-zhi-tong-zhi-ren-wu)

step1 : 任务名称。

step2 : 选择通知的渠道 （当前支持 webhook 通道对接）

step3 : 设置通知的对象 。 （支持可以添加多个审批对象）

1.触发时机 ：当有申请时系统会触发任务发送通知，通知审批人。

2.审批对象：可输入 手机号、邮箱、工号 等 ，可确定通知对象的字段 , 依据对接场景灵活设置 。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MkHDH_hoYCtwZ-jUbqK%2F-MkHE0vybL4GyDMxMlV5%2Fimage.png?alt=media&token=f396e4c4-1e9b-473d-9f42-296178de4db2)
