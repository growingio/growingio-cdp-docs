---
id: enterprise-security-setting
sidebar_position: 1
---

# 安全设置

## 简介[](#jian-jie)

为保证企业信息安全，降低数据泄露风险，企业管理员根据企业对系统信息安全等级要求自定义账号安全、登录安全、全局水印等策略。


## 功能说明[](#gong-neng-shuo-ming)

### 密码规则
对【账号密码】类型账号，可设置密码规则：
- 密码字符类型默认3种。至少1种，最多4种
- 限制密码长度。默认8个字符，最短可设置8个字符，最长32个字符。
- 限制密码定期失效须重置密码。默认为 0 即不限制，最长可设置 365 天
- 限制新密码与历史密码的重复。默认与前1次密码不重复，最多
- 限制与前 5 次密码不重复，0次表示不检查历史密码重复

![图 1](/img/portal-mmgz_enterprise-security-setting.png)  

### 个人安全设置

开启个人安全设置后，【个人中心】将展示【安全设置】Tab，用户可绑定安全设备，用于身份验证。
安全设备支持：短信、邮箱、MFA设备。
![图 2](/img/portal-graqsz_enterprise-security-setting.png)  

开启后，个人中心效果：
![图 3](/img/portal-grzxaqsz_enterprise-security-setting.png)  

### 二次登录验证

开启二次验证后，用户登录时，需要完成设置的身份验证方式后，才可登录。

- 当【个人安全设置】开启时，才可使用。
- 支持的验证方式：在【个人安全设置】中选择的验证方式。

![图 4](/img/portal-zcdlyz_enterprise-security-setting.png)  

### 防暴力破解

开启后，当用户登录错误次数达到安全次数后，帐号被锁定。

![图 5](/img/portal-fblpj_enterprise-security-setting.png)  

### 登录会话设置

开启保持登录状态的限制，超时后登录会话将失效。

![图 6](/img/portaldlhh_enterprise-security-setting.png)  


### 全局水印

打开全局水印，所有登录后的系统页面将展示水印，水印内容为姓名+帐号

![图 1](/img/portal-enterprisesetting-watermark_enterprise-management.png)  

