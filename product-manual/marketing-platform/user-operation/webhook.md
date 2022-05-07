---
id: ma-webhook
sidebar_position: 2
---

# webhook

## Webhook功能性介绍

对于已经有建设自己的 CRM 系统的客户，CRM 中已经可以发送短信、Push， 只需要使用 GIO 的分群和事件触发的能力，用 Webhook 是一个比较灵活的解决方 案，用户只需要在运营平台的 Webhook 配置中完成前面此类人群规则的传递，信息发送的动作由客户自己来完成。

运营平台 Webhook 功能支持将分群信息(用户属性)发送到自己的内部系统 (push、发券系统、短信、邮件系统等)。同时，也支持将信息发送到自己的后 台，例如当用户发生了某些行为后若干次数后，客户可以在后台增加某个用户的 会员积分等。


### 对接 Push

运营平台支持第三方 PUSH 对接。只需通过配置请求地址即可实现对接第三方Push 平台功能。

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ2MITXG7wh_UKfVI9image.png)


### 对接邮件/短信

若用户希望针对不同分群用户发送不同的定制化短信/邮件时，可通过 webhook 配置功能实现分客群、自动触发的短信发送管理。在“webhook 配置-请求地址”位置设置短信/邮件接口地址，填写模板参数。最后在创建webhook活动中进行邮件内容文案的设置

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ3-cgjBoJ8F7sX0M4image.png)

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ3r0yRniR48sWo3MFimage.png)

短信文本可通过上述步骤中的参数进行设置。


### 对接发券

若用户拥有自建的优惠券系统，但是不支持圈选指定用户发券的功能，可通 过 webhook 配置功能实现通过自建优惠券系统发券的目标。在“webhook 配置- 请求地址”位置设置自建发券系统的接口地址，即可实现发券功能。

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ4LR8K49P10YzDuHGimage.png)

同时，也支持针对不同群组创建对应的 webhook 活动

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ4Zmbot9_Rnw6cCXUimage.png)


## webhook配置说明&应用实例

###  配置新的webhook通道

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ5ajLQZumNP8lXBK_image.png)

(1)点击智能运营

(2)点击产品配置

(3)做常规配置中，选择webhook配置

(4)点击新建webhook通道

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ5oI7YqvMy3Qv9P5timage.png)

(5) 确定webhook通道名称（客户内部统一即可）

(6)确定请求地址（即客户开放给gio的调用接口）

(7)确定鉴权方式（可选“密钥”、“Basic Authentication”、“无”）

(8)用户属性（支持登陆用户/访问用户两种用户类型，需要在gio的数 据平台中维护和管理，默认值是作为数据缺失时的默认显示）

(9)模板参数（gio不做任何判断，完全由客户的研发工程师根据客户自身系统的入参要求设定，默认值是作为数据缺失时的默认显示）

--用户属性和模板参数最多支持设置10个

(10)测试效果（在上述5～6内容填写完毕后，可以进行测试，目的是确认webhook通道建立成功，与客户系统的交互正常可用）

​
### 建立webhook运营活动

当webhook通道建立完成后，就可以进行相对应的运营活动配置

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ6cAUuOKh1NKMT8Y2image.png)

（1）点击运营活动

（2）选择webhook

（3）点击新建webhook

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ6kp_J670vYoosXoLimage.png)

（4）选择用户分群

（5）选择webhook通道

（6）选择触发类型![](blob:https://growingio.atlassian.net/ef874264-b69b-4f16-ac08-fbed535732b4#media-blob-url=true&id=a3f4c5c3-2909-4663-885d-56b82f13d0a7&collection=contentId-1470825243&contextId=1470825243&mimeType=image%2Fpng&name=image-20200715-030531.png&size=139016&width=834&height=549)​

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ7K_VESSUHa_zKwF_image.png)

（7）模板内容填写

（8）发送时间设置


## 应用实例

### 【故事1】

白鸽公司是一家会员制电商公司，拥有自建的优惠券系统，但是不支持圈选指定用户发券的功能，同时对接了GIO的webhook功能。

运营人员小雪现在要上线一个运营任务：针对公司昨日有加入购物车动作但还未下单的黄金vip等级会员（用户分群），每人发一张面值100元的优惠券（模板参数）


#### A. webhook通道参数配置如下

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ7d1Affg8RFjPix9fimage.png)

* webhook通道名称：客户自己定，从客户视角，这个webhook通道是对接自建的优惠券系统，所以可以叫做“白鸽卡券中心”
    
* 请求地址：客户自建的发券系统提供给gio的接口地址
    
* 鉴权方式：如果选择鉴权就设置密钥
    
* 用户属性：不需要设置，可在配置webhook活动时通过客群选择时选择
    
* 模板参数：在这个故事中，webhook是调客户自建的发券系统，只需要传券的面值金额即可，所以参数设定可以如下：
    

_参数名称：amount_

_显示名称：券面值_

_参数类型：整数_

_默认值：-_

* 测试成功后保存即可
    

#### B. 创建对应的webhook活动

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ7kiVvSDobBqbUQZ-image.png)

* 选择客群
    
* 选择刚创建的“白鸽卡券中心”通道
    
* 触发设置：一次性
    
* 模板参数：在故事1中就是优惠券的金额，100元（这里也可以点击测试效果，验证功能畅通）
    

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ7rLieqQnVfMw6GIoimage.png)

* 设置发送时间
    
* 上线/保存草稿

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ7vAEVxFoK3baUCmEimage.png)

* 上线后可见
    

### 【故事2】

运营人员小雪现在要上线一个运营任务：针对公司昨日有加入购物车动作但还未下单的黄金vip等级会员（用户分群），再通过用户id（用户属性），白鸽内部自行计算历史交易额大于5000元的用户，这些用户每人发一张面值100元的优惠券（模板参数）

那么用户属性参数可以配置如下：

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ84-GFPTvg4RGAUGAimage.png)

**_参数名称：userid_**

**_用户属性：用户登陆id_**

**_默认值：-_**


### 【故事3】

白鸽公司是一家会员制电商公司，对接了第三方短信通道，同时对接了GIO的webhook功能。

运营人员小雪现在要上线一个运营任务：针对公司黄金vip等级会员用户，在其生日当天（用户分群），每人发一条祝福短信，并且短信文案为“亲爱的xxx先生/女士（用户属性），在这个属于您的精彩的日子，白鸽祝您生日快乐！“（模板参数）

这里只讲模板参数的设置，在这个故事中，不再是对接自建的券系统，而是对接客户的短信通道。具体参数设置如下：![](blob:https://growingio.atlassian.net/498d503a-5cea-49cc-8433-dd63c734393e#media-blob-url=true&id=1c46efe8-2c5f-4abe-a6e2-328e5459d68e&collection=contentId-1470825243&contextId=1470825243&mimeType=image%2Fpng&name=image-20200715-031346.png&size=187643&width=1271&height=628)​

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ8A_Pz0U5iNWDg8RMimage.png)

**_参数名称：message_**

**_显示名称：短信_**

**_参数类型：文本_**

**_默认值：-_**

在创建webhook活动时，短信文本可设置

![](/img/assets-M2qbZInaXgdm8kkNosp-MDZ13zDgwD_h1s7W32k-MDZ8DuHMvx_bFcmbGKJimage.png)
